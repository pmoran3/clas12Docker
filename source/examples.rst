
.. |br| raw:: html

   <br>



.. _examples:

.. note::

   In the examples below, the local user directory "max" is made available to the docker image with the mount directive::

     -v /home/max:/jlab/work/max

.. _runningGEMCExample:


Running GEMC
============

Run the container in batch mode (substitute the max's path with your home dir path)

 docker run -it --rm  -v /home/max:/jlab/work/max jeffersonlab/clas12simulations:iprod bash

Use the internal generator
--------------------------

Use the clas12.gcard in /jlab/workdir to launch gemc. For example, to run 200 events in batch mode using 4 GeV electrons at theta=20 degrees and phi=5 degrees::

 gemc -USE_GUI=0 -INPUT_GEN_FILE="lund, dvcs.lund" -N=200 -BEAM_P="e-, 4*GeV, 20*deg, 5*deg"

|br|

Use a LUND generated file
-------------------------

Use the clas12.gcard in /jlab/workdir to launch gemc. For example, to run 200 events in batch mode using
generated events in a `lund file <https://gemc.jlab.org/gemc/html/documentation/generator/lund.html>`_ in the local directory /home/max (mounted in /jlab/work/max)::

 cd /jlab/work/max
 gemc -USE_GUI=0 -INPUT_GEN_FILE="lund, dvcs.lund" -N=200 /jlab/work/clas12.gcard

This will produce an output with 200 generated events in evio format.

|br|

.. _runningevio2hipoExample:

Convert GEMC evio output to hipo
================================

Use evio2hipo to convert the gemc output into hipo.

Notice that the field maps scaling are -1 for standard gcard settings, but make sure you match the values if you are not using the provided gcard::

 evio2hipo -r 11 -t -1.0 -s -1.0 -i out.ev -o gemc.hipo

- Tours: -1 = inbending electrons
- Solenoid -1: = field points upstream
- Run geometry 11: = default simulation geometry run number


|br|

.. _runningCoatjaveExample:

Reconstruction
==============

Use the script "createCookClara" in your path to setup the input file, output directory and (optional) the number of threads::

 createClaraCook.csh gemc.hipo 4

This will create the setup file "cook.clara".

Then run clara-shell to launch reconstruction::

 clara-shell cook.clara
