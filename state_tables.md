## Authorization System

| **Current State** | **Inputs**                                       | **Next State** | **Outputs**        |
|--------------------|-------------------------------------------------|----------------|--------------------|
| IDLE              | username, password entered                      | CHECK          | authorized = 0     |
| CHECK             | Valid credentials (username == USERNAME and password == PASSWORD) | AUTHORIZED     | authorized = 0     |
| CHECK             | Invalid credentials                             | IDLE           | authorized = 0     |
| AUTHORIZED        | -                                               | IDLE           | authorized = 1     |


## General Management System

| **Current State** | **Inputs**                     | **Next State**       | **Outputs**                                 |
|--------------------|-------------------------------|-----------------------|---------------------------------------------|
| IDLE              | user_id entered              | VALIDATE             | access_granted = 0, operation_success = 0  |
| VALIDATE          | Valid user_id                | OPERATION_CHECK      | access_granted = 1, operation_success = 0  |
| VALIDATE          | Invalid user_id              | IDLE                 | access_granted = 0, operation_success = 0  |
| OPERATION_CHECK   | Valid operation for role     | SUCCESS              | operation_success = 1                      |
| OPERATION_CHECK   | Invalid operation for role   | FAILURE              | operation_success = 0                      |
| SUCCESS           | -                            | IDLE                 | access_granted = 0, operation_success = 0  |
| FAILURE           | -                            | IDLE                 | access_granted = 0, operation_success = 0  |


## Smart Lighting System

| **Current State** | **Inputs**                                                                                      | **Next State** | **Outputs**     |
|--------------------|------------------------------------------------------------------------------------------------|----------------|-----------------|
| IDLE              | manual_switch = 1                                                                             | ON             | light = 1       |
| IDLE              | light_sensor = 1 and (motion_sensor = 1 or (hour >= NIGHT_START or hour < NIGHT_END))          | ON             | light = 1       |
| IDLE              | manual_switch = 0, light_sensor = 0, and no motion or night condition                          | OFF            | light = 0       |
| ON                | manual_switch = 0 and no valid conditions for light to stay on                                 | OFF            | light = 0       |
| ON                | Valid conditions persist (manual switch, motion, or light sensor active)                       | ON             | light = 1       |
| OFF               | manual_switch = 1                                                                             | ON             | light = 1       |
| OFF               | Valid conditions appear (light_sensor, motion, or night condition)                            | ON             | light = 1       |
| OFF               | No conditions met                                                                             | OFF            | light = 0       |


## White Goods Control System

| **Current State** | **Inputs**                                                  | **Next State**  | **Outputs**          |
|--------------------|------------------------------------------------------------|-----------------|----------------------|
| IDLE              | manual_laundry = 1                                         | LAUNDRY_ON      | laundry_on = 1       |
| IDLE              | hour == LAUNDRY_AUTO_START                                 | LAUNDRY_ON      | laundry_on = 1       |
| IDLE              | manual_dishwasher = 1                                      | DISHWASHER_ON   | dishwasher_on = 1    |
| IDLE              | hour == DISHWASHER_AUTO_START                              | DISHWASHER_ON   | dishwasher_on = 1    |
| IDLE              | manual_oven = 1                                            | OVEN_ON         | oven_on = 1          |
| IDLE              | hour == OVEN_AUTO_START                                    | OVEN_ON         | oven_on = 1          |
| LAUNDRY_ON        | manual_laundry = 0 and hour != LAUNDRY_AUTO_START          | IDLE            | laundry_on = 0       |
| DISHWASHER_ON     | manual_dishwasher = 0 and hour != DISHWASHER_AUTO_START    | IDLE            | dishwasher_on = 0    |
| OVEN_ON           | manual_oven = 0 and hour != OVEN_AUTO_START                | IDLE            | oven_on = 0          |


## Smart Home Control System

| **Current State** | **Inputs**                                                      | **Next State**  | **Outputs**           |
|--------------------|----------------------------------------------------------------|-----------------|-----------------------|
| IDLE              | manual_curtain = 1                                             | CURTAIN_OPEN    | curtain_open = 1      |
| IDLE              | !sunlight_sensor                                               | CURTAIN_OPEN    | curtain_open = 1      |
| IDLE              | sunlight_sensor                                                | CURTAIN_CLOSED  | curtain_open = 0      |
| IDLE              | manual_window = 1                                              | WINDOW_OPEN     | window_open = 1       |
| IDLE              | temp_sensor = 1 and air_quality_sensor = 1                     | WINDOW_OPEN     | window_open = 1       |
| IDLE              | !(temp_sensor and air_quality_sensor)                          | WINDOW_CLOSED   | window_open = 0       |
| IDLE              | manual_door_lock = 1                                           | DOOR_LOCKED     | door_locked = 1       |
| IDLE              | manual_door_lock = 0                                           | DOOR_UNLOCKED   | door_locked = 0       |
| CURTAIN_OPEN      | manual_curtain = 0 and sunlight_sensor                         | CURTAIN_CLOSED  | curtain_open = 0      |
| WINDOW_OPEN       | manual_window = 0 and !(temp_sensor and air_quality_sensor)    | WINDOW_CLOSED   | window_open = 0       |
| DOOR_LOCKED       | manual_door_lock = 0                                           | DOOR_UNLOCKED   | door_locked = 0       |


