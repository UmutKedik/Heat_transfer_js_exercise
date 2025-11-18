🌞 Solar Thermal Tank Simulation (Web Interface)

This project provides a simple but practical simulation of a solar-heated water tank.
The goal is to estimate how the tank temperature evolves over multiple days based on:

Solar panel area

Tank volume

Daily average ambient temperature

Daily sun exposure

Panel efficiency

Heat-loss characteristics

Everything runs directly in the browser using HTML, CSS, and JavaScript.
No backend or external dependencies are required except Chart.js for visualization.

🎯 Purpose

The simulation is not meant to be a full thermodynamic model.
Instead, it aims to provide a lightweight engineering approximation that reacts to real-world changes:

Solar irradiance varies throughout the day

Panel efficiency changes with temperature

Heat loss increases as tank temperature rises

Pump runtime is tracked during sun hours

Temperature data is sampled hourly for performance

This makes the tool useful for quick feasibility checks, educational demos, or general solar-thermal calculations.

🧮 How the Model Works
1. Time Step

The simulation runs internally with a 60-second time step (1 minute).
This keeps the temperature calculation smooth without causing performance issues.

2. Solar Irradiance Curve

Instead of assuming constant sunlight, irradiance is modeled using a half-sine curve:

irradiance = sin(π * progress) * peakValue


This creates:

Low radiation in the morning

Maximum radiation at midday

Symmetric decrease in the evening

3. Panel Efficiency

Efficiency is slightly reduced at higher tank temperatures:

eff = baseEff – 0.002 × (TankTemp – 25°C)


A lower and upper bound is applied (0.50 – 0.90), preventing unrealistic values.

4. Heat Loss

Heat loss grows as the difference between tank and ambient temperature increases.
A dynamic factor (up to +50%) is applied to simulate stronger heat rejection at high ΔT.

5. Hourly Data Sampling

To keep the chart responsive, only one data point per hour is plotted,
even though the physical simulation runs every minute.

🖥️ User Interface

The interface allows users to enter:

Panel area (m²)

Tank volume (L)

Average daily temperature (°C)

Sun exposure duration (hours)

Days to simulate

Base panel efficiency

Peak irradiance (W/m²)

Heat-loss coefficient

Results include:

Final tank temperature

Total pump runtime

Daily temperature summary table

Temperature vs. time graph (Chart.js)

All calculations occur in the browser — no backend required.

🗂️ Project Structure
/index.html      → UI layout
/style.css       → Dark-themed styling
/script.js       → Simulation logic + chart rendering


The JavaScript file contains:

Input validation

Core simulation loop

Hourly sampling system

Daily summary generation

Chart.js integration

🛠️ Technologies Used

HTML5

CSS3 (custom dark theme)

JavaScript (ES6)

Chart.js for visualization

There are no external frameworks.
Everything is implemented manually to keep the project lightweight and easily auditable.

📌 Example Output

Final tank temperature after X days

Pump runtime in hours

Hour-by-hour temperature curve

Daily temperature table

The chart updates instantly when the user reruns the simulation with different parameters.

⚠️ Assumptions & Limitations

This model intentionally simplifies several real-world factors:

Water is treated as perfectly mixed (uniform temperature).

Weather conditions (clouds, wind, humidity) are not included.

Solar panel orientation, tilt angle, and shading are not modeled.

Pipe heat losses and pump efficiency are ignored.

Irradiance is approximated with a sine curve—not measured data.

Despite these limitations, the simulation still provides useful estimates for typical solar-thermal setups.
