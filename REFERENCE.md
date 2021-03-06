# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

* [`dehydrated`](#dehydrated): Main class used to setup the system.
* [`dehydrated::apache`](#dehydratedapache): Serve challenges with Apache
* [`dehydrated::changed`](#dehydratedchanged): Trigger a refresh of the certificates
* [`dehydrated::config`](#dehydratedconfig): Manage dehydrated configuration
* [`dehydrated::cron`](#dehydratedcron): Manage cron task to refresh certificates
* [`dehydrated::domains`](#dehydrateddomains): Manage the domains.txt file
* [`dehydrated::package`](#dehydratedpackage): Manage the dehydrated package
* [`dehydrated::repo`](#dehydratedrepo): Manage the dehydrated code
* [`dehydrated::user`](#dehydrateduser): Manage the dehydrated user

### Defined types

* [`dehydrated::certificate`](#dehydratedcertificate): Class used to describe the certificates that should be maintained.

### Functions

* [`dehydrated::apache::vhost_attributes`](#dehydratedapachevhost_attributes): Return the apache::vhost SSL configuration for a host
* [`dehydrated::certsdir`](#dehydratedcertsdir): Return the root directory of dehydrated certificates
* [`dehydrated::ssl_cert_file`](#dehydratedssl_cert_file): Return the full path to a certificate file
* [`dehydrated::ssl_chain_file`](#dehydratedssl_chain_file): Return the full path to a certificate chain file
* [`dehydrated::ssl_fullchain_file`](#dehydratedssl_fullchain_file): Return the full path to a certificate fullchain file
* [`dehydrated::ssl_privkey_file`](#dehydratedssl_privkey_file): Return the full path to a private key file

### Tasks

* [`cleanup`](#cleanup): Cleanup certificates not managed by dehydrated anymore
* [`renew`](#renew): Renew certificates about to expire

### Plans

* [`dehydrated::renew`](#dehydratedrenew): Renew certificates about to expire

## Classes

### <a name="dehydrated"></a>`dehydrated`

Main class used to setup the system.

#### Parameters

The following parameters are available in the `dehydrated` class:

* [`apache_user`](#apache_user)
* [`bin`](#bin)
* [`etcdir`](#etcdir)
* [`group`](#group)
* [`package`](#package)
* [`user`](#user)
* [`repo_source`](#repo_source)
* [`repo_revision`](#repo_revision)
* [`dependencies`](#dependencies)
* [`apache_integration`](#apache_integration)
* [`cron_integration`](#cron_integration)
* [`ip_version`](#ip_version)
* [`ca`](#ca)
* [`ca_terms`](#ca_terms)
* [`license`](#license)
* [`challengetype`](#challengetype)
* [`keysize`](#keysize)
* [`openssl_cnf`](#openssl_cnf)
* [`hook`](#hook)
* [`hook_chain`](#hook_chain)
* [`renew_days`](#renew_days)
* [`private_key_renew`](#private_key_renew)
* [`private_key_rollover`](#private_key_rollover)
* [`key_algo`](#key_algo)
* [`contact_email`](#contact_email)
* [`ocsp_must_staple`](#ocsp_must_staple)
* [`timeout`](#timeout)

##### <a name="apache_user"></a>`apache_user`

Data type: `String`

User account of apache httpd.

##### <a name="bin"></a>`bin`

Data type: `String`

Path to the dehydrated command.

##### <a name="etcdir"></a>`etcdir`

Data type: `String`

Path to the dehydrated configuration directory.

##### <a name="group"></a>`group`

Data type: `String`

Group of the user account used to manage certificates.

Default value: `'dehydrated'`

##### <a name="package"></a>`package`

Data type: `Optional[String]`

Name of the package providing dehydrated.

##### <a name="user"></a>`user`

Data type: `String`

User account used to manage certificates.

Default value: `'dehydrated'`

##### <a name="repo_source"></a>`repo_source`

Data type: `String`

URL of the repository providing dehydrated.

Default value: `'https://github.com/dehydrated-io/dehydrated.git'`

##### <a name="repo_revision"></a>`repo_revision`

Data type: `String`

Revision to fetch from the repository providing dehydrated.

Default value: `'v0.7.0'`

##### <a name="dependencies"></a>`dependencies`

Data type: `Array[String]`

Extra dependencies needed to run dehydrated.

Default value: `[]`

##### <a name="apache_integration"></a>`apache_integration`

Data type: `Boolean`

Setup apache to serve the generated challenges.

Default value: ``false``

##### <a name="cron_integration"></a>`cron_integration`

Data type: `Boolean`

Setup cron to automatically renew certificates.

Default value: ``false``

##### <a name="ip_version"></a>`ip_version`

Data type: `Optional[Variant[Integer[4,4],Integer[6,6]]]`

Use only this IP version for name resolution.

Default value: ``undef``

##### <a name="ca"></a>`ca`

Data type: `Optional[Stdlib::Httpurl]`

Path to certificate authority.

Default value: ``undef``

##### <a name="ca_terms"></a>`ca_terms`

Data type: `Optional[Stdlib::Httpurl]`

Path to certificate authority license terms redirect.

Default value: ``undef``

##### <a name="license"></a>`license`

Data type: `Optional[String]`

Path to license agreement.

Default value: ``undef``

##### <a name="challengetype"></a>`challengetype`

Data type: `Optional[Enum['http-01', 'dns-01']]`

Challenge type to be used.

Default value: ``undef``

##### <a name="keysize"></a>`keysize`

Data type: `Optional[Integer[0]]`

Default keysize for private keys.

Default value: ``undef``

##### <a name="openssl_cnf"></a>`openssl_cnf`

Data type: `Optional[String]`

Path to openssl config file.

Default value: ``undef``

##### <a name="hook"></a>`hook`

Data type: `Optional[String]`

Program or function called in certain situations.

Default value: ``undef``

##### <a name="hook_chain"></a>`hook_chain`

Data type: `Optional[Boolean]`

Chain clean_challenge|deploy_challenge arguments together into one hook call per certificate.

Default value: ``undef``

##### <a name="renew_days"></a>`renew_days`

Data type: `Optional[Integer[0]]`

Minimum days before expiration to automatically renew certificate.

Default value: ``undef``

##### <a name="private_key_renew"></a>`private_key_renew`

Data type: `Optional[Boolean]`

Regenerate private keys instead of just signing new certificates on renewal.

Default value: ``undef``

##### <a name="private_key_rollover"></a>`private_key_rollover`

Data type: `Optional[Boolean]`

Create an extra private key for rollover.

Default value: ``undef``

##### <a name="key_algo"></a>`key_algo`

Data type: `Optional[Enum['rsa', 'prime256v1', 'secp384r1']]`

Which public key algorithm should be used?

Default value: ``undef``

##### <a name="contact_email"></a>`contact_email`

Data type: `String`

E-mail address Let's Encrypt can use to reach you regarding your certificates.

##### <a name="ocsp_must_staple"></a>`ocsp_must_staple`

Data type: `Optional[Boolean]`

Option to add CSR-flag indicating OCSP stapling to be mandatory.

Default value: ``undef``

##### <a name="timeout"></a>`timeout`

Data type: `Optional[Integer[0]]`

Execution timeout for dehydrated tool.

Default value: ``undef``

### <a name="dehydratedapache"></a>`dehydrated::apache`

Serve challenges with Apache

### <a name="dehydratedchanged"></a>`dehydrated::changed`

Trigger a refresh of the certificates

### <a name="dehydratedconfig"></a>`dehydrated::config`

Manage dehydrated configuration

### <a name="dehydratedcron"></a>`dehydrated::cron`

Manage cron task to refresh certificates

### <a name="dehydrateddomains"></a>`dehydrated::domains`

Manage the domains.txt file

### <a name="dehydratedpackage"></a>`dehydrated::package`

Manage the dehydrated package

### <a name="dehydratedrepo"></a>`dehydrated::repo`

Manage the dehydrated code

### <a name="dehydrateduser"></a>`dehydrated::user`

Manage the dehydrated user

## Defined types

### <a name="dehydratedcertificate"></a>`dehydrated::certificate`

Class used to describe the certificates that should be maintained.

#### Parameters

The following parameters are available in the `dehydrated::certificate` defined type:

* [`domains`](#domains)

##### <a name="domains"></a>`domains`

Data type: `Array[String]`

List of Subject Alternative Names (SAN) to include in the certificate

Default value: `[]`

## Functions

### <a name="dehydratedapachevhost_attributes"></a>`dehydrated::apache::vhost_attributes`

Type: Puppet Language

Return the apache::vhost SSL configuration for a host

#### Examples

##### 

```puppet
apache::vhost { $hostname:
  port => 443,
  ssl  => true,
  [...]
  *    => dehydrated::apache::vhost_attributes($hostname)
}
```

#### `dehydrated::apache::vhost_attributes(String $hostname)`

Return the apache::vhost SSL configuration for a host

Returns: `Hash[String,String]` Virtual host configuration for the host

##### Examples

###### 

```puppet
apache::vhost { $hostname:
  port => 443,
  ssl  => true,
  [...]
  *    => dehydrated::apache::vhost_attributes($hostname)
}
```

##### `hostname`

Data type: `String`

The name of the host to consider

### <a name="dehydratedcertsdir"></a>`dehydrated::certsdir`

Type: Puppet Language

Return the root directory of dehydrated certificates

#### `dehydrated::certsdir()`

Return the root directory of dehydrated certificates

Returns: `String` The directory of dehydrated certificates

### <a name="dehydratedssl_cert_file"></a>`dehydrated::ssl_cert_file`

Type: Puppet Language

Return the full path to a certificate file

#### `dehydrated::ssl_cert_file(String $hostname)`

Return the full path to a certificate file

Returns: `String` The path of the cerificate file

##### `hostname`

Data type: `String`

The name of the host to consider

### <a name="dehydratedssl_chain_file"></a>`dehydrated::ssl_chain_file`

Type: Puppet Language

Return the full path to a certificate chain file

#### `dehydrated::ssl_chain_file(String $hostname)`

Return the full path to a certificate chain file

Returns: `String` The path of the cerificate chain file

##### `hostname`

Data type: `String`

The name of the host to consider

### <a name="dehydratedssl_fullchain_file"></a>`dehydrated::ssl_fullchain_file`

Type: Puppet Language

Return the full path to a certificate fullchain file

#### `dehydrated::ssl_fullchain_file(String $hostname)`

Return the full path to a certificate fullchain file

Returns: `String` The path of the cerificate fullchain file

##### `hostname`

Data type: `String`

The name of the host to consider

### <a name="dehydratedssl_privkey_file"></a>`dehydrated::ssl_privkey_file`

Type: Puppet Language

Return the full path to a private key file

#### `dehydrated::ssl_privkey_file(String $hostname)`

Return the full path to a private key file

Returns: `String` The path of the private key file

##### `hostname`

Data type: `String`

The name of the host to consider

## Tasks

### <a name="cleanup"></a>`cleanup`

Cleanup certificates not managed by dehydrated anymore

**Supports noop?** true

#### Parameters

##### `dehydrated_dir`

Data type: `Optional[Stdlib::AbsolutePath]`

The directory of dehydrated

### <a name="renew"></a>`renew`

Renew certificates about to expire

**Supports noop?** false

## Plans

### <a name="dehydratedrenew"></a>`dehydrated::renew`

Renew certificates about to expire

#### Parameters

The following parameters are available in the `dehydrated::renew` plan:

* [`targets`](#targets)

##### <a name="targets"></a>`targets`

Data type: `TargetSpec`

Target fifor certificates renewal

