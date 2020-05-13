---
author:
- Caroline Möller
title: The oemof.thermal package
subtitle: How to use the new thermal components
institute: Reiner Lemoine Institut, Beuth University of Applied Sciences
classoption: aspectratio=169
date: \today
theme: rli
urlcolor: rlilinkcolor
header-includes:
- |
  \newcommand{\tel}{+49 (0)30 1208 434 75}
  \newcommand{\email}{caroline.moeller@rl-institut.de}
  \newcommand{\finalstatement}{Enjoy stating a final statement ;-)}
  \tikzset{
  invisible/.style={opacity=0},
  visible on/.style={alt={#1{}{invisible}}},
  alt/.code args={<#1>#2#3}{%
    \alt<#1>{\pgfkeysalso{#2}}{\pgfkeysalso{#3}} % \pgfkeysalso doesn't change the path
  },
  }
  \usepackage{blindtext}
---

# The oemof.thermal package

- Contains thermal components for energy system optimization with oemof.solph
  - Compression heat pump and chiller
  - Stratified thermal storage
  - Solar thermal collector
  - Concentrating solar power

- To be released soon: absorption heat pump - [PR #74](https://github.com/oemof/oemof-thermal/pull/74)
- To be released in an extra repository: district heating network (DHNx)

BILD
Beschriftung anpassen: oemof.thermal


# How to install the oemof.thermal package

pip install ....


# How to use the components

two methods:
- precalculation
- facade

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

# Stratified thermal storage

:::::: {.columns}
::: {.column  width=55%}
- Explain
- what's
- to
- see
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
    height=5,
    temp_h=95,
    temp_c=60,
    temp_env=10,
    u_value=u_value,
    min_storage_level=0.05,
    max_storage_level=0.95,
    capacity=1,
    efficiency=0.9,
    marginal_cost=0.0001
)
~~~

\normalsize

# Stratified thermal storage

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

# Cogeneration: Emission allocation

# Questions?

- If you have further questions:
  - Use the oemof forum: ....
  - Contact: caroline.moeller@rl-institut.de

