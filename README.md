# caelum-platform-alveo

Caelum platform package for AMD Alveo cards. Use it with a target provider, usually [caelum-target-vitis](https://github.com/SkuldNorniern/caelum-target-vitis).

| id | card | Vitis shell | memory |
|----|------|-------------|--------|
| `alveo::u50` | Alveo U50 | xilinx_u50_gen3x16_xdma_5_202210_1 | 8 GB HBM |
| `alveo::u55c` | Alveo U55C | xilinx_u55c_gen3x16_xdma_3_202210_1 | 16 GB HBM |
| `alveo::u280` | Alveo U280 | xilinx_u280_gen3x16_xdma_1_202211_1 | 8 GB HBM, 2x DDR4 |

```toml
[target-dependencies]
vitis = { git = "https://github.com/SkuldNorniern/caelum-target-vitis" }
alveo = { git = "https://github.com/SkuldNorniern/caelum-platform-alveo" }

[target.u50]
provider = "vitis"
platform = "alveo::u50"
```

each `platforms/<id>/` has:

```text
platform.toml   name, part, modes (hw_emu, hw), what it needs from a provider (xclbin, xrt-host),
                [env] handed to the provider (VITIS_PLATFORM), [memory] for writing connectivity
xrt.ini         runtime / emulation logging, copied next to the xclbin
```

what stays in the project: `kernel.xml` and the connectivity config (`nk=`, `sp=kernel_1.in:HBM[0:1]`), they depend on the kernel's own port names.

the shell versions are the current ones AMD ships for each card; if yours is older, override `VITIS_PLATFORM` in a copy of the platform or install the matching shell.

not here on purpose: generic AXI (axi.cael), BRAM / URAM / DSP wrappers (amd-fpga.cael).
