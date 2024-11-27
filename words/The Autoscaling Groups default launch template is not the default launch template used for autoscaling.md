I run into this recently, and it was pretty confusing, so I'm posting in the hopes it will help at least someone else.

#### Default & Latest
AWS Autoscaling Groups use Launch Templates. One of the Launch template versions gets the additional property "default", and one gets the property "latest". By default, `default`=`latest`. `Latest` is set automatically and always points to the latest incremental version of the launch template. `Default` can be updated manually and will no longer automatically point to latest if you update it at least once.

Now, you'd expect that the default Launch Template version is the one used when scaling right? Right, and it usually is, except when it isn't.

When you do an instance refresh to update your ASG to a different version of your launch template, you'll typically set the "Desired Configuration". The JSON looks like this:

```
"DesiredConfiguration": {
  "MixedInstancesPolicy": {
	  "LaunchTemplate": {
		  "LaunchTemplateSpecification": {
			  "LaunchTemplateName": "$NAME",
			  "Version": "$VERSION_AFTER_UPGRADE"
		  }
	  }
  }
}
```

This version that you set here creates a new "property", which we've taken to calling "desired version".

#### Visibility
This hidden `desired` version property is invisible via Console (until an instance refresh is complete) or the CLI. It's only visible as the version shown in the console after an instance refresh is complete. It doesn't get labeled as default, it's just the one shown on the interface. This desired version set to whatever we used in the latest instance refresh.

#### Functionality
This `desired` version is used for all scaling activity:
* Instance refresh (expected)
* Scaling out during the instance refresh
* Replacing unhealthy instances

In short, `desired` version will be chosen over `default`, no matter what the default is.

This has been a confusing discovery for us so I'm documenting both to vent at a confusing design choice, and to help discoverability of this issue for future engineers.