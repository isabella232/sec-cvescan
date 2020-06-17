# CVEScan

The Ubuntu Security Team at Canonical regularly publishes a JSON file containing
information about packages with security updates. The source of the information is
the [Ubuntu CVE Tracker](https://launchpad.net/ubuntu-cve-tracker). The information
contained in the JSON file is similar to the information published in OVAL files but
the format is designed specifically to work with the CVEScan tool.

## About CVEScan

CVEScan is a python script that downloads the JSON file described above
and uses it to compare versions of packages with security fixes to version of packages
installed on your Ubuntu system or listed in a package manifest file. CVEScan produces
a useful report that tells you if you are missing any security patches.

## Using CVEScan

The recommended way to use CVEScan is by using the snap.
```
sudo snap install cvescan
```
```
cvescan
```

There is more detailed usage information in the help.
```
$> cvescan -h

usage: cvescan [-h] [-c CVE-IDENTIFIER] [-p {critical,high,medium,all}] [-s]
               [-u UCT_FILE] [-m MANIFEST_FILE] [-n] [--show-links]
               [--unresolved] [-v] [-x]

Scan an Ubuntu system for known vulnerabilities.

optional arguments:
  -h, --help            show this help message and exit
  -c CVE-IDENTIFIER, --cve CVE-IDENTIFIER
                        Report if this system is vulnerable to a specific CVE.
  -p {critical,high,medium,all}, --priority {critical,high,medium,all}
                        'critical' = show only critical CVEs.
                        'high'     = show critical and high CVEs (default)
                        'medium'   = show critical and high and medium CVEs
                        'all'      = show all CVES (no filtering based on priority)
  -s, --silent          Enable script/Silent mode: To be used with '-c <cve-identifier>'.
                        Do not print text output; exit 0 if not vulnerable, exit 1 if vulnerable.
  -u UCT_FILE, --uct-file UCT_FILE
                        Specify an UCT JSON file to use instead of downloading the latest from people.canonical.com.
  -m MANIFEST_FILE, --manifest MANIFEST_FILE
                        Enable manifest mode. Do not scan the localhost. Instead, run a scan against the
                        specified package manifest file.
                        Note: Package manifest files can be generated by running
                              `dpkg-query -W > manifest.txt` on the host you wish to scan.
  -n, --nagios          Enable Nagios mode for use with NRPE.
                        Typical nagios-style "OK|WARNING|CRITICAL|UNKNOWN" messages
                         and exit codes of 0, 1, 2, or 3.
                        0/OK = not vulnerable to any known and patchable CVEs of the
                         specified priority or higher.
                        1/WARNING = vulnerable to at least one known CVE of the specified
                         priority or higher for which there is no available update.
                        2/CRITICAL = vulnerable to at least one known and patchable CVE of
                         the specified priority or higher.
                        3/UNKNOWN = something went wrong with the script, or oscap.
  --show-links          Provide links to the Ubuntu CVE Tracker for each CVE.
  --unresolved          Show CVEs that have not yet been resolved.
  -v, --verbose         Enable verbose messages.
  -x, --experimental    Enable eXperimental mode. Use experimental (also called "alpha") data
                        from the Ubuntu CVE tracker. The alpha UCT files include information about
                        package updates available for users of Ubuntu Advantage running systems
                        with ESM Apps and ESM Infra enabled.
```

## Running CVEScan from Source

If you have cloned this repo you can also run CVEScan as a python script.
```
python3 -m cvescan
```

Or, you can install it as a python module.
```
pip3 install --user .
```

## Development

### Installing precommit hooks
To install the precommit hooks, run

    pip3 install --user pre-commit
    ~/.local/bin/pre-commit install

### Running the test suite
You can run the automated test suite by running

    python3 setup.py test.

An HTML code coverage report will be generated at `./htmlcov`. You can view
this report by running

    firefox ./htmlcov/index.html
