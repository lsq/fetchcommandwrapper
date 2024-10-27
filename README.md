# About

**fetchcommandwrapper** combines
download tool [aria2](https://aria2.github.io/)
with variable `GENTOO_MIRRORS`
to speed up distfile downloads of [Portage](https://wiki.gentoo.org/wiki/Portage)
by downloading from multiple mirrors at the same time.
**fetchcommandwrapper** integrates with Portage
through variables `FETCHCOMMAND` (and `RESUMECOMMAND`), hence the name.


# Installation

## System-wide installation in Gentoo

```console
# sudo emerge -av app-portage/fetchcommandwrapper
```
You can then append line `source /usr/share/fetchcommandwrapper/make.conf`
to file `/etc/portage/make.conf` to ease integration with Portage.


## Development from a Git clone

```console
# pip install --user --editable .
```
## 


It plugged into portage replacing wget for downloads, facilitating ${GENTOO_MIRRORS} and aria2 to both download faster and distribute loads across mirrors. A hack for sure, but with some potential. Back then public interest was non-existent, fetchcommandwrapper had some issues — e.g. metadata.xsd downloads failed and some sites rejected downloading before it made aria2 dress like wget — and I stopped using it myself, eventually. With the latest bug reports, bugfixes and release of version 0.8 in Gentoo, fetchcommandwrapper is ready for general use now. To give it a shot, you `emerge app-portage/fetchcommandwrapper` and append `source /usr/share/fetchcommandwrapper/make.conf` to `/etc/portage/make.conf`. Done. If you have extra options that you would like to pass to aria2c, put them in `${FETCHCOMMANDWRAPPER_EXTRA}`. `${FETCHCOMMANDWRAPPER_OPTIONS}` only for fetchcommendwrapper itself; for example
```
FETCHCOMMANDWRAPPER_OPTIONS="--link-speed=600000"
```
tells fetchcommandwrapper that my download link has 600KB/s only and makes aria2 in turn drop connections to mirrors that cannot keep up with at least a third of that, so that faster mirrors get a chance to take their place. For non-ebuild bugs, feel free to use https://github.com/gentoo/fetchcommandwrapper/issues to report. Best, Sebastian
