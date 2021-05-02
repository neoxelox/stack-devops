# Managed PostgreSQL

## Connexion

First of all add your PC public IP and the Kubernetes Cluster to the allowed IP list of the database in order to secure it from unwanted accesses.
Get the database credentials in the Digital Ocean dashboard. For external use (as with Datagrip) go with the Public connexion. For the Kubernetes cluster or any other resource that is in the same VPC network, use always the Private connection that will go faster without leaving the fiber cables of the same datacenter.

The database needs `sslmode: require` in the connexion and this cannot be changed (the client only must specify this). If more safety is wanted and you do want to prevent from database spoofing (so improbable), the CA certificates from the database can be downloaded and installed in the client application.

Set the maximum pool connections to the database in your as the number of `Backend server connection limit` that's in the tab connections of tha dashboard.

Change the maintenance window to `monday 2-6 am`.

## Errors

> **Cannot connect to the database SQLSTATE 28000 and IP must be included in pg_hba.conf.**

This is probably that the `sslmode` is not specified or it is not `require`.
Also check the database credentials.

## Documentation

> **Creating new users and databases.**

It is possible to create new databases and users by going to the users tab. However they have superuser permissions by default and if you want to decrease them you have to do it manually over a SQL connection.

---

- https://www.digitalocean.com/docs/databases/postgresql/how-to/secure/
- https://www.digitalocean.com/docs/databases/postgresql/how-to/modify-user-privileges/
- https://www.digitalocean.com/docs/databases/postgresql/how-to/manage-connection-pools/
