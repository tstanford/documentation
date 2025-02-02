# Linux

Tim Stanford

This is my reference document with tips and tricks that I have discovered while working with linux.

- [Linux](#linux)
  - [User Management](#user-management)
    - [Add a new user](#add-a-new-user)
    - [Add a user to a group](#add-a-user-to-a-group)
  - [Make a full nested directory structure](#make-a-full-nested-directory-structure)
  - [SSH](#ssh)
    - [Make a connection to a server as another user using a private key](#make-a-connection-to-a-server-as-another-user-using-a-private-key)
    - [Make a connection and ignore host check checking](#make-a-connection-and-ignore-host-check-checking)
  - [File permissions for the .ssh profie](#file-permissions-for-the-ssh-profie)
  - [Creating an SSH keypair](#creating-an-ssh-keypair)
  - [Displaying exports available for an NFS server](#displaying-exports-available-for-an-nfs-server)
  - [Show all mounted filesystems:](#show-all-mounted-filesystems)
  - [Show all mounted filesystems in a tree:](#show-all-mounted-filesystems-in-a-tree)
  - [Encrypting STDIN](#encrypting-stdin)
  - [Decrypting STDIN](#decrypting-stdin)
  - [recursive search and replace from command line](#recursive-search-and-replace-from-command-line)
  - [Create a new linux drive using a specific UUID](#create-a-new-linux-drive-using-a-specific-uuid)
  - [Resize a disk](#resize-a-disk)
  - [Linux permissions](#linux-permissions)
    - [change owner leaving group owner intact](#change-owner-leaving-group-owner-intact)
    - [change owner to slde99 and group to slde99](#change-owner-to-slde99-and-group-to-slde99)
    - [change group for file](#change-group-for-file)
    - [set userid (suid)](#set-userid-suid)
  - [kill processes for a specific user](#kill-processes-for-a-specific-user)
  - [find out the real pathname of a symlink, recursively.](#find-out-the-real-pathname-of-a-symlink-recursively)
  - [find out the real pathname of a file](#find-out-the-real-pathname-of-a-file)
  - [Get delimited list of hosts with a specific prefix and pass it to a custom script](#get-delimited-list-of-hosts-with-a-specific-prefix-and-pass-it-to-a-custom-script)
  - [yum download only](#yum-download-only)
  - [Recursive Search and replace](#recursive-search-and-replace)
  - [Recursively set all directories with execute access](#recursively-set-all-directories-with-execute-access)
  - [List running services](#list-running-services)


## User Management

### Add a new user

    useradd [username]

### Add a user to a group

The `-a` switch indicates that you wish to assign an *additional* group for the user. If you miss this out, you're specifying that the user will only have this group. So be careful!

    usermod -a -G [group] [user]

On RHEL, users with permissions to run commands as root using sudo will need to be part of the `wheel` group.

## Make a full nested directory structure

    mkdir -p /opt/mgmt/mytools/something

## SSH

### Make a connection to a server as another user using a private key

    ssh user@server -i /path/to/privatekey

### Make a connection and ignore host check checking

    ssh server -o "StrictHostKeyChecking=no"

This setting can also be added to the ssh configuration file. Either the user or global configuration file. `~/.ssh.config` or `/etc/ssh/ssh_config`

    Host *
        StrictHostKeyChecking no

The host key will still be added to the known_hosts file. This could be a problem is the server you are connecting to is rebuild with a different host key. The SSH connection will fail with a warning about a man in the middle attack (or something like that).

It is possible to prevent the key being added to the known_hosts file by adding `UserKnownHostsFile /dev/null` to the config file.

    Host *
        StrictHostKeyChecking no
        UserKnownHostsFile /dev/null

## File permissions for the .ssh profie

Each user can have an SSH profile that is unique to them. This profile consists of an .ssh directory in their home directory and several files consisting of public and private keys, connection configuration, known keys, authorized keys.

It is important that this directory and the files within are owned by the user that owns the home directory. The permissions should be set so that only the user can access these files.

* The directory `~/.ssh` should be set with `chmod 700`
* The files within `~/.ssh` should be set with `chmod 600`

## Creating an SSH keypair

To generate an SSH key pair, use the following account. You may need to create the directory ~/.ssh. When prompted for locations and passphrases, just go with the defaults by hitting enter.

    ssh-keygen

## Displaying exports available for an NFS server

On the client:

    showmount -e [servername]

Example:

    showmount -e wbp-testzone-nfs2

Output:

    Export list for wbp-testzone-nfs2:
    /opt/vebnet/mgmt/v2-ng *
    /opt/vebnet/mgmt/v3-di *
    /opt/vebnet/mgmt/v3-ng *
    /opt/vebnet/mgmt/v3-qa *
    /opt/vebnet/mgmt/v3-ci *

## Show all mounted filesystems:

    mount

## Show all mounted filesystems in a tree:

    findmnt

## Encrypting STDIN

    echo hello | openssl enc -e -aes256 > outfile

## Decrypting STDIN

    cat outfile | openssl enc -d -aes256

## recursive search and replace from command line

    grep -rl LIVE_META | xargs sed -i 's/LIVE_META/LIVE_I3_META/g'

## Create a new linux drive using a specific UUID

Find the device name using:
    lsblk

Omit UUID to let linux create a new one.

    sudo -s
    parted /dev/sdb mklabel gpt
    parted -a opt /dev/sdb mkpart ext4 0% 100%
    mkfs.ext4 -L nfsexports /dev/sdb1 -U 5fe730d9-6c03-486b-ad5f-3086cc2e5018

## Resize a disk

    sudo -s
    umount /var/wbp
    parted /dev/sdb resizepart 1 100%
    resize2fs /dev/sdb1
    mount /var/wbp

## Linux permissions

### change owner leaving group owner intact

    chown slde99 filename

### change owner to slde99 and group to slde99

    chown slde99: filename

### change group for file

    chown :deployers filename

### set userid (suid)

    chmod u+s myscript.sh

## kill processes for a specific user

    ps -aux | grep stuartl | awk '{print $2}' | sudo xargs kill

## find out the real pathname of a symlink, recursively.

    readpath -f [name]

## find out the real pathname of a file

    realpath [name]

## Get delimited list of hosts with a specific prefix and pass it to a custom script

    cat /etc/hosts | grep wbp-i- | awk '{print $2}' | xargs ./run.sh

## yum download only

    yum install --downloadonly --downloaddir=<directory> <package

## Recursive Search and replace

    find . -type f -exec sed -i 's/hello/bye/g' "{}" +;

## Recursively set all directories with execute access
    find /path/to/base/dir -type d -exec chmod 750 {} +

## List running services

    systemctl list-unit-files --type service -all

## Use journalctl 

### View errors ordered by more recent.

sudo journalctl -p 0..4 -r

| n | type     |
| - | -------- | 
| 0 | emerg    | 
| 1 | alert    |
| 2	| crit     |
| 3	| err      |
| 4	| warning  |
| 5	| notice   |
| 6 | info     |
| 7 | debug    |
