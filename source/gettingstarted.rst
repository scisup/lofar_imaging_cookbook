Introduction to LOFAR computing facilities [#f1]_
=================================================

------------------------
The LOFAR cluster layout
------------------------

The correlated data coming from the Cobalt [#f2]_ correlator are stored on a cluster of machines called CEP4_ cluster. CEP4_ has been added to the LOFAR offline system at the beginning of 2017. Till December 2016, another cluster of computing machines was used to store and process the data (CEP2). Nowadays, CEP4_ is normally used by the Radio Observatory to process the data through the initial stages of the data reduction (flagging and averaging of the visibilities), while another CEP facility is currently used by both the commissioners and LOFAR users to manually play with the data and understand which strategy to use for the calibration and the imaging: the new  commissioning cluster `CEP3`_.
CEP4_ facility provides technologies that were not available on CEP2, especially with respect to resource management.

In the following sections we will focus on discussing the architecture of CEP facilities as well as their usage policies.

.. _CEP4:

--------------------------------
The LOFAR phase 4 cluster - CEP4
--------------------------------

The LOFAR CEP4 cluster is composed by 50 compute nodes (**cpu01-50**), 4 GPU nodes (**gpu01-04**), 18 storage nodes (**data01-18**), 50 compute nodes (**cpu01-50**), 2 meta-data nodes (**meta01-02**), 2 head nodes (**head01-head02**) and 1 management node (**mgmt01**).
A detailed description of all the packages available on the new cluster and on its network interface can be found on the `wiki <https://www.astron.nl/lofarwiki/doku.php?id=cep4:system>`_. Processed data products will usually made available to the user via the Long-Term Archive, but may also be copied to the `CEP3`_ cluster upon request for further analysis by the user in the original proposal. Due to the intensive nature of the standard data pipelines and the need for these compute resources to be allocated and scheduled by Radio Observatory staff, access to the resources on CEP4 will be strictly limited, with a few exceptions, to the Radio Observatory. In the following, a short description of the computing characteristics/performances of the new cluster is given.

The Lofar Phase 4 cluster consists of:

+ 50 compute nodes (called cpu01..cpu50)
+ 4 GPU nodes (gpu01..gpu04)
+ 18 storage nodes (data01..data18)
+ 2 meta-data nodes (meta01..meta02)
+ 2 head nodes (head01..head02)
+ 1 management node (mgmt01)

Each node is reachable as XXXX.cep4.control.lofar. Users are only allowed on head01 and head02. Each compute node consists of:

+ CPU: Intel Xeon E5-2680v3 2.5 GHz (12 cores, HyperThreading disabled)
+ Memory: 256GB @ 2133 MHz
+ Disk: 2x 300GB 10Krpm SAS RAID
+ Network: 2x 1GbE, 2x 10GbE, 1x FDR InfiniBand

Each GPU node consists of:

+ CPU: Intel Xeon E5-2630v3 2.4 GHz (8 cores, HyperThreading disabled)
+ Memory: 320GB @ 1866 MHz
+ Disk: 2x 300GB 10Krpm SAS RAID + 2x 6TB 7.2Krpm SAS RAID
+ Network: 2x 1GbE, 2x 10GbE, 1x FDR InifiniBand

Each head node consists of:

+ CPU: Intel Xeon E5-2603v3 1.6 GHz (6 cores, HyperThreading disabled)
+ Memory: 128GB at 1600 MHz
+ Disk: 2x 300GB 10Krpm SAS RAID + 2x 6TB 7.2Krpm SAS RAID
+ Network: 2x 1GbE, 2x 10GbE, 1x FDR InifiniBand

The other nodes are not accessible (storage, meta-data, and management nodes).

**Storage:** The storage and meta-data nodes provide about 2PB LustreFS global filesystem through the InfiniBand network to all nodes in the data partition, thus implying that all nodes see the same data.

**Processing:** CEP4 will use a SLURM batch scheduling system to schedule and run all observation and processing jobs on the cluster.

NOTE: It is emphasised again that CEP4 is not meant for commissioning work. For that, commissioners can use CEP3 (see access policies here). It is emphasized that the disks on CEP3 are not intended for long term storage of results. As it is impossible for the Observatory to micro-manage the disk space, commissioners should be aware that disk deletions could happen with very little warning.

----
CEP3
----

The CEP3 cluster is available since November 2014 and allows running science processing close to the CEP4 facility as well as for commissioning work. An overview of the hardware and software as well as of major policies and procedures is available on the `LOFAR wiki <http://www.lofar.org/operations/doku.php?id=cep3:start>`__. The cluster consists of 24 equivalent servers with the following specifications:

+ DELL PowerEdge R720 Rack server
+ Dual Intel Xeon e5 2660 v2 processors (10 cores each)
+ 128 GB memory
+ 4x 8 TB internal disk configured in RAID 6 (24 TB net capacity)
+ 10 GE data interconnect
+ 1 GE management network

In the future the servers can be fitted with up to two GPU cards (e.g. NVIDIA K20X).

Two head nodes (lhd001 & lhd002) are available for logging in and (limited) interactive development and processing purposes. Access to CEP3 can only be done through the **lhdhead.offline.lofar** head node, access to the twenty two worker nodes is managed through a job management system. Users are required to submit requests for processing jobs/sessions on the worker nodes. In general, data will be distributed across the local disks on the worker nodes and processing jobs are distributed accordingly. 

**USAGE POLICY:** Observing, CEP4 processing time and the use of CEP3 are allocated by the LOFAR Programme Committee and the ILT director during the regular proposal evaluation stages, or under Director's Discretionary Time. Access and use of CEP3 is under the sole control of the Radio Observatory's Science Operations & Support (SOS). Access for Users will be granted only at the discretion of the Science Operations & Support. Users should conform to the access, resource allocation and data deletion policies issued by the SOS at all times.

To have access to CEP3 a formal request must be submitted to sos@astron.nl or be explicitly given in a proposal for LOFAR observing time. When submitting a request users should clearly include the following information:

+ A brief explanation of why access to CEP3 is required (e.g., you do not have access to suitable computing resources elsewhere)
+ Project to be worked on (i.e. commissioning, cycle or archived data (post) processing)
+ Description of the kind of processing for which CEP3 access is requested
+ List of collaborators (if any) who should also have access
+ General description of the data to be processed (e.g. data size)
+ Estimated processing time required

Users awarded with access to CEP3 will be able to access the cluster for a limited period of time (2 months by default). The awarded period starts:

+ from the moment the user's data is copied from CEP4 (after Radio Observatory pipeline processing) to CEP3
+ following the timeline communicated to the user via the SOS notification and available on the `wiki <http://www.lofar.org/operations/doku.php?id=cep3:earlyaccess>`__.

At the beginning of a Cycle, users requesting CEP3 processing time in their observing proposals can derive this timeline by checking the observing schedule, which is available `here <http://www.astron.nl/radio-observatory/cycles/cycles>`__. Access timelines related to observing programs involving observations spread in time will be discussed between the PI and Science Support. In general, info about CEP3 access of users are detailed on the LOFAR `wiki <http://www.lofar.org/operations/doku.php?id=cep3:earlyaccess>`__. After the granted period on CEP3 has expired, all users data products generated on the cluster will be automatically and promptly removed, to enable new users to have enough disk space to perform their data reduction.

Extensions to the default 8-weeks period will be granted only in exceptional circumstances and only if properly justified through a formal request to be sent to sos@astron.nl no later than 1 week before the expiration of your access privileges. Monitoring of node usage during allocated time will be performed and the evaluation of extension requests will be based on such statistics.

.. _Logging on to CEP3:

------------------
Logging on to CEP3
------------------

As mentioned above, normal users have access only to CEP3 head node(s), while the access to processing nodes is controlled using the Slurm cluster management software. In the head node users can experience the quality of the data and understand the best approach to use in the lof node(s) for the calibration and imaging of the visibilities. After Science Support has set up a reservation on a particular processing node(s), you should have a reservationID needed for setting up access to the working node(s).

To access CEP3, begin by logging on to **portal.lofar.eu** [#f3]_ ::

   ssh -Y <user name>@portal.lofar.eu

where *<user name>* is likely to be the user's surname.  Type in your default password [#f4]_. Once you are on the portal, you can then log in to the front end (you are requested to use **lhdhead.offline.lofar**) [#f5]_ as ::

   ssh -Y lhdhead.offline.lofar

If this is the first time you will be logging onto the cluster, you are advised to change your password by typing ::

   ypasswd
   
in the usual fashion (old default password, new password, confirm new password).

In order to log on to (for example) **lof019** [#f6]_, start a Slurm job from the head node **lhdhead.offline.lofar**. Any job will do, but we advice starting an interactive bash shell ::

   srun --reservation=<reservationID> -N<nr of nodes> bash -i

This should give you a prompt (or more than one if you have more nodes on your job). Once you have the Slurm job running and log using ssh-keys enabled (see the section on `generating SSH keys`_), you are allowed standard SSH access with X-forwarding to the reserved nodes from the head node starting from a new terminal screen on the head node **lhdhead.offline.lofar** ::

   ssh -XY <user name>@lof019

Once on the compute node, you will be located in your home directory ( */home/<user name>*), which is visible from any node.

For more information on the cluster architecture/properties, see:

+ `LOFAR cluster page on the wiki <http://www.lofar.org/operations/doku.php?id=public:lofar_cluster>`_
+ `CEP3 page on the wiki <http://www.lofar.org/operations/doku.php?id=cep3:start>`_

.. _Setting up your working environment:

-----------------------------------
Setting up your working environment
-----------------------------------

^^^^^^^^^^^^^
Login scripts
^^^^^^^^^^^^^

After an account is created, you will have a separate CEP3 *$HOME* directory. At the first login, it will be empty and needs to be setup properly to be able to use the provided tools and programs on CEP3. Log in to the front end cluster and from your *$HOME* directory follow the approaches reported below.

+ Delete any potential **.profile** or **.cshrc** file that might be in your **$HOME**.
+ Copy over the appropriate **cshrc** or **bashrc** depending on your (t)CSH or BASH login shells. ::

    ln -s /opt/cep/login/cshrc $HOME/.cshrc
    
or ::

    ln -s /opt/cep/login/bashrc $HOME/.profile
    
+ Exit and log in again. You should now see a welcome message.

For BASH, make sure your **.bashrc** is as clean as possible, that means not cluttered with variables (especially LOFARROOT, LD_LIBRARY_PATH & PYTHONPATH should not have -too many- default settings); although this probably applies to (t)csh as well.

The Lofar Login Environment provides a basic environment to run all system-installed packages and tools (like python). Non-system packages have been installed in **/opt/cep** and the software environment can be setup in a flexible way using the `Modules Software Environment Management software <modules.sourceforge.net>`_. This provides a flexible way to load and unload specific packages or versions of packages. Some of the useful *module* command to manipulate the software environment are listed below:

.. csv-table:: Example module commands to manipulate the software environment
   :header: "Command", "Description", "Example"
   
   "module avail", "List all available package and versions", ""
   "module load <package>", "Load a specific package", "'module load lofar'."
   "module load <package>/<version>", "Load a specific version of the package", "module load casa/4.2.1"
   "module list", "List all loaded packages", ""
   "module unload <package>", "Unload a package", "module unload lofar"
   "module purge", "Unload all loaded packages", ""
   "module help", "Display help information", ""
   
Note that loading a particular software package using **module load** will also load other packages that the specified package depends on. For example, ""

    module load lofar
    
will load dependent packages like `casacore <https://github.com/casacore/casacore>`_, `casarest <https://github.com/casacore/casarest>`_, and `python-casacore <https://github.com/casacore/python-casacore>`_.

Also note that the **lofar** module loads the latest stable version of the LOFAR software which is released twice a year. To load an older stable release of LOFAR software, you should load **lofar/<version>**. If you wish to use the latest "daily build" which contains pre-release software that are under active development, you can do so by running **module load lofim**. The pre-release software is built on CEP3 every day and so you load the pre-release software from a specific day by running **module load lofim/<day>**.

Some of the commonly used packages are 

+ aips
+ AOFlagger
+ CASA
+ Sagecal 
+ Dysco
+ Generic pipeline
+ Prefactor
+ Factor
+ PyBDSF
+ DAL
+ DS9
+ Karma 
+ Duchamp
+ LoSoTo
+ LSMTool
+ RMextract
+ RMSynthesis
+ PyRMSynth
+ Wsclean

Detailed information about how to activate and use the above packages can be found on the `LOFAR wiki <https://www.astron.nl/lofarwiki/doku.php?id=cep3:usersoftware>`__.

You can also create a file in your home directory **.mypackages** that contains a list of all packages to initialize at login time. For example, if this file contains the line ::

    casa lofar
    
the login scripts will initialize the CASA and the LOFAR imaging pipeline software for you at login time.

More information about the LOFAR login environment can be found on the `LOFAR wiki <http://www.lofar.org/operations/doku.php?id=public:lle>`__. Also, an updated list of the software packages installed on CEP3 can be found `here <http://www.lofar.org/operations/doku.php?id=cep3:usersoftware>`__.

Processing can now take place. Once you have logged onto this compute node, you should create your own working directory using ::

    mkdir /data/scratch/<username>
    
You can now **cd** into it and use it as your working space. You can copy in here the data provided by the Radio Observatory by e.g. typing::

    > scp -r <user name>@lhdhead.offline.lofar:/data/<user>/<LOFAR dataset> .
    
where **<LOFAR dataset>** has the syntax **LXXXXX** [#f8]_. 

.. _generating SSH keys:

^^^^^^^^^^^^^^^^^^^^^^
Generation of SSH keys
^^^^^^^^^^^^^^^^^^^^^^

We use the Secure Shell (SSH) on the LOFAR Central Processing (CEP) to connect to different systems. This page explains how this can be used without having to supply a password each time you want to connect to a system (very useful to run things such as `BBS <./bbs.html>`_.  on nodes of a cluster, or other remote machines). With normal SSH you always have to give a password. If you use a private and public key, you can access systems where your public key is in **$HOME/.ssh/authorized_keys** from the system where you have the private key.

The following steps will allow you to generate SSH keys on a Linux or OS X machine. From the front end node **lhdhead.offline.lofar** set up passwordless access to the **lof** nodes (if you have a job running to provide you access) via SSH: 

+ create the directory $HOME/.ssh if it does not already exist.
+ The following command allows you to generate the SSH keys ::

    ssh-keygen -t rsa
    
+ The above command creates a set of public and private keys in **$HOME/.ssh**. Copy the public key to **authorized_keys** as ::

    cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

+ Note that **\$HOME/.ssh/authorized_keys** must be available on all the machines you need to access with this key; since your home directory is automatically mounted on all the cluster nodes, they should already be accessible---you can copy it to other, external, systems if required.

See the `LOFAR wiki <http://www.lofar.org/wiki/doku.php?id=public:ssh-usage>`__ for additional information and instructions for a Windows machine.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Disable SSH Host Key Checking
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Normally, when you first connect to a new host, SSH will prompt you for confirmation of the host key::

   $ ssh lof019
   The authenticity of host 'lce019 (10.176.0.19)' can't be established.
   RSA key fingerprint is 73:27:96:cd:f5:04:b7:c3:57:47:49:97:8b:87:8b:15.
   Are you sure you want to continue connecting (yes/no)? 
   
When trying to run a command over many compute (and/or storage) nodes using
multiple SSH connections, that can get pretty annoying. To get around it, set
**StrictHostKeyChecking** to **no** in **\$HOME/.ssh/config**::

   $ cat ~/.ssh/config
   StrictHostKeyChecking no

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Copying data from and to CEP3 cluster
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Data transfers from CEP4 to CEP3 should always be coordinated with the Radio Observatory [#f7]_. Data retrieval from LTA locations as well as from/to other computing facilities is also possible as detailed in `the LOFAR wiki <http://www.lofar.org/wiki/doku.php?id=cep3:userdata>`__. Although access to the CEP3 systems can only be done through the **lhdhead.offline.lofar** head node, data transfers to the outside world can be done directly. *Because data will be transferred via the LOFAR portal, care should be taken not to flood the available network bandwidth with the public internet. Thus we recommend to limit the bandwidth to not disturb the portal access of other users. Note that the portal capacity is 120MB/s*.


.. rubric:: Footnotes

.. [#f1] This chapter is maintained by `M. Iacobelli <mailto:iacobelli@astron.nl>`_.
.. [#f2] It is located in Groningen, The Netherlands.
.. [#f3] The actual host name is lfw.lofar.eu (lfw=LOFAR firewall), but this alias will work fine.
.. [#f4] Your default password will be communicated to you at the moment of the creation of your Lofar account by `Teun Grit <mailto:grit@astron.nl>`_.
.. [#f5] You may have to log out of and log in again to the portal first.
.. [#f6] The Radio Observatory will assign you with a suitable *lof* node to work on.
.. [#f7] sos[at]astron[dot]nl
.. [#f8] **"L"** stays for LOFAR, **XXXXX** is the ID number of the observation, which is assigned to it at the moment of the scheduling.
