# puppet-limits [![Build Status](https://secure.travis-ci.org/saz/puppet-limits.png)](http://travis-ci.org/saz/puppet-limits)

Manage user and group limits via Puppet

This module manages the limits of the PAM module pam_limits.

## How to use

`include ::limits`

## Compatibility

This module has been tested to work with Puppet v3 (with and without the future
parser) and v4 with Ruby versions 1.8.7 (Puppet v3 only), 1.9.3, 2.0.0 and
2.1.0.

### Purge limits.d directory

The class `limits` will purge the limit.d directory as default.
You can explicit change this with the parameter `purge_limits_d_dir`
or just do not call the class.

```puppet
	class { 'limits': }

    limits::limits { 'username_nofile':
      ensure     => present,
      user       => 'username',
      limit_type => 'nofile',
      hard       => 16384,
      soft       => 16384,
    }
```
### Do NOT purge limits.d directory explicit

```puppet
    class { 'limits':
      purge_limits_d_dir => false,
    }

    limits::limits { 'username_nofile':
      ensure     => present,
      user       => 'username',
      limit_type => 'nofile',
      hard       => 16384,
    }
```

### Set both limit types in one line

```puppet
    limits::limits { 'username_nofile':
      ensure     => present,
      user       => 'username',
      limit_type => 'nofile',
      both       => 16384,
    }
```
One of hard, soft or both must be set!
