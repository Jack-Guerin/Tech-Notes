# Parse Fields that May or May Not be Present
Note that every "sub field" is optional under Subject, and that Subject captures the entire fieldset for review.

```
(Subject:(?<Subject>
    (\s+Security\sID:\s+(?<Subject_SecurityID>.+?)(?:\n|$))?
    (\s+Account\sName:\s+(?<Subject_AccountName>.+?)(?:\n|$))?
    (\s+Account\sDomain:\s+(?<Subject_AccountDomain>.+?)(?:\n|$))?
    (\s+Logon\sID:\s+(?<Subject_LogonID>.+?)(?:\n|$))?
    (\s+Logon\sType:\s+(?<Subject_LogonType>.+?)(?:\n|$))?
    )?
)?
```

That regular expression must be used without whitespace in Splunk transforms.conf, like this
```
[extract-security-xml]
REGEX = (Subject:(?<Subject>(\s+Security\sID:\s+(?<Subject_SecurityID>.+?)(?:\n|$))?(\s+Account\sName:\s+(?<Subject_AccountName>.+?)(?:\n|$))?(\s+Account\sDomain:\s+(?<Subject_AccountDomain>.+?)(?:\n|$))?(\s+Logon\sID:\s+(?<Subject_LogonID>.+?)(?:\n|$))?(\s+Logon\sType:\s+(?<Subject_LogonType>.+?)(?:\n|$))?)?)?
SOURCE_KEY = EventXML
````

## See for more info
- https://docs.splunk.com/Documentation/SplunkCloud/latest/Data/Advancedsourcetypeoverrides
- https://docs.splunk.com/Documentation/Splunk/latest/Data/DataIngest
- https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Configureadvancedextractionswithfieldtransforms
- https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Exampleconfigurationsusingfieldtransforms
- https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Createandmaintainsearch-timefieldextractionsthroughconfigurationfiles
