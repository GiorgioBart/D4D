# DfD Docker for Dicer
Docker image for DICER modelling on custom Eclipse 

This project aims to build a Docker image suitable for using the DICER tool  https://github.com/DICERs/DICER in a container.

To obtain this result it was necessary to add some plugin to the default installation of Eclipse and find a way to use Eclipse itself (a GUI application) via Docker.

"Installation and updates are managed in Eclipse using a provisioning platform called p2. Fundamentally, p2 is a technology for provisioning and managing Eclipse- and Equinox-based applications."

http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.platform.doc.isv%2Fguide%2Fp2_director.html

The provided equinox_script file show the command line instruction to perform suche operation (Provisioning without running the target application)


