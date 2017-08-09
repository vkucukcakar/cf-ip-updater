# cf-ip-updater

Cloudflare IP updater

* Downloads Cloudflare IPv4 and IPv6 lists and merge
* IP address and list validation just in case
* Compatible with any daemon, server or firewall
* With raw mode, writes IP list to a raw text file, reloads related service
* With csf mode, updates csf.allow and csf.ignore files using IP addresses, reloads csf


## Requirements

* PHP-CLI with openssl extension

## Installation

* Install PHP-CLI with openssl extension if not installed (OS dependent)
	
* Install cf-ip-updater.php to an appropriate location and give execute permission

	$ cd /usr/local/src/

	$ git clone https://github.com/vkucukcakar/cf-ip-updater.git	

	$ cp cf-ip-updater/cf-ip-updater.php /usr/local/bin/
	
* Give execute permission if not cloned from github

	$ chmod +x /usr/local/bin/cf-ip-updater.php
	

## Usage

Usage: cf-ip-updater.php [OPTIONS]

Available options:

-u, --update                          *: Download IP lists and update the configuration files

-f, --force                            : Force update

-r, --reload                           : Trigger reload command on list update

-c < command >, --command=<command>      : Set related service reload command

-t <seconds>, --timeout=<seconds>      : Set download timeout

-n, --nocert                           : No certificate check

-o <filename>, --output=<filename>    *: Write IP list as a new raw text file (old file will be overwritten)

-a <filename>, --allow=<filename>      : Output csf.allow file that csf will use to allow IPs

-i <filename>, --ignore=<filename>     : Output csf.ignore file that lfd will use to ignore IPs

-p, --ports                            : Space separated ports to be used by csf.allow (leave empty for all ports)

-s <urls>, --sources=<urls>            : Override download sources (space separated URLs)

-v, --version                          : Display version and license information

-h, --help,                            : Display usage

 
## Examples

### Examples (raw mode)

	$ cf-ip-updater.php -u -o "/etc/csf-ip-updater.txt"

	$ cf-ip-updater.php -u -o "/etc/csf-ip-updater.txt" --reload --command="myscript.sh"


### Examples (csf mode)


	$ cf-ip-updater.php -u -r

	$ cf-ip-updater.php -u -r --ports="80 443"

	
## Caveats

* The script will run in "raw" mode if -o (--output) option is defined, and in "csf" mode if not defined.

## Nginx users

* If you are planning to use this script with Nginx ngx_http_realip_module, you would better use [ngx-cf-ip](https://github.com/vkucukcakar/ngx-cf-ip )
* If you are planning to use this script with Nginx ngx_http_realip_module and Docker, you would better use the image [vkucukcakar/ngx-cf-ip](https://hub.docker.com/r/vkucukcakar/ngx-cf-ip/ )
