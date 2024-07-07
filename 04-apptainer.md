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

## Overview

This is an optional section for people to try as an alternative to docker. This section will provide an overview of how to use apptainer images on a remote cluster. A pre-requisite to using these images is a pre-existing installation of apptainer. These directions are provided without any guarantees. The images have been verified to work. However, some tuning may need to be done with your specific configuration/permission to allow remote windows (e.g., a jupyter-lab browser or a ROOT TBrowser) to open. 


### Python tools container

Download the python image from the folder listed [here](https://cernbox.cern.ch/s/eOLXvywJ9EJUP3Q)

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

You can replace * with the name of your cluster. For example, the your cluster address might be Computing.Univ.Edu. If you do not know what to do, you can put * and it will apply to any remote connection.

When you log into your cluster, prepend the option -L.

```
ssh -L localhost:8888:localhost:8888 <YOUR USERNAME>@YOUR_CLUSTER_ADDRESS
```

Next go back to the directory where you downloaded the python image. Type the following: 

```
jupyter-lab --no-browser --port=8888 --ip 127.0.0.1
```

Click on the Jupyter notebook icon to open a new notebook. 

If you still are having issues, check to see if you have a jupyter config file. To create one, do
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
