Retrieved from: https://www.ibm.com/support/pages/node/6444205 on [[2022-03-05]]. Keeping here because I'm pretty sure it'll disappear eventually.

---

# Expired K3s certificates are not automatically rotated causing connection issues

## Problem

Cached K3s certificates are not cleared when automatically rotated.


K3s generates internal certificates with a 1-year lifetime. Restarting the K3s service automatically rotates certificates that expired or are due to expire within 90 days. However, the version of K3s used with App Host does not clear out the cached certificate, which causes the same problem. Therefore, the cache needs to be cleared manually.
  

## Symptom

Using the kubectl cli tool results in the following error:

```
 Unable to connect to the server: x509: certificate has expired or is not yet valid
```

***Note: Apps that are currently running continue to run with no issues

  

## Cause

The currently used version of K3s (v1.18) does not clear the cached certificate.  So even if the certificates are rotated by a K3s restart, the problem persists.

  

## Diagnosing The Problem

  

Changes to an existing app that uses the SOAR platform does not succeed. This includes file changes, secret changes, deploy or undeploy, and upgrade requests.

  

Installing a new app, the status remains in a ‘Deploying’ state. A tooltip instructs the user to run sudo appHostPackageLogs. Running this command or any other command that starts with kubectl gives you the following error:

  

```
#: kubectl get pods -A
Unable to connect to the server: x509: certificate has expired or is not yet valid
```

  

You can check the expiration data of a cached certificate by running the following command on the App Host server:

```
openssl s_client -connect localhost:6443 -showcerts < /dev/null 2>&1 | openssl x509 -noout -enddate 
```

  

  

## Resolving The Problem

As a precautionary measure backup the TLS dir.

```bash
sudo tar -czvf /var/lib/rancher/k3s/server/apphost-cert.tar.gz /var/lib/rancher/k3s/server/tls
```

Remove the following file.

```bash
sudo rm /var/lib/rancher/k3s/server/tls/dynamic-cert.json
```

Remove the cached certificate from a kubernetes secret.

```bash
sudo kubectl --insecure-skip-tls-verify=true delete secret -n kube-system k3s-serving
```

Restart the K3s service to rotate the certificates.

```bash
sudo systemctl restart k3s
```

Verify that kubectl commands function.

```bash
sudo kubectl get pods -A
```

Additionally, you can verify that all K3s internal certificates are no longer due to expire.

```bash
sudo su
```

```bash
for i in `ls /var/lib/rancher/k3s/server/tls/*.crt`; do echo $i; openssl x509 -enddate -noout -in $i; done
```

Or run

```bash
curl -v -k https://localhost:6443 [https://localhost:6443] to confirm the new date of your app host cert
```