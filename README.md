## Install the Kie-Server
This documentation will use the EAP server to install the kie server.

### Install EAP 7
Download EAP 7 from the Red Hat access site.<br>
https://access.redhat.com/products/red-hat-jboss-enterprise-application-platform/<br>
This documentation uses **jboss-eap-7.0.0.zip**

Unzip this file into an installation directory
```sh
> unzip jboss-eap-7.0.0.zip
```
This will create a directory named `jboss-eap-7.0.0`.  This will also be the directory where the kie-server will be installed.

### Install BRMS for EAP 7
Download the kie-server from the Red Hat access site.<br>
https://access.redhat.com/products/red-hat-jboss-brms/<br>

NOTE: Make sure to unzip this file into the EAP 7 directory.  It will update the jboss-eap-7.0.0 directory.

```sh
> unzip jboss-brms-7.x.x.GA-deployable-eap7.x.zip
```

### Create User and Role
The kie-server is protected by basic authentication.  Therefore, an appropriate user with the correct role must be created.  The following command can be used to create the user.
```sh
> jboss-eap-7.0/bin/add-user.sh -a --user controllerUser --password controllerUser1234 --role kie-server,rest-all
```

NOTE: Use your own `--user` and `--password` values.

### Start the EAP Server
The EAP server is now ready to be started.  Again, there are several ways to start the server depending on your configuration.  For this documentation, we will use `standalone.sh`.

First, set the `M2_HOME` environment variable to the location of the `.m2` directory.

```sh
> export M2_HOME=/home/sunil/.m2
```
The KJar would have been installed into the `.m2/repository` directory.  This is from where the kie-server will install the kjar.  **That is, the kie-server uses the maven repository to find the kjar and to deploy it into the service**

Now, start EAP.
```sh
> jboss-eap-7.0/bin/standalone.sh
```

### Verify Kie-Server Installation

Use any browser to access the following page (if you chose the default values).

```
[GET] http://localhost:8080/kie-server/services/rest/server/containers
```

You should see the following output:
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<response type="SUCCESS" msg="List of created containers">
    <kie-containers/>
</response>
```
