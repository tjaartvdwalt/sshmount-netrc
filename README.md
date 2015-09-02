# sshmount-netrc

[![PyPI version](https://badge.fury.io/py/sshmount-netrc.svg)](http://badge.fury.io/py/sshmount-netrc)

A small Python script that mounts ssh mount points using authentication from your .netrc (or alternatively .authinfo) file.

## Dependencies

You will need the `sshfs` package installed and in the `PATH`.

On Arch linux it is located in the Community repo. You can install it using:

    pacman -S sshfs

## Installation

    python setup.py install

## Usage

### netrc configuration

Your netrc file should have a line matching the following pattern:

    machine my_server_name    login my_login    password my_password

### command

Its simplest form: 

    sshmount-netrc my_server_name

Specifying a custom mount point:

    sshmount-netrc -m my_mount_point my_server_name

Specifying a custom netrc location:

    sshmount-netrc -f ~/.authinfo my_server_name

### default mount point

If no mount<sub>point</sub> is specified the following default will be used

    ~/mnt/my_login@my_server_name

### result

Under the hood, this script will then execute the following linux commad:

    echo my_password | sshfs -o password_stdin my_login@my_server_name: /my_mount_point

## Limitation

Currently you cannot have multiple logins on one machine. This is due to a long standing shortcoming  in the Python netrc library.
At the time of writing the bug describing it has not been resolved: <http://bugs.python.org/issue11416>
