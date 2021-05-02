# Spaces - Managed S3-like buckets

## Connexion

In order to have https for serving static assets over a bucket in a subdomain the simplest option is to move the DNS records of your subdomain to Digital Ocean registries. CNAMEing the DNS records manually didn't quite work.

Activate the `serve over a CDN` option of the bucket.

## Errors

> **Permission error when accessing recently added media in the bucket.**

Purge bucket's CDN cache.

## Documentation

> **Porting DNS records to Digital Ocean servers without losing email service of your provider.**

In your provider DNS settings do not deactivate MX records. In Digital Ocean create a MX DNS record in your domain as: `MX DOMAIN MX_SERVER_HOST. 10 14400`.

---
