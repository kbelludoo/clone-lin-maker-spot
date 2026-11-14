# clone-lin-maker-spot

Experimental **LIN** clone of Maker/Sky `Spotter.poke`
(uint64-scale WAD'=RAY'=ONE=1e9, explicit OSM `val`/`has`, `par`, `mat`, `wad_ray`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/spot.sol` sha256 `f772861927801ca1e32ba818ffc55df6ceffcc530ac3d8b6b223e7411bed118f` blob `2f5b98d9160e6f4f5c7943a964dcc47bb2c2c862`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_spot.lin`](src/lin_maker_spot.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_spot_c11.c`](test/oracles/maker_spot_c11.c)
- **Transpilable kernel:** [`test/oracles/maker_spot_kernel.c`](test/oracles/maker_spot_kernel.c)
- **Proofs (lin-open only):** `examples/maker_spot/` and `make maker-spot-proof`
- **Class:** EXPERIMENTAL uint64-scale. Not mainnet uint256. Not a production OSM/vat replacement.

Named goldens (uint64-scale, `RAY'=1e9`):

| id | inputs | spot |
|---|---|---|
| 150% of val=3e9 | has=1 par=1e9 mat=1.5e9 | **2000000000** |
| stale OSM | has=0 | **0** |
| 200% of val=4e9 | mat=2e9 | **2000000000** |
| par=$2 of val=4e9 | par=2e9 mat=1e9 | **2000000000** |
| wad_ray=1000 | val=3e6 | **2000000000** |

`has` / `val` / `wad_ray` / `par` / `mat` / `one` are arguments (Solidity uses
`pip.peek()`, storage `par`/`ilks[ilk].mat`, and `10 ** 9` WAD→RAY).
`7e9*3e9` fail-closes while naive i64 wraps. Distinct from Clipper.kick OSM top.

## Reproduce proofs (in lin-open)

```
make maker-spot-proof
```

## Not claimed

Uint256 / mainnet OSM / RAY=1e27 / actual `vat.file`. LIN replacing Maker, Sky,
or the EVM. TVL or dollar savings. zk soundness. Clipper.kick. Hidden pip SLOADs.
