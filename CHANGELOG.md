# Change Log

## Released

## 2.1.0

### Added

- Added Linting with typescript-eslint
- Added .gitignore and .npmignore file
- Added 2 functions for building service data (managed & custom rules) to remove redundant code

### Changed

- Refactoring bin file: outsource capacity checks & other functions to helpers.ts
- Transform capacity.json to Typescript Type Rule
- Start refactoring lib file: get rid of redundant code and use JS shortcuts
- Extend types of the Config interface
- Restructuring runtime properties:  introduce separate layer for PreProcess and PostProcess
- New types for Firewall Manager API and CDK mapping
## 2.0.0

### Added
1. preProcessRuleGroups and postProcessRuleGroups - you can decide now where the Custom or ManagedRules should be added to.

2. RuleLabels - A label is a string made up of a prefix, optional namespaces, and a name. The components of a label are delimited with a colon. Labels have the following requirements and characteristics:

    - Labels are case-sensitive.

    - Each label namespace or label name can have up to 128 characters.

    - You can specify up to five namespaces in a label.

    - Components of a label are separated by colon (:).
### Changed

1. Values Structure:

 - Removed (Rules and ManagedRuleGroups)
 - Added PreProcess and PostProcess

ℹ️ See [example json](./values/example-waf.json).

2. Optimized RuleGroup Splitting - RuleGroups will now be splitted into Groups with up to 1000 WCU.

## 1.0.4

### Added

1. Added S3LoggingBucketName to json. You need to specify the S3 Bucket where the Logs should be placed in now. We also added a Prefix for the logs to be aws conform (Prefix: AWSLogs/AWS_ACCOUNTID/FirewallManager/AWS_REGION/).

2. Added Testing your WAF with [GoTestWAF](https://github.com/wallarm/gotestwaf). To be able to check your waf we introduced the **SecuredDomain** Parameter in the json which should be your Domain which will be checked using the WAF tool.

3. Introduced three new Parameters in the taskfile (**WAF_TEST**,**CREATE_DIAGRAM** and **CDK_DIFF**).

| Parameter   |      Value      |
|----------|:-------------:|
| WAF_TEST |  true (testing your waf with GoTestWAF) </br> false (Skipping WAF testing)  |
| CREATE_DIAGRAM |  true (generating a diagram using draw.io) </br> false (Skipping diagram generation)  |
| CDK_DIFF |  true (generating a cdk before invoking cdk deploy) </br> false (Skipping cdk diff)  |

4. Add schema validation
## 1.0.3

### Added

New Support for Captcha - You can now add Captcha as Action to your WAFs. AWS WAF Captcha is available in the US East (N. Virginia), US West (Oregon), Europe (Frankfurt), South America (Sao Paulo), and Asia Pacific (Singapore) AWS Regions and supports Application Load Balancer, Amazon API Gateway, and AWS AppSync resources.
## 1.0.2

### Added 
#### Rule Name 
You can now name your Rules. If you define a Name in your RulesArray the Name + a Base36 Timestamp will be used for creation of your Rule - otherwise a name will be generated. This will help you to query your logs in Athena. The same Rulename also apply to the metric just with adding "-metric" to the name.
## 1.0.1

Updated Readme - Community Release
## 1.0.0

### Added

1. Automated Capactiy Calculation via [API - CheckCapacity](https://docs.aws.amazon.com/waf/latest/APIReference/API_CheckCapacity.html)
2. Algorithm to split Rules into RuleGroups
3. Automated Update of RuleGroup if Capacity Changed 
3. Add [ManagedRuleGroups](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html) via configuration file
4. Automated Generation of draw.io [diagram](https://app.diagrams.net/) for each WAF
5. Checking of the softlimit quota for WCU set in the AWS Account (Stop deployment if Caluclated WCU is above the quota)
6. Easy configuration of WAF Rules trough json file.
7. Deployment Hash to deploy same WAF more than one time for testing and/or blue/green deployments.
8. Stopping deployment if soft limit will be exceeded:  **Firewall Manager policies per organization per Region (L-0B28E140)** - **Maximum number of web ACL capacity units in a web ACL in WAF for regional (L-D9F31E8A)**
9. NEW **RegexMatchStatement** and **IPSetReferenceStatement** is working now 🚀



