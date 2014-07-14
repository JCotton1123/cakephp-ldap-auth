cakephp-ldap-auth
=================

CakePHP LDAP Authentication

* Simple to setup & it allows you <b>continue to use AuthComponent</b> with the <b>Form authenticator</b>
* Authenticate against Active Directory
* Authenticate users using the bind method instead of relying on an LDAP datasource configured with static credentials
* Retrieve an arbitrary list of user attributes from LDAP and populate the Auth session variable with them.
* Retrieve a list of the user's groups.
* Require a specific group membership to allow the user to log in.

## Setup

**If you're using AD, you must login with a username of the form Domain\username or username@domain.com**

* Drop the supplied BaseAuthenticate.php into Controller/Components/Auth
* Define the required and desired settings for AuthComponent (they will be passed along)

Ex:

```php
    $this->Auth->authenticate = array(
        'Form' => array(
            'host' => array(
                'dc1.domain.com',
                'dc2.domain.com'
            ),
            'baseDn' => 'DC=domain,DC=com',
            'userAttributes' => array(
                'cn',
                'sn',
                'givenname'
            ),
            'requireGroup' => 'Network Administrators',
        )
    );
```

## Caveats

* Probably not the best way to implement this but its simple
* The user's primary group is ignored. Sorry if this is a deal breaker. If you care to know why, look at the comments within the source.
* I've never tested this with anything but AuthComponent and the Form authenticator.

## To Do

* Make things more agnostic so it supports authentication against OpenLDAP or others.
* Fix styling issues
