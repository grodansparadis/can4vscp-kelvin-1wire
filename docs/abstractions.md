# Abstractions

A VSCP unit is  describing it's configuration to the world with a register model where each register is eight bit in width. This is often inconvenient for a human user who is used to higher level types and this is what <em>abstractions</em> are there for. They sit above registers and specify types as strings, floats, integers and other such higher level types.

## B Constant

B constant for the **on board** NTC sensor.

| Name | Type | Description |
| --- | --- | --- |
| BetaSensor0 | uint32_t | B constant for the on board NTC sensor. |

## Temperature registers

| Name | Type | Description |
| --- | --- | --- |
| TemperatureSensor0 | float | Current temperature sensor 0. |
| TemperatureSensor1 | float | Current temperature sensor 1. |
| TemperatureSensor2 | float | Current temperature sensor 2. |
| TemperatureSensor3 | float | Current temperature sensor 3. |
| TemperatureSensor4 | float | Current temperature sensor 4. |
| TemperatureSensor5 | float | Current temperature sensor 5. |
| TemperatureSensor6 | float | Current temperature sensor 6. |
| TemperatureSensor7 | float | Current temperature sensor 7. |
| TemperatureSensor8 | float | Current temperature sensor 8 (on-board sensor). |

## Low alarm

| Name | Type | Description |
| --- | --- | --- |
| LowAlarmSensor0 | int32_t | Low alarm sensor 0. |
| LowAlarmSensor1 | int32_t | Low alarm sensor 1. |
| LowAlarmSensor2 | int32_t | Low alarm sensor 2. |
| LowAlarmSensor3 | int32_t | Low alarm sensor 3. |
| LowAlarmSensor4 | int32_t | Low alarm sensor 4. |
| LowAlarmSensor5 | int32_t | Low alarm sensor 5. |
| LowAlarmSensor6 | int32_t | Low alarm sensor 6. |
| LowAlarmSensor7 | int32_t | Low alarm sensor 7. |

## High alarm

| Name | Type | Description |
| --- | --- | --- |
| HighAlarmSensor0 | int32_t | High alarm sensor 0. |
| HighAlarmSensor1 | int32_t | High alarm sensor 1. |
| HighAlarmSensor2 | int32_t | High alarm sensor 2. |
| HighAlarmSensor3 | int32_t | High alarm sensor 3. |
| HighAlarmSensor4 | int32_t | High alarm sensor 4. |
| HighAlarmSensor5 | int32_t | High alarm sensor 5. |
| HighAlarmSensor6 | int32_t | High alarm sensor 6. |
| HighAlarmSensor7 | int32_t | High alarm sensor 7. |

## Absolute low temperature

| Name | Type | Description |
| --- | --- | --- |
| AbsoluteLowSensor0 | int32_t | Absolute low sensor 0. |
| AbsoluteLowSensor1 | int32_t | Absolute low sensor 1. |
| AbsoluteLowSensor2 | int32_t | Absolute low sensor 2. |
| AbsoluteLowSensor3 | int32_t | Absolute low sensor 3. |
| AbsoluteLowSensor4 | int32_t | Absolute low sensor 4. |
| AbsoluteLowSensor5 | int32_t | Absolute low sensor 5. |
| AbsoluteLowSensor6 | int32_t | Absolute low sensor 6. |
| AbsoluteLowSensor7 | int32_t | Absolute low sensor 7. |

## Absolute high temperature

| Name | Type | Description |
| --- | --- | --- |
| AbsoluteHighSensor0 | int32_t | Absolute high sensor 0. |
| AbsoluteHighSensor1 | int32_t | Absolute high sensor 1. |
| AbsoluteHighSensor2 | int32_t | Absolute high sensor 2. |
| AbsoluteHighSensor3 | int32_t | Absolute high sensor 3. |
| AbsoluteHighSensor4 | int32_t | Absolute high sensor 4. |
| AbsoluteHighSensor5 | int32_t | Absolute high sensor 5. |
| AbsoluteHighSensor6 | int32_t | Absolute high sensor 6. |
| AbsoluteHighSensor7 | int32_t | Absolute high sensor 7. |

## Sensor calibration registers

| Name | Type | Description |
| --- | --- | --- |
| CalibrationSensor0 | int32_t | Calibration for sensor 0. |
| CalibrationSensor1 | int32_t | Calibration for sensor 1. |
| CalibrationSensor2 | int32_t | Calibration for sensor 2. |
| CalibrationSensor3 | int32_t | Calibration for sensor 3. |
| CalibrationSensor4 | int32_t | Calibration for sensor 4. |
| CalibrationSensor5 | int32_t | Calibration for sensor 5. |
| CalibrationSensor6 | int32_t | Calibration for sensor 6. |
| CalibrationSensor7 | int32_t | Calibration for sensor 7. |
