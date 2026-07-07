= deb_packages
Create the deb package file

== Update your DEBIAN/control file

----
Package: qc
Version: 1.0
Section: utils
Priority: optional
Architecture: all
Maintainer: Your Name <you@example.com>
Description: Installs Robot Framework environment

Depends: python3, python3-pip, python3-tk
----

== Clean postinst should look like

----
#!/bin/bash
set -e

python3 -m pip install robotframework
python3 -m pip install robotframework-seleniumlibrary
python3 -m pip install pyserial
python3 -m pip install pandas

exit 0
----

== Convert into deb package

----
dpkg-deb -Zgzip --build ./qc
----

* `.qc` is the current directory deb package name

== Run after creating deb package

* apt update
* apt install -y ./qc.deb