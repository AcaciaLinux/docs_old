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
