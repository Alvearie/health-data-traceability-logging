# CADF Serialization Example

This is an example of a CADF event representing an activity that entails data access.

```
{
  "typeURI": "http://schemas.dmtf.org/cloud/audit/1.0/event", 
  "id": "a80dc5ee-be83-48ad-ad5e-6577f2217637"
  ""eventType": "activity", 
  "action": "write",    
  "outcome": "success", 
  "reason": {"reasonCode": "200", "reasonType": "HTTP"}, 
  "eventTime": "2014-01-17T23:23:38+0000", 
  "initiator": { 
    "id": "IBMid-XXX0076Y8P",
    "typeURI": "service/security/account/user", 
    "name": "example@ca.ibm.com"",  
    "credential": { 
      "token" 
    }, 
    "host": { 
      "agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:72.0) Gecko/20100101 Firefox/72.0", 
      "address": "123.456.27.109"
    },
    "geolocation": {
      "regionICANN": "CA", "state": "ON", "city": "Markham"
    }
  },
  "target": { 
    "id": "0f126160203748a5b4923f2eb6e3b7db", 
    "typeURI": "data/file", 
    "name": "nova" 
    "geolocation": {
      "regionICANN": "US", "state": "TX"
    }
  }, 
  "observer": {
    "id": "0f126160203748a456cd2c794f29a",
    "typeURI": "service/compute/servers", 
    "name": "some-application",
    "host": { 
      "address": "123.456.227.19"
    }
    "geolocation": {
      "latitude": "N372207.90",
      "longitude": "W1220210.20",
      "accuracy": "100"
    }
  },
  "tags": [
    "correlation-id?value=bcac04dc-e0be-4110-862c-347088a7836a"
  ]
} 
```
