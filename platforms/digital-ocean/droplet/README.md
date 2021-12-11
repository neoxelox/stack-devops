# Droplets - Compute VMs

## Connexion

IMPORTANT: IF USING DOCKER DIRECTLY IN THE SERVER DO NOT EXPOSE DIRECTLY THE CONTAINER PORTS TO THE INTERNET.
THERE IS A VULNERABILITY CALLED `kdevtmpfsi` WHICH WILL USE THE 100% CPU TO MINE CRYPTO!

USE `expose` DIRECTIVE IN DOCKER-COMPOSE FOR CONTAINERS THAT DO NOT NEED TO BE EXPOSED TO THE HOST/INTERNET.
USE `ports 127.0.0.1:XXXX:XXXX` DIRECTIVE BINDING TO THE HOST IP SO CONTAINER ARE NOT EXPOSED DIRECTLY TO THE INTERNET.

IMPORTANT!: `fail2ban` SHOULD BE INSTALLED IMMEDIATELY AFTER CREATING THE DROPLET!

IMPORTANT!: If enabling `ufw` firewall BEFORE exitting the ssh session you must allow incoming connections to por 22.
Otherwise you would lock out and you will never be able to access that droplet!

```
sudo ufw allow 22/tcp
```

## Errors

> **Permission error when accessing local postgresql database.**

Check universal firewall, ufw, allows that connection with `ufw status`.
If not run the following command to allow it:

```
ufw allow from 127.0.0.1 to any port 5432
```

For external connections, change the it to your public IP address.

## Documentation

> **Enabling Universal Firewall UFW for enhanced security.**

Run:

```
ufw enable
ufw list
```

---

- https://koacervate.blogspot.com/2020/05/your-containers-cpu-usage-is-more-than.html?m=0
