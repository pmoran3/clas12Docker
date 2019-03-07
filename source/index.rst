.. clas12softwarePage documentation master file, created by
   sphinx-quickstart on Thu Jul 26 10:01:44 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. |br| raw:: html

   <br>

|br|

The CLAS12 software packages are distributed using docker images.


Quickstart
==========

Use the following command to run the clas12 software image::

 docker run -it --rm jeffersonlab/clas12simulations:iprod bash


|br|

Software content
================

The clas12simulations docker image contains:
 - "deep" generators
 - gemc with the clas12 geometry
 - CLARA
 - Coatjava
 - the *CLAS12_BIN*, *CLAS12_LIB*, *CLAS12_INC* dirs and environment variables

|br|

Current production version (tag "iprod" or "latest" or no tag):
---------------------------------------------------------------
- clasdis, generate-dis, dvcsgen generator executables
- gemc 4.3.0
- Clara 4.3.3
- Coatjava 5.7.4
- ced 1.06


Tag 1.0:
--------


- gemc 4a.2.5
- Clara 4.3.3
- Coatjava 5b.7.1
- ced 1.06


|br|





Batch mode
==========

Use the following command to open a bash session on the container (the first time you run this it will also download it). You can also replace bash with tcsh::

 
 docker run -it --rm jeffersonlab/clas12simulations:iprod bash

This will open a bash session in the /jlab/workdir directory. See :ref:`various examples <examples>` of running various executables. |br|

|br|

Graphic mode (**browser**)
==========================

Use the following command to pass the 6080 port to noVnc so the container can be opened on a brower::

 docker run -it --rm -p 6080:6080 jeffersonlab/clas12simulations:iprod

Using your web brower open the page::

 http://localhost:6080

After clicking connect the linux desktop is shown with a running shell.|br| |br|


|br| |br|

.. note::

 I suggest to set the noVNC settings as follows:

 - Scaling mode: remote
 - Share mode active (this will ensure if you open another browser session, it will show the same instance of the container)
 - On the docker preferences try to make available as much memory as possible.


|br| |br|

You can stop the docker container at any time with CTRL-C

|br|

Graphic mode (**vnc**)
======================

Use the following command to pass the 5901 and the 6080 ports necessary to open the container with a vnc client::

 docker run -it --rm  -p 6080:6080 -p 5901:5901 jeffersonlab/clas12simulations:iprod

You can now open localhost:5901 with your vnc client.

|br|

Native interactive mode (no opengl)
===================================

On a mac, if you allow access from localhost with::

 1. Activate the option ‘Allow connections from network clients’ in XQuartz settings
    (Restart XQuartz (to activate the setting)
 2. xhost +127.0.0.1

Then you can run docker and use the local X server with::

 docker run -it --rm -e DISPLAY=docker.for.mac.localhost:0 jeffersonlab/clas12simulations:iprod bash

You can run gemc in batch mode this way, but still enjoy the ability to open windows on the local host.

|br|

Mounting your directories to the container
==========================================

The container will always start with the "pristine" image. In other words every work the the container filesystem will be lost when you exit docker.
You can use the option::

 -v /host/directory:/container/directory

to mount your local OS directories to be visible in docker. For example, to mount the "maximilian" home directory in a /max dir in the container::

 docker run -it --rm  -v /home/max:/jlab/work/max jeffersonlab/clas12simulations:iprod bash

*/jlab/work//max* will now point to maximilian home dir. You can save work here.

|br|

Examples
========

.. toctree::
	:maxdepth: 1

	examples

|

Troubleshooting
---------------

- `Solving Docker permission denied while trying to connect to the Docker daemon socket <https://techoverflow.net/2017/03/01/solving-docker-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket/>`_

|



