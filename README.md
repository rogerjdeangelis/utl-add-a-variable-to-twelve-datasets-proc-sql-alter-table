# utl-add-a-variable-to-twelve-datasets-proc-sql-alter-table
Add a variable to twelve datasets proc sql alter table 

    Add a variable to twelve datasets proc sql alter table                                                            
                                                                                                                      
    github                                                                                                            
    https://tinyurl.com/ycy5gxvx                                                                                      
    https://github.com/rogerjdeangelis/utl-add-a-variable-to-twelve-datasets-proc-sql-alter-table                     
                                                                                                                      
    SAS-L                                                                                                             
    https://listserv.uga.edu/cgi-bin/wa?A2=SAS-L;3aeca166.1901d                                                       
                                                                                                                      
    INPUT  (12 datasets)                                                                                              
    ====================                                                                                              
                                                                                                                      
    Filename d:\sd1                                                                                                   
                                                                                                                      
     #     SAS Table                                                                                                  
                                                                                                                      
     1  GASHAW_VW3_201801                                                                                             
     2  GASHAW_VW3_201802                                                                                             
     3  GASHAW_VW3_201803                                                                                             
     4  GASHAW_VW3_201804                                                                                             
     5  GASHAW_VW3_201805                                                                                             
     6  GASHAW_VW3_201806                                                                                             
     7  GASHAW_VW3_201807                                                                                             
     8  GASHAW_VW3_201808                                                                                             
     9  GASHAW_VW3_201809                                                                                             
    10  GASHAW_VW3_201810                                                                                             
    11  GASHAW_VW3_201811                                                                                             
    12  GASHAW_VW3_201812                                                                                             
                                                                                                                      
    run;quit;                                                                                                         
                                                                                                                      
    * create 12 datasets;                                                                                             
    data _null_;                                                                                                      
     do i=1 to 12;                                                                                                    
        call symputx('i',put(i,z2.));                                                                                 
        rc=dosubl('                                                                                                   
          data "d:/sd1/gashaw_vw3_2018&i..sas7bdat";                                                                  
             x=1;                                                                                                     
          run;quit;                                                                                                   
        ');                                                                                                           
     end;                                                                                                             
    run;quit;                                                                                                         
                                                                                                                      
    EXAMPLE OUTPUT                                                                                                    
    --------------                                                                                                    
                                                                                                                      
    WORK.LOG total obs=12                                                                                             
                                                                                                                      
      I    RC                 STATUS                                                                                  
                                                                                                                      
      1     0    gashaw_vw3_201801 Variable Added                                                                     
      2     0    gashaw_vw3_201802 Variable Added                                                                     
      3     0    gashaw_vw3_201803 Variable Added                                                                     
      4     0    gashaw_vw3_201804 Variable Added                                                                     
      5     0    gashaw_vw3_201805 Variable Added                                                                     
      6     0    gashaw_vw3_201806 Variable Added                                                                     
      7     0    gashaw_vw3_201807 Variable Added                                                                     
      8     0    gashaw_vw3_201808 Variable Added                                                                     
      9     0    gashaw_vw3_201809 Variable Added                                                                     
     10     0    gashaw_vw3_201810 Variable Added                                                                     
     11     0    gashaw_vw3_201811 Variable Added                                                                     
     12     0    gashaw_vw3_201812 Variable Added                                                                     
                                                                                                                      
                                                                                                                      
    PROCESS                                                                                                           
    =======                                                                                                           
                                                                                                                      
    %symdel i / nowarn;                                                                                               
    data log;                                                                                                         
                                                                                                                      
     do i=1 to 12;                                                                                                    
        call symputx('i',put(i,z2.));                                                                                 
                                                                                                                      
        rc=dosubl('                                                                                                   
          proc sql;                                                                                                   
            alter table "d:/sd1/gashaw_vw3_2018&i..sas7bdat"                                                          
            add abc num                                                                                               
          ;quit;                                                                                                      
          %let cc=&syserr;                                                                                            
        ');                                                                                                           
                                                                                                                      
        * uses hiddon dragon space;                                                                                   
        if symgetn('cc')=0 then status=cats("gashaw_vw3_2018",put(i,z2.)," Variable Added");                          
        else status=cats("gashaw_vw3_2018",put(i,z2.)," Failed Update");                                              
        output;                                                                                                       
     end;                                                                                                             
     stop;                                                                                                            
                                                                                                                      
    run;quit;                                                                                                         
                                                                                                                      
                                                                                                                      
                                                                                                                      
                                                                                                                      
