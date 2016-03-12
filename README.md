## Itunes Connect Reporter

ItunesConnect [Reporter tool](http://help.apple.com/itc/appsreporterguide/#/itcbe21ac7db)

## Example

```go
package main

import (
    "log"
    "os"
    "io/ioutil"
    "github.com/chapsuk/itunes-reporter"
)

func main() {
    cfg := reporter.Config{
        UserID: <USER_ID>,
        Password: <PASSWORD>,
        Mode: "Normal", // "Robot.xml"
    }
     
    cli, err := reporter.NewClient(cfg)
    handleError(err)
    
    res, err := cli.GetSalesStatus()
    handleError(err)
    log.Printf("(%s) SalesStatusResponse: %s", cfg.Mode, string(res))
    // (Normal) Response: Sales and Trends Reporter is currently available.
    // (Robot.xml) Response: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <Status>
    //     <Code>0</Code>
    //     <Message>Sales and Trends Reporter is currently available.</Message>
    // </Status>
    
    res, err = cli.GetFinanceStatus()
    handleError(err)
    log.Printf("(%s) FinanceStatusResponse: %s", cfg.Mode, string(res))
    // (Normal) FinanceStatusResponse: Finance Reporter is currently available.
    // (Robot.xml) FinanceStatusResponse: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <Status>
    //     <Code>0</Code>
    //     <Message>Finance Reporter is currently available.</Message>
    // </Status>
    
    res, err = cli.GetSalesAccounts()
    handleError(err)
    log.Printf("(%s) SalesAccountsResponse: %s", cfg.Mode, string(res))
    // (Normal) SalesAccountsResponse: ACCOUNT_NAME, ACCOUNT_NUMBER
    // ACCOUNT_NAME, ACCOUNT_NUMBER
    //(Robot.xml) SalesAccountsResponse: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <Accounts>
    //     <Account>
    //         <Name>ACCOUNT_NAME</Name>
    //         <Number>ACCOUNT_NUMBER</Number>
    //     </Account>
    //     <Account>
    //         <Name>ACCOUNT_NAME</Name>
    //         <Number>ACCOUNT_NUMBER</Number>
    //     </Account>
    // </Accounts>
    
    res, err = cli.GetFinanceAccounts()
    handleError(err)
    log.Printf("(%s) FinanceAccountsResponse: %s", cfg.Mode, string(res))
    // (Normal) FinanceAccountsResponse: ACCOUNT_NAME, ACCOUNT_NUMBER
    // ACCOUNT_NAME, ACCOUNT_NUMBER
    // (Robot.xml) FinanceAccountsResponse: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <Accounts>
    //     <Account>
    //         <Name>ACCOUNT_NAME</Name>
    //         <Number>ACCOUNT_NUMBER</Number>
    //     </Account>
    //     <Account>
    //         <Name>ACCOUNT_NAME</Name>
    //         <Number>ACCOUNT_NUMBER</Number>
    //     </Account>
    // </Accounts>    
    
    res, err = cli.GetSalesVendors(<ACCOUNT_NUMBER>)
    handleError(err)
    log.Printf("(%s) SalesVendorsResponse: %s", cfg.Mode, string(res))
    // (Normal) SalesVendorsResponse: <VENDOR_NUMBER>
    // (Robot.xml) SalesVendorsResponse: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <Vendors>
    //     <Vendor><VENDOR_NUMBER></Vendor>
    // </Vendors>
    
    res, err = cli.GetFinanceVendorsAndRegions(<ACCOUNT_NUMBER>)
    handleError(err)
    log.Printf("(%s) FinanceVendorsResponse: %s", cfg.Mode, string(res))
    // (Normal) FinanceVendorsResponse: The following reports are available for vendor <VENDOR_NUMBER>:
    // AU:Financial
    // CA:Financial
    // ...
    // (Robot.xml) FinanceVendorsResponse: <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    // <VendorsAndRegions>
    //     <Vendor>
    //         <Number>VENDOR_NUMBER</Number>
    //         <Region>
    //             <Code>AU</Code>
    //             <Reports>
    //                 <Report>Financial</Report>
    //             </Reports>
    //         </Region>
    //         <Region>
    //             <Code>CA</Code>
    //             <Reports>
    //                 <Report>Financial</Report>
    //             </Reports>
    //         </Region>
    //     ...
    //     </Vendor>
    // </VendorsAndRegions>
    
    res, err = cli.GetSalesReport(<ACCOUNT_NUMBER>, <VENDOR_NUMBER>, "Sales", "Summary", "Daily", "20160309")
    handleError(err)
    fileName := "SalesReport_20160309.gz"
    ioutil.WriteFile(fileName, res, 0644)
    file, err := os.Open(fileName)
    handleError(err)
    info, err := file.Stat()
    handleError(err)
    log.Printf("%v", info)
    // &{SalesReport_20160309.gz 7331 420 {63593414246 0 0x49e0a0} 0xc820414090}
}

func handleError(err error) {
    if err != nil {
        log.Print(err)
        os.Exit(1)
    }
}
```

# TODO

* Implement Finance.getReport
* Fix build queryInput string
