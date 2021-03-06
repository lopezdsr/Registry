---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Adding images to your namespace
{: #registry_images_}

You can securely store and share Docker images with other users by adding images to your namespace in {{site.data.keyword.registrylong}}.
{:shortdesc}

Every image that you want to add to your namespace must exist on your local computer first. You can either download (pull) an image from another repository to your local computer, or build your own image from a Dockerfile by using the Docker `build` command. To add an image to your namespace, you must upload (push) the local image to your namespace in {{site.data.keyword.registrylong_notm}}.


Do not put personal information in your container images, namespace names, description fields (for example, in registry tokens), or in any image configuration data (for example, image names or image labels).
{:tip}


## Pulling images from another registry
{: #registry_images_pulling}

You can pull (download) an image from any private or public registry source, and then tag it for later use in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

<img src="images/images_pull.png" width="800" style="width:800px;" alt="Pull an image from a private or public registry to your computer."/>

**Before you begin**

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in {{site.data.keyword.registrylong_notm}}](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `ibmcloud login` command again.


Download the image, see [Pull an image](index.html#registry_images_pulling) in the Getting Started documentation.

If you get an "unauthorized: authentication required" or a "denied: requested access to the resource is denied" message, run the `ibmcloud cr login` command.
{:tip}


After you pull an image and tag it for your namespace, you can upload (push) the image from your local computer to your namespace.


## Pushing Docker images to your namespace
{: #registry_images_pushing}

You can push (upload) an image to your namespace in {{site.data.keyword.registrylong_notm}} to securely store and share your image with other users.
{:shortdesc}

<img src="images/images_push.png" width="800" style="width:800px;" alt="Push an image from your computer to your private registry."/>

**Before you begin**

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Pull](#registry_images_pulling) or [build](#registry_images_creating) an image on your local computer and tag the image with your namespace information.
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `ibmcloud login` command again.


To upload (push) an image, complete the following steps:

1. Log in to the CLI.

   ```
   ibmcloud cr login
   ```
   {: pre}

   You must log in if you pull an image from your private {{site.data.keyword.registrylong_notm}}.
  {:tip}

2. To view all namespaces that are available in your account, run the `ibmcloud cr namespace-list` command.
3. [Upload the image to your namespace.](index.html#registry_images_pushing)

   If you get an `unauthorized: authentication required` or a `denied: requested access to the resource is denied` message, run the `ibmcloud cr login` command.
   {:tip}


After you push your image to your private registry, you can do one of the following tasks:

- [Manage security with Vulnerability Advisor](../va/va_index.html) to find information about potential security issues and vulnerabilities.
- [Create a cluster and use this image to deploy a container](/docs/containers/container_index.html#container_index) to the cluster in {{site.data.keyword.containerlong_notm}}.


## Copying images between registries
{: #registry_images_copying}

You can pull an image from a registry in one region and push it to a registry in another region so that you can share the image with users in both regions.
{:shortdesc}

<img src="images/images_copy.svg" width="800" style="width:800px;" alt="Copy an image from any  private or public registry to your private {{site.data.keyword.Bluemix_notm}} registry."/>

**Before you begin**

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `ibmcloud login` command again.


To copy an image between two registries, complete the following steps:

1. [Pull an image from a registry](#registry_images_pulling).
2. [Push the image to another registry](#registry_images_pushing). Make sure that you use the correct domain name for the new region you're targeting.

After you copy your image, you can do one of the following tasks:

- [Managing image security with Vulnerability Advisor](../va/va_index.html) to find information about potential security issues and vulnerabilities.
- [Create a cluster and use this image to deploy a container](/docs/containers/container_index.html#container_index) to the cluster in {{site.data.keyword.containerlong_notm}}.


## Building Docker images to use them with your namespace
{: #registry_images_creating}

You can build a Docker image directly in {{site.data.keyword.Bluemix_notm}} or create your own Docker image on your local computer and upload (push) it to your namespace in {{site.data.keyword.registrylong_notm}}.
{:shortdesc}

**Before you begin**

- [Install the CLI](registry_setup_cli_namespace.html#registry_cli_install) to work with images in your namespace.
- [Set up your own namespace in the {{site.data.keyword.registrylong_notm}} private registry](registry_setup_cli_namespace.html#registry_namespace_add).
- [Make sure that you can run Docker commands without root permissions](https://docs.docker.com/engine/installation/linux/linux-postinstall). If your Docker client is set up to require root permissions, you must run `ibmcloud login`, `ibmcloud cr login`, `docker pull`, and `docker push` commands with `sudo`.

  If you change your permissions to run Docker commands without root privileges, you must run the `ibmcloud login` command again.


A Docker image is the basis for every container that you create. An image is created from a Dockerfile, which is a file that contains instructions to build the image. A Dockerfile might reference build artifacts in its instructions that are stored separately, such as an app, the app's configuration, and its dependencies.

If you want to take advantage of {{site.data.keyword.Bluemix_notm}} compute resources and internet connection or Docker is not installed on your workstation, build your image directly in {{site.data.keyword.Bluemix_notm}}. If you need to access resources in your build that are on servers that are behind your firewall, build your image locally.

To build your own Docker image, complete the following steps:

1. Create a local directory where you want to store the build context. The build context contains your Dockerfile and related build artifacts, such as the app code. Navigate to this directory in a command line window.
2. Create a Dockerfile.
  1. Create a Dockerfile in your local directory.

     ```
     touch Dockerfile
     ```
     {: pre}

  2. Use a text editor to open the Dockerfile. At a minimum, you must add the base image to build your image from. Replace _&lt;source_image&gt;_ and _&lt;tag&gt;_ with the image repository and tag that you want to use. If you are using an image from another private registry, define the full path to the image in this private registry.

     ```
     FROM <source_image>:<tag>
     ```
     {: pre}

     **Example**
     To create a Dockerfile that is based on the public {{site.data.keyword.IBM_notm}} {{site.data.keyword.appserver_short}} Liberty (ibmliberty) image, use the following code:

     ```
     FROM registry.<region>.bluemix.net/ibmliberty:latest
     LABEL description="This is my test Dockerfile"
     EXPOSE 9080
      ```
     {: pre}

     This example adds a label to the image metadata and exposes port 9080. For more Dockerfile instructions that you can use, see the [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/).

3. Decide on a name for your image. The image name must be in the following format:

   ```
   registry.<region>.bluemix.net/<my_namespace>/<repo_name>:<tag>
   ```
   {: pre}

   where _&lt;my_namespace&gt;_ is your namespace information, _&lt;repo_name&gt;_ is the name of your repository, and _&lt;tag&gt;_ is the version that you want to use for your image. To find your namespace, run the `ibmcloud cr namespace-list` command.

4. Take note of the path to the directory that contains your Dockerfile. If you run the commands in the following steps while your working directory is set to where your build context is stored, you can replace _&lt;directory&gt;_ with a period (.).
5. Choose to either build your image directly in {{site.data.keyword.Bluemix_notm}} or build and test your image locally before you push it to {{site.data.keyword.Bluemix_notm}}.
  - To build the image directly in {{site.data.keyword.Bluemix_notm}}, run the following command:

    ```
    ibmcloud cr build -t <image_name> <directory>
    ```
    {: pre}

    where _&lt;image_name&gt;_ is the name of your image and _&lt;directory&gt;_ is the path to the directory.
   
   For more information about the `ibmcloud cr build` command, see [{{site.data.keyword.registrylong_notm}} CLI](registry_cli.html).

  - To build and test your image locally before you push it to {{site.data.keyword.Bluemix_notm}}, complete the following steps:
    1. Build the image from your Dockerfile on your local computer and tag it with your image name.

       ```
       docker build -t <image_name> <directory>
       ```
       {: pre}

       where _&lt;image_name&gt;_ is the name of your image and _&lt;directory&gt;_ is the path to the directory.

    2. Optional: Test your image on your local computer before you push it to your namespace.

       ```
       docker run <image_name>
       ```
       {: pre}

       Replace _&lt;image_name&gt;_ with the name of your image.

    3. After you create your image and tag it for your namespace, [you can push your image to your namespace private registry](#registry_images_pushing).

To use Vulnerability Advisor to check the security of your image, see [Managing image security with Vulnerability Advisor](../va/va_index.html).


## Deleting images from your private {{site.data.keyword.Bluemix_notm}} repository
{: #registry_images_remove}

You can delete unwanted images from your private repository by using either the graphical user interface (GUI) or the CLI.
{:shortdesc}

If you want to delete a private repository and its associated images, see [Deleting a private repository and any associated images](#registry_repo_remove).

Public {{site.data.keyword.IBM_notm}} images cannot be deleted from your private {{site.data.keyword.Bluemix_notm}} repository, and do not count towards your quota.

Deleting an image can't be undone. Deleting an image that is being used by an existing deployment might cause scale up, reschedule, or both, to fail.
{:tip}


### Deleting images from your private {{site.data.keyword.Bluemix_notm}} repository by using the CLI
{: #registry_images_remove_cli}

You can delete unwanted images from your private repository by using the CLI.
{:shortdesc}

Deleting an image can't be undone. Deleting an image that is being used by an existing deployment might cause scale up, reschedule, or both, to fail.
{:tip}

To delete an image by using the CLI, complete the following steps:

1.  Log in to {{site.data.keyword.Bluemix_notm}} by running the `ibmcloud login` command.
2.  To delete an image, run the following command:

    ```
    ibmcloud cr image-rm IMAGE
    ```
    {: pre}

    Where _IMAGE_ is the name of the image that you want to remove, in the format `repository:tag`.

    If a tag is not specified in the image name, the image tagged `latest` is deleted by default. You can delete multiple images by listing each private {{site.data.keyword.Bluemix_notm}} registry path in the command with a space between each path.

    To find the names of your images, run `ibmcloud cr image-list`. Combine the content of the Repository and Tag columns to create the image name in the format `repository:tag`.
 {:tip}

3.  Verify that the image was deleted by running the following command, and check that the image does not show in the list.

    ```
    ibmcloud cr image-list
    ```
    {: pre}


### Deleting images from your private {{site.data.keyword.Bluemix_notm}} repository by using the GUI
{: #registry_images_remove_gui}

You can delete unwanted images from your private image repository by using the graphical user interface (GUI).
{:shortdesc}

Deleting an image can't be undone. Deleting an image that is being used by an existing deployment might cause scale up, reschedule, or both, to fail.
{:tip}

To delete an image by using the GUI, complete the following steps:

1.  Log in to the {{site.data.keyword.Bluemix_notm}} console ([https://console.bluemix.net](https://console.bluemix.net)) with your IBMid.
2.  If you have multiple {{site.data.keyword.Bluemix_notm}} accounts, select the account and region that you want to use from the account menu.
3.  Click **Catalog**.
4.  Select the **Containers** category and click the **Container Registry** tile.
5.  Click **Private Repositories**. A list of your private repositories is displayed.
6.  Click the row that contains the repository that contains the image that you want to delete.
7.  In the row that contains the image that you want to delete, click the **open and close list of options** icon, select **Delete Image**. Ensure that you've selected the correct image because this action can't be undone. Click **Delete**.


## Deleting a private repository and any associated images
{: #registry_repo_remove}

You can delete private repositories that are no longer required, and any associated images, by using the graphical user interface (GUI).
{:shortdesc}

When you delete a repository, all images in that repository are deleted. This action can't be undone.
{:tip}

Before you begin, back up any images that you want to keep.

To delete a repository by using the GUI, complete the following steps:

1.  Log in to the {{site.data.keyword.Bluemix_notm}} console ([https://console.bluemix.net](https://console.bluemix.net)) with your IBMid.
2.  If you have multiple {{site.data.keyword.Bluemix_notm}} accounts, select the account and region that you want to use from the account menu.
3.  Click **Catalog**.
4.  Select the **Containers** category and click the **Container Registry** tile.
5.  Click **Private Repositories**. A list of your private repositories is displayed.
6.  In the row that contains the private repository that you want to delete, click the **open and close list of options** icon, select **Delete Repository**. Ensure that you've selected the correct repository because this action can't be undone. Click **Delete**.

