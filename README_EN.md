# Casing Running Calculator

An advanced Excel-based engineering calculation suite for modeling and evaluating casing runs in vertical, directional, and horizontal oil and gas wells.

This project includes two separate versions of the calculator:
1. 🇷🇺 **`Калькулятор_спуска_обсадных_колонн.xlsx`** — Russian version.
2. 🇺🇸 **`Casing_Running_Calculator.xlsx`** — English version (all sheets, labels, formulas, conditional formatting, and status logic fully translated).

---

## 🚀 Key Features

The calculator implements comprehensive mathematical modeling to ensure casing strings are successfully run to planned depth without risks of lock-up, mechanical yielding, pipe failure, or formation fracturing:

*   **Mixed Casing Strings Configurator**: Allows designing hybrid casing strings composed of up to 3 separate pipe sections (different outer/inner diameters, steel grades, and weights).
*   **Tension & Drag Calculations**: Models hook loads during run-in-hole (RIH) and pull-out-of-hole (POOH) taking into account HFS survey parameters and the capstan effect.
*   **Buckling Limit Analysis**: Calculates critical sinusoidal and helical buckling thresholds across all wellbore sections (preventing division-by-zero on vertical sections).
*   **Surge & Swab Hydraulics**: Computes hydrodynamic pressures generated during casing running using a Bingham-Plastic narrow slot model, yielding dynamic Equivalent Circulating Density (ECD).
*   **Pipe Integrity & Limits (API/von Mises)**:
    *   *Collapse resistance* mapped against hydrostatic pressure.
    *   *Burst resistance* using Barlow's formula under pressure test conditions.
    *   *Triaxial von Mises equivalent stress* on the inner wall for a rigorous combined stress check.
*   **Interactive Dashboard (Summary)**: A premium KPI summary tab featuring automated color coding and a detailed hazardous interval tracker.

---

## 📐 Mathematical Model & Physical Calculations

### 1. Normal Force in Curved Wellbores
To capture capstan tension-drag coupling in three-dimensional bends, the contact normal force $N_i$ is calculated as:
$$N_i = \sqrt{\left( w_{bi} \cdot \sin\theta_{avg} \right)^2 + \left( T_i \cdot \Delta\beta_i \cdot \frac{\pi}{180} \right)^2}$$
where:
*   $w_{bi}$ is the buoyant weight of the casing, N/m.
*   $\theta_{avg}$ is the average inclination of the interval, deg.
*   $T_i$ is the local axial tension (resolved via a neutral-point lookup to prevent circular loops), N.
*   $\Delta\beta_i$ is the dogleg/spatial curvature angle, deg.

### 2. Buckling Thresholds
*   **Vertical Section** (Lubinski criteria, preventing division-by-zero at $\sin\theta = 0$):
    $$F_{crit\_sin} = 1.94 \cdot \sqrt[3]{E \cdot I \cdot w_b^2}$$
*   **Inclined Section** (Dawson-Paslay criteria):
    $$F_{crit\_sin} = 2 \cdot \sqrt{\frac{E \cdot I \cdot w_b \cdot \sin\theta}{r}}$$
*   **Helical Buckling Limit**:
    $$F_{crit\_hel} = 1.41 \cdot F_{crit\_sin}$$

### 3. Surge Pressures & Dynamic ECD
For a Bingham-Plastic fluid flowing in a narrow annulus, the pressure gradient is:
$$\frac{dP}{dz} = \frac{12 \cdot PV \cdot v_{ann}}{(D_{hole} - OD)^2} + \frac{6 \cdot YP}{D_{hole} - OD}$$
where annular fluid velocity is:
$$v_{ann} = v_{run} \cdot \left( \frac{OD^2}{D_{hole}^2 - OD^2} + K_c \right)$$
The dynamic ECD is then computed relative to the vertical depth (TVD):
$$ECD = \rho_{mud} + \frac{P_{surge} \cdot 10^6}{9.81 \cdot TVD}$$

### 4. Triaxial von Mises Stress Check
Mechanical integrity is checked at the inner pipe wall (worst-case stress state):
$$\sigma_z = \frac{Q_i + P_i \cdot 9810}{\text{Area}_{steel}}$$
$$\sigma_{\theta} = \frac{P_{test} \cdot OD}{2 \cdot t}$$
$$\sigma_r = -\frac{P_{test} + 2 \cdot P_{hydro}}{2}$$
$$\sigma_{eq} = \sqrt{\sigma_z^2 + \sigma_{\theta}^2 + \sigma_r^2 - \sigma_z\sigma_{\theta} - \sigma_{\theta}\sigma_r - \sigma_r\sigma_z}$$
The structural safety factor is: $SF_{strength} = \frac{Y_p}{\sigma_{eq}}$.

---

## 📁 Workbook Structure

1.  **Input Data**:
    *   Casing specs, well geometries, mud properties, rig capacities.
    *   *Mixed Casing String Configurator* (G4:N7) table.
2.  **Well Profile**:
    *   Survey parameters: Measured Depth (MD), True Vertical Depth (TVD), Inclination, Azimuth, DLS, and Section Type.
3.  **Calculations**:
    *   Step-by-step segment calculations (columns A to AS) for normal force, tension/compression profiles, buckling, collapse, burst, surge, ECD, and von Mises stresses.
4.  **Charts**:
    *   Plotted RIH and POOH loads against rig hook load capacities and limits.
5.  **Summary**:
    *   KPI panel (11 parameters) featuring conditional safety alerts and an active warning listing of any intervals violating margins.

---

## 🛠️ System Requirements & Usage

*   Requires **Microsoft Excel** (2016 or newer) or any compatible spreadsheet software (LibreOffice, Google Sheets).
*   Upon opening the spreadsheet, make sure to enable editing/external links when prompted to activate conditional formatting styles and formulas.
*   The workbook is fully automated: simply update inputs on the **Input Data** sheet, and all downstream calculations and graphs will refresh.

---

## 🧑‍💻 Author
*   **GitHub**: [@Nikolasmega](https://github.com/Nikolasmega)

---

## 💸 Support the Project
If you find this tool useful, you can support its development with a donation. Any contribution motivates further updates and new features!

**Cryptocurrency Wallet Address:** `0x9c0E67b2792aCf0c73CfB5891d58861167aD9918`

**Supported Networks:** Polygon · BNB Chain

Any amount is welcome and highly appreciated! 🙏

