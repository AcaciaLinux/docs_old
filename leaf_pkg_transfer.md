# Leaf package handling

Leaf handles its packages by making GET requests to the server. This allows leaf to retrieve a package list that is always up to date, as well as allowing the reference of older packages.

# get

The main tag of the GET request is the `get` tag, its contents can be:

```txt
- packagelist
- jsonpackagelist
- package
- version
- versions
```

#### packagelist

This attribute allows leaf to obtain its package list

#### jsonpackagelist

This is here for future compatibility

#### package

The main tag that gets used, this is the tag that initiates a transfer of a package file, it requires the `pkgname` and optionally the `version` tag.

**Answer:** A binary stream of the package contents

#### version

This allows leaf to query the newest version available for a package, requires the `pkgname` tag.

**Answer:** The real version of the supplied package in string form and the semantic version after a semicolon: `325;3.2.5` 

#### versions

This allows leaf to query a list of all the available versions of a package, requires the `pkgname` tag.

**Answer:** A newline separated list of the versions available:

```
351;3.5.1
352;3.5.2
360;3.6.0
```

# pkgname

This is a simple string that contains the name of the requested package.

# version

This is the real_version of the package. We do not work with the semantic version because of incompatibility reasons across packages.

# Errors

Errors get passed through HTTP codes. The body of the response contains additional information in string form

```txt
- 400    The request has been malformed
            ->    E_REQUEST    The request to the server is malformed
            ->    E_GET        The get= tag is not existing
            ->    E_PKGNAME    The pkgname= tag is missing
            ->    E_VERSION    The version= tag is missing
- 404    The information, package or version have not been found
            ->    E_GENERAL    The information in general could not be found (such as the package list)
            ->    E_PACKAGE    The package could not be found
            ->    E_VERSION    The package version could not be found
```


