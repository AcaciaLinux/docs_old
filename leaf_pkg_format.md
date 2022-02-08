# AcaciaLinux pkg format

- based on zip format
- contains data directory and leaf.pkg (Manifest) file

# data

- data directory contains the packages various files, e.g:
  /usr/bin/monn
  /usr/lib/libmonn.so
  /usr/local/man/monnman.db

# leaf.pkg

- leaf.pkg file contains package information
  name=Monn package
  version=0.69.420-monn-lts
  files=[/usr/bin/monn, /usr/lib/libmonn.so, /usr/local/man/monnman.db]
  dependencies=[monn1,monn2,monn3]



# Other scripts

There are 2 scripts that are optional:

- preinstall.sh

- postinstall.sh

They can be present but do not have to be, if they are, they will have to have the executable flag set, so you can "disable" these scripts if they are not needed.

### preinstall.sh

This script gets run once the package has been downloaded and extracted, it can prepare files, compile the package or anything that needs to be done before deploying the package

### postinstall.sh

If the package depends on some cleanup or other files that can be deployed after the main package deployment this script gets executed.
