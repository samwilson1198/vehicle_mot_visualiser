# Vehicle MOT Data Visualiser 🚗

This repository contains a submission for the **2025 Plotnine Contest**. The Jupyter notebook retrieves and analyses MOT (Ministry of Transport) test history for a specified vehicle using the DVSA (Driver and Vehicle Standards Agency) MOT History API. It produces an adaptive two-part visualisation:

- A mileage plot showing the vehicle's odometer readings over time.
- A fault plot displaying the number and severity of faults recorded during MOT tests.

This visualisation is exported into the `outputs/` folder.

You can either query the official DVSA MOT History API (requires credentials) **or** re-run the notebook using the included example JSON files in `data/`.

I created this project to:

- Improve my knowledge of Python and use Plotnine for the first time (frequent R user).
- Develop a tool to better visualise vehicle history (the UK GOV MOT checker can be intimidating).

---

## Contents

```
.
├── code.ipynb          # Main Jupyter Notebook with the full analysis + plotting workflow
├── data/               # Example JSON files for 5 vehicles from DVSA MOT history lookups
├── outputs/            # Generated visualisations (saved as PNG files)
└── README.md           # This file
```

> Note: The examples in `data/` are `MW02WVU.json`, `SK05HZC.json`, `YE55XSR.json`, `OY15CGK.json`, `MF68CZR.json`, and `outputs/` contains visualisations generated for these vehicles.

---

## What the notebook does (overview)

1. **Data extraction** — either requests MOT history from the DVSA MOT History API or loads a local example JSON from `data/`.
2. **Processing** — normalises and flattens returned JSON structures into a tidy `pandas.DataFrame` of MOT tests (date, odometer, faults, test result, etc.).
3. **Visualisation** — builds two plotnine plots:
   - **Mileage plot** — shows recorded odometer readings / mileage across MOT tests.
   - **Fault plot** — visualises the number and severity/type of faults recorded across tests.
4. **Combined figure** — stacks the two plots and saves a high-resolution PNG to `outputs/{registration}.png`.

---

## Dependencies

The notebook imports and uses the following Python packages:

- `plotnine`
- `mizani`
- `pandas`
- `numpy`
- `requests`
- `json`
- `datetime`

---

## Quick start — using the example JSON file(s)

1. Put one of the example JSON files into the `data/` directory (or confirm the included files are present).
2. Open the notebook:
3. In the data extraction and processing cells, run cell 3 (and not cell 2), which loads a local JSON file (the notebook includes a prompt that asks for a filename — enter e.g. `MW02WVU.json`). Run the notebook cells in order.
4. After the cells run, the final plot will be saved to `outputs/{registration}.png` and the plot object displayed in the notebook.

---

## Quick start — using the DVSA MOT History API

If you prefer to fetch live data from the DVSA MOT History API, do the following:

1. Register for access to the DVSA MOT History API and obtain the required credentials (`https://documentation.history.mot.api.gov.uk/`).
2. In the notebook, set the following variables (or modify the notebook to read them from environment variables):

```python
VEHICLE_REGISTRATION = "YOUR_REGISTRATION"
CLIENT_ID = "YOUR_CLIENT_ID"
CLIENT_SECRET = "YOUR_CLIENT_SECRET"
API_KEY = "YOUR_API_KEY"
TOKEN_URL = "https://..."   # as required by the DVSA OAuth2 endpoint
SCOPE = "..."               # if required
```

3. Run cell 2 (and not cell 3), which will obtain an access token and call the API. The notebook contains helper functions to request an OAuth2 token and then retrieve vehicle history from the endpoint.
4. Proceed to the plotting cells — the notebook will save the final plot under `outputs/{registration}.png`.

---

## Output details

- Saved plot path format: `outputs/{registration}.png` (high-resolution PNG).
- The notebook automatically creates `outputs/` if it does not exist.

- `plotnine` & `mizani` for the plotting grammar and scales
- `pandas` for data processing

---

