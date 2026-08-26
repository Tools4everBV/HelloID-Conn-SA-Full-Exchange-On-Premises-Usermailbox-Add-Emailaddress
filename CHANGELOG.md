# Changelog

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [2.0.0] - 2026-08-26

### Added

- Added datasource `Exchange-On-Premises-Get-All-MailDomains` to retrieve and select accepted mail domains with automatic pre-selection of current mailbox domain
- Added datasource `Exchange-On-Premises-Get-Usermailbox-Wildcard-Name-Alias` with improved filtering for user mailboxes using RecipientTypeDetails
- Added datasource `Exchange-On-Premises-Check-EmailAddress-Unique` with enhanced validation logic that distinguishes between email addresses in use by the selected mailbox versus other recipients
- Added mailPrefix and mailDomain properties to mailbox objects for better form handling
- Added ExchangeGuid property to mailbox selection for more reliable identity management
- Added HiddenFromAddressListsEnabled column to mailbox selection grid
- Added actionMessage variable for better error context tracking throughout all scripts
- Added finally blocks to all datasources for guaranteed session cleanup
- Added property selection limiting to reduce memory usage and improve performance
- Added authentication parameter to session creation for explicit authentication method

### Changed

- Refactored form from 2 datasources to 3 specialized datasources with clearer separation of concerns
- Changed mailbox identity reference from UserPrincipalName to ExchangeGuid in task execution
- Changed email validation to use Get-Recipient instead of Get-Mailbox for comprehensive recipient checking
- Changed session management to use parameter splatting for improved readability and maintainability
- Changed Import-PSSession to import only required commands instead of all commands
- Changed session option parameters to explicitly set SkipCACheck, SkipCNCheck, and SkipRevocationCheck to false
- Changed form field names for consistency (gridMailbox to selectedmailbox, searchMailbox to searchValue)
- Changed grid columns to display DisplayName first and removed Alias column
- Changed filter logic to use RecipientTypeDetails for precise mailbox type filtering
- Updated audit logging to use InstanceId instead of GUID for session tracking
- Updated error handling with detailed line number and script line information

### Fixed

- Fixed validation logic to correctly identify when an email address is already in use by the selected mailbox (valid scenario) versus other mailboxes (invalid scenario)
- Fixed session cleanup by ensuring Remove-PSSession is called in finally blocks even when errors occur
- Fixed memory usage issues by selecting only required properties instead of all mailbox properties

### Removed

- Removed automatic email address uniqueness finder that appended numbers (1, 2, 3, etc.) to create unique addresses
- Removed unused searchOUs variable references

## [1.0.2] - 2022-08-24

### Added

- Added version number and updated code for SA-agent and auditlogging

## [1.0.1] - 2021-11-16

### Added

- Added version number and updated all-in-one script

## [1.0.0] - 2021-04-29

Initial release of HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-Emailaddress.

### Added

- Initial release for adding email addresses to Exchange On-Premises user mailboxes
