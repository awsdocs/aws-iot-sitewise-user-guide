# Configure an OPC\-UA source \(CLI\)<a name="configure-opc-ua-source-cli"></a>

You can define OPC\-UA data sources in a gateway capability\. You must define all of your OPC\-UA sources in a single capability configuration\.

For more information about defining sources with the AWS Command Line Interface, see [Configuring data sources \(AWS CLI\)](configure-source-cli.md)\.

This capability has the following versions\.


| Version | Namespace | 
| --- | --- | 
| 1 | iotsitewise:opcuacollector:1 | 

## OPC\-UA capability configuration parameters<a name="opc-ua-source-parameters-cli"></a>

When you define OPC\-UA sources in a capability configuration, you must specify the following information in the `capabilityConfiguration` JSON document:

`sources`  
A list of OPC\-UA source definition structures that each contain the following information:    
`name`  
A unique, friendly name for the source\.  
`endpoint`  
An endpoint structure that contains the following information:    
`certificateTrust`  
A certificate trust policy structure that contains the following information:    
`type`  
The certificate trust mode for the source\. Choose one of the following:  
+ `TrustAny` – The gateway trusts any certificate when it connects to the OPC\-UA source\.
+ `X509` – The gateway trusts an X\.509 certificate when it connects to the OPC\-UA source\. If you choose this option, you must define `certificateBody` in `certificateTrust`\. You can also define `certificateChain` in `certificateTrust`\.  
`certificateBody`  
\(Optional\) The body of an X\.509 certificate\.  
This field is required if you choose `X509` for `type` in `certificateTrust`\.  
`certificateChain`  
\(Optional\) The chain of trust for an X\.509 certificate\.  
This field is used only if you choose `X509` for `type` in `certificateTrust`\.  
`endpointUri`  
The local endpoint of the OPC\-UA source\. For example, your local endpoint might look like `opc.tcp://203.0.113.0:49320`\.  
`securityPolicy`  
The security policy to use so that you can secure messages that are read from the OPC\-UA source\. Choose one of the following:  
+ `NONE` – The gateway doesn't secure messages from the OPC\-UA source\. We recommend that you choose a different security policy\. If you choose this option, you must also choose `NONE` for `messageSecurityMode`\.
+ `BASIC256_SHA256` – The `Basic256Sha256` security policy\.
+ `AES128_SHA256_RSAOAEP` – The `Aes128_Sha256_RsaOaep` security policy\.
+ `AES256_SHA256_RSAPSS` – The `Aes256_Sha256_RsaPss` security policy\.
+ `BASIC128_RSA15` – \(Deprecated\) The `Basic128Rsa15` security policy is deprecated in the OPC\-UA specification because it's no longer considered secure\. We recommend that you choose a different security policy\. For more information, see [Basic128Rsa15](http://opcfoundation.org/UA-Profile/UA/SecurityPolicy%23Basic128Rsa15)\.
+ `BASIC256` – \(Deprecated\) The `Basic256` security policy is deprecated in the OPC\-UA specification because it's no longer considered secure\. We recommend that you choose a different security policy\. For more information, see [Basic256](http://opcfoundation.org/UA-Profile/UA/SecurityPolicy%23Basic256)\.
If you choose a security policy other than `NONE`, you must choose `SIGN` or `SIGN_AND_ENCRYPT` for `messageSecurityMode`\. You must also configure your source server to trust the gateway\. For more information, see [Enabling your source servers to trust the gateway](enable-source-trust.md)\.  
`messageSecurityMode`  
The message security mode to use to secure connections to the OPC\-UA source\. Choose one of the following:  
+ `NONE` – The gateway doesn't secure connections to the OPC\-UA source\. We recommend that you choose a different message security mode\. If you choose this option, you must also choose `NONE` for `securityPolicy`\.
+ `SIGN` – Data in transit between the gateway and the OPC\-UA source is signed but not encrypted\.
+ `SIGN_AND_ENCRYPT` – Data in transit between the gateway and the OPC\-UA source is signed and encrypted\.
If you choose a message security mode other than `NONE`, you must choose a `securityPolicy` other than `NONE`\. You must also configure your source server to trust the gateway\. For more information, see [Enabling your source servers to trust the gateway](enable-source-trust.md)\.  
`identityProvider`  
An identity provider structure that contains the following information:    
`type`  
The type of authentication credentials required by the source\. Choose one of the following:  
+ `Anonymous` – The source doesn't require authentication to connect\.
+ `Username` – The source requires a user name and password to connect\. If you choose this option, you must define `usernameSecretArn` in `identityProvider`\.  
`usernameSecretArn`  
\(Optional\) The ARN of an AWS Secrets Manager secret\. The gateway uses the authentication credentials in this secret when it connects to this source\. You must attach secrets to your gateway's IoT SiteWise connector to use them for source authentication\. For more information, see [Configuring source authentication](configure-source-authentication.md)\.  
This field is required if you choose `Username` for `type` in `identityProvider`\.  
`nodeFilterRules`  
A list of node filter rule structures that define the OPC\-UA data stream paths to send to the AWS Cloud\. You can use node filters to reduce your gateway's startup time and CPU usage by only including paths to data that you model in AWS IoT SiteWise\. By default, gateways upload all OPC\-UA paths except those that start with `/Server/`\. To define OPC\-UA node filters, you can use node paths and the `*` and `**` wildcard characters\. For more information, see [Using OPC\-UA node filters](opc-ua-node-filters.md)\.  
Each structure in the list must contain the following information:    
`action`  
The action for this node filter rule\. You can choose the following option:  
+ `INCLUDE` – The gateway includes only data streams that match this rule\.  
`definition`  
A node filter rule structure that contains the following information:    
`type`  
The type of node filter path for this rule\. You can choose the following option:  
+ `OpcUaRootPath` – The gateway evaluates this node filter path against the root of the OPC\-UA path hierarchy\.  
`rootPath`  
The node filter path to evaluate against the root of the OPC\-UA path hierarchy\. This path must start with `/`\.  
`measurementDataStreamPrefix`  
A string to prepend to all data streams from the source\. The gateway adds this prefix to all data streams from this source\. Use a data stream prefix to distinguish between data streams that have the same name from different sources\. Each data stream should have a unique name within your account\.  
`propertyGroups`  
\(Optional\) The list of property groups that define the `deadband` and `scanMode` requested by the protocol\.    
`name`  
The name of the property group\. This should be a unique identifier\.  
`deadband`  
The `deadband` structure that contains the following information:    
`type`  
The supported types of deadband\. Accepted values are `ABSOLUTE` and `PERCENT`\.  
`value`  
The value of the deadband\. When `type` is `ABSOLUTE`, this value is a unitless double\. When `type` is `PERCENT`, this value is a double between `1` and `100`\.  
`eguMin`  
\(Optional\) The engineering unit minimum when using a `PERCENT` deadband\. You set this if the OPC\-UA server doesn't have engineering units configured\.  
`eguMax`  
\(Optional\) The engineering unit maximum when using a `PERCENT` deadband\. You set this if the OPC\-UA server doesn't have engineering units configured\.  
`timeoutMilliseconds`  
The duration in milliseconds before timeout\. The minimum is `100`\.  
`scanMode`  
The `scanMode` structure that contains the following information:    
`type`  
The supported types of `scanMode`\. Accepted values are `POLL` and `EXCEPTION`\.  
`rate`  
The sampling interval for the scan mode\.

