# Sense

Common Message Structure to be used in Industrial IoT while working with OPC UA, Modbus, Object Based Protocols. The message structure is in draft level. The message format is in Json format, we yet to define Protocol Buffer and Avro formats.

We categorize message structure into normal and minified format, for normal vs constrainted devices. we are working on minified format. 

Every message defined here shall be used in MQTT, HTTP, Web Socket Payload for sending, retriving information. 

Each message shall contain a mandatory type information, which further classify the message format in the json object.

A *type* of the message can be 'read', 'write', 'subscribe', 'unsubscribe', 'process', 'status', 'alert', 'diagnostic' or 'config' type.

'process' is a type of the message send from device to cloud, to be used to report process conditions as parameter such as current process details such as current temperature, current pressure, energy, total energy for the process industry, or success, failure for the discrete part manufacturing plants. Classifying 'process' variable at edge device reduce a large workload in the upstream and cloud system.

'alert' is a type of the message send from device to cloud, to be used to report process alert such as high temperature, out of service, too low fuel status. 

'status' is a type of the message send from device to cloud, to be used to report device status like running, stopped, in maintenance, pause, etc. 

'diagnostic' is a type of the message send from device to cloud, to be used to report device internal details which may help a service engineer to troubleshoot the device like single/noise ratio, noise, freq, etc.

'config' is a type of the message send from device to cloud when device internal configuration got changed like unit changed from 'celcious' to farenheit or speed changed to km/hr to miles/hr or calibration factors changed that may affect the overall device parameters.

"id" is a unique message id send from the device to cloud, that consist a the unique number, for the upstream system to find if any duplicates.

"timestamp" is a time when the message was sent from the device to cloud, assuming that the exact same time, the values are captured in the device. If the values are not captured at the time of the timestamp value, then each value should include a timestamp that represent the value was captured. 

"device_id" is the id of the device that sends the message. It should be in string format. 

"payload" represent the information that has been send with the message, like the process values. Based on the "type" values, the values in the payload is categoried. if teh "type" is process, the "payload" contains process values.  

## Process

```json
{
    "type": "process",
    "id": 123,
    "timestamp": 1213232323232,
    "device_id": "323123123",
    "values": [
        {
            "name": "temp",
            "value": 2343.2343,
            "unit": 12
        },
        {
            "name": "humidity",
            "value": 80
        },
    ]
}
```

## Alert


```json
{
    "type": "alert",
    "id": 123,
    "timestamp": 1213232323232,
    "device_id": "323123123",
    "values": [
        {
            "name": "high_temp",
            "value": true,
            "ack": 1
        },
        {
            "name": "low_fuel",
            "value": false,
            "ack": 0
        }
    ]
}
```

## Status


```json
{
    "type": "status",
    "id": 123,
    "timestamp": 1213232323232,
    "device_id": "323123123",
    "values": [
        {
            "name": "running",
            "value": 1
        },
        {
            "name": "communication",
            "value": 1
        },
        {
            "name": "ethernet",
            "value": 1
        }
    ]
}
```

## Read Data on demand
```json
{
    "type": "read",
    "id": 123,
    "device_id": "323123123",
    "items": [
        {
            "name": "flowrate"
        },
        {
            "name": "temperature"
        },
        {
            "name": "pressure"
        }
    ]
}
```
 

## Read Response for the ReadDataRequest
```json
{
    "type": "read-response",
    "id": 123,
    "reply_id": 12324343,
    "device_id": "323123123",
    "values": [
        {
            "name": "flowrate",
            "value": 12
        },
        {
            "name": "temperature",
            "value": 34
        },
        {
            "name": "pressure",
            "value": 12
        }
    ]
}
```


## Write Data on demand
```json
{
    "type": "write",
    "id": 123,
    "device_id": "323123123",
    "values": [
        {
            "name": "flowrate",
            "value": 324
        },
        {
            "name": "temperature",
            "value": 34
        }
    ]
}
```
 

## Read Response for the ReadDataRequest
```json
{
    "type": "write-response",
    "id": 123,
    "reply_id": 12324343,
    "device_id": "323123123",
    "results": [
        {
            "name": "flowrate",
            "status": 1
        },
        {
            "name": "temperature",
            "status": 1
        }
    ]
}
```
