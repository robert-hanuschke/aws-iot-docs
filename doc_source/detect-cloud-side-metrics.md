# Cloud\-side metrics<a name="detect-cloud-side-metrics"></a>

When creating a Security Profile, you can specify your IoT device's expected behavior by configuring behaviors and thresholds for metrics generated by IoT devices\. The following are cloud\-side metrics, which are metrics from AWS IoT\.

## Message size \(aws:message\-byte\-size\)<a name="detect-message-size"></a>

The number of bytes in a message\. Use this metric to specify the maximum or minimum size \(in bytes\) of each message transmitted from a device to AWS IoT\.

Compatible with: Rules Detect \| ML Detect

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Units: bytes 

**Example**  

```
{
  "name": "Max Message Size",
  "metric": "aws:message-byte-size",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "value": {
      "count": 1024
    },
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{

  "name": "Large Message Size",
  "metric": "aws:message-byte-size",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p90"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Message size ML behavior",
  "metric": "aws:message-byte-size",
  "criteria": {
	 "consecutiveDatapointsToAlarm": 1,
	 "consecutiveDatapointsToClear": 1,
	 "mlDetectionConfig": {
	   "confidenceLevel": "HIGH"
   }
	},
  "suppressAlerts": true
}
```

An alarm occurs for a device if during three consecutive five\-minute periods, it transmits messages where the cumulative size is more than that measured for 90 percent of all other devices reporting for this Security Profile behavior\.

## Messages sent \(aws:num\-messages\-sent\)<a name="detect-messages-sent"></a>

The number of messages sent by a device during a given time period\.

Use this metric to specify the maximum or minimum number of messages that can be sent between AWS IoT and each device in a given period of time\.

Compatible with: Rules Detect \| ML Detect

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Units: messages 

Duration: a non\-negative integer\. Valid values are 300, 600, 900, 1800, or 3600 seconds\.

**Example**  

```
{

  "name": "Out bound message count",
  "metric": "aws:num-messages-sent",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "value": {
      "count": 50
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
    },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{

  "name": "Out bound message rate",
  "metric": "aws:num-messages-sent",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p99"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Messages sent ML behavior",
  "metric": "aws:num-messages-sent",
  "criteria": {
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1,
    "mlDetectionConfig": {
      "confidenceLevel": "HIGH"
    }
  },
  "suppressAlerts": true
}
```

## Messages received \(aws:num\-messages\-received\)<a name="detect-messages-received"></a>

The number of messages received by a device during a given time period\.

Use this metric to specify the maximum or minimum number of messages that can be received between AWS IoT and each device in a given period of time\.

Compatible with: Rules Detect \| ML Detect

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Units: messages 

Duration: a non\-negative integer\. Valid values are 300, 600, 900, 1800, or 3600 seconds\.

**Example**  

```
{
  "name": "In bound message count",
  "metric": "aws:num-messages-received",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "value": {
      "count": 50
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
    },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{
  "name": "In bound message rate",
  "metric": "aws:num-messages-received",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p99"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Messages received ML behavior",
  "metric": "aws:num-messages-received",
  "criteria": {
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1,
    "mlDetectionConfig": {
      "confidenceLevel": "HIGH"
    }
  },
  "suppressAlerts": true
}
```

## Authorization failures \(aws:num\-authorization\-failures\)<a name="detect-auth-failures"></a>

Use this metric to specify the maximum number of authorization failures allowed for each device in a given period of time\. An authorization failure occurs when a request from a device to AWS IoT is denied \(for example, if a device attempts to publish to a topic for which it does not have sufficient permissions\)\. 

Compatible with: Rules Detect \| ML Detect

Unit: failures 

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Duration: a non\-negative integer\. Valid values are 300, 600, 900, 1800, or 3600 seconds\.

**Example**  

```
{
  "name": "Authorization Failures",
  "metric": "aws:num-authorization-failures",
  "criteria": {
    "comparisonOperator": "less-than",
    "value": {
      "count": 5
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{
  "name": "Authorization Failures",
  "metric": "aws:num-authorization-failures",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p50"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Authorization failures ML behavior",
  "metric": "aws:num-authorization-failures",
  "criteria": {
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1,
    "mlDetectionConfig": {
      "confidenceLevel": "HIGH"
    }
  },
  "suppressAlerts": true
}
```

## Source IP \(aws:source\-ip\-address\)<a name="detect-ip-address"></a>

The IP address from which a device has connected to AWS IoT\.

Use this metric to specify a set of allowed \(formerly referred to as whitelisted\) or denied \(formerly referred to as blacklisted\) Classless Inter\-Domain Routings \(CIDR\) from which each device must or must not connect to AWS IoT\.

Compatible with: Rules Detect

Operators: in\-cidr\-set \| not\-in\-cidr\-set 

Values: a list of CIDRs

Units: n/a

**Example**  

```
{
  "name": "Denied source IPs",
  "metric": "aws:source-ip-address",
  "criteria": {
    "comparisonOperator": "not-in-cidr-set",
    "value": {
      "cidrs": [ "12.8.0.0/16", "15.102.16.0/24" ]
    }
  },
  "suppressAlerts": true
}
```

## Connection attempts \(aws:num\-connection\-attempts\)<a name="detect-num-connection-attempts"></a>

The number of times a device attempts to make a connection in a given time period\.

Use this metric to specify the maximum or minimum number of connection attempts for each device\. Successful and unsuccessful attempts are counted\.

Compatible with: Rules Detect \| ML Detect

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Units: connection attempts

Duration: a non\-negative integer\. Valid values are 300, 600, 900, 1800, or 3600 seconds\.

**Example**  

```
{
  "name": "Connection Attempts",
  "metric": "aws:num-connection-attempts",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "value": {
      "count": 5
    },
    "durationSeconds": 600,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{
  "name": "Connection Attempts",
  "metric": "aws:num-connection-attempts",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p10"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Connection attempts ML behavior",
  "metric": "aws:num-connection-attempts",
  "criteria": {
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1,
    "mlDetectionConfig": {
      "confidenceLevel": "HIGH"
    }
  },
  "suppressAlerts": false
}
```

## Disconnects \(aws:num\-disconnects\)<a name="detect-num-disconnects"></a>

The number of times a device disconnects from AWS IoT during a given time period\.

Use this metric to specify the maximum or minimum number of times a device disconnected from AWS IoT during a given time period\.

Compatible with: Rules Detect \| ML Detect

Operators: less\-than \| less\-than\-equal \| greater\-than \| greater\-than\-equal 

Value: a non\-negative integer 

Units: disconnects

Duration: a non\-negative integer\. Valid values are 300, 600, 900, 1800, or 3600 seconds\.

**Example**  

```
{
  "name": "Disconnections",
  "metric": "aws:num-disconnects",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "value": {
      "count": 5
    },
    "durationSeconds": 600,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using a `statisticalThreshold`**  

```
{
  "name": "Disconnections",
  "metric": "aws:num-disconnects",
  "criteria": {
    "comparisonOperator": "less-than-equal",
    "statisticalThreshold": {
      "statistic": "p10"
    },
    "durationSeconds": 300,
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1
  },
  "suppressAlerts": true
}
```

**Example using ML Detect**  

```
{
  "name": "Disconnects ML behavior",
  "metric": "aws:num-disconnects",
  "criteria": {
    "consecutiveDatapointsToAlarm": 1,
    "consecutiveDatapointsToClear": 1,
    "mlDetectionConfig": {
      "confidenceLevel": "HIGH"
    }
  },
  "suppressAlerts": true
}
```