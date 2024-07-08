---
title: "Apptainer for CMS open data"
teaching: 15
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions 

- What apptainer images are available for my work with the CMS open data?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Download the ROOT and python images and build your own container

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: prerequisites

- Apptainer installed on your remote cluster
- A copy of the container images: Downlowd the sif from [here](https://cernbox.cern.ch/s/eOLXvywJ9EJUP3Q)

::::::::::::::::::::::::::::::::::::::::::::::::


## Overview

This is an optional section for people to try as an alternative to docker. This section will provide an overview of how to use apptainer images on a remote cluster. A pre-requisite to using these images is a pre-existing installation of apptainer. The images have been verified to work. These directions are provided without any guarantees as some tuning on your own side may need to be done with your specific configuration/permission to allow remote windows (e.g., a jupyter-lab browser or a ROOT TBrowser) to open. 

If you intend to use these images during the workshop, please make sure you download the images before the workshop. The images are between about 0.5 to 1 GB, and may take 30 minutes or more to download.


### Python tools container

After you have the pre-requisite .sif images downloaded to your system 

Start the container with

```
apptainer shell python-vnc_python3.10.5.sif
```

You will get a container prompt similar to this:

```
Singularity>
```

This is a bash shell in the container.

You can now open jupyter lab from the container prompt by typing

```
bash jupyter-lab --ip=0.0.0.0 --no-browser
```

The result should be a web link that you can enter into your browser to see your jupyter notebook.

:::::::::::::::::::::::::::::: callout

### Link does not work?

Try replacing `127.0.0.1` in the link with `localhost`.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Click on the Jupyter notebook icon to open a new notebook. 

If this still doesn't work, you may need to modify your ssh file.

Check your config file here by 

```bash
cat ~/.ssh/config
```

If you do not have the above file, create the above file. 
Once you have the file, add the following to it:

```
Host *
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null
```

You can replace * with the name of your cluster. For example, your cluster address might be something like @Computing.Univ.Edu. If you do not know what to do, you can put * and it will apply to any remote connection.

When you log into your cluster, prepend the option -L.

```
ssh -L localhost:8888:localhost:8888 <YOUR USERNAME>@YOUR_CLUSTER_ADDRESS
```

Next go back to the directory where you downloaded the python image and have opened the container. Type the following in the container: 

```
jupyter-lab --no-browser --port=8888 --ip 127.0.0.1
```

The result should be a web link that you can enter into your browser to access your jupyter notebook. Click on the Jupyter notebook icon to open a new notebook. 


:::::::::::::::::::::::::::::: callout

### Still no jupyter notebook?

Check to see if you have a jupyter config file. 

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

To create one, type
```
jupyter notebook --generate-config
```
Change the line 

```
c.ServerApp.open_browser = False
```
to 

```
c.ServerApp.open_browser = True
```

### ROOT tools container

Download the ROOT image from the folder listed [here](https://cernbox.cern.ch/s/eOLXvywJ9EJUP3Q)

Start the container with

```
apptainer shell root-vnc_latest.sif 
```

You will get a container prompt similar to this:

```
Singularity>
```

If you type:
```
root
```
you will get a welcome message, and a root prompt that looks like

```
root [0]
```


::::::::::::::::::::::::::::::::::::: keypoints 

- You have now set up apptainer containers to work with CMS Open Data.
- You know how to open a graphical window of ROOT or a jupyterlab in your browser using software installed in the container.

::::::::::::::::::::::::::::::::::::::::::::::::
