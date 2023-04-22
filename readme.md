This uses the recommended [meta-st-openstlinux](https://github.com/STMicroelectronics/meta-st-openstlinux) distro.

Experiments with `poky` distro can be found [here](https://github.com/cracked-machine/stm32_poky).

The layers directory contains the meta layers required for a `kirkstone` build. Commit versions are dictated by `ST`. See [oe_manifest](https://github.com/STMicroelectronics/oe-manifest/blob/openstlinux-5.15-yocto-kirkstone-mp1-v22.11.23/default.xml) for exact revisions.

Note, due to the _unique_ way in which `ST` have structured their layers, their setup script will fail if [bitbake](https://github.com/openembedded/bitbake) is not nested within [openembedded-core](https://github.com/openembedded/openembedded-core). This is nuts because the `bitbake` repo is not usually nested within `openembedded-core`. So if you want to use submodules (and you should) it means you have to fork [openembedded-core](https://github.com/openembedded/openembedded-core) so that you can push a permanent branch that nests [bitbake](https://github.com/openembedded/bitbake). You also have to remove `bitbake` from the [.gitignore](layers/openembedded-core/.gitignore) file to add the bitbake submodule.
__There is no reason I can see why `ST` couldn't have put these two repos side-by-side!__ 

The forked repo with special branch can be found [here](https://github.com/cracked-machine/openembedded-core/tree/2022-04.4_openstlinux-5.15-yocto-kirkstone-mp1-v22.11.23) 

### Environment

Designed be run in a container. See [devcontainer.json](.devcontainer/devcontainer.json)
If you don't have access to the container you can build it by first cloning the [embedded_linux_dockerfiles](https://github.com/cracked-machine/embedded_linux_dockerfiles) repoistory.

### Build

Use the task.json or run the following command line

```
cd layers/poky && \
TEMPLATECONF=/workspaces/stm32_poky/layers/meta-test/conf/templates/stm32mp157f_dk2 source oe-init-build-env ../../workdir
```

Depending on the selection made during the previous step, select either:

```
bitbake st-image-core
```

or 

```
bitbake st-image-weston
```


### Create raw file for SD Card 

```
sudo build-openstlinuxweston-stm32mp13-disco/tmp-glibc/deploy/images/stm32mp13-disco/scripts/create_sdcard_from_flashlayout.sh build-openstlinuxweston-stm32mp13-disco/tmp-glibc/deploy/images/stm32mp13-disco/flashlayout_core-image-minimal/deleteall/FlashLayout_disco_stm32mp157f-dk2-deleteall.tsv
```