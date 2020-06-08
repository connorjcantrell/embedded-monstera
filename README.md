# embedded-monstera
Growing a Monstera is easy. Let's over complicate it by building an embedded device that logs temperature, humidity, light, and soil moisture to a database. This database may later be used for data analysis and building an automated watering system.


## Phase 1: Plant Condition Device
Battery powered embedded device capable of sending remote messages of current sensor data and alerts (Low battery, etc)

Inputs:
- Soil Moisture
- Soil Temperature
- Light Sensor
- Air Temperature & Humidity Sensor


## Phase 2: Main Controller (Raspberry Pi 3b+ running Ubuntu 18.04)
1. Listens for incoming messages from device(s) 
    - Recieves sensor data
    - Receives alerts from device(s)
2. Handles messages
    - Logs sensor data to PostgreSQL database
    - Recieves emergency alerts and notifies user
2. Takes routine daily photo of plant and stores to local storage
3. Analyzes data and determines plant health and optimal watering periods/ durations
4. Sends reports via text message of plant health and recommended watering procedures 
5. (Optional) Sends message back to Automated Watering Device with instructions


In the future, machine learning models can analyze database records to determine optimal growing conditions based on sensor data and images. 

Python scripts can also be used for producing weekly data visualization charts including:
- Image overlays to track plant growth
- Air to soil temperature phasing
- Humidity variation
- Soil moisture variation
- etc

## Phase 3: Automated Watering Device
This device (perhaps the same device as Plant Condition Device), will be listening for a call to water the plant. The incoming message will specify watering duration.

Upon receiving a message, an binary output signal will be sent to open a solenoid. Being as though this is an indoor plant, it would be a gravity fed water line coming from a 1-2 gallon tank. (This tank would need to be manually refilled). The tank would be equipped with a float sensor to track water level of tank. 

If the tank reaches a critically low level, a message will be sent back to the main controller 
If water flow isn't occuring while solenoid is open, an alert will be sent back to main controller

Inputs:
- Flow sensor
- Float sensor

Outputs:
- Solenoid
