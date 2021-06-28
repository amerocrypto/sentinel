# Amero Sentinel



[![Build Status](https://travis-ci.org/dashpay/sentinel.svg?branch=master)](https://travis-ci.org/dashpay/sentinel)

> An automated governance helper for amero Masternodes.

Sentinel is an autonomous agent for persisting, processing and automating amero governance objects and tasks. It is a Python application which runs alongside the AmeroCore instance on each amero Masternode.

## Table of Contents
- [Install](#install)
  - [Dependencies](#dependencies)
- [Usage](#usage)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Maintainer](#maintainer)
- [Contributing](#contributing)
- [License](#license)

## Install

These instructions cover installing Sentinel on Ubuntu 18.04 / 20.04.

### Dependencies

Update system package list and install dependencies:

    $ sudo apt-get update
    $ sudo apt-get -y install git python3 virtualenv

Make sure Python version 3.6.x or above is installed:

    python3 --version

Make sure the local AmerocCore daemon running is at least version 0.15.0.

    $ amerod --version | head -n1

### Install Sentinel

Clone the Sentinel repo and install Python dependencies.

    $ git clone https://github.com/amerocrypto/sentinel.git && cd sentinel
    $ virtualenv -p $(which python3) ./venv
    $ ./venv/bin/pip install -r requirements.txt

## Usage

Sentinel is "used" as a script called from cron every minute.

### Set up Cron

Set up a crontab entry to call Sentinel every minute:

    $ crontab -e

In the crontab editor, add the lines below, replacing '/path/to/sentinel' to the path where you cloned sentinel to:

    * * * * * cd /path/to/sentinel && ./venv/bin/python bin/sentinel.py >/dev/null 2>&1

### Test Configuration

Test the config by running tests:

    $ ./venv/bin/py.test ./test

With all tests passing and crontab setup, Sentinel will stay in sync with amerod and the installation is complete

## Configuration

An alternative (non-default) path to the `dash.conf` file can be specified in `sentinel.conf`:

    dash_conf=/path/to/dash.conf

## Troubleshooting

To view debug output, set the `SENTINEL_DEBUG` environment variable to anything non-zero, then run the script manually:

    $ SENTINEL_DEBUG=1 ./venv/bin/python bin/sentinel.py


## License

Released under the MIT license, under the same terms as AmeroCore itself. See [LICENSE](LICENSE) for more info.