## Climate Control System

| **Current State**  | **Inputs**                                                      | **Next State**      | **Outputs**               |
|---------------------|----------------------------------------------------------------|---------------------|---------------------------|
| IDLE               | manual_heater = 1                                             | HEATER_ON           | heater_on = 1            |
| IDLE               | temp < TEMP_LOW_THRESHOLD                                      | HEATER_ON           | heater_on = 1            |
| IDLE               | manual_ac = 1                                                 | AC_ON               | ac_on = 1                |
| IDLE               | temp > TEMP_HIGH_THRESHOLD                                     | AC_ON               | ac_on = 1                |
| IDLE               | manual_humidifier = 1                                         | HUMIDIFIER_ON       | humidifier_on = 1        |
| IDLE               | humidity < HUMIDITY_LOW_THRESHOLD                              | HUMIDIFIER_ON       | humidifier_on = 1        |
| IDLE               | manual_dehumidifier = 1                                       | DEHUMIDIFIER_ON     | dehumidifier_on = 1      |
| IDLE               | humidity > HUMIDITY_HIGH_THRESHOLD                             | DEHUMIDIFIER_ON     | dehumidifier_on = 1      |
| HEATER_ON          | manual_heater = 0 and temp >= TEMP_LOW_THRESHOLD              | IDLE                | heater_on = 0            |
| AC_ON              | manual_ac = 0 and temp <= TEMP_HIGH_THRESHOLD                 | IDLE                | ac_on = 0                |
| HUMIDIFIER_ON      | manual_humidifier = 0 and humidity >= HUMIDITY_LOW_THRESHOLD  | IDLE                | humidifier_on = 0        |
| DEHUMIDIFIER_ON    | manual_dehumidifier = 0 and humidity <= HUMIDITY_HIGH_THRESHOLD | IDLE              | dehumidifier_on = 0      |


## AC Control System

| **Current State** | **Inputs**                                   | **Next State** | **Outputs**    |
|--------------------|---------------------------------------------|----------------|----------------|
| IDLE              | manual_ac = 1                              | AC_ON          | ac_on = 1      |
| IDLE              | temp > target_temp_high                    | AC_ON          | ac_on = 1      |
| IDLE              | temp <= target_temp_high and manual_ac = 0 | IDLE           | ac_on = 0      |
| AC_ON             | manual_ac = 0 and temp <= target_temp_high | IDLE           | ac_on = 0      |
| AC_ON             | manual_ac = 1 or temp > target_temp_high   | AC_ON          | ac_on = 1      |


## Heating Control System

| **Current State** | **Inputs**                                   | **Next State** | **Outputs**    |
|--------------------|---------------------------------------------|----------------|----------------|
| IDLE              | manual_heater = 1                          | HEATER_ON      | heater_on = 1  |
| IDLE              | temp < target_temp_low                     | HEATER_ON      | heater_on = 1  |
| IDLE              | temp >= target_temp_low and manual_heater = 0 | IDLE           | heater_on = 0  |
| HEATER_ON         | manual_heater = 0 and temp >= target_temp_low | IDLE           | heater_on = 0  |
| HEATER_ON         | manual_heater = 1 or temp < target_temp_low | HEATER_ON      | heater_on = 1  |


## Safety System

| **Current State** | **Inputs**                              | **Next State** | **Outputs**  |
|--------------------|-----------------------------------------|----------------|--------------|
| IDLE              | arm_system = 1 and motion_sensor = 1   | ALARM_ON       | alarm = 1    |
| IDLE              | arm_system = 1 and motion_sensor = 0   | IDLE           | alarm = 0    |
| IDLE              | arm_system = 0                        | IDLE           | alarm = 0    |
| ALARM_ON          | arm_system = 0                        | IDLE           | alarm = 0    |
| ALARM_ON          | arm_system = 1 and motion_sensor = 1   | ALARM_ON       | alarm = 1    |






