# pyats_parser
This library is a workaround to use PyATS parser libraries outside PyATS workflow which consist of declaring devices in a testbed and connect to device with pyATS, execute command with pyATS and finally parse output.

With pyats_parser you just have to fill the cli return collected by NSO live status, netmiko , etc... 

# Installation

```
pip install pyats-parser
```
# Usage
```python
from pyats_parser import parser

show_version = """
RP/0/RSP0/CPU0:MY-DEVICE#show version
Thu Jun 24 14:25:48.716 CEST
Cisco IOS XR Software, Version 7.1.15
Copyright (c) 2013-2020 by Cisco Systems, Inc.

Build Information:
 Built By     : bob
 Built On     : Wed Apr 29 12:55:55 PDT 2020
 Built Host   : iox-ucs-032
 Workspace    : /auto/srcarchive11/prod/7.1.15/asr9k-x64/ws
 Version      : 7.1.15
 Location     : /opt/cisco/XR/packages/
 Label        : 7.1.15

cisco ASR9K () processor
System uptime is 1 year 6 weeks 5 days 18 hours 42 minutes

RP/0/RSP0/CPU0:MY-DEVICE#
"""

result = parser.parse(show_version,"show version","iosxr")
```

And you will get the structured output as a dictionary :
```python
{'operating_system': 'IOSXR', 
 'software_version': '7.1.15', 
 'device_family': 'ASR9K',
 'uptime': '1 year 6 weeks 5 days 18 hours 42 minutes'}
```

- Commands supported : https://pubhub.devnetcloud.com/media/genie-feature-browser/docs/#/parsers
- OS platform and model supported : https://pubhub.devnetcloud.com/media/unicon/docs/user_guide/supported_platforms.html#/
    
This library is inspired from : https://github.com/CiscoDevNet/ansible-pyats/blob/master/library/pyats_parse_command.py

## License

This project is licensed to you under the terms of the [Cisco Sample Code License](https://raw.githubusercontent.com/rtrjl/nso_restconf/master/LICENSE).
