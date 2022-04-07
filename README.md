# icy - a command-line Icinga2 API client

## Introduction

This is a lightweight Icinga2 client replacing the features I cared
about in the classic UI, now discontinued.

## Installation

### Set up Icinga2 API

On a Debian machine, username and password are configured in
/etc/icinga2/conf.d/api-users.conf and API in
/etc/icinga2/features-enabled/api.conf .

The API requires SSL wrapping. Again on Debian machines, the certs
go in /var/lib/icinga2/certs/HOSTNAME.crt (a Let's Encypt
fullchain.pem) and /var/lib/icinga2/certs/HOSTNAME.key (Let's Encrypt
privkey.pem).

### Set up client credentials

You will need a credentials file, a JSON file containing keys:

    "host": the Icinga2 machine's hostname
    "port": its API port
    "username": its API username
    "password": its API password

## Operation (icy)

Command-line parameters are:

-c (point to credentials file)

-a ("all") - list all services, even ones that are showing "OK" or on
hosts that are down

-s SERVICE - filter the listed services.

and optionally one or more HOSTNAMES

So for example:

icy - show non-OK services on OK hosts, and host status line for down hosts.

icy -a - show all services on all hosts

icy -s mdraid - show only non-OK "mdraid" services

icy -a -s mdraid - show all "mdraid" services

icy -a wuerfelbrenner - show all services on host wuerfelbrenner

## Operation (icy-downtime)

This uses a restricted subset of the Icinga's downtime functionality.

List current downtimes with:

icy-downtime (-c conffile)

Put HOSTA and HOSTB and all their services into a 2-hour downtime,
effective immediately, with a message:

icy-downtime -d -m "Users are boring" HOSTA HOSTB

For a different duration, append XhYmZs for hours, minutes and seconds
(not all elements are needed).

Remove downtimes on HOSTA and HOSTB:

icy-downtime -u HOSTA HOSTB

Remove downtimes on all hosts:

icy-downtime -u -a

## Todo

- start/end downtime

## Licence

- Gnu GPL v2 (or later, at your discretion)
