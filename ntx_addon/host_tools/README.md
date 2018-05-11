## mk_update_zip_package.sh

```
all         : contains all the upgrade files (include u-boot, kernel, ramdisk, logo, system, recovery)
system      : only upgrade android system
firmware    : only upgrade firmware without system (include u-boot, kernel, ramdisk, logo, recovery)
mk          : contains all the upgrade files for eng to user build
repartition : same as all, but wipes data and recreate partitions
```

`repartition` uses information in `ntx_addon/host_tools/make_partition.sh` [[link](https://github.com/rbx-rdm/pp1/blob/ba42f8f64bf320ee012e66900d6b4889a88f2383/ntx_addon/host_tools/make_partition.sh#L37)] to recreate partitions.
