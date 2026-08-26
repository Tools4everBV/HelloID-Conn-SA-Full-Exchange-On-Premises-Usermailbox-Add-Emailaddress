# HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-Emailaddress

| :information_source: Information                                                                                                                                                                                                                                                                                                                                                          |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| This repository contains the connector and configuration code only. The implementer is responsible for acquiring the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements. |

## Description

_HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-Emailaddress_ is a template designed for use with HelloID Service Automation (SA) Delegated Forms. It can be imported into HelloID and customized according to your requirements.

By using this delegated form, you can add additional email addresses to Exchange On-Premises user mailboxes. The following options are available:

1.  Search and select a user mailbox by name, alias, or primary SMTP address
2.  Select the email domain from accepted mail domains
3.  Enter the email prefix for the new email address
4.  The email address is validated for uniqueness across all recipients
5.  The new email address is added to the selected user mailbox
6.  All changes are logged with detailed audit information

## Getting started

### Requirements

- **Exchange On-Premises Environment**:<br>
  A working Exchange On-Premises environment with remote PowerShell access enabled. The Exchange server must be accessible from the network where the HelloID agent is running.

- **Exchange Admin Credentials**:<br>
  Administrative credentials with sufficient permissions to query mailboxes, accepted domains, and modify mailbox email addresses. The account must have permissions to execute Get-Mailbox, Get-Recipient, Get-AcceptedDomain, and Set-Mailbox cmdlets.

- **Network Access**:<br>
  Network connectivity from the HelloID agent to the Exchange server's PowerShell endpoint. Ensure firewall rules allow connections to the Exchange Connection URI.

- **PowerShell Remoting**:<br>
  PowerShell remoting must be enabled on the Exchange server. The connector uses New-PSSession to establish remote sessions with the Microsoft.Exchange configuration.

### Connection settings

The following user-defined variables are used by the connector.

| Setting               | Description                                              | Mandatory |
| --------------------- | -------------------------------------------------------- | --------- |
| ExchangeConnectionUri | The URI to the Exchange PowerShell endpoint              | Yes       |
| ExchangeAdminUsername | The username to connect to Exchange (domain\user format) | Yes       |
| ExchangeAdminPassword | The password to connect to Exchange                      | Yes       |

## Remarks

### Email Address Validation Logic

The connector validates email addresses by checking all recipients (users, shared mailboxes, room mailboxes, etc.) in the Exchange environment. If the email address is already assigned to the selected mailbox, the validation passes since the address is already owned by that mailbox. If the email address is in use by a different recipient, the validation fails and displays which recipient is using the address.

### ExchangeGuid Usage

The connector uses ExchangeGuid instead of UserPrincipalName or other identifiers to reference mailboxes in the Set-Mailbox command. This ensures accurate mailbox identification even when UserPrincipalName or other attributes change.

### Session Management

All datasources and tasks use consistent session management with try-catch-finally blocks to ensure proper cleanup. Sessions are automatically disconnected even if errors occur during execution. Only required Exchange cmdlets are imported to minimize overhead.

### Memory Optimization

The connector selects only required mailbox properties to limit memory usage and improve query performance, especially in large Exchange environments with thousands of mailboxes.

### Accepted Domains

The mail domain selector automatically pre-selects the current domain of the selected mailbox when loading accepted domains, making it easier to add alternate addresses in the same domain.

## Development resources

### PowerShell cmdlets

The following Exchange PowerShell cmdlets are used by the connector:

| Cmdlet             | Description                                    | Used In                             |
| ------------------ | ---------------------------------------------- | ----------------------------------- |
| Get-Mailbox        | Retrieves mailbox information                  | Get-Usermailbox-Wildcard-Name-Alias |
| Get-Recipient      | Retrieves recipient information for validation | Check-EmailAddress-Unique           |
| Get-AcceptedDomain | Retrieves accepted mail domains                | Get-All-MailDomains                 |
| Set-Mailbox        | Adds email address to mailbox                  | Task: Add email address             |

### API documentation

- [Exchange Server PowerShell (Exchange Management Shell)](https://learn.microsoft.com/en-us/powershell/exchange/exchange-management-shell)
- [Connect to Exchange servers using remote PowerShell](https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell)
- [Get-Mailbox cmdlet reference](https://learn.microsoft.com/en-us/powershell/module/exchange/get-mailbox)
- [Set-Mailbox cmdlet reference](https://learn.microsoft.com/en-us/powershell/module/exchange/set-mailbox)
- [Get-Recipient cmdlet reference](https://learn.microsoft.com/en-us/powershell/module/exchange/get-recipient)
- [Get-AcceptedDomain cmdlet reference](https://learn.microsoft.com/en-us/powershell/module/exchange/get-accepteddomain)

## Getting help

> :bulb: **Tip:**  
> _For more information on Delegated Forms, please refer to our [documentation](https://docs.helloid.com/en/service-automation/delegated-forms.html) pages_.

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
