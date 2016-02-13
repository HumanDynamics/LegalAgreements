# MIT Human Dynamics Lab 

Repository for Computable Contracts Research and Development 

# Extracting Contracts from Edgar Filings 

Couple searches that reveal most  recent filings with contracts: 
* https://searchwww.sec.gov/EDGARFSClient/jsp/EDGAR_MainAccess.jsp?search_text=%22ex-10%22&sort=Date&formType=Form8K&isAdv=true&stemming=true&numResults=100&numResults=100

* https://searchwww.sec.gov/EDGARFSClient/jsp/EDGAR_MainAccess.jsp?search_text=EX-10&sort=Date&formType=Form8K&isAdv=true&stemming=true&numResults=100&numResults=100

Open Knowledge Foundation:
* https://github.com/datasets/edgar

* https://discuss.okfn.org/t/getting-structured-sec-edgar-data/71 


Good Links to Gather Context:

* http://www.sec.gov/spotlight/xbrl/viewers.shtml 

* https://datapreview.sec.gov/previewer/ 

* http://www.slideshare.net/afalk42/xbrl-us-altova-webinar


## GAAP Material Contracts tags:

element id="us-gaap_BankruptcyClaimsDescriptionOfMaterialContractsAssumedOrAssigned

* Line 1149:
'<xs:element id='us-gaap_BankruptcyClaimsDescriptionOfMaterialContractsAssumedOrAssigned' name='BankruptcyClaimsDescriptionOfMaterialContractsAssumedOrAssigned' nillable='true' substitutionGroup='xbrli:item' type='xbrli:stringItemType' xbrli:periodType='duration' />'


* Line 1151
'<xs:element id='us-gaap_BankruptcyClaimsAmountOfClaimsOnMaterialContractsRejected' name='BankruptcyClaimsAmountOfClaimsOnMaterialContractsRejected' nillable='true' substitutionGroup='xbrli:item' type='xbrli:monetaryItemType' xbrli:balance='credit' xbrli:periodType='instant' />'

* Line 1157
'<xs:element id='us-gaap_BankruptcyClaimsDescriptionOfMaterialContractsRejected' name='BankruptcyClaimsDescriptionOfMaterialContractsRejected' nillable='true' substitutionGroup='xbrli:item' type='xbrli:stringItemType' xbrli:periodType='duration' />'


## Also See Property Type Tags: 

* xs:element name="property" type="PROPERTY_TYPE" 




## To download all XBRL documents:

Go to ftp://ftp.sec.gov/edgar/full-index/     
Crawl ftp://ftp.sec.gov/edgar/full-index/20XX/QTRX/xbrl.idx ( for example,     ftp://ftp.sec.gov/edgar/full-index/2015/QTR1/xbrl.idx )      
Filter lines in each xbrl.idx by the form type you are interested in. For example:    
1000180|SANDISK CORP|10-K|2015-02-10|edgar/data/1000180/0001000180-15-000013.txt    
Download ftp://ftp.sec.gov/<url> -- for example, ftp://ftp.sec.gov/edgar/data/1000180/0001000180-15-000013.txt    
Extract XBRL document beginning with <?xml>   

To Scrape Edgar Contracts into Hadoop     
SEC EDGAR Oil Contracts Finder    
https://github.com/pudo/edgar-oil-contracts (can widen this scope to all contracts, not limit to oil related contracts)    



# A hacky way to download the documents:  

1. go to ftp://ftp.sec.gov/edgar/daily-index/
2. then find a file with the following company.XXXXXXXX.idx (where XXXXXXXX is the full date)
3. download the file by using `wget ftp://ftp.sec.gov/edgar/daily-index/<PATH_to_file>/company.XXXXXXXX.idx`
4. To process it you need to convert it to csv by running the following command       
  a. On your computer(using Terminal) navigate to the folder that has company.XXXXXXXX.idx    
  b. cat company.XXXXXXXX.idx | sed 's/  \+/;/g' > company.csv    
  c. Now you have a CSV file and the separator character is ; instead of ,    
5. To download more than one just cat the file with wget the last field    
  a. for i in `cat company.csv | cut -d';' -f5 `; do wget "ftp://ftp.sec.gov/$i" ;done
