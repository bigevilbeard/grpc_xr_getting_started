# IOS-XR over GRPC


This public repo contains python code that can be used to interact with the Cisco IOS XR devices.The environment is pre-configured to access the [Cisco DevNet Always-On Sandbox](https://devnetsandbox.cisco.com/RM/Diagram/Index/e83cfd31-ade3-4e15-91d6-3118b867a0dd?diagramType=Topology). You can edit the variables in the environment to point to your own IOS-XR device.


This package contains a library with the methods that are available to use over gRPC with IOS-XR boxes after 6.0.0. The API has several methods which allows a user to send simple RPC commands such as get and push using YANG and JSON.

The repo consists of two main components:

The compiled pb2 file from the proto definition.
A Python module accessing the pb2 file with the library bindings.

## Information

XR devices ship with the YANG files that define the data models they support. Using a management protocol such as NETCONF or gRPC, you can programmatically query a device for the list of models it supports and retrieve the model files.

gRPC is an open-source RPC framework. It is based on Protocol Buffers (Protobuf), which is an open source binary serialization protocol. gRPC provides a flexible, efficient, automated mechanism for serializing structured data, like XML, but is smaller and simpler to use. You define the structure using protocol buffer message types in .proto files. Each protocol buffer message is a small logical record of information, containing a series of name-value pairs.

## Getting Started


### Python Environment Setup
It is recommended that this code be used with Python 3.6. It is highly recommended to leverage Python Virtual Environments (venv).

Follow these steps to create and activate a venv.

### OS X or Linux
```
virtualenv venv --python=python3.6
source venv/bin/activate
```

### Enable gRPC

SSH in to the Always-On Sandbox IOS XR router and turn on gRPC and disable tls, below is an example configuration

```
grpc
 port 57777
 no-tls 
```

## Code Example "Get Interfaces"

To get all the interfaces from the Always-On Sandbox IOS-XR device, we can run this small piece of code derived from OpenConfig YANG models and serialise this as `JSON`. Change to into the `examples` diretory and run the following code, this uses the yang model https://github.com/YangModels/yang/blob/master/vendor/cisco/xr/653/openconfig-interfaces.yang and will print all the interface from the Always-On Sandbox IOS-XR device in the `json` format.

```
(venv)python grpc_example.py 
{
    "openconfig-interfaces:interfaces": {
        "interface": [
            {
                "name": "Loopback100",
                "config": {
                    "name": "Loopback100",
                    "type": "iana-if-type:softwareLoopback",
                    "enabled": true,
                    "description": "***MERGE LOOPBACK 100****"
                },
                "subinterfaces": {
                    "subinterface": [
                        {
                            "index": 0,
                            "openconfig-if-ip:ipv4": {
                                "addresses": {
                                    "address": [
                                        {
                                            "ip": "1.1.1.100",
                                            "config": {
                                                "ip": "1.1.1.100",
                                                "prefix-length": 32
                                            }
                                        }
                                    ]
                                }
                            }
                        }
                    ]
                }
            },
[/snip]
```



## About me

Network Automation Developer Advocate for Cisco DevNet.
Find me here: [LinkedIn](https://www.linkedin.com/in/stuarteclark/) / [Twitter](https://twitter.com/bigevilbeard)

Thanks to Karthik Kumaravel and Patrick "Bench Press 500" Rockholz for their code samples and debugging skills.
