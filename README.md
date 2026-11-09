# sdsg-data

Data files for the Cambridge Part II course *Stellar Dynamics and the Structure of Galaxies* (SDSG).
The files are attached to [GitHub releases](https://github.com/vasilybelokurov/sdsg-data/releases), not stored in the repository.

## `gaia_dr3_nearby.fits`

Nearby red giants with Gaia DR3 radial velocities. The course uses it to measure Oort's constant A in Lecture 4 (`oort_constants_gaia.ipynb`).

Download:

```
https://github.com/vasilybelokurov/sdsg-data/releases/download/v1/gaia_dr3_nearby.fits
```

```python
from astropy.table import Table
d = Table.read('https://github.com/vasilybelokurov/sdsg-data/releases/download/v1/gaia_dr3_nearby.fits')
```

- 86,490 stars, 23 columns, 12.5 MB
- SHA-256: `2653ce3623f486b82fa104c08575f6c45d9f76e66b696ac2f91a444571bfbc7d`

### Selection (as present in the data)

- Gaia DR3 `parallax > 2` mas (distance below about 500 pc)
- `phot_g_mean_mag < 16`, with a Gaia DR3 `radial_velocity` for every star
- `teff < 5200` K and `logg < 3.5`: red giants

### Columns

| Column | Unit | Source |
|---|---|---|
| `source_id`, `ra`, `dec`, `parallax`, `parallax_error`, `pmra`, `pmdec`, `pmra_error`, `pmdec_error`, `ruwe`, `phot_g_mean_mag`, `bp_rp`, `phot_bp_rp_excess_factor`, `radial_velocity`, `radial_velocity_error` | deg, mas, mas/yr, mag, km/s | Gaia DR3 `gaia_source` |
| `ebv` | mag | Schlegel, Finkbeiner & Davis (1998) E(B−V) at the star's position |
| `r_med_geo`, `r_med_photogeo` | pc | Bailer-Jones et al. (2021) geometric and photogeometric distances |
| `allwise_w1`, `allwise_w2` | mag | AllWISE `w1mpro`, `w2mpro`, nearest counterpart within 1 arcsec |
| `mh`, `teff`, `logg` | dex, K, dex | Andrae, Rix & Chandra (2023), XGBoost parameters from XP spectra* |

All columns except `mh`, `teff` and `logg` were checked against the source catalogues for a random sample of 2,000 stars and agree exactly. The file was assembled from the copies of these catalogues in WSDB, the survey database at the Institute of Astronomy, Cambridge.

\* `mh`, `teff` and `logg` are close to, but not identical with, the current release (v2.1) of the Andrae et al. catalogue. The median differences are 0.02 dex in [M/H], 21 K in T_eff and 0.04 dex in log g, and 8% of the stars are not in v2.1. They most likely come from an earlier release of that catalogue. The cuts `teff < 5200` K and `logg < 3.5` select red giants.

### Sources and licences

- Gaia DR3: Gaia Collaboration, Vallenari et al. (2023), [A&A 674, A1](https://ui.adsabs.harvard.edu/abs/2023A%26A...674A...1G). Gaia data are released under [CC BY-SA 3.0 IGO](https://creativecommons.org/licenses/by-sa/3.0/igo/).
- Distances: Bailer-Jones et al. (2021), [AJ 161, 147](https://ui.adsabs.harvard.edu/abs/2021AJ....161..147B).
- Reddening: Schlegel, Finkbeiner & Davis (1998), [ApJ 500, 525](https://ui.adsabs.harvard.edu/abs/1998ApJ...500..525S).
- AllWISE: Cutri et al. (2013), [AllWISE explanatory supplement](https://wise2.ipac.caltech.edu/docs/release/allwise/expsup/); WISE: Wright et al. (2010), [AJ 140, 1868](https://ui.adsabs.harvard.edu/abs/2010AJ....140.1868W).
- Metallicities: Andrae, Rix & Chandra (2023), [ApJS 267, 8](https://ui.adsabs.harvard.edu/abs/2023ApJS..267....8A); catalogue on [Zenodo 7945154](https://zenodo.org/records/7945154) (CC BY 4.0).

This derived table is distributed under CC BY-SA 3.0 IGO. If you use it, please cite the papers above.
