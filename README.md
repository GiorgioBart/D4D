# DfD Docker for Dicer
Docker image for DICER modelling on custom Eclipse 

This project aims to build a Docker image suitable for using the DICER tool  https://github.com/DICERs/DICER in a container.

To obtain this result it was necessary to add some plugin to the default installation of Eclipse and find a way to use Eclipse itself (a GUI application) via Docker.

All started from this Eclipse release: http://eclipse.c3sl.ufpr.br/technology/epp/downloads/release/neon/1a/eclipse-java-neon-1a-linux-gtk-x86_64.tar.gz 

Then via equinox p2 were added the necessary Plugin (Ecore tools,GMF,EMF and the "Eclipse Reflective Ecore Model Diagram Editor"):  
"Installation and updates are managed in Eclipse using a provisioning platform called p2. Fundamentally, p2 is a technology for provisioning and managing Eclipse- and Equinox-based applications."

http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.platform.doc.isv%2Fguide%2Fp2_director.html

The provided equinox_script file show the command line instruction to perform such operation (Provisioning without running the target application).

At the end the necessary instructions to get GUI interface were added to the Docker image.
Actually all was tested only on Ubunu 16.04 with Docker 1.12.2

To connet to the X11 socket the user used by the image and the local user must have the same user and group id (e.g 1000)  
