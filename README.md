# utl-current-state-of-reading-and-writing-sas7bdats--sas7bcats--V5-V8-SAS-transport-files
Current state of reading and writing SAS V9.4 SAS7bdats, SAS7bcats, and V5/V8 xport files without SAS. 
Current state of reading and writing SAS V9.4 SAS7bdats, SAS7bcats, and V5/V8 xport files without SAS.        
                                                                                                              
Read and write SAS files without any SAS installation                                                         
Writing SAS7bdats is not open source yet. Writing V5/V8 transport files is open source.                       
The free SAS universal viewer no longer supports converting SAS7bdats to CSV files?                           
                                                                                                              
  Read SAS7bdats and/or V5/V8 export datasets and read sas simple SAS7bcats formats                           
                                                                                                              
      1. R (open source)                                                                                      
          Read sas7bdat and sas7bcat                                                                          
            Haven package reads sas7bdat and sas catalogs (Python is slightly better)                         
      2. Python (open source best product to read SAS datasets and sas7bcats)                                 
      3. WPS World Programming System ( SAS Clone has free addition outside US)                               
         Available worldwide except in the USA. More functional                                               
         that SAS analytic version($9,000 first year?)                                                        
         $,1500 per year, available in India, Europe, Africa, South America ...?                              
      4. StatTransfer (read sas7bdats $500 per year for commercial use?)                                      
      5. DBMS Copy(was free?. Still free for Virginia Commonwealth University faculty, staff and students.    
         In 2002, DBMS/Copy was acquired by SAS. SAS discontinued development of DBMD copy.                   
      6. Carolina (read sas7bdats using Java $1,000 per year)                                                 
      7. SPSS (reads SAS7bdats $99 per month)                                                                 
      8. CozyRoc ($4,000 server license perpetual?)                                                           
                                                                                                              
  Write SAS SAS7bdats and/or V5/V8 export datasets and read sas formats                                       
  Note only                                                                                                   
                                                                                                              
      1. R                                                                                                    
         SASxport                                                                                             
           Create V5 xport(long variable names - 200 char strings)                                            
           and V8(long variable names and long strings(32k)                                                   
         Writing sas7bdats is under development                                                               
      2. Python  (create SAS v5 export files)                                                                 
      3. StatTransfer (write SAS datasets)                                                                    
      4. WPS (free express edition- commercial version $1,500 per year -                                      
         has no limit on the size of SAS datasets created by R)                                               
      5. DBMS Copy (Only Free for Virginia Commonwealth University faculty, staff and students)               
      6. Carolina  (uses JDBC? )                                                                              
      7. SPSS (writes SAS7bdats $99 per month?)                                                               
      8. CozyRoc ($4,000 server license perpetual -Inserts data in SAS sas7bdat dataset?)                     
         https://www.cozyroc.com/ssis/sas                                                                     
                                                                                                              
Working examples in R and Python                                                                              
                                                                                                              
In R                                                                                                          
                                                                                                              
  see reproducible example and doc                                                                            
     https://tinyurl.com/rxasm43                                                                              
                                                                                                              
   1. Read a sas7bdat                                                                                         
   2. Write a V8 SAS transport file (long variable names and long char strings)                               
   3. In SAS convert the transport file to a SAS7bdat                                                         
                                                                                                              
     library(haven);                                                                                          
     have<-read_sas("d:/sd1/have.sas7bdat"); * sas dataset;                                                   
     write_xpt(have,"d:/xpt/have8.xpt",version=8);                                                            
                                                                                                              
In Python                                                                                                     
                                                                                                              
  https://tinyurl.com/y4todtld                                                                                
                                                                                                              
   1. Read a SAS7badt                                                                                         
   2. Write a V5 export file                                                                                  
                                                                                                              
     import pandas as pd;                                                                                     
     import pyreadstat;                                                                                       
     want, meta = pyreadstat.read_sas7bdat('d:/sd1/have.sas7bdat');                                           
     print(want);                                                                                             
     print(meta.column_names);                                                                                
     print(meta.column_labels);                                                                               
     print(meta.column_names_to_labels);                                                                      
     print(meta.number_rows);                                                                                 
     print(meta.number_columns);                                                                              
     print(meta.file_label);                                                                                  
     print(meta.file_encoding);                                                                               
     pyreadstat.write_xport(want, 'd:/xpt/want.xpt',table_name='want');                                       
                                                                                                              
R and Python  (Python read sas7bdat and create V8 transport)                                                  
  (Python does not support V8 transport files)                                                                
                                                                                                              
  see for reproducible example                                                                                
                                                                                                              
   https://tinyurl.com/y6hhmoon                                                                               
                                                                                                              
   1. read sas7bdat                                                                                           
   2. Convert panda dataframe to feather file                                                                 
   3. R read feather file                                                                                     
   4. Create R dataframe from feather file                                                                    
   5. Convert feather file to V5/V8 transport file                                                            
                                                                                                              
   Python                                                                                                     
     import pandas as pd;                                                                                     
     import feather;                                                                                          
     import numpy as np;                                                                                      
     import pandas as pd;                                                                                     
     from sas7bdat import SAS7BDAT;                                                                           
     with SAS7BDAT("d:/sd1/class.sas7bdat") as m:;                                                            
     .   mdata = m.to_data_frame();                                                                           
     print(mdata);                                                                                            
     feather.write_dataframe(mdata, "d:/fth/df.fth");                                                         
                                                                                                              
   R                                                                                                          
     library(haven);                                                                                          
     library(feather);                                                                                        
     library(data.table);                                                                                     
     want<-as.data.table(read_feather(path="d:/fth/df.fth"));                                                 
     write_xpt(have,"d:/xpt/have8.xpt",version=8);                                                            
                                                                                                              
2. SAS Xport file to excel                                                                                    
                                                                                                              
  see reproducible example and doc                                                                            
                                                                                                              
  https://github.com/rogerjdeangelis/utl_sas_v5_transport_file_to_excel                                       
                                                                                                              
     library(SASxport);                                                                                       
     library(XLConnect);                                                                                      
     have<-read.xport("d:/xpt/have.xpt");                                                                     
     wb <- loadWorkbook("d:/xls/have.xlsx", create = TRUE);                                                   
     createSheet(wb, name = "have");                                                                          
     writeWorksheet(wb, have, sheet = "have");                                                                
     saveWorkbook(wb);                                                                                        
                                                                                                              
3. Convert SAS format catalog to SAS V5/V8 xport file                                                         
                                                                                                              
  for reproducible example                                                                                    
   https://tinyurl.com/ydfxhmny                                                                               
                                                                                                              
   library(haven);                                                                                            
   library(SASxport);                                                                                         
   apycat <- read_sas("d:/sd1/class.sas7bdat", catalog_file="d:/sd1/rfmt.sas7bcat");                          
   fmtsex<-as.data.frame(attributes(apycat$SEX));                                                             
   fmtsex[] <- lapply(fmtsex, as.character);                                                                  
   colnames(fmtsex)<-c("FORMAT","HAVEN","FROM");                                                              
   fmtsex$TO<-rownames(fmtsex);                                                                               
   write.xport(fmtsex,file="d:/xpt/fmtsex.xpt");                                                              
                                                                                                              
                                                                                                              
4. Python reading a simple standalone SAS format catalog and covert to panda dataframe or                     
   R dataframe                                                                                                
                                                                                                              
   for reporducible example                                                                                   
   https://tinyurl.com/y6sacr7n                                                                               
                                                                                                              
   import pyreadr;                                                                                            
   import pandas as pd;                                                                                       
   import pyreadstat;                                                                                         
   df, meta = pyreadstat.read_sas7bcat("d:/sd1/pyfmt.sas7bcat");                                              
   print(meta.value_labels);                                                                                  
   want=pd.DataFrame.from_dict(meta.value_labels);                                                            
   want.index.name = "START";                                                                                 
   want.reset_index(inplace=True);                                                                            
   want.info();                                                                                               
   print(want);                                                                                               
   pyreadr.write_rds("d:/rds/pycat.Rds", want);                                                               
                                                                                                              
  R                                                                                                           
   library(haven);                                                                                            
   pytable <- readRDS("d:/rds/pycat.Rds");                                                                    
   pytable;                                                                                                   
                                                                                                              
                                                                                                              
