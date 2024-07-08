---
title: "Apptainer for CMS open data"
teaching: 15
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions 

- What apptainer images are available for my work with the CMS open data?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Download the ROOT and python images and launch the containers on a remote cluster

::::::::::::::::::::::::::::::::::::::::::::::::


## Prerequisites

::::::::::::::::::::::::::::::::::::: callout

### pre-requisites

- Apptainer installed on your remote cluster
- A copy of the ROOT and Python container images: Downlowd the .sif files from [here](https://cernbox.cern.ch/s/eOLXvywJ9EJUP3Q)

::::::::::::::::::::::::::::::::::::::::::::::::


## Introduction

This is an optional section for you to try out as an alternative to docker. This section will provide an overview of how to use `apptainer` images on a remote cluster. Apptainer is a package that many clusters install to manage containerized software, particularly if a batch job system is connected to the cluster. If your cluster has Apptainer available, you can use our Open Data toolkits without requesting additional software installation on the cluster itself. 

Although the images have been verified to work, additional work may need to be done on your side to tune your specific configurations/permissions to allow remote windows (e.g., a jupyter-lab browser or a ROOT TBrowser) to open. If you intend to use these images during the workshop, please make sure you download the images before the workshop. The images are between about 0.5 to 1 GB, and may take 30 minutes or more to download.

## Python tools container

After you have the pre-requisite .sif images downloaded to your system, copy them onto the remote cluster that you will use to analyze Open Data, perhaps using `scp`.

Start the Python container with:

```bash
apptainer shell python-vnc_python3.10.5.sif
```

You will get a container prompt similar to this:

```output
Singularity>
```

This is a bash shell in the container. You can now open jupyter lab from the container prompt by typing

```bash
Singularity> jupyter-lab --ip=0.0.0.0 --no-browser
```

The result should be a web link that you can enter into your browser to see your jupyter notebook. Click on the Jupyter notebook icon to open a new notebook.

:::::::::::::::::::::::::::::: callout

### Link does not work?

Try replacing `127.0.0.1` in the link with `localhost`. 

If that change doesn't work, you may need to modify your ssh file and remote cluster login command. Check the ssh config file on your local computer (not the remote cluster):

```bash
cat ~/.ssh/config
```

Add the following lines to your config file (you can create the file if it does not exist):

```
Host *
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null
```

You can replace * with the name of your cluster. For example, your cluster address might be something like @Computing.Univ.Edu. If you do not know what to do, you can put * and it will apply to any remote connection.
When you log into your cluster, prepend the option -L and provide ports for displays:

```bash
ssh -L localhost:8888:localhost:8888 <YOUR USERNAME>@YOUR_CLUSTER_ADDRESS
```

Next go back to the directory where you downloaded the python image and have opened the container. Type the following in the container: 

```bash
Singularity> jupyter-lab --no-browser --port=8888 --ip 127.0.0.1
```

The result should be a web link that you can enter into your browser to access your jupyter notebook. Click on the Jupyter notebook icon to open a new notebook. 

### Still no jupyter notebook?

Check to see if you have a jupyter config file. To create one, log in to the remote cluster and enter the apptainer shell. Then execute:

```bash
Singularity> jupyter-lab --generate-config
```
It will print out the path to a `jupyter_lab_config.py` file, which may be in your home directory outside the apptainer shell in `.jupyter/jupyter_lab_config.py`. Change the line:

```
c.ServerApp.open_browser = False
```
to 

```
c.ServerApp.open_browser = True
```

Then try again to open the juypter notebook from the jupyter lab webpage.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## ROOT tools container

Download the ROOT image from the folder listed [here](https://cernbox.cern.ch/s/eOLXvywJ9EJUP3Q) and copy it onto your remote cluster.

Start the container with:

```bash
apptainer shell root-vnc_latest.sif 
```

You will get a container prompt similar to this:

```output
Singularity>
```

If you type:
```bash
Singularity> root
```
you will get a welcome message, and a root prompt that looks like

```bash
Singularity> root [0]
```
## Exercises

:::::::::::::::::::::::::: challenge

## Homework: confirm your containers work

Please visit the [assignment form](https://docs.google.com/forms/d/e/1FAIpQLSdxsc-aIWqUyFA0qTsnbfQrA6wROtAxC5Id4sxH08STTl8e5w/viewform) and answer a few questions about your container. You need to sign in and <strong style="color: red;">click on the submit button</strong> in order to save your work.  You can go back to edit the form at any time.

::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::: challenge

## Challenges from the previous episode

If you skipped the previous episode because you are working on a remote cluster, [go back one page](03-docker-for-cms-opendata.md#exercises) and try the exercises using apptainer. The main goal of these exercises is to make sure you are able to execute important commands inside the containers and access stored files. If you need help, contact us in Mattermost.

::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

- You have now set up apptainer containers to work with CMS Open Data.
- You know how to open a graphical window of ROOT or a jupyterlab in your browser using software installed in the container.

::::::::::::::::::::::::::::::::::::::::::::::::
