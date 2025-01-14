# Test setup

`ci/lava` directory contains directories with names corresponding to build MACHINE names.
New directories should only be added after the build is available for a given MACHINE.
All files in the `ci/lava/<MACHINE>` directory should have `.yaml` extension.
Each file should be a valid LAVA job template.

# LAVA job templates

Job templates can use the following variables:
 - `DEVICE_TYPE`: name of the LAVA device type or alias. Full list can be found on [LAVA master web interface](https://lava.infra.foundries.io/scheduler/device_types)
 - `GITHUB_SHA`: Commit ID corresponding to the github action trigger
 - `BUILD_FILE_NAME`: Name of the build artifact to be downloaded. It's constructed as: `core-image-base-${DEVICE_TYPE}.rootfs.qcomflash.tar.gz`
 - `BUILD_DOWNLOAD_URL`: URL where the build artifacts can be found. This variable is constructed as: `${{inputs.url}}/${DEVICE_TYPE}/${BUILD_FILE_NAME}` where `{{inputs.url}}` comes from the build action.
 - `GITHUB_RUN_ID`: ID of the current Github run.

After variable substitution the file should form a valid LAVA job definition.
