# Sense

Common Message Structure to be used in Industrial IoT while working with OPC UA, Modbus, Object Based Protocols. The message structure is in draft level. The message format is in Json format, we yet to define Protocol Buffer and Avro formats.

We categorize message structure into normal and minified format, for normal vs constrainted devices. we are working on minified format. 

Every message defined here shall be used in MQTT, HTTP, Web Socket Payload for sending, retriving information. 

Each message shall contain a mandatory type information, which further classify the message format in the json object.

A Type of the message can be 'read', 'write', 'subscribe', 'unsubscribe', 'process', 'status', 'alert', 'diagnostic' or 'config' type.

'process' is a type of the message send from device to cloud, to be used to report process conditions as parameter such as current process details such as current temperature, current pressure, energy, total energy for the process industry, or success, failure for the discrete part manufacturing plants. Classifying 'process' variable at edge device reduce a large workload in the upstream and cloud system.

'alert' is a type of the message send from device to cloud, to be used to report process alert such as high temperature, out of service, too low fuel status. 

'status' is a type of the message send from device to cloud, to be used to report device status like running, stopped, in maintenance, pause, etc. 

'diagnostic' is a type of the message send from device to cloud, to be used to report device internal details which may help a service engineer to troubleshoot the device like single/noise ratio, noise, freq, etc.

'config' is a type of the message send from device to cloud when device internal configuration got changed like unit changed from 'celcious' to farenheit or speed changed to km/hr to miles/hr or calibration factors changed that may affect the overall device parameters.



```json
{
    "type": "process",
    "id": 123,
    timestamp: 1213232323232
    thing_id: "",
    values: [
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

