Primary configuration elements are:
* [OS-Base](./Configuration/OS-Base.md)
* [Platform](broken-link Platform)
* [Image](broken-link Image)

## build-jail

Build jails provide an isolation for running the image build process, where the package manager runs inside.

Required attributes:
    * build-image: the jail image used for running the build (req. for docker)
    * build-init: the jail init program used for running the build (req. for docker)
    * confdir: the config directory prefix — used for as prefix for copying config files (eg. repo keys)
