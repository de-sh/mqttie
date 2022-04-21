# mqttie :necktie:

**:construction: This is a pre-alpha project, tread carefully :construction:**

An interactive MQTT client for the CLI, inspired from [httpie](https://github.com/httpie/httpie) and built with [rumqttc](https://docs.rs/rumqttc).

Users will be able to use the `mqtt` command as follows:
1. Publish to `this/is/a/topic` on the broker at `host:port`:
```sh
mqtt PUB this/is/a/topic --json { "key": value } --broker host:port
```
2. Subscribe to `this/is/a/topic` on the broker at `host:port`:
```sh
mqtt SUB this/is/a/topic --broker host:port
```

When connecting to the broker, a user must provide their protocol of choice using the host field, by default it shall be `tcp://`. The broker's port address may also be left empty, in which case mqttie will connect to the default MQTT port `1883`. To connect with TLS support, users can provide their `.pem` files with the flags `--ca_certificate`, `--device_certificate` and `--device_private_key` (`-ca`, `-cert` and `-key` in short). 

For simplicity, one may prefer to provide broker details in a JSON file with the following format, along with the `--auth` or `-a` flags:
```json
{
    "device_id": "1234",
    "broker": "example.com",
    "port": 1883,
    "authentication": {
        "ca_certificate": "-----BEGIN CERTIFICATE...",
        "device_certificate": "-----BEGIN CERTIFICATE...",
        "device_private_key": "-----BEGIN RSA PRIVATE KEY..."
    }
}
```
**NOTE:** In case of non-TLS connections, just omit the `"authentication"` entry.

When publishing, users can also set the QoS value for publish messages by using the `--qos` or `-q` flag and providing one of 0, 1 or 2. Users can also choose whether or not the message should be retained by the broker by using the `--retained` or `-r` flag.