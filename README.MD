# Windows Application Uninstaller Ansible Playbook

This repository contains an Ansible Playbook for uninstalling specified Windows applications across your Windows infrastructure using either NTLM or Kerberos for authentication.

## Overview

The Playbook `uninstall_win_app.yml` interacts with Windows hosts to find and uninstall a specified application by its name. The process uses the `win_shell` module to discover the `ProductID` of the application and then uses the `win_package` module to uninstall it.

## Prerequisites

- Ansible 2.9 or higher.
- A Windows environment to run the playbook against.
- Windows Remote Management (WinRM) configured on the target hosts for Ansible.
- Credentials and necessary permissions to uninstall applications on the target Windows hosts.

## Usage

1. Clone the repository to your Ansible control node.
2. Edit the `all_windows_hosts_ntlm.yml` or `all_windows_hosts_kerberos.yml` files in the `group_vars` directory to match your environment and credentials.
3. Edit the `hosts.yml` file and enter the correct hosts.
4. Run the playbook using the following command:

```shell
ansible-playbook uninstall_win_app.yml
```

## Playbook Variables
The Playbook uses the following variable:

- app_name: The name of the application to be uninstalled. This should be set to the exact name of the application as it appears in Windows.


## Group Vars
There are two group var files provided for different authentication methods:

- all_windows_hosts_ntlm.yml: Use this if you prefer NTLM authentication.
- all_windows_hosts_kerberos.yml: Use this if you prefer Kerberos authentication.

Each file contains these variables:

- ansible_user: The username for the connection.
- ansible_password: The password for the connection.
- ansible_connection: Specifies the connection type to use (winrm).
- ansible_port: The port on which WinRM is listening on the target hosts (default is 5985).
- ansible_winrm_transport: The transport method for WinRM (either ntlm or kerberos).

## Security Note
Do not store plaintext passwords in your group_vars files. It is highly recommended to use Ansible Vault to encrypt sensitive information.

## Contributing
Contributions to this playbook are welcome. Please ensure that you update tests as appropriate.

## License
Specify your license or if you're using a standard license like MIT, you can use the corresponding short text.