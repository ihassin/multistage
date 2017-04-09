# Multistage ansible example with vagrant

This repo shows an example of setting up multi-stage environments with Vagrant and Ansible.

## Pre-requisites

### create some entries in your /etc/hosts file

```
# Multistage-staging
33.33.33.11             staging-web.com
33.33.33.12             staging-db.com
 
# Multistage-prod
33.33.33.22             prod-web.com
33.33.33.23             prod-db.com
```
These host names will be used by ansible.

### Replace my public key with yours

Paste in your __public__ rsa key in roles/common/files/rsa.pub
 
## Run ansible via vagrant

```
vagrant up|provision
```
At the end of the run, you should have 4 servers: 2 for staging and 2 for production.
You can test to make sure that different values were applied based on the environments by examining $RAILS_ENV and ~/database.yml:
 
```
ssh staging-web-deploy@staging-web.com
cat database.yml # => staging-db-stuff
echo $RAILS_ENV # => test
```

# References

Thank you for your work:
 [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-manage-multistage-environments-with-ansible)
, [Ross Tuck](http://rosstuck.com/multistage-environments-with-ansible/) and [Osvaldo Toja](http://toja.io/using-host-and-group-vars-files-in-ansible/).
