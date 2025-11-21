 # ☀️ Solar Tank Temperature Simulator

This project is something play around with how a solar-heated water tank might behave over time.
The goal wasn’t to create a perfect scientific model, but to have a simple browser-based simulation where you can change a few parameters and see how the tank temperature and panel temperature moves.

I tried to keep the logic readable so It will be easier to edit later.

## 🔧 What the Simulation Does

The simulation estimates tank temperature changes based on:

solar irradiance

panel area

tank area

tank volume

heat losses to environment

panel efficiency (drops slightly when tank gets hotter)

average outside air temperature

how many hours you want to simulate

starting tank temperature

Every minute of simulated time, the code calculates:

incoming solar heat (only during sun hours)

heat loss to outside air

new tank temperature

Then it records one value per hour so the chart doesn’t explode.

## 🖥️ Tech Used

HTML – simple form + layout

CSS – for styling

JavaScript – all logic lives here

Chart.js – for the graph (temperature vs time)

Everything is in three separate files for clarity:
index.html, style.css, script.js.

## ▶️ How to Run It

After you extract whole files in same folder:
Just open index.html in any browser.
No server required.

## 📝 How to Use

When the page loads:

Enter panel area (m²)

Enter tank volume (L)

Enter tank area (m²)

Enter starting tank temperature

Enter isolation inputs

Set average outdoor temp

Set how many sunlight hours your area has

Choose simulation time in hours

Hit Run Simulation

You’ll see:

final tank temperature

total pump runtime

temperature curve over the whole period


## 📐 Model Equations

Solar irradiance:
I(t) = I_peak * [ sin( PI * (t_day / t_sun) ) ]^1.3 * (1 - 0.15*r)

Temperature-dependent efficiency:
eta(T_panel) = eta_base * (1 - 0.0035 * (T_panel - 25))

Solar gain:
Q_solar = A * I(t) * eta(T_panel)

Heat loss:
k_base = (lambda / d) * A_tank
k_eff  = k_base * (1 + f)
f      = min(0.5, (ΔT/40)*0.5)
Q_loss = k_eff * (T - T_amb)

Energy balance:
T_new = T_old + (Q_solar - Q_loss) / (m * c_p) * dt
