# containers
Each folder contains a makefile for creating and running podman containers as systemd services.

## Pi-hole
Pi-hole is a network-level advertisement and Internet tracker blocking application
* Create container
  ```
  sudo make create [--ipaddr=192.168.1.2] [--password=foo123]
  ```

* Install as a systemd service and run container
  ```
  sudo make service start
  ```

## Unifi
UniFi Network Controller for managing network devices from Ubiquiti  
* Create container
  ```
  sudo make create [--ipaddr=192.168.1.2]
  ```

* Install as a systemd service and run container
  ```
  sudo make service start
  ```
