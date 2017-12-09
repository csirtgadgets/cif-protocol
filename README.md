# 1. Goals

The CIF protocol is a simple protocol for communicating with a CIF.

* To enable simple communication with CIF

# 2. License

This Specification is free software; you can redistribute it and/or modify it under the terms of the MPLv2 License (see `LICENSE` file).

# 3. Change Process

This document is governed by the [Consensus-Oriented Specification System (COSS)](http://www.digistan.org/spec:1/COSS). In addition:

* Comments MUST be logged as [new issues](https://github.com/blog/411-github-issue-tracker).
* Contributions MUST be logged as [new pull-requests](https://help.github.com/articles/creating-a-pull-request).

# 4. Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

# 5. Protocol
## Indicator Class
The Indicator class is the top level class for describing indicator information. For each class, the semantics will be described and the relationship with other classes will be depicted with UML.

```
+------------------+
| Message          |
+------------------+
| REAL version     |
| binary id        |
| binary client_id |
| enum mtype       |
| binary data      |
+------------------+
```

#####*The Indicator class has the following attributes:*

### version
Required. [REAL](#real-numbers). The specification version number to which this class conforms. While the protocol itself conforms to a [semantic versioning](http://semver.org/), implemented, the protocol version should conform to a REAL (float/double) number using "tenths", to the right of the decimal as a placeholder. Examples:

Semver | REAL
-------|-------
```0.0.1```  | ```0.0010```
```1.0.01``` | ```1.0001```
```2.1.2```  | ```2.1020```
```0.01.01```| ```0.0101```

### binary id
Required. This is the ZeroMQ socket identity.

### binary client_id
Optional. This is the ZeroMQ client socket identity when routing a message using routers.

### enum mtype
Required. This is the message type.

```
PING = 1
PING_WRITE = 2
INDICATORS_CREATE = 3
INDICATORS_SEARCH = 4
INDICATORS_DELETE = 5
TOKENS_SEARCH = 6
TOKENS_CREATE = 7
TOKENS_DELETE = 8
TOKENS_EDIT = 9
```

### string token
Required. API Token.

### binary data
Optional. Data payload being transmitted.

# 6. Examples
```
from cif_protocol.msg import Msg
...

Msg(mtype='ping', token='1234').send(s.socket)
Msg(mtype='indicators_search', token='1234', data=json.dumps(filters)).send(s.socket)
```

# 7. References
## Known Implementations

* cif-protocol-py - [github.com/csirtgadgets](https://github.com/csirtgadgets/cif-protocol-py)
