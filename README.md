# SunPy hands-on tutorial, ESPD Summer School 2026

<div>
<img src="./images/sunpy_logo.png" width="450" align="left"/>
</div>

This repo has the notebooks for the SunPy hands-on session at the **2nd European Solar Physics Division (ESPD) Summer School**, Dubrovnik, Croatia, **27 April to 1 May 2026** ([school webpage](https://oh.geof.unizg.hr/index.php/en/meetings/espd-school-2026)).

The session runs **Monday 27 April, 14:30 to 17:30** (split by a coffee break) and is the first hands-on of the week. By the end you'll be able to query, load and analyse multi-instrument solar data with sunpy and its affiliated packages.

## Resources to keep open

* [sunpy.org](https://sunpy.org/)
* [sunpy documentation](https://docs.sunpy.org/en/stable/)
* [Affiliated packages](https://sunpy.org/project/affiliated.html)
* [Example gallery](https://docs.sunpy.org/en/stable/generated/gallery/index.html)
* [Matrix chat](https://openastronomy.element.io/#/room/#sunpy:openastronomy.org)
* [OpenAstronomy Discourse](https://community.openastronomy.org/c/sunpy/5)

## Notebook overview

There are four notebooks, all built around a single real solar event, the M-class flare on **2022-04-02** from active region 12975, observed by **SDO/AIA**, **SOHO/LASCO**, and **Solar Orbiter (EUI / MAG)**.

| # | Notebook | What it covers |
|---|---|---|
| 1 | `1_solar_data_search_and_download.ipynb` | `astropy.units`, an overview of `Fido`, building queries with `Time` / `Instrument` / `Wavelength` / `Sample`, downloading and path templating, combining queries with `\|` and `&`, the SOAR client via `sunpy_soar`, CDAWeb, and HEK metadata queries |
| 2 | `2_data_containers_map_and_timeseries.ipynb` | `TimeSeries` (GOES/XRS, Solar Orbiter/MAG, slicing, resampling), `Map` (attributes, WCS, world/pixel coordinates, plotting, rotation, `submap`, `resample`), `MapSequence` and animations, running differences, `WCSAxes` and `plot_coord`, intensity slices along a path |
| 3 | `3_coordinates_framework.ipynb` | `SkyCoord` with solar frames (Helioprojective, Heliographic Stonyhurst, Heliocentric), frame transformations and observer-based frames, spacecraft positions via `get_horizons_coord`, multi-observer maps (AIA ↔ EUI) and `reproject_to`, heliographic CAR reprojection, and `sunpy.coordinates.spice` for SPICE kernels |
| 4 | `4_example_workflow.ipynb` | End-to-end multi-instrument analysis of the 2022-04-02 M-class flare: GOES/XRS light curve, AIA L1 → L1.5 with `aiapy`, EUI submap and rotate, LASCO/C2 via `hvpy`, reprojecting AIA onto LASCO with `assume_spherical_screen`, HMI + HEK active-region overlays |

## How to run

You have two options: **Google Colab** (zero install) or **local install** (recommended for the in-person school).

### Path A: Google Colab

Click the badge for the notebook you want and it opens in Colab:

| Notebook | Open in Colab |
|---|---|
| 1. Solar data search and download | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hayesla/ESPD_2026/blob/main/1_solar_data_search_and_download.ipynb) |
| 2. Data containers, Map and TimeSeries | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hayesla/ESPD_2026/blob/main/2_data_containers_map_and_timeseries.ipynb) |
| 3. Coordinates framework | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hayesla/ESPD_2026/blob/main/3_coordinates_framework.ipynb) |
| 4. Example workflow | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hayesla/ESPD_2026/blob/main/4_example_workflow.ipynb) |

In Colab you'll need to `pip install` the dependencies in the first cell of each notebook (the install cell is already there at the top, see also `requirements.txt`). Files don't persist between Colab notebook sessions, so each notebook re-fetches the data it needs. On a local install everything goes into `./data/` and is reused across notebooks, so that's the smoother experience if you can install before Monday.

### Path B: Local install (recommended)

#### 1. Clone the repo

```bash
git clone https://github.com/hayesla/ESPD_2026.git
cd ESPD_2026
```

#### 2. Create the environment

With **conda** (Miniconda or Anaconda):

```bash
conda env create -f environment.yml
conda activate espd-sunpy-2026
```

If solving feels slow, the libmamba solver speeds conda up: `conda install -n base conda-libmamba-solver && conda config --set solver libmamba`.

Or with **mamba** ([fast conda drop-in replacement](https://mamba.readthedocs.io/)):

```bash
mamba env create -f environment.yml
mamba activate espd-sunpy-2026
```

If you don't use conda/mamba, a plain virtualenv works:

```bash
python -m venv .venv
source .venv/bin/activate     # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

#### 3. Launch JupyterLab

```bash
jupyter lab
```

Start with `1_solar_data_search_and_download.ipynb`.

## Data layout

The notebooks download everything into a single `./data/` folder at the repo root using `Fido.fetch(..., path="./data/{file}")`. Files downloaded by notebook 1 are reused by notebooks 2 to 4, so run the notebooks in order the first time through.

## Pre-session checklist

Before Monday:

1. Clone the repo and create the environment (see above).
2. Open `1_solar_data_search_and_download.ipynb` and run the imports cell. You should see sunpy 7.1 or newer, with no errors.
3. Run a small `Fido` query (the `a.Time(...) + a.Instrument("AIA")` example near the top). If this errors, you likely have a network/proxy issue, so fall back to Colab.

If anything fails, open an [issue](https://github.com/hayesla/ESPD_2026/issues) or ping me on the school's communication channel.

## Credits

Tutorial by **Laura A. Hayes** (Dublin Institute for Advanced Studies, Ireland), building on the [2024 ESPD SunPy tutorial](https://github.com/hayesla/ESPD_2026SummerSchoolSunPy), with thanks to the **SunPy community** and contributors to the affiliated packages used here: `aiapy`, `sunpy-soar`, `sunkit-instruments`, `sunkit-image`, `reproject`, `hvpy`, and `astropy`.

Released under the [BSD 3-Clause License](LICENSE).
