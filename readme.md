This uses the recommended [meta-st-openstlinux](https://github.com/STMicroelectronics/meta-st-openstlinux) distro.

Experiments with `poky` distro can be found [here](https://github.com/cracked-machine/stm32_poky).

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