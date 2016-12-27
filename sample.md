Pewdata Package Rstudio Presentation
========================================================
author: Adam Glover
date: 12/26/16
autosize: true

Introduction
========================================================
This presentation will cover usage of pewdata package in R and exploratory research of Pew Research Center Mobile Commerce Questionaire


Pewdata
========================================================
Pew Research allows users to download data referenced in articles on the website. The follwing dataset measures mobile commerce. 

```r
# install package Hmisc. This will allow me to interact with the .sav file
library(Hmisc)
# assign the file path to mobile using the function spss.get
mobile <- spss.get('/Users/ag/Desktop/pew_data/Mobile.sav', use.value.labels=TRUE)
# view table columns
names(mobile)
```

```
 [1] "psraid"   "sample"   "int.date" "state"    "cregion"  "usr"     
 [7] "intuse"   "emlocc"   "home3nw"  "modem3b"  "tw"       "sns"     
[13] "pial10a"  "pial10b"  "pial10c"  "pial11"   "pial12a"  "pial12b" 
[19] "pial12c"  "pial12d"  "pial12e"  "pial13"   "ql1a"     "qc1"     
[25] "hh1"      "employ"   "par"      "sex"      "age"      "educ"    
[31] "hisp"     "race"     "inc"      "reg"      "party"    "partyln" 
[37] "zipcode"  "weight"   "standwt" 
```

Summary of dataset
========================================================


```
     psraid            sample       int.date              state    
 Min.   :100003   Landline:600   Min.   :10512   California  : 79  
 1st Qu.:101162   Cell    :400   1st Qu.:10512   Texas       : 74  
 Median :102308                  Median :10612   Florida     : 61  
 Mean   :141252                  Mean   :10654   Ohio        : 44  
 3rd Qu.:200748                  3rd Qu.:10712   Pennsylvania: 43  
 Max.   :202171                  Max.   :10812   Illinois    : 39  
                                                 (Other)     :660  
      cregion     usr                           intuse   
 Northeast:146      : 62   Yes                     :769  
 Midwest  :256   R  :188   No                      :230  
 South    :389   S  :492   (DO NOT READ) Don’t know:  1  
 West     :209   U  :258   (DO NOT READ) Refused   :  0  
                                                         
                                                         
                                                         
                      emlocc                        home3nw   
 Yes                     :716   Yes                     :701  
 No                      :284   No                      : 86  
 (DO NOT READ) Don’t know:  0   (DO NOT READ) Don’t know:  0  
 (DO NOT READ) Refused   :  0   (DO NOT READ) Refused   :  0  
                                NA's                    :213  
                                                              
                                                              
                                                              modem3b   
 Cable modem                                                      :231  
 Wireless connection (either AirCard, ‘land-based’ or ‘satellite’):189  
 DSL-enabled phone line                                           :165  
 Dial-up telephone line                                           : 46  
 Fiber optic connection                                           : 44  
 (Other)                                                          : 26  
 NA's                                                             :299  
                        tw                            sns     
 Yes                     : 84   Yes                     :460  
 No                      :701   No                      :325  
 (DO NOT READ) Don’t know:  2   (DO NOT READ) Don’t know:  1  
 (DO NOT READ) Refused   :  0   (DO NOT READ) Refused   :  1  
 NA's                    :213   NA's                    :213  
                                                              
                                                              
                     pial10a                        pial10b   
 Yes                     :496   Yes                     :178  
 No                      :101   No                      :814  
 (DO NOT READ) Don’t know:  1   (DO NOT READ) Don’t know:  4  
 (DO NOT READ) Refused   :  2   (DO NOT READ) Refused   :  4  
 NA's                    :400                                 
                                                              
                                                              
                     pial10c                         pial11   
 Yes                     :179   Yes                     : 71  
 No                      :817   No                      :822  
 (DO NOT READ) Don’t know:  1   (DO NOT READ) Don’t know:  1  
 (DO NOT READ) Refused   :  3   (DO NOT READ) Refused   :  2  
                                NA's                    :104  
                                                              
                                                              
                                          pial12a   
 Yes, have done this                          :309  
 No, have not done this                       :585  
 Have done this but not in last 30 days (VOL.):  1  
 Cell phone is not able to do this (VOL.)     :  0  
 (DO NOT READ) Don’t know                     :  1  
 (DO NOT READ) Refused                        :  0  
 NA's                                         :104  
                                          pial12b   
 Yes, have done this                          :170  
 No, have not done this                       :723  
 Have done this but not in last 30 days (VOL.):  0  
 Cell phone is not able to do this (VOL.)     :  2  
 (DO NOT READ) Don’t know                     :  1  
 (DO NOT READ) Refused                        :  0  
 NA's                                         :104  
                                          pial12c   
 Yes, have done this                          :171  
 No, have not done this                       :719  
 Have done this but not in last 30 days (VOL.):  1  
 Cell phone is not able to do this (VOL.)     :  5  
 (DO NOT READ) Don’t know                     :  0  
 (DO NOT READ) Refused                        :  0  
 NA's                                         :104  
                                          pial12d   
 Yes, have done this                          :128  
 No, have not done this                       :761  
 Have done this but not in last 30 days (VOL.):  1  
 Cell phone is not able to do this (VOL.)     :  6  
 (DO NOT READ) Don’t know                     :  0  
 (DO NOT READ) Refused                        :  0  
 NA's                                         :104  
                                          pial12e   
 Yes, have done this                          :100  
 No, have not done this                       :788  
 Have done this but not in last 30 days (VOL.):  2  
 Cell phone is not able to do this (VOL.)     :  5  
 (DO NOT READ) Don’t know                     :  0  
 (DO NOT READ) Refused                        :  1  
 NA's                                         :104  
                             pial13   
 Yes, purchased at store        : 65  
 Yes, purchased at another store: 14  
 Yes, purchased online          : 25  
 No, did not purchase           : 62  
 (DO NOT READ) Don’t know       :  5  
 (DO NOT READ) Refused          :  0  
 NA's                           :829  
                                       ql1a    
 Yes, someone in household has cell phone: 31  
 No                                      : 69  
 Don't know/Refused (VOL.)               :  4  
 NA's                                    :896  
                                               
                                               
                                               
                        qc1           hh1       
 Yes, has a home telephone:214   Min.   :1.000  
 No, no home telephone    :184   1st Qu.:1.000  
 Don't know/Refused (VOL.):  2   Median :2.000  
 NA's                     :600   Mean   :2.094  
                                 3rd Qu.:2.000  
                                 Max.   :9.000  
                                                
                       employ                           par     
 Employed full-time       :396   Yes                      :224  
 Employed part-time       :108   No                       :767  
 Not employed             :492   Don't know/Refused (VOL.):  9  
 Don't know/Refused (VOL.):  4                                  
                                                                
                                                                
                                                                
     sex           age       
 Male  :478   Min.   :18.00  
 Female:522   1st Qu.:40.75  
              Median :57.00  
              Mean   :56.58  
              3rd Qu.:71.00  
              Max.   :99.00  
                             
                                                                         educ    
 High school graduate, Grade 12, or GED certificate                        :281  
 College or university graduate (BA, BS or other four-year degree received):215  
 Some college or university work, but no four-year degree                  :212  
 Post graduate or professional schooling after college                     :164  
 High school incomplete (Grades 9-11)                                      : 55  
 Technical, trade or vocational school AFTER high school                   : 39  
 (Other)                                                                   : 34  
                        hisp                                  race    
 Yes                      : 73   White                          :814  
 No                       :906   Black or African-American      : 92  
 Don't know/Refused (VOL.): 21   Asian or Pacific Islander      : 17  
                                 Mixed race                     : 17  
                                 Native American/American Indian: 13  
                                 Other (SPECIFY)                : 11  
                                 Don't know/Refused (VOL.)      : 36  
                        inc     
 Don't know/Refused (VOL.):214  
 $50,000 to under $75,000 :133  
 $20,000 to under $30,000 :102  
 $30,000 to under $40,000 : 90  
 $40,000 to under $50,000 : 83  
 $75,000 to under $100,000: 81  
 (Other)                  :297  
                                                                                 reg     
 Are you ABSOLUTELY CERTAIN that you are registered to vote at your current address:769  
 Are you PROBABLY registered, but there is a chance your registration has lapsed   : 35  
 Are you NOT registered to vote at your current address                            :161  
 [VOL. DO NOT READ] Don’t know/Refused                                             : 35  
                                                                                         
                                                                                         
                                                                                         
                       party                                partyln   
 Republican               :265   Republican                     :123  
 Democrat                 :259   Democratic                     :137  
 Independent              :370   Other/Don't know/Refused (VOL.):216  
 No preference (VOL.)     : 42   NA's                           :524  
 Other party (VOL.)       :  4                                        
 Don't know/Refused (VOL.): 60                                        
                                                                      
            zipcode        weight          standwt      
 99999          : 28   Min.   : 1.000   Min.   :0.2016  
 06790          :  2   1st Qu.: 2.312   1st Qu.:0.4661  
 15122          :  2   Median : 3.812   Median :0.7684  
 17007          :  2   Mean   : 4.961   Mean   :1.0000  
 20852          :  2   3rd Qu.: 6.438   3rd Qu.:1.2975  
 27909          :  2   Max.   :15.125   Max.   :3.0485  
 (Other)        :962                                    
```
Exploratory Research - Demographics
========================================================

