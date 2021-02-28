<!--


  ** DO NOT EDIT THIS FILE
  **
  ** 1) Make all changes to `README.yaml`
  ** 2) Run`make readme` to rebuild this file.
  **
  ** (We maintain HUNDREDS of open source projects. This is how we maintain our sanity.)
  **


  -->

# ansible-role-pureftpd

[![Build Status](https://travis-ci.org/hadenlabs/ansible-role-pureftpd.svg?branch=main)](https://travis-ci.org/hadenlabs/ansible-role-pureftpd) [![Issues](https://img.shields.io/github/issues/hadenlabs/ansible-role-pureftpd.svg)](https://github.com/hadenlabs/ansible-role-pureftpd/issues) [![Latest Release](https://img.shields.io/github/release/hadenlabs/ansible-role-pureftpd.svg)](https://travis-ci.org/hadenlabs/ansible-role-pureftpd/releases)

Installs Pure-FTPd on Debian/Ubuntu Linux.

This role installs and configures the latest version of Pure-FTPd from the Pure-FTPd via apt (on Debian-based systems). You will likely need to do extra setup work after this role has installed Pure-FTPd.

This project is part of our comprehensive [hadenlabs](https://hadenlabs.com) roles of ansible.

It's 100% Open Source and licensed under the [MIT](LICENSE).

## Requirements

None.

## Usage

```bash
make setup
```

## Quick Start

<no value>

## Examples

### common

```hcl

  - hosts: server
    roles:
      - role: hadenlabs.pureftpd

```

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yaml`):

    pure_ftpd_root: "/var/ftp"

A directory path at which to scope the FTP server access.

    pure_ftpd_user: "ftp"

The system-level user that the FTP daemon performs operations under. This user is setup without login permissions (can't ssh into system) but owns all of the files uploaded via the FTP server.

    pure_ftpd_group: "ftp-sys-group"

The system-level group that the FTP daemon performs operations under. This is the group assigned to all files uploaded via the FTP server.

    pure_ftpd_vusers:
      - name: "ftp"
        password: "FTPisSoC00l?"
        dir: "/var/ftp" # optional

A list of user definitions virtual FTP users. If left empty, defaults to a single user with the username `ftp` and password `ftp`. `name` and `password` are required fields. `dir` is optional and defaults to the value of `ftp_root`.

Since the array of `virtual_users` needs to contain secret credentials, it is recommended to create an [Ansible Vault][vault]-encrypted variable file to include that contains your users and overrides the role default vars.

    pure_ftpd_tls: true

Turns on/off support for FTP TLS encryption. It is strongly recommended that this remain `true`.

    pure_ftpd_allow_insecure: false

When TLS encryption is enabled, the default is to not allow non-encrypted, insecure connections. Setting this value to `true` will allow both secure and insecure connections. Requires that `enable_tls` be `true`.

    pure_ftpd_pem: ""

The contents of the PEM certificate to use for FTP TLS encryption. It is recommended to create an [Ansible Vault][vault]-encrypted variable file to include that contains your PEM certificate.

If no `pure_ftpd_pem` is provided, a PEM certificate is generated using `openssl`.

    pure_ftpd_openssl_config: {}

The `openssl_config` vars object controls the generation of an openssl PEM certificate + key combination.

The sub-properties of the `openssl_config` object are as follows:

      days: "365"

The number of days for which the certificate is valid.

      size: "2048"

The size of the certificate key. The larger, the more secure.

      country: ""
      state: ""
      locality: ""
      org: ""
      unit: ""
      common: ""
      email: ""

The values of the certificate subject information.

## Help

**Got a question?**

File a GitHub [issue](https://github.com/hadenlabs/ansible-role-pureftpd/issues), send us an [email][email] or join our [Slack Community][slack].

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/hadenlabs/ansible-role-pureftpd/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://hadenlabs.com) with our other projects, we would love to hear from you! Shoot us an [email](mailto:support@hadenlabs.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

1.  **Fork** the repo on GitHub
2.  **Clone** the project to your own machine
3.  **Commit** changes to your own branch
4.  **Push** your work back up to your fork
5.  Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to rebase the latest changes from "upstream" before making a pull request!

### Versioning

Releases are managed using github release feature. We use [Semantic Versioning](http://semver.org) for all the releases. Every change made to the code base will be referred to in the release notes (except for cleanups and refactorings).

## Copyright

Copyright © 2018-2021 [Hadenlabs](https://hadenlabs.com)

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

The MIT License (MIT)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Source: <https://opensource.org/licenses/MIT>

## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

This project is maintained and funded by [Hadenlabs][https://hadenlabs.com]. Like it? Please let us know at <support@hadenlabs.com>

### Contributors

| [![Luis Mayta][luismayta_avatar]][luismayta_homepage]<br/>[Luis Mayta][luismayta_homepage] |
| ------------------------------------------------------------------------------------------ |

[luismayta_homepage]: https://github.com/luismayta
[luismayta_avatar]: https://github.com/luismayta.png?size=150
