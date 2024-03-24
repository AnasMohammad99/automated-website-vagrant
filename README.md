# Project Vagrant Environment

## Overview
This Vagrant environment is configured to manage and automate the setup of our development environment.

## Prerequisites
- Vagrant installed on your system
- VirtualBox or another compatible provider

## Vagrantfile
Our `Vagrantfile` is written in Ruby and defines the configuration for our virtual machines. It includes:

- **Multi-Machine Setup**: Loop over VM definitions to apply configurations.
- **Locale Configuration**: Overwrite host locale in SSH sessions to avoid failures.

## Usage
To get started, run the following command in the directory containing the `Vagrantfile`:

```bash
vagrant up
```
## Shell Script Explanation

The shell script included in the `Vagrantfile` performs the following actions to set up a web server and deploy a website:

```bash
<<-SHELL
  sudo apt update                     # Updates the list of available packages and their versions
  sudo apt install apache2 wget unzip zip -y  # Installs Apache2 and utilities for downloading and extracting files
  systemctl start apache2             # Starts the Apache2 service
  systemctl enable apache2            # Enables the Apache2 service to start on boot
  mkdir -p /tmp/finance               # Creates a directory for temporary files during the setup
  cd /tmp/finance                     # Changes the current directory to the newly created directory
  wget https://www.tooplate.com/zip-templates/2135_mini_finance.zip  # Downloads a zip file containing the website template
  unzip -o 2135_mini_finance.zip      # Extracts the zip file, overwriting existing files without prompting
  cp -r 2135_mini_finance/* /var/www/html/  # Copies the extracted files to the Apache2 web root directory
  systemctl restart apache2           # Restarts the Apache2 service to apply changes
  cd /tmp/                            # Changes the directory back to /tmp
  rm -rf /tmp/finance                 # Removes the temporary directory and its contents
SHELL