```

Landline     Cell 
     600      400 
```

```

             Alabama               Alaska              Arizona 
                  14                    0                   31 
            Arkansas           California             Colorado 
                  10                   79                   20 
         Connecticut             Delaware District of Columbia 
                  15                    5                    4 
             Florida              Georgia               Hawaii 
                  61                   23                    0 
               Idaho             Illinois              Indiana 
                   5                   39                   27 
                Iowa               Kansas             Kentucky 
                  14                    7                   18 
           Louisiana                Maine             Maryland 
                  16                    8                   18 
       Massachusetts             Michigan            Minnesota 
                  13                   32                   24 
         Mississippi             Missouri              Montana 
                  16                   21                    9 
            Nebraska               Nevada        New Hampshire 
                   7                    8                    4 
          New Jersey           New Mexico             New York 
                  22                    9                   38 
      North Carolina         North Dakota                 Ohio 
                  33                    5                   44 
            Oklahoma               Oregon         Pennsylvania 
                  16                   15                   43 
        Rhode Island       South Carolina         South Dakota 
                   2                   16                    3 
           Tennessee                Texas                 Utah 
                  27                   74                   14 
             Vermont             Virginia           Washington 
                   1                   31                   19 
       West Virginia            Wisconsin              Wyoming 
                   7                   33                    0 
```

```

Northeast   Midwest     South      West 
      146       256       389       209 
```

```

  Male Female 
   478    522 
```

![plot of chunk unnamed-chunk-3](sample-figure/unnamed-chunk-3-1.png)
