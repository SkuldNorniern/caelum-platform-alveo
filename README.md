# caelum-platform-alveo

AMD Alveo cards as Caelum platforms, for [caelum-target-vitis](https://github.com/SkuldNorniern/caelum-target-vitis).

| id | Vitis shell | memory |
|----|-------------|--------|
| `alveo::u50` | xilinx_u50_gen3x16_xdma_5_202210_1 | 8 GB HBM |
| `alveo::u55c` | xilinx_u55c_gen3x16_xdma_3_202210_1 | 16 GB HBM |
| `alveo::u280` | xilinx_u280_gen3x16_xdma_1_202211_1 | 8 GB HBM, 2x DDR4 |

```toml
[target.u50]
provider = "vitis"
platform = "alveo::u50"
```

older shell on your card: override `VITIS_PLATFORM` in a copy of the platform. kernel.xml and the connectivity cfg stay in the project.

## vivado only

the cards also run a plain Vivado bitstream (no shell, no XRT, JTAG). these platforms don't cover that yet, use the part directly:

```toml
[target.u50-bare]
provider = "vivado"
part = "xcu50-fsvh2104-2-e"
xdc = "constraints/u50.xdc"
mode = "bitstream"
```

`xbmgmt program --base` puts the shell back.
