# utl-rereading-a-string-to-extract-and-concatenate-subtext-in-the-correct-order
Rereading a string to extract and concatenate subtext in the correct order
    Rereading a string to extract and concatenate subtext in the correct order                                             
                                                                                                                           
    github                                                                                                                 
    https://tinyurl.com/yytubpc5                                                                                           
    https://github.com/rogerjdeangelis/utl-rereading-a-string-to-extract-and-concatenate-subtext-in-the-correct-order      
                                                                                                                           
    There are other ways to do this                                                                                        
                                                                                                                           
        1. trastrn and trim                                                                                                
        2. call scan                                                                                                       
        3. utl_pop                                                                                                         
                                                                                                                           
    But the method below can even work across records.                                                                     
                                                                                                                           
    SAS Forum                                                                                                              
    https://tinyurl.com/y3zmlsj2                                                                                           
    https://communities.sas.com/t5/SAS-Programming/Extracting-sub-string-variables-based-on-conditions/m-p/542012          
                                                                                                                           
                                                                                                                           
    *_                   _                                                                                                 
    (_)_ __  _ __  _   _| |_                                                                                               
    | | '_ \| '_ \| | | | __|                                                                                              
    | | | | | |_) | |_| | |_                                                                                               
    |_|_| |_| .__/ \__,_|\__|                                                                                              
            |_|                                                                                                            
    ;                                                                                                                      
                                                                                                                           
    AB.ID = dsn.varID AB.name = dsn.pname and and AB.custid=dsn.customerid                                                 
    AB.custid=dsn.customerid and AB.ID = dsn.varID AB.name = dsn.pname and                                                 
    AB.name = dsn.pname and AB.ID = dsn.varID and AB.custid=dsn.customerid                                                 
                                                                                                                           
    *            _               _                                                                                         
      ___  _   _| |_ _ __  _   _| |_                                        | Rules                                        
     / _ \| | | | __| '_ \| | | | __|                                       |                                              
    | (_) | |_| | |_| |_) | |_| | |_                                        |  Even though we have random                  
     \___/ \__,_|\__| .__/ \__,_|\__|                                       |  locations in the string                     
                    |_|                                                     |          OUTPUT                              
    ;                                                                       |          ------                              
    AB.custid=dsn.customerid and AB.ID = dsn.varID AB.name = dsn.pname and  |    name varID customerid                     
    AB.ID = dsn.varID AB.name = dsn.pname and and AB.custid=dsn.customerid  |    name varID customerid                     
    AB.name = dsn.pname and AB.ID = dsn.varID and AB.custid=dsn.customerid  |    name varID customerid                     
                                                                                                                           
            OUTPUT            STR1    STR2        STR3                                                                     
                                                                                                                           
     name varID customerid    name    varID    customerid                                                                  
     name varID customerid    name    varID    customerid                                                                  
     name varID customerid    name    varID    customerid                                                                  
                                                                                                                           
    *          _       _   _                                                                                               
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                    
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                   
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                  
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                  
                                                                                                                           
    ;                                                                                                                      
                                                                                                                           
    data want;                                                                                                             
       length output $22;                                                                                                  
                                                                                                                           
       input    @"pname"      +(-5)  str1 $5.                                                                              
             @1 @"varID"      +(-5)  str2 $5.                                                                              
             @1 @"customerid" +(-10) str3 $11.;                                                                            
                                                                                                                           
       output=catx(" ",str1,str2,str3);                                                                                    
       keep output;                                                                                                        
    cards4;                                                                                                                
    AB.name = dsn.pname and AB.ID = dsn.varID and AB.custid=dsn.customerid                                                 
    AB.ID = dsn.varID AB.name = dsn.pname and and AB.custid=dsn.customerid                                                 
    AB.custid=dsn.customerid and AB.ID = dsn.varID AB.name = dsn.pname and                                                 
    ;;;;                                                                                                                   
    run;quit;                                                                                                              
                                                                                                                           
                                                                                                                           
                                                                                                                           
