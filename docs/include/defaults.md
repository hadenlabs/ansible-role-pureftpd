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
