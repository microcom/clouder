Images
======

The Image menu is the place where you’ll manage the images of your containers. You need to build them before they can be deployed in your containers.

.. image:: images/image-list.png

When you build an image, a new image version will be created, so an image must contain all the information needed to build it. This include :

- The name of the image. You can only use here lowercase, digit and underscore.

- The current version of the image. This is used for the version name which will use the format ${current_version}.${current_datetime}.

- The parent image to use. We recommend building a base image containing the packages you need to launch your process (like supervisor, cron, syslog etc…) which you can then use as a parent for the other images.

- If the image is privileged, you shall not use this option unless really required because the container will be able to access the host system. It can be useful in at least one case, if you want to build a container which host other containers (see clouder_template_docker for example).

- Check the public checkbox if you want all users of the Clouder to be able to use this image. Otherwise, a user can only access an image if he is the manager of this image (or an administrator).

.. image:: images/gettingstarted-odoo-image.png

Then you have the Dockerfile field, used to know which commands shall be executed during the image building. Follow the Docker documentation https://docs.docker.com/reference/builder/ if you don’t know how to write it.

Note that the commands FROM (use parent field), MAINTENER (use the sysadmin email), VOLUME (use the volumes configuration) and EXPOSE (use the ports configuration) are automatically inserted in the Dockerfile during the building process, so you don’t have to take care of them.

| Then you have the volumes configuration. This is used both to indicate the volume of the container but also the directory to backup in the container. When you restore a container backup, all volumes will be erased and replaced by the backup, the rest of the container will be untouched. Also after the restore and if filled, the volume will be chown with the systemuser value to ensure rights are correctly attributed.
| You can also map a directory to a directory in the host system with the host path option. This is especially useful to get the archives of the application you want to host in the container, in this case you often want to check the readonly checkbox to ensure the container can’t modify the directory in the host system.

| Next you have the ports configuration, used to know the ports which need to be exposed to the outside of the container, to the local network or to the whole Internet.
| In the container, one field will be added : the hostport which is the port to access the localport in the container from outside of the host system. It is automatically attributed within the port range of the server but you can also force a specific port (Especially needed for the Bind, Proxy and Postfix applications which have to listen on ports 25, 53, 80 and 443 of the host system)

| Then, if you have a parent image, you have to select the parent version you want to use. Else you have to specify the FROM statement like you would use in a Dockerfile (example : debian:latest).
| You also have to specify the registry container where the image will be stored. For more information about this very specific kind of container, see the `Getting Started chapter <getting-started.rst>`_.

Finally, you can press the build button. This will create a new image version, named from the current date, and execute the commands to build it and store it in the registry.

.. image:: images/image-form-version.png

If you want to check the commands results, you can open the log in the version window.

.. image:: images/image-form-version-log.png

Remember you can manage your own images, but you also can use the ready-to-use images from the clouder_template_* modules until you feel confident enough to create yours. In this case, you just have to press the build button.



