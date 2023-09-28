# Creating an App
- See https://dev.splunk.com/enterprise/docs/developapps
- See https://dev.splunk.com/enterprise/tutorials/module_getstarted

Essentially, make a folder with the app name, then add files. You really don't need much to get started, just a local folder and an inputs.conf file.

To activate, copy/move to ```$SPLUNK_HOME/etc/apps/appname/...``` or on the server at ```.../splunk/etc/deployment-apps/```

Structure:
```
$SPLUNK_HOME/etc/apps/appname/
  /bin
    README
  /default and/or  /local
    app.conf
    inputs.conf
    props.conf
    transforms.conf
    /data
      /ui
        /nav
          default.xml
        /views
          README
  /metadata
    default.meta
    local.meta
```
- /bin contains supporting files (scripts, etc.)
- /local is where user-customized configurations, navigation components, and views are stored.
- /default/data/ui/nav and /local/data/ui/nav folders contain settings for the navigation bar at the top of your app in the default.xml file.
- /default/data/ui/views and /local/data/ui/views folders contain the .xml files that define dashboards in your app


# Inputs.conf

Create/edit the file at ```.../myapp/local/inputs.conf``` and add a [\[stanza\]](https://docs.splunk.com/Splexicon:Stanza) for each input desired ([reference](https://docs.splunk.com/Documentation/Splunk/latest/Data/Monitorfilesanddirectorieswithinputs.conf))
- Editing this requires a restart the SplunkForwarder service
- Note: you may not receive logs immediately depending on the stanza's checkpointInterval setting

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

# Terminology
add-on:

- A type of app that runs on the Splunk platform and provides specific capabilities to other apps, such as getting data in, mapping data, or providing saved searches and macros. An add-on is not typically run as a standalone app. Instead, an add-on is a reusable component that supports other apps across a number of different use cases.
