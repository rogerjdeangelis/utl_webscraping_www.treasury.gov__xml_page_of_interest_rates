# utl_webscraping_www.treasury.gov__xml_page_of_interest_rates
Webscraping www.treasury.gov  xml page of interest rates. You could cut and paste but this data is updated.

    ```  Webscraping www.treasury.gov  xml page of interest rates.                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  You could cut and paste but this data is updated.                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  INPUT                                                                                                                                                        ```
    ```  =====                                                                                                                                                        ```
    ```    https://www.treasury.gov/resource-center/data-chart-center/interest-rates/Pages/TextView.aspx?data=yield                                                   ```
    ```                                                                                                                                                               ```
    ```    WEB page has this table in XML                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```    This text defines the node for the table                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```    $("table .text_view_data:contains('04/14/17')").parent().remove();                                                                                         ```
    ```                                                                                                                                                               ```
    ```    Chrome renders the table like this                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```     Date         1 Mo      3 Mo      6 Mo      1 Yr      2 Yr      3 Yr      5 Yr      7 Yr     10 Yr      20 Yr    30 Yr                                     ```
    ```                                                                                                                                                               ```
    ```    11/01/17      1.06      1.18      1.30      1.46      1.61      1.74      2.01      2.22      2.37      2.63      2.85                                     ```
    ```    11/02/17      1.02      1.17      1.29      1.46      1.61      1.73      2.00      2.21      2.35      2.61      2.83                                     ```
    ```    11/03/17      1.02      1.18      1.31      1.49      1.63      1.74      1.99      2.19      2.34      2.59      2.82                                     ```
    ```    11/06/17      1.03      1.19      1.30      1.50      1.61      1.73      1.99      2.17      2.32      2.58      2.80                                     ```
    ```    11/07/17      1.05      1.22      1.33      1.49      1.63      1.75      1.99      2.17      2.32      2.56      2.77                                     ```
    ```    11/08/17      1.05      1.23      1.35      1.53      1.65      1.77      2.01      2.19      2.32      2.57      2.79                                     ```
    ```    11/09/17      1.07      1.24      1.36      1.53      1.63      1.75      2.01      2.20      2.33      2.59      2.81                                     ```
    ```    11/10/17      1.06      1.23      1.37      1.54      1.67      1.79      2.06      2.27      2.40      2.67      2.88                                     ```
    ```    11/13/17      1.07      1.24      1.37      1.55      1.70      1.82      2.08      2.27      2.40      2.67      2.87                                     ```
    ```    11/14/17      1.06      1.26      1.40      1.55      1.68      1.81      2.06      2.26      2.38      2.64      2.84                                     ```
    ```                                                                                                                                                               ```
    ```  WORKING CODE                                                                                                                                                 ```
    ```  ============                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     R                                                                                                                                                         ```
    ```      xml_page <- read_html(url);                                                                                                                              ```
    ```      rates <- xml_page %>%                                                                                                                                    ```
    ```        html_nodes(".text_view_data") %>%                                                                                                                      ```
    ```        html_text();                                                                                                                                           ```
    ```      want<-gather(as.data.frame(rates), key = "rates");                                                                                                       ```
    ```      write.xport(want,file="d:/xpt/rates.xpt");                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     SAS                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```      libname xpt xport "d:/xpt/rates.xpt";                                                                                                                    ```
    ```      data rates(drop=nams:);                                                                                                                                  ```
    ```        retain grp 0;                                                                                                                                          ```
    ```        array nams[0:12] $6 ("date","_1Mo","_3Mo","_6Mo","_1Yr","_2Yr","_3Yr5","_Yr7","_Yr","_10Yr","_20Yr","_30Yr");                                          ```
    ```        %utl_rens(xpt.want);                                                                                                                                   ```
    ```        set want;                                                                                                                                              ```
    ```        if mod(_n_-1,12)=0 then grp=grp+1;                                                                                                                     ```
    ```        nam=nams[mod(_n_-1,12)];                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      proc transpose data=rates out=ratXpo(drop=_name_ _label_ grp);                                                                                           ```
    ```        by grp;                                                                                                                                                ```
    ```        id nam;                                                                                                                                                ```
    ```        var date_mon136_yer12357_dec102030;                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  OUTPUT                                                                                                                                                       ```
    ```  ======                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```     WORK.RATXPO total obs=10                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```         DATE      _1MO    _3MO    _6MO    _1YR    _2YR    _3YR5    _YR7    _YR     _10YR    _20YR    _30YR                                                    ```
    ```                                                                                                                                                               ```
    ```       11/01/17    1.06    1.18    1.30    1.46    1.61    1.74     2.01    2.22    2.37     2.63     2.85                                                     ```
    ```       11/02/17    1.02    1.17    1.29    1.46    1.61    1.73     2.00    2.21    2.35     2.61     2.83                                                     ```
    ```       11/03/17    1.02    1.18    1.31    1.49    1.63    1.74     1.99    2.19    2.34     2.59     2.82                                                     ```
    ```       11/06/17    1.03    1.19    1.30    1.50    1.61    1.73     1.99    2.17    2.32     2.58     2.80                                                     ```
    ```       11/07/17    1.05    1.22    1.33    1.49    1.63    1.75     1.99    2.17    2.32     2.56     2.77                                                     ```
    ```       11/08/17    1.05    1.23    1.35    1.53    1.65    1.77     2.01    2.19    2.32     2.57     2.79                                                     ```
    ```       11/09/17    1.07    1.24    1.36    1.53    1.63    1.75     2.01    2.20    2.33     2.59     2.81                                                     ```
    ```       11/10/17    1.06    1.23    1.37    1.54    1.67    1.79     2.06    2.27    2.40     2.67     2.88                                                     ```
    ```       11/13/17    1.07    1.24    1.37    1.55    1.70    1.82     2.08    2.27    2.40     2.67     2.87                                                     ```
    ```       11/14/17    1.06    1.26    1.40    1.55    1.68    1.81     2.06    2.26    2.38     2.64     2.84                                                     ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://stackoverflow.com/questions/47307510/r-webscraping-an-xml-page                                                                                       ```
    ```                                                                                                                                                               ```
    ```  Henry Navarro profile                                                                                                                                        ```
    ```  https://stackoverflow.com/users/7888588/henry-navarro                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  url <- "https://www.treasury.gov/resource-center/data-chart-center/interest-rates/Pages/TextView.aspx?data=yield"                                            ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %utl_submit_r64('                                                                                                                                            ```
    ```  source("c:/Program Files/R/R-3.3.2/etc/Rprofile.site",echo=T);                                                                                               ```
    ```  library(rvest);                                                                                                                                              ```
    ```  library(tidyr);                                                                                                                                              ```
    ```  library(SASxport);                                                                                                                                           ```
    ```  library(Hmisc);                                                                                                                                              ```
    ```  url <- "https://www.treasury.gov/resource-center/data-chart-center/interest-rates/Pages/TextView.aspx?data=yield";                                           ```
    ```  xml_page <- read_html(url);                                                                                                                                  ```
    ```  rates <- xml_page %>%                                                                                                                                        ```
    ```    html_nodes(".text_view_data") %>%                                                                                                                          ```
    ```    html_text();                                                                                                                                               ```
    ```  want<-gather(as.data.frame(rates), key = "rates");                                                                                                           ```
    ```  want$rates<-as.character(want$rates);                                                                                                                        ```
    ```  label(want$rates) <-"date_mon136_yer12357_dec102030";                                                                                                        ```
    ```  write.xport(want,file="d:/xpt/rates.xpt");                                                                                                                   ```
    ```  ');                                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  proc datasets lib=work kill;                                                                                                                                 ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  libname xpt xport "d:/xpt/rates.xpt";                                                                                                                        ```
    ```  data rates(drop=nams:);                                                                                                                                      ```
    ```    retain grp 0;                                                                                                                                              ```
    ```    array nams[0:12] $6 ("date","_1Mo","_3Mo","_6Mo","_1Yr","_2Yr","_3Yr5","_Yr7","_Yr","_10Yr","_20Yr","_30Yr");                                              ```
    ```    %utl_rens(xpt.want);                                                                                                                                       ```
    ```    set want;                                                                                                                                                  ```
    ```    if mod(_n_-1,12)=0 then grp=grp+1;                                                                                                                         ```
    ```    nam=nams[mod(_n_-1,12)];                                                                                                                                   ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  /*                                                                                                                                                           ```
    ```  WORK.RATES total obs=120                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```                      DATE_MON136_                                                                                                                             ```
    ```                        YER12357_                                                                                                                              ```
    ```  Obs    GRP      NAM   DEC102030                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```    1     1      date    11/01/17                                                                                                                              ```
    ```    2     1      _1Mo    1.06                                                                                                                                  ```
    ```    3     1      _3Mo    1.18                                                                                                                                  ```
    ```    4     1      _6Mo    1.30                                                                                                                                  ```
    ```    5     1      _1Yr    1.46                                                                                                                                  ```
    ```    6     1      _2Yr    1.61                                                                                                                                  ```
    ```  ...                                                                                                                                                          ```
    ```  */                                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  proc transpose data=rates out=ratXpo(drop=_name_ _label_ grp);                                                                                               ```
    ```    by grp;                                                                                                                                                    ```
    ```    id nam;                                                                                                                                                    ```
    ```    var date_mon136_yer12357_dec102030;                                                                                                                        ```
    ```  run;quit;                                                                                                                                                    ```

