# nix-linux-setup

> Attempt to patch the Nix package manager

## Description

This installer only fixes UID (user id) ranges when creating `nixbld`
users.  By default the installer will assign UID from 30001 and
counting.  As it stands, those uid are not reserved UID for system
users (users that you shouldn’t connect to).

The default Debian derivative behavior is to use the file
`/etc/login.defs` if configured or those values:

```conf
SYS_UID_MIN		  100
SYS_UID_MAX		  999
```

where `SYS_UID_MIN` is the minimum and `SYS_UID_MAX` is the maximum
UID for system users.  The starting system UID is 999 counting
downward (and until one is not already taken).

This is the only universal solution in order to hide the `nixbld`
users from the display manager login screen (GDM, LightDM, ...).

!["Nix build users in LightDM"][screenshot]

[screenshot]: ./screenshot.png "Nix build users in LightDM"

## Installing

First clone this repository:
```bash
git clone https://github.com/notetiene/nix-linux-setup.git
cd nix-linux-setup.git
./install --daemon
```

This script will download the latest tarball for your architecture
from `https://nixos.org/nix/install`.  It will also check its
integrity and it will finally apply the modifications to its
installer.

This script /should/ be forward compatible since it does not rely on
any particular Nix version.  However, major modifications from the
installer sould issue an error.

## Licensing

### Explanation

In order to respect the freedom of others, this repository is licensed
with the GPL version 3 or later.  Any other derivative works *must* be
distributed as GPLv3.  While the added work must be GPL compatible,
the combination *must* be distributed as GPLv3+.  This means the
contributed work *can* be public domain or X11/MIT, Apache, etc.  But
a combination (including parts of this program) *must* be GPLv3+
licensed.

This explanation is necessary because many people confuse the term
/GPL compatible license/ in that the combinated work could be in those
licenses. Only the added work can be licensed with a GPL compatible
license.

For a list of GPL compatible liscenses, please visit the [GNU
website][GPLCompatibleLicenses].

### License

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

Note: GPLv3+ means GPL version 3 (or at your option) any later
version.

[GPLCompatibleLicenses]: https://www.gnu.org/licenses/license-list.en.html#GPLCompatibleLicenses