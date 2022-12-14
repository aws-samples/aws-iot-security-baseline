## AWS IoT Security Baseline

AWS IoT security baseline (AISB) is a set of security controls that create a minimum foundation for customers to build secure IoT solutions on AWS. The AISB controls discussed in this blog are designed for mitigating the most common security risks without requiring significant effort. As your connected device fleet grows and you implement more complex use cases, you can scale and build upon these controls based on your threat model. They form the basis of your security posture and are focused on securing device credentials, least privilege access control, enabling logging and visibility, auditing device policies and monitoring your environment.

Refer to AWS IoT Security Baseline blog for details.

## AISB Solution Architecture 

The AISB solution architecture shows an IoT / IIoT device sending data to AWS IoT Core. Data from the edge device is sent to AWS for data storage, processing, analytics, and visualization. Along with the telemetry data, the IoT / IIoT device can also be configured  to send security event information to AWS using AWS IoT Device Defender. This event information is combined with cloud-based events to identify security misconfigurations and detect anomalies in the device behavior and notify personnel to respond to security events. 

![AISB solution architecture](https://github.com/aws-samples/aws-iot-security-baseline/blob/main/images/blog_image.png)

- [AWS IoT Device Defender](https://aws.amazon.com/iot-device-defender/) makes it easy to audit device configurations, detect device anomalies, and receive alerts to help secure your IoT device fleet.

- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) makes it easy to observe and monitor AWS resources and applications in the cloud and on premises. When AWS IoT logging is enabled, AWS IoT sends event information to CloudWatch logs. [Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) is used to trigger an [AWS Lambda](https://aws.amazon.com/lambda/) function to identify device certificates that require rotation. 

- [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (SNS) is a managed service that is used by AWS IoT Device Defender to send out security alerts and notifications to authorized personnel when an audit fails or behavior anomalies are detected. 

- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) monitors and records account activity across your AWS infrastructure, giving you control over storage, analysis, and remediation actions.

- [Amazon GuardDuty](https://aws.amazon.com/guardduty/) is a threat detection service that continuously monitors your AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation.


## AISB Solution Deployment

Deploy [this](https://github.com/aws-samples/aws-iot-security-baseline/blob/main/template/aws_iot_security_baseline.yaml) AWS CloudFormation template to provision the AISB resources in your account. The template accepts the following parameters:

- Email to receive security event notifications - email address that would be subscribed to the SNS topic to send out alerts
- Deploying X.509 certificates generated by AWS IoT - boolean parameter to setup certificate expiry notifications in case you are using AWS IoT generated certificates
- Device certificate rotation policy requirements (in years) - in case you are using AWS IoT generated certificates but would like to receive alerts according to your own certificate rotation requirements
- Is AWS IoT Core logging enabled in the account? - selecting 'No' would enable AWS IoT Core Logging in your account 

## Cleanup

To clean up your resources, delete the stack in the AWS CloudFormation console.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

