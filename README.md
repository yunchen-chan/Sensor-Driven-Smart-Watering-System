# Design and Preliminary Validation of a Low-Cost ESP32-Based Soil-Moisture Feedback Irrigation System

## Plain-Language Summary

Plants are often watered on a fixed schedule even when the soil is already wet. I built and tested a low-cost prototype that measures soil moisture and automatically activates a small pump only when the soil becomes dry.

The system uses an ESP32, a soil-moisture sensor, an LCD screen, and a water pump. Based on my soil tests, I selected 2200 as the dry-soil threshold. The prototype successfully displayed live readings and automatically watered the soil when this threshold was reached.

## Research Extension: Soil-Moisture Sensor Calibration

To evaluate the reliability of the soil-moisture sensor, a replicated calibration study was conducted using independently prepared soil samples.

- **Independent variable:** water added to the soil (0–40 g)
- **Dependent variable:** ESP32 ADC reading
- **Experimental rounds:** 3
- **Independent soil samples:** 11
- **Total ADC measurements:** 55
- **Main replicated conditions:** 0 g, 20 g, and 40 g, each tested using three independently prepared samples
- **Technical repeats:** five ADC readings per soil sample

The results showed a consistent decrease in ADC reading as added water increased. The mean ADC readings for the replicated conditions were approximately:

| Water added | Mean ADC reading |
|---:|---:|
| 0 g | 3308.8 |
| 20 g | 1871.7 |
| 40 g | 1112.2 |

A descriptive linear fit across all five water levels produced an R² value of approximately 0.962. The initial prediction for the 30 g condition differed from the subsequently measured mean by approximately 7.1%.

The complete raw dataset, statistical analysis, experimental protocol, limitations, and calibration graph are available in the [`data`](data/) folder.

## Project Background

I first created a school science-communication project about climate change, SCL water-retention technology, and smart agriculture. I made a poster, recorded an introduction video, displayed the project at school, and collected 30 survey responses.

I then developed one idea from that project into a working interdisciplinary embedded-systems prototype combining electrical and electronic engineering with computer science: a low-cost ESP32 smart watering system.

The system checks whether soil is dry. If the soil is too dry, it automatically turns on a small water pump for a few seconds. An LCD screen shows the soil reading and current system status.

## How It Works

Soil moisture sensor → ESP32 → dryness threshold → water pump → plant

In this project, I tested the sensor with real soil, calibrated the moisture threshold, assembled the hardware, debugged connection problems, and documented the process.

## Research Question

How reliably can calibrated soil-moisture readings be used by a low-cost ESP32 feedback system to detect dry soil and trigger automatic irrigation?

## Research Objective

The objective of this project is to design, calibrate, and preliminarily evaluate a low-cost automatic irrigation controller that uses soil-moisture feedback to identify dry conditions and activate a water pump safely.

## Hypothesis

Based on preliminary sensor observations, I hypothesized that a calibrated ADC threshold could distinguish dry soil from adequately moist soil, trigger irrigation when necessary, and prevent pump activation when the sensor signal was abnormal.

## Main Features

- ESP32 programmed with MicroPython
- Soil moisture sensor for real-time readings
- LCD screen for soil values and system status
- LED indicator during watering
- Automatic water pump control
- Sensor calibration based on experimental data
- 
## Methodology

1. Individual hardware components were tested separately before being integrated into the final prototype.
2. The soil-moisture sensor was tested in wet, slightly dry, and very dry soil to observe differences in raw ADC readings.
3. Based on these observations, a raw ADC value of 2200 was selected as the preliminary dryness threshold.
4. The program averages five consecutive sensor readings to reduce short-term signal fluctuation.
5. The pump, LCD, LED, and sensor-failure response were tested as parts of the complete automatic-control system.
6. 
## System Logic

1. The ESP32 reads the soil moisture sensor.
2. If the soil reading is below 100, the system shows `SENSOR CHECK`.
3. If the soil reading is 2200 or higher, the soil is considered dry.
4. The water pump runs for 3 seconds.
5. The system waits for 60 seconds before measuring again.
6. If the soil is not dry, the LCD shows `MOIST OK`.

## Testing and Calibration Results

| Soil condition | Raw ADC reading | System response |
|---|---:|---|
| Wet soil | About 1000-1500 | Do not water |
| Slightly dry soil | About 1700-1800 | Do not water yet |
| Very dry soil | About 2900 | Watering is needed |
| Final watering threshold | 2200 or higher | Pump runs for 3 seconds |
| Unstable sensor signal | Below 100 or repeatedly 0 | Show `SENSOR CHECK` and do not water |

**Note:** These values are raw ADC readings from 0 to 4095. They are not percentages or millilitres.

## Hardware

- ESP32 development board
- Resistive soil moisture sensor module
- 16x2 I2C LCD display
- Small water pump and tubing
- LED
- Jumper wires and power supply

## Current Status

The core prototype has been built and tested successfully:

- Soil sensor reading and calibration
- LCD display
- Manual pump test
- Automatic watering logic
## Limitations

- Soil readings vary with soil type, sensor placement, and environmental conditions.
- The current prototype does not use the water-level sensor for automatic safety shutdown.
## Future Improvements

- Add a more reliable water-level safety system
- Add Wi-Fi data logging
- Create a mobile dashboard
- Compare water use with fixed-schedule watering
- Add anonymized user-survey results about smart agriculture

## Project Context

This prototype developed from my earlier science-communication project about climate change, smart agriculture, SCL water-retention technology, and data-driven irrigation.

## Survey Results

I also conducted a small student questionnaire about SCL technology, climate change, and sensor-guided smart agriculture. The survey received 30 valid responses and provided context for the design of this prototype.
[View the survey results]

## Research Report

A replicated calibration experiment was conducted across three experimental rounds using five water-addition conditions (0 g, 10 g, 20 g, 30 g, and 40 g). The study includes 11 independently prepared samples, 55 formal ADC measurements, statistical analysis, threshold evaluation, limitations, and photographic evidence.

📄 [Read the full soil-moisture calibration report](reports/soil-moisture-calibration-report-updated.pdf)

## Experimental Data

The calibration dataset contains 55 formal ADC measurements collected from 11 independently prepared samples across five water-addition conditions.

- [View the raw calibration data (CSV)](data/soil_moisture_calibration_raw_data.csv)
- [Download the dataset and statistical analysis (Excel)](data/soil_moisture_calibration_results.xlsx)

## License

MIT License