## Capability configuration examples<a name="opc-ua-source-example-cli"></a>

The following example defines an OPC\-UA gateway capability configuration from a payload stored in a JSON file\.

```
aws iotsitewise update-gateway-capability-configuration \
  --capability-namespace "iotsitewise:opcuacollector:1" \
  --capability-configuration file://opc-ua-configuration.json
```

**Example : OPC\-UA source configuration**  
The following `opc-ua-configuration.json` file defines a basic, insecure OPC\-UA source configuration\.  

```
{
  "sources": [
    {
      "name": "Wind Farm #1",
      "endpoint": {
        "certificateTrust": {
          "type": "TrustAny"
        },
        "endpointUri": "opc.tcp://203.0.113.0:49320",
        "securityPolicy": "NONE",
        "messageSecurityMode": "NONE",
        "identityProvider": {
          "type": "Anonymous"
        },
        "nodeFilterRules": []
      },
      "measurementDataStreamPrefix": ""
    }
  ]
}
```

**Example : OPC\-UA source configuration with defined property groups**  
The following `opc-ua-configuration.json` file defines a basic, insecure OPC\-UA source configuration with defined property groups\.  

```
{
    "sources": [
        {
            "name": "source1",
            "endpoint": {
                "certificateTrust": {
                    "type": "TrustAny"
                },
                "endpointUri": "opc.tcp://10.0.0.9:49320",
                "securityPolicy": "NONE",
                "messageSecurityMode": "NONE",
                "identityProvider": {
                    "type": "Anonymous"
                },
                "nodeFilterRules": [
                    {
                        "action": "INCLUDE",
                        "definition": {
                            "type": "OpcUaRootPath",
                            "rootPath": "/Utilities/Tank/*"
                        }
                    }
                ]
            },
            "measurementDataStreamPrefix": "propertyGroups",
           "propertyGroups": [
 
                {
                    "name": "Deadband_Abs_5",
                    "nodeFilterRuleDefinitions": [
                        {
                            "type": "OpcUaRootPath",
                            "rootPath": "/Utilities/Tank/Temperature/TT-001"
                        },
                        {
                            "type": "OpcUaRootPath",
                            "rootPath": "/Utilities/Tank/Temperature/TT-002"
                        }
                    ],
                    "deadband": {
                        "type":"ABSOLUTE",
                        "value": 5.0,
                        "timeoutMilliseconds": 120000
                    }
                },
                {
                    "name": "Polling_10s",
                    "nodeFilterRuleDefinitions": [
                        {
                            "type": "OpcUaRootPath",
                            "rootPath": "/Utilities/Tank/Pressure/PT-001"
                        }
                    ],
                    "scanMode": {
                        "type": "POLL",
                        "rate": 10000
                    }
                },
                {
                    "name": "Percent_Deadband_Timeout_90s",
                    "nodeFilterRuleDefinitions": [
                        {
                            "type": "OpcUaRootPath",
                            "rootPath": "/Utilities/Tank/Flow/FT-*"
                        }
                    ],
                    "deadband": {
                        "type":"PERCENT",
                        "value": 5.0,
                        "eguMin": -100,
                        "eguMax": 100,
                        "timeoutMilliseconds": 90000
                    }
                }
            ]
        }
    ]
}
```

