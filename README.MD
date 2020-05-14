# BiztalkPowershellAdapter

This is a custom BizTalk in-process send adapter for running powershell scripts/commands from BizTalk on local or remote servers.

## Introduction

This code implements an async sendport adapter to Microsoft BizTalk Server 2020 for runnning powershell scripts/commands locally or at remote server.


### Send port settings

Send port configuration
- Script: powershell script to be running
- Host: computername of the server where script should be run. Not used when running script in local server
- Username: user for running remote scripts, if needed
- Password: password for user

### Passing message to script

Adapter passes the message coming to send port to script as a parameter $message (local scripts) or $xmlmessage (remote running scripts).

Example of how to read contents of $message in script:
```
# read message body (xml) to variable
$xml = [xml] $message.GetBody()
# get element value from xml
$param = $xml.PowershellAdapter.Parameter1 
```

Example of how to read contents of $xmlmessage in script and pass it to cmd-file in remote server: 
```
# get the $xmlmessage param as xml
param([xml]$xmlmessage)
# get element value from xml
$param = $xmlmessage.PowershellAdapter.Parameter1
# pass $param value to cmd-file and run it
cmd.exe /c 'C:\Test\run.bat' $param 
```


## TODO

- Needs extensive testing
- Better install and usage instructions
- Include install binary to repo

