========================================================================
             APISout Standalone Appliance Operations Manual
========================================================================
Product Asset   : APISout High-Throughput Data Normalization Engine
Active Version  : v1.0.0 (Closed Corporate Tier Build)
Vendor Profile  : Apis Labs LLC
Contact Node    : contact@apislabs.net
System Format   : Pre-Compiled Read-Only Container Image Snapshot
========================================================================

SYSTEM REQUIREMENTS:
* Operating System : Cross-Platform Compatibility 
                     - Enterprise Linux (Ubuntu, RHEL, Debian, Rocky)
                     - Microsoft Windows Server / Windows 10 & 11
                     - macOS (Intel & Apple Silicon Architecture)
* Core Container   : Docker Engine (v20.10+), Docker Desktop, or Podman
* Network Binding  : Access requires Port 9001 to be unallocated 
                     (Unless custom re-mapped via initialization)

---

[CRITICAL ENVIRONMENT PREREQUISITES]

Before executing any engine commands, your host computer must have a functional 
container virtualization engine installed and running in the background. If 
your terminal returns a 'command not recognized' error, initialize your 
subsystem using the appropriate checklist below:

For Microsoft Windows Server / Windows 10 & 11:
1. Download the executable bundle from: https://docker.com
2. Run the installer and ensure the WSL 2 backend infrastructure feature is enabled.
3. Launch the Docker Desktop application from your Windows Start Menu.
4. Wait until the status light in the lower-left corner of the dashboard turns solid Green.

For Apple macOS:
1. Download and install Docker Desktop for Mac (select the Intel or Apple Silicon build).
2. Launch Docker from your Applications folder and allow the engine daemon to initialize.

For Enterprise Linux:
1. Install the native Docker engine via your system package manager.
2. Verify the system service controller is active by running: sudo systemctl start docker

---

[DEPLOYMENT INSTRUCTIONS] 2-Step Local Installation Sequence

Follow this terminal sequence exactly to load and spin up the complete
APISout standalone appliance on your corporate server network mesh:

Step 1: Load the Pre-Compiled Binary Image Layers into Your Registry
------------------------------------------------------------------------
Open your system terminal application environment (PowerShell on Windows, 
or Terminal on macOS/Linux), navigate inside this unzipped directory folder 
tree path, and execute the native Docker recovery command to unpack the 
filesystem grid:

  docker load -i apisout-appliance-v1.0.0.tar.gz

Verify that the image is successfully registered under your repository list 
by running 'docker images'. You will see 'apislabs/apisout:1.0.0'.


Step 2: Initialize the Standalone Production Microservice Container
------------------------------------------------------------------------
Execute this run string to map the internal ports and spin up the container:

  docker run -d -p 9001:9001 --restart always --name apisout_core apislabs/apisout:1.0.0

(Note: Linux enterprise hosts may require prepending 'sudo' depending on local system 
group permissions mapping rules).

The application container is now permanently active in the background.

---

[NETWORK CUSTOMIZATION] Changing the External Listening Port

If port 9001 is already allocated or blocked by another corporate firewall 
policy on your host server, you can map the engine to any preferred open 
port (such as 8080 or 80) without modifying internal appliance code. 

To override, adjust the left-hand side of the port flag (-p [HOST]:[CONTAINER]) 
during initialization:

  docker run -d -p 8080:9001 --restart always --name apisout_core apislabs/apisout:1.0.0

Following this re-mapping, the administrative panel will resolve cleanly at 
the custom designated port: http://localhost:8080

---

[INTERFACE LAYOUT] Accessing the Platform Administrative Dashboard

Open any corporate browser page layout on the same network interface and 
navigate straight to the embedded local monitoring control panel:

  http://localhost:9001  (Or your custom mapped port)

* To use a branded internal corporate path scheme rather than localhost, 
  append '127.0.0.1 apisout.local' to your server's /etc/hosts routing table, 
  allowing administrators to access the dashboard panel directly at:
  http://apisout.local:9001

========================================================================
          Copyright (c) 2026 Apis Labs LLC. All Rights Reserved.
========================================================================