**Example : OPC\-UA source configuration with properties**  
The following JSON example for `opc-ua-configuration.json` defines an OPC\-UA source configuration with the following properties:  
+ Trusts any certificate\.
+ Uses the `BASIC256` security policy to secure messages\.
+ Uses the `SIGN_AND_ENCRYPT` mode to secure connections\.
+ Uses authentication credentials stored in a Secrets Manager secret\.
+ Filters out data streams except those whose path starts with `/WindFarm/2/WindTurbine/`\.
+ Adds `/Washington` to the start of every data stream path to distinguish between this "Wind Farm \#2" and a "Wind Farm \#2" in another area\.

```
{
  "sources": [
    {
      "name": "Wind Farm #2",
      "endpoint": {
        "certificateTrust": {
          "type": "TrustAny"
        },
        "endpointUri": "opc.tcp://203.0.113.1:49320",
        "securityPolicy": "BASIC256",
        "messageSecurityMode": "SIGN_AND_ENCRYPT",
        "identityProvider": {
          "type": "Username",
          "usernameSecretArn": "arn:aws:secretsmanager:region:123456789012:secret:greengrass-windfarm2-auth-1ABCDE"
        },
        "nodeFilterRules": [
          {
            "action": "INCLUDE",
            "definition": {
              "type": "OpcUaRootPath",
              "rootPath": "/WindFarm/2/WindTurbine/"
            }
          }
        ]
      },
      "measurementDataStreamPrefix": "/Washington"
    }
  ]
}
```

**Example**  
The following JSON example for `opc-ua-configuration.json` defines an OPC\-UA source configuration with the following properties:  
+ Trusts a given X\.509 certificate\.
+ Uses the `BASIC256` security policy to secure messages\.
+ Uses the `SIGN_AND_ENCRYPT` mode to secure connections\.

