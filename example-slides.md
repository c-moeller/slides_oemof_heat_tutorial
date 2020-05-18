---
author: Caroline Möller, Christoph Pels Leusden, Franziska Pleißner, Jakob Wolf, Jann Launer, Marie-Claire Gering, Silke Köhler
title: The oemof.thermal package
subtitle: How to use the new thermal components
institute: Reiner Lemoine Institut, Beuth University of Applied Sciences
classoption: aspectratio=169
date: May 13, 2020
theme: default
urlcolor: blue
---

# The oemof.thermal package

:::::: {.columns}
::: {.column  width=55%}
- Provides tools to model thermal energy components in energy system optimization as an extension of oemof.solph
  - Stratified thermal storage
  - Solar thermal collector
  - Concentrating solar power
  - Compression heat pump and chiller
  - To be released soon: absorption heat pump - [PR #74](https://github.com/oemof/oemof-thermal/pull/74)
:::

::: {.column  width=45%}
\includegraphics[width=\textwidth]{img/content/oemof_solph_komponente_v3.png}
:::
::::::


# How to install the oemof.thermal package

Install oemof.thermal by running

~~~bash
pip install oemof.thermal
~~~

in your virtualenv.

\vspace{0.4cm}

In your code, you can import moduls like:

~~~python
from oemof.thermal import concentrating_solar_power
~~~

\vspace{0.4cm}

Find the examples here: [https://github.com/oemof/oemof-thermal/tree/master/examples](https://github.com/oemof/oemof-thermal/tree/master/examples)

\vspace{0.4cm}

Find the documentation at [https://oemof-thermal.readthedocs.io](https://oemof-thermal.readthedocs.io).


# How to use the oemof.thermal package

- There are two ways:
  - Use the oemof.thermal facades, which are based on the [oemof.tabular.facades module](https://oemof-tabular.readthedocs.io/en/stable/reference/oemof.tabular.html), for a simple way to set up an oemof.solph component for your energy system - Facades are provided for the three technologies "stratified thermal storage", "solar thermal collector" and "concentrating solar power".
  - Use the collection of functions for each technology independently to perform pre-calculations of an optimization model or postprocess optimization results


# Stratified thermal storage

:::::: {.columns}
::: {.column  width=55%}
- Large-scale sensible heat storage with perfect stratification
- Two zones with cold ($T_C$) and hot($T_H$) temperature
- When charging/discharging the storage the thermocline moves down and up
- Losses through the surface depend on the size of the hot and cold zone
- For the storage investment mode, you provide a diameter, but leave height and capacity open and set expandable=True.
:::

::: {.column  width=45%}
\includegraphics[width=\textwidth]{img/content/stratified_thermal_storage.png}
:::
::::::

# Stratified thermal storage

\scriptsize

~~~ python
from oemof import solph
from oemof.thermal.facades import StratifiedThermalStorage

thermal_storage = StratifiedThermalStorage(
    label='thermal_storage',
    bus=solph.Bus('heat'),
    diameter=2,
    temp_h=95,
    temp_c=60,
    temp_env=10,
    u_value=u_value,
    expandable=True,
    capacity_cost=50,
    storage_capacity_cost=400,
    min_storage_level=0.05,
    max_storage_level=0.95,
    efficiency=0.98,
    marginal_cost=0.0001
)
~~~

\normalsize


# Solar thermal collector

:::::: {.columns}
::: {.column  width=55%}
- Explain
- what's
- to
- see
:::

::: {.column  width=45%}
\includegraphics[width=\textwidth]{img/content/solar_thermal_collector.png}
:::
::::::

# Solar thermal collector

\tiny

~~~python
from oemof import solph
from oemof.thermal.facades import SolarThermalCollector

collector = SolarThermalCollector(
    label='solar_collector',
    heat_out_bus=solph.Bus(label='thermal'),
    electricity_in_bus=solph.Bus(label='electricity'),
    electrical_consumption=0.02,
    peripheral_losses=0.05,
    aperture_area=1000,
    latitude=52.2443,
    longitude=10.5594,
    collector_tilt=10,
    collector_azimuth=20,
    eta_0=0.73,
    a_1=1.7,
    a_2=0.016,
    temp_collector_inlet=20,
    delta_temp_n=10,
    irradiance_global=input_data['global_horizontal_W_m2'],
    irradiance_diffuse=input_data['diffuse_horizontal_W_m2'],
    temp_amb_col=input_data['temp_amb'],
)
~~~

\normalsize

# Solar thermal collector

# Concentrating solar power

:::::: {.columns}
::: {.column  width=65%}
- Explain
- what's
- to
- see
:::

::: {.column  width=35%}
\includegraphics[width=\textwidth]{img/content/concentrating_solar_power_2_zugeschnitten.png}
:::
::::::

# Concentrating solar power

\tiny

~~~python
from oemof import solph
from oemof.thermal.facades import Collector

collector = Collector(
    label='solar_collector',
    heat_bus=solph.Bus(label='thermal_bus'),
    electrical_bus=solph.Bus(label='electrical_bus'),
    electrical_consumption=0.05,
    additional_losses=0.2,
    aperture_area=1000,
    loss_method='Janotte',
    irradiance_method='horizontal',
    latitude=23.614328,
    longitude=58.545284,
    collector_tilt=10,
    collector_azimuth=180,
    x=0.9,
    a_1=-0.00159,
    a_2=0.0000977,
    eta_0=0.816,
    c_1=0.0622,
    c_2=0.00023,
    temp_collector_inlet=435,
    temp_collector_outlet=500,
    temp_amb=input_data['t_amb'],
    irradiance=input_data['E_dir_hor']
)
~~~

\normalsize

# Concentrating solar power


# Compression heat pump and chillers

:::::: {.columns}
::: {.column  width=75%}
- Explain
- what's
- to
- see
:::

::: {.column  width=25%}
\includegraphics[width=\textwidth]{img/content/heatpump_col.png}
:::
::::::

# Compression heat pump and chillers

\small

~~~python
COP = calc_cops(
    temp_high,
    temp_low,
    quality_grade,
    temp_threshold_icing,
    consider_icing,
    factor_icing,
    mode
)
~~~

\normalsize

# Compression heat pump and chillers

# Cogeneration: Emission allocation

# Questions?

- If you have further questions:
  - Use the oemof forum: ....
  - Contact: caroline.moeller@rl-institut.de

