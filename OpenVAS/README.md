# OpenVAS Documentation 

## Install - Docker

```bash
sudo apt update

sudo apt install docker.io

sudo docker run -d -p 443:443 --name openvas mikesplain/openvas
```

## Create a Scan

1. Within OpenVAS, click on Scans, then Tasks. (You can close out the pop-up welcome message)

2. Click on the star icon and select New Task.

3. Fill out the following scan information:
  - Name: LabScan Scan Targets: (click on the star icon next to "Target)", replace "unnamed" with "localhost", then click "Create".
  - Schedule: Check the box next to "Once" Alterable Task: Mark "Yes"

4. Click the Create button.
