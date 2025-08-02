# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-08-02

### Added
- **OpenLDAP/FreeIPA/389 Directory Server support**
  - Flexible DN construction based on `ldap_type` configuration
  - Support for `uid=username,cn=users,cn=accounts,dc=domain,dc=com` DN format
  - `login_attribute` configuration for different LDAP schemas
- **Enhanced Error Handling**
  - Graceful handling of null LDAP attributes
  - Safe array access for LDAP attribute mapping
  - Improved UserIdentity management for Shield compatibility
- **Extended Configuration Options**
  - Comprehensive configuration comments for both AD and OpenLDAP
  - Example configurations for different LDAP server types
  - OpenLDAP/FreeIPA optimized attribute lists
- **Enhanced User Entity**
  - Override `touchIdentity()` method to handle null identities
  - Extended UserModel to use enhanced User entity
  - Automatic email identity creation for LDAP users

### Changed
- **Default Attribute List**: Updated to OpenLDAP/FreeIPA compatible attributes
- **Package Name**: Changed from `rakoitde/shieldldap` to `fortyseeds/ci4-shield-ldap`
- **Documentation**: Complete rewrite with examples for both AD and OpenLDAP
- **Composer Configuration**: Enhanced with keywords and dual authorship

### Fixed
- **Type Errors**: Fixed null assignment to typed properties
- **Undefined Array Keys**: Safe access to LDAP attributes with fallbacks
- **UserIdentity Issues**: Automatic creation and management of user identities
- **LDAP Manager**: Enhanced attribute loading with null safety

## [1.1.0] - Database Migration Enhancement

### Fixed
- **Dynamic Table Name**: DB Migration now reads table name from `Auth.php` config instead of hardcoded 'user' table
  - Migration now uses `config('Auth')->userProvider['table']` for proper table detection
  - Supports custom user table names configured in Shield
  - Backwards compatible with existing installations

### Technical Details
- Updated migration to dynamically detect user table name from Shield configuration
- Improved compatibility with custom Shield installations using non-standard table names

## [1.x] - Original Version

### Features
- Active Directory authentication support
- Basic LDAP connection and user management
- CodeIgniter 4 Shield integration
- User attribute synchronization

---

## Migration Guide from v1.x to v2.0

### 1. Update Configuration
```php
// Add these new properties to your AuthLDAP config:
public string $ldap_type = 'ad'; // or 'ldap' for OpenLDAP/FreeIPA
public string $login_attribute = 'uid'; // for OpenLDAP/FreeIPA
```

### 2. Update Attributes List
For OpenLDAP/FreeIPA, replace the attributes array:
```php
public array $attributes = [
    'uid', 'cn', 'dn', 'distinguishedName', 'entryUUID', 'entryDN',
    'displayName', 'title', 'description', 'givenName', 'sn', 'mail',
    'telephoneNumber', 'mobile', 'o', 'ou', 'l', 'postalCode', 'street',
    'employeeNumber', 'employeeType', 'departmentNumber',
    'krbPrincipalName', 'krbCanonicalName', 'ipaUniqueID', 'memberOf'
];
```

### 3. Update Composer
```bash
composer remove rakoitde/shieldldap
composer require fortyseeds/ci4-shield-ldap
```