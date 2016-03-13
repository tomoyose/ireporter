## Itunes Connect Reporter

Golang implementation of [Reporter tool](http://help.apple.com/itc/appsreporterguide/#/itcbe21ac7db)

## Install 

```bash
go get github.com/chapsuk/ireporter/cmd/ireporter/
``` 

## Flags

```
:> $GOPATH/bin/ireporter -h
Usage of /Users/makras/Projects/golang/bin/ireporter:
  -account int
    	If your Apple ID has access to multiple accounts, you’ll need to specify the account number you’d like to use.
  -app string
    	Sales or Finance
  -cmd string
    	Command (for example, getHelp). (default "getHelp")
  -date string
    	Specific time covered by the report (for example, 20150201).
  -dateType string
    	Length of time covered by the report (for example, Daily or Weekly).
  -mode string
    	Reporter has two modes of operation: Normal and Robot.
Normal mode is intended for an actual user that executes ad-hoc commands. Messages are displayed in easily readable text.
Robot mode is intended for an automated script that’s used regularly. Messages in robot mode are displayed in XML for easy parsing. (default "Normal")
  -password string
    	Your Apple ID’s password.
  -reportSubtype string
    	Level of detail in the report (for example, Summary).
  -reportType string
    	Type of information contained in report (for example, Sales).
  -userId string
    	Your Apple ID for iTunes Connect.
  -vendor int
    	Vendor number of the report to download. For a list of your vendor numbers, use the getVendors command.
```
        
## Usage

```
:> $GOPATH/bin/ireporter -userId <USER_ID> -password <PASSWORD> -app Sales -cmd getHelp

Sales commands include:
	 getHelp: Returns this help message. No arguments.
	 getStatus: Returns status of Sales and Trends application. No arguments.
	 getAccounts: Returns list of available accounts. No arguments.
	 getVendors: Returns list of available vendor numbers. No arguments.
	 getReport: Downloads a report. Arguments: Vendor Number, Report Type, Report Subtype, DateType, Date.
For more details, see Reporter guide: http://help.apple.com/itc/appsreporterguide/#/itcbe21ac7db
```

# TODO

* Finance.getReport
* Fix build queryInput string
