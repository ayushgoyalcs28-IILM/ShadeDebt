# ShadeDebt — Design better shade, before building it

**Environmental Hacks 2026 · Heat & Water track · WeMakeDevs × AWS**

ShadeDebt is an interactive infrastructure-planning prototype that evaluates how effectively public bus shelters protect the **passenger waiting area**, not merely whether a roof exists.

**Live app:** https://main.d1vctqaaosmqub.amplifyapp.com/

## Experience

1. Search an approved catalogue of **6,880 Delhi-area stop locations**, or use an illustrative example. OpenStreetMap road geometry supplies an **estimated** road alignment when available; this is not a surveyed shelter bearing.
2. Enter essential dimensions for the existing shelter and waiting space.
3. Draw a custom replacement canopy and adjust its height and position.
4. Move the afternoon timeline (12 PM–5 PM IST) to see calculated sunlight and shadows, comparing **Before** and **After**.
5. Run the **sampled year-ahead optimizer**: evaluate each candidate canopy placement using 12 representative monthly dates and five afternoon sun positions per date (60 samples).

The core metric is the average fraction of the waiting area protected from direct-beam sunlight. ShadeDebt (unshaded area × time, m²·h) is available as a supporting technical measure.

## Technology

- **Frontend:** React, TypeScript, Vite, interactive SVG architectural simulation.
- **Physics:** SunCalc solar geometry; metric east/north ground coordinates; polygon-clipping for intersections and shade coverage.
- **Optimization:** Bounded search over translated canopy placements with consistent solar sampling across the year.
- **AWS:** Amplify Hosting frontend and AWS Lambda versioned optimization API, with local Web Worker fallback.
- **Data:** Authorized historical Delhi bus-stop catalogue plus approximate OpenStreetMap nearest-road axis.

## Run locally

```bash
npm ci
npm run check
npm test
npm run build
npm run dev
```

For cloud deployment: `npm run build:lambda`, `npm run package:amplify`, and consult `docs/FINAL_RELEASE.md`.

## Scientific and source limitations

ShadeDebt models **geometric direct-beam shade**, not temperature, thermal comfort, structural adequacy, legality of construction, or shade from clouds. Stop coordinates are historical location records, not surveyed roof dimensions. Automatic road orientation is an estimate and needs physical confirmation before professional use. Yearly optimization samples 60 solar instants rather than continuously simulating all 365 days.

Bus-stop data derived from the [Delhi Bus Routes Dataset on Kaggle](https://www.kaggle.com/datasets/lourduradjou/delhi-bus-routes-dataset); the participant reports receiving hackathon-use permission from the dataset team. Attribution and limitations are included in `public/data/delhi-stops-provenance.json`. OpenStreetMap © OpenStreetMap contributors. See https://www.openstreetmap.org/copyright.

## AI disclosure

ChatGPT (OpenAI) substantially assisted with product research, planning, software architecture, implementation, debugging, visual design and documentation. The participant handled integration corrections, local testing and AWS account deployment.

**Status:** Hackathon prototype; not construction-grade engineering software.
