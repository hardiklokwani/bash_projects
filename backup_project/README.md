# Project Title

Automated Backup Solutions Using Rsync

## Description

This project is a simple backup solution that uses the `rsync` command to synchronize files from a local machine to a remote virtual machine. `rsync` is a fast and versatile
command-line utility that synchronizes files and directories between two locations over a remote shell, or from/to a remote Rsync daemon.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine and remote virtual machine.

### Prerequisites

- `rsync` installed on both the local machine and the remote virtual machine. If not then :
  ```bash
  sudo apt-get rsync (for Ubuntu)

### Installing

1. Clone the repository to your local machine:

   ```bash
   'git clone https://github.com/hardiklokwani/bash_projects.git`

### Usage

2. Allow the firewall in your remote server to accept requests from your local server’s ip by using:
    ```bash
    sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="<home_server_IP>" accept'
    
3. Configure rsync to connect to your remote virtual machine. Replace <remote_username> and <remote_ip> with your remote machine's username and IP address:
   ```bash
   rsync -avz simple-php-website/ <username@ipaddress_of_remote_server>:Desktop/backup/
   
4. If by any chance you delete some important file. You can simply reverse the commands :
`rsync -avz <username@ipaddress_of_remote_server>:Desktop/backup/ simple-php-website/`

5. Now we will create a job that will run everyday and backup our files.

To create a job we use :

`crontab -e`

and in the editor we type :

`0 0 * * * rsync -avz simple-php-website/ <username@ip_of_remote_server>:Desktop/backup/`


### Advance Backup Strategy


suppose we created a new directory :

`mkdir include-exclude/`

Now we created some .jpg files inside it :

`cd include-exclude` 

`touch file{1..10}.jpg`

This command will create ten .jpg files named from file1 to file10 within the include-exclude directory.

Here, we also create one .php file :

`touch file11.php`

This command will create a .php file named file11 within the include-exclude directory.

Now, let’s assume that we want to backup only the .php file and not the .jpg files then I will use this :

`rsync -avz - -include ‘*.php’ - -exclude ‘*.jpg’ include-exclude/ <username@ip_of_remote_server>:Desktop/backup/`

The `--include` and `--exclude` options allow for more specific control over which files are copied during the rsync operation. The `--include` option will specify the files to be included in the backup, while the `--exclude` option specifies the files to be excluded. It's important to note that the order of these options matters. Rsync processes the include and exclude options in the order they appear. So, if an exclude option appears before an include option for the same set of files, the files will be excluded.

Now we can create a new job :

`crontab -e`

and then :

`0 0 * * * rsync -avz - -include ‘*.php’ - -exclude ‘*.jpg’ include-exclude/ <username@ip_of_remote_server>:Desktop/backup/`

### Contributing

Contributions are welcome. Please submit a pull request with your changes.

### Authors

Hardik Lokwani
