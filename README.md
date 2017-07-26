# csf-cf-ip

Cloudflare IP updater for CSF (ConfigServer Security & Firewall)

* Downloads Cloudflare IPv4 and IPv6 lists and merge
* IP address and list validation just in case
* Updates csf.allow and csf.ignore files using IP addresses
* Reloads csf


## Requirements

* PHP-CLI with openssl extension
* CSF (ConfigServer Security & Firewall)


## Installation

* Install CSF (ConfigServer Security & Firewall) if not installed (OS dependent)

* Install PHP-CLI with openssl extension if not installed (OS dependent)
	
* Install csf-cf-ip.php to an appropriate location and give execute permission

	$ cd /usr/local/src/

	$ git clone https://github.com/vkucukcakar/csf-cf-ip.git	

	$ cp csf-cf-ip/csf-cf-ip.php /usr/local/bin/
	
* Give execute permission if not cloned from github

	$ chmod +x /usr/local/bin/csf-cf-ip.php
	

## Usage

Usage: csf-cf-ip.php [OPTIONS]

Available options:

-u, --update                          *: Download IP lists and update the configuration files

-f, --force                            : Force update

-r, --reload                           : Make csf reload configuration

-c <command>, --command=<command>      : Set csf reload command

-t <seconds>, --timeout=<seconds>      : Set download timeout

-n, --nocert                           : No certificate check

-p, --ports                            : Space separated ports to be used by csf.allow

-a <filename>, --allow=<filename>      : Output csf.allow file that csf will use to allow IPs

-i <filename>, --ignore=<filename>     : Output csf.ignore file that lfd will use to ignore IPs

-s <urls>, --sources=<urls>            : Override download sources (space separated URLs)

-v, --version                          : Display version and license information

-h, --help,                            : Display usage

 
## Examples

	$ csf-cf-ip.php -r

	$ csf-cf-ip.php -r -a "/etc/csf/csf.allow" -i "/etc/csf/csf.ignore"

	$ csf-cf-ip.php --reload --command="csf -r" --allow="/etc/csf/csf.allow" --ignore="/etc/csf/csf.ignore"

	
## Caveats

* csf reload command can be platform dependent. That's why there is a --command parameter implemented.
