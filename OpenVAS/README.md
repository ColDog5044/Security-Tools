# OpenVAS Documentation (This Documentation is out-of-date. Use the Docker method instead.)

## Install - Debian

```bash
sudo add-apt-repository ppa:mrazavi/openvas
sudo apt-get update
sudo apt-get install -y sqlite3
sudo apt-get install -y openvas9
sudo service openvas-manager restart
```

## Create a Scan

1. Within OpenVAS, click on Scans, then Tasks. (You can close out the pop-up welcome message)

2. Click on the star icon and select New Task.

3. Fill out the following scan information:
  - Name: LabScan Scan Targets: (click on the star icon next to "Target)", replace "unnamed" with "localhost", then click "Create".
  - Schedule: Check the box next to "Once" Alterable Task: Mark "Yes"

4. Click the Create button.
