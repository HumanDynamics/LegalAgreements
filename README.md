# MIT Human Dynamics Lab 

Repository for Computable Contracts Research and Development 

# Extracting Contracts from Edgar Filings 

A hacky way to download the documents:  

1. go to ftp://ftp.sec.gov/edgar/daily-index/
2. then find a file with the following company.XXXXXXXX.idx (where XXXXXXXX is the full date)
3. download the file by using `wget ftp://ftp.sec.gov/edgar/daily-index/<PATH_to_file>/company.XXXXXXXX.idx`
4. To process it you need to convert it to csv by running the following command       
  a. On your computer(using Terminal) navigate to the folder that has company.XXXXXXXX.idx    
  b. cat company.XXXXXXXX.idx | sed 's/  \+/;/g' > company.csv    
  c. Now you have a CSV file and the separator character is ; instead of ,    
5. To download more than one just cat the file with wget the last field    
  a. for i in `cat company.csv | cut -d';' -f5 `; do wget "ftp://ftp.sec.gov/$i" ;done
