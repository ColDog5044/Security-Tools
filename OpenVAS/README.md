# OpenVAS Documentation 

## Install - Docker

```bash
sudo apt update

sudo apt install docker.io

sudo docker run -d -p 443:443 -p 9390:9390 -e OV_PASSWORD=securepass123 --name openvas mikesplain/openvas
```

## Docker commands

### Check status of the process:

    docker top openvas

## Run bash inside the container:

    docker exec -it opencas bash

## Create a Scan

Username: admin
Password: admin

https://127.0.0.1

1. Within OpenVAS, click on Scans, then Tasks. (You can close out the pop-up welcome message)

2. Click on the star icon and select New Task.

3. Fill out the following scan information:
  - Name: LabScan Scan Targets: (click on the star icon next to "Target)", replace "unnamed" with "localhost", then click "Create".
  - Schedule: Check the box next to "Once" Alterable Task: Mark "Yes"

4. Click the Create button.