```
{
  "sources": [
    {
      "name": "Wind Farm #3",
      "endpoint": {
        "certificateTrust": {
          "type": "X509",
          "certificateBody": "-----BEGIN CERTIFICATE-----
MIICiTCCAfICCQD6m7oRw0uXOjANBgkqhkiG9w
 0BAQUFADCBiDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZ
 WF0dGxlMQ8wDQYDVQQKEwZBbWF6b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIw
 EAYDVQQDEwlUZXN0Q2lsYWMxHzAdBgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5
 jb20wHhcNMTEwNDI1MjA0NTIxWhcNMTIwNDI0MjA0NTIxWjCBiDELMAkGA1UEBh
 MCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBb
 WF6b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMx
 HzAdBgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5jb20wgZ8wDQYJKoZIhvcNAQE
 BBQADgY0AMIGJAoGBAMaK0dn+a4GmWIWJ21uUSfwfEvySWtC2XADZ4nB+BLYgVI
 k60CpiwsZ3G93vUEIO3IyNoH/f0wYK8m9TrDHudUZg3qX4waLG5M43q7Wgc/MbQ
 ITxOUSQv7c7ugFFDzQGBzZswY6786m86gpEIbb3OhjZnzcvQAaRHhdlQWIMm2nr
 AgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAtCu4nUhVVxYUntneD9+h8Mg9q6q+auN
 KyExzyLwaxlAoo7TJHidbtS4J5iNmZgXL0FkbFFBjvSfpJIlJ00zbhNYS5f6Guo
 EDmFJl0ZxBHjJnyp378OD8uTs7fLvjx79LjSTbNYiytVbZPQUQ5Yaxu2jXnimvw
 3rrszlaEXAMPLE=
-----END CERTIFICATE-----",
          "certificateTrust": "-----BEGIN CERTIFICATE-----
MIICiTCCAfICCQD6m7oRw0uXOjANBgkqhkiG9w
 0BAQUFADCBiDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZ
 WF0dGxlMQ8wDQYDVQQKEwZBbWF6b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIw
 EAYDVQQDEwlUZXN0Q2lsYWMxHzAdBgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5
 jb20wHhcNMTEwNDI1MjA0NTIxWhcNMTIwNDI0MjA0NTIxWjCBiDELMAkGA1UEBh
 MCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdTZWF0dGxlMQ8wDQYDVQQKEwZBb
 WF6b24xFDASBgNVBAsTC0lBTSBDb25zb2xlMRIwEAYDVQQDEwlUZXN0Q2lsYWMx
 HzAdBgkqhkiG9w0BCQEWEG5vb25lQGFtYXpvbi5jb20wgZ8wDQYJKoZIhvcNAQE
 BBQADgY0AMIGJAoGBAMaK0dn+a4GmWIWJ21uUSfwfEvySWtC2XADZ4nB+BLYgVI
 k60CpiwsZ3G93vUEIO3IyNoH/f0wYK8m9TrDHudUZg3qX4waLG5M43q7Wgc/MbQ
 ITxOUSQv7c7ugFFDzQGBzZswY6786m86gpEIbb3OhjZnzcvQAaRHhdlQWIMm2nr
 AgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAtCu4nUhVVxYUntneD9+h8Mg9q6q+auN
 KyExzyLwaxlAoo7TJHidbtS4J5iNmZgXL0FkbFFBjvSfpJIlJ00zbhNYS5f6Guo
 EDmFJl0ZxBHjJnyp378OD8uTs7fLvjx79LjSTbNYiytVbZPQUQ5Yaxu2jXnimvw
 3rrszlaEXAMPLE=
-----END CERTIFICATE-----"
        },
        "endpointUri": "opc.tcp://203.0.113.2:49320",
        "securityPolicy": "BASIC256",
        "messageSecurityMode": "SIGN_AND_ENCRYPT",
        "identityProvider": {
          "type": "Anonymous"
        },
        "nodeFilterRules": []
      },
      "measurementDataStreamPrefix": ""
    }
  ]
}
```