presentation
========================================================
author: 
date: 
autosize: true

First Slide
========================================================

Untidy 
<table>
  <tr>
    <th><br>id</th>
    <th>var</th>
    <th>val_jan</th>
    <th>val_aug<br></th>
  </tr>
  <tr>
    <td>1</td>
    <td>City</td>
    <td>Mannheim</td>
    <td>Mannheim</td>
  </tr>
  <tr>
    <td>1</td>
    <td>temperature</td>
    <td>5C / 41F<br></td>
    <td>30C / 86F</td>
  </tr>
  <tr>
    <td>2</td>
    <td>City</td>
    <td>Hamburg</td>
    <td>Hamburg</td>
  </tr>
  <tr>
    <td>2</td>
    <td>temperature</td>
    <td>-5C / 23F</td>
    <td>25C / 77F</td>
  </tr>
</table>

Tidy
<table>
  <tr>
    <th><br>id</th>
    <th>City</th>
    <th>month</th>
    <th><br>temp_C</th>
    <th>temp_F</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Mannheim</td>
    <td>jan</td>
    <td>5</td>
    <td>41</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Mannheim</td>
    <td>aug</td>
    <td>25</td>
    <td>77</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Hamburg</td>
    <td>jan</td>
    <td>-5</td>
    <td>23</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Hamburg</td>
    <td>aug</td>
    <td>25</td>
    <td>77</td>
  </tr>
</table>

Slide With Code
========================================================


```r
summary(cars)
```

```
     speed           dist       
 Min.   : 4.0   Min.   :  2.00  
 1st Qu.:12.0   1st Qu.: 26.00  
 Median :15.0   Median : 36.00  
 Mean   :15.4   Mean   : 42.98  
 3rd Qu.:19.0   3rd Qu.: 56.00  
 Max.   :25.0   Max.   :120.00  
```

Slide With Plot
========================================================

![plot of chunk unnamed-chunk-2](presentation-figure/unnamed-chunk-2-1.png)
