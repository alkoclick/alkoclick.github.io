Originally posted to Medium on [[2022-05-17]] at : [https://medium.com/@alkoclick/using-kotlin-sealed-classes-to-map-out-a-domain-space-1e69c9ccd6e3.](https://medium.com/@alkoclick/using-kotlin-sealed-classes-to-map-out-a-domain-space-1e69c9ccd6e3.) It ended up shared across some Kotlin and android publications and is one of my most popular posts on the platform

---

The following is one of my favorite Kotlinic patterns: Using sealed classes to enumerate all possible return value groups of an API. This allows consumers to then easily act on different layers and manage the response there however they see fit.

This is not a uniquely Kotlinic pattern, in fact it's largely how Go has structured its error handling paradigm, but I believe the Kotlin OOP abstractions really make this pattern shine for all types of values and more than just error handling.

## Quick Kotlin glossary

-   `object` = singleton, an object that only has one instance
-   `data class` = immutable POJO (Plain Old Java Object)
-   `sealed class` = a class with a limited number of children, specified only in compile time (and in the same file for direct children, or any file for indirect children (children of children))

## The sealed magic

We break down our code in Gradle modules, that also correspond to JPMS modules. We create our own wrappers for things such as HTTP functionality or Shipping, which are wrappers over the various domain specific tools we use (e.g for HTTP or DB operations).

This is a part of our Sendcloud module, wrapping Sendcloud API calls in Lorthos, a project we are running in [Thalatta](https://thalatta.io/).

And yes, those are the actual comments we have in code. We take that part quite seriously!

```kotlin
/**  
 * Represents any possible response the Sendcloud API may return  
 *  
 * Normal generics won't work, because we don't want to add a type arg to all children (e.g the Singleton [NoBody])  
 * So, we use `out T` because  
 *  - This translates to SendcloudResponse<anything that is a T>  
 *  - Nothing is a subtype of everything, because it has no instances     
 * [See more on SO](https://stackoverflow.com/questions/54804289/type-safe-usage-of-generic-sealed-classes)  
 */  
sealed class SendcloudResponse<out T>

/**  
 * Sendcloud successfully authorized and executed our request, yielding the response [value]  
 */  
data class SendcloudValid<T>(val value: T) : SendcloudResponse<T>()

/**  
 * Sendcloud failed to process our request as expected. The [message] has more, human-readable, info  
 */  
abstract class SendcloudInvalid : SendcloudResponse<Nothing>() { 
	abstract val message: String  
}

/**  
 * If you got here, stuff is bad. The response we got had no body, or we didn't get a response at all.  
 * It is possible the response returned had other fields complete and just not the body.  
 * In that case, consider overriding the [lorthos.shipping.common.adapter.SendcloudResponseDeserializer.deserialize] logic  
 */  
object NoBody : SendcloudInvalid() { 
	override val message = "Could not communicate with Sendcloud. Either Lorthos did not properly create a request, or Sendcloud API is unavailable"  
}

/**  
 * Sendcloud API has received our request, but did not execute it. Usually 400 or 401  
 *  
 * @see [API Docs (https://docs.sendcloud.sc/api/v2/shipping/#errors)  
 */  
data class BodyError(  
    val code: Int,  
    override val message: String,  
    val request: String  
) : SendcloudInvalid()

class BodyError(  
    val code: Int,  
    override val message: String,  
    val request: String  
) : SendcloudInvalid()

/**  
 * Simple wrapper around [BodyError], because that's how Sendcloud returns it initially  
 */  
data class BodyErrorWrapper(val error: BodyError)
```

# Reifieds

The [reified type](https://kotlinlang.org/docs/inline-functions.html#reified-type-parameters) keyword allows us to have access to the type information within the function, something that we otherwise can't do with normal generics (at least not without using \**gasps*\* Reflection!)

So we use a few reifieds, such as this one, to avoid needing to pass around class arguments (note that Tentacle is our Http wrapper module around OkHttp):

```kotlin
/**  
 * Sends an authenticated request to the Sendcloud service with the given body  
 *  
 * @param endpoint the request target endpoint, in the form of "/target"  
 * @param body the request body, expected in JSON  
 *  
 * @return the raw string response body if it exists, or null  
 */  
protected inline fun <reified T : Any> post(endpoint: String, body: String): SendcloudResponse<T> =  
    Tentacle.post(BASE_API + endpoint, body, SendcloudCredentials.credentials, Headers.contentJson)  
        .let { SendcloudResponseDeserializer.deserialize(it) }
```

# Deserializer

The component below processes the various responses into our new types

The `toModel` function here leads to our JSON wrapper module (around Jackson), because the input in JSON. The resulting JSON can have multiple forms, or even be completely missing in the case of some errors, which is why we need a function to assist in unmarshalling, instead of just pointing to our data classes. 

```kotlin
object SendcloudResponseDeserializer {  
    // this can't be private due to inlining -_-  
    val logger = Logger(javaClass)
    
	inline fun <reified T : Any> deserialize(sendcloudResponse: String?): 
	  SendcloudResponse<T> =  
        when (sendcloudResponse) {  
            null -> NoBody  
            else -> logger.runCatching("Failed to cast into expected response type, falling back to Sendcloud error") {  
                SendcloudValid(sendcloudResponse.toModel(T::class))  
            }  
                ?: sendcloudResponse.toModel(BodyErrorWrapper::class).error  
        }  
}
```


# Callers

This allows callers at a place, far, far away, to be able to smoothly write code like this

```kotlin
fun createParcel(order: Order, browser: WebBrowser) { 
  when (val response = OrderShippingViewRequests.createParcel(order)) {  
    is SendcloudInvalid -> browser.toast("Failed to create parcel", response.message, ToastClass.ERROR, autohide = false)  
    is SendcloudValid<Parcel> -> browser.toast("Parcel created", "", ToastClass.SUCCESS)  
  }  
}
```

#articles 