stat433\_hw1\_webscraping
================
Jenna Ji
Feb 3, 2021

``` r
# read html
library(rvest)
```

    ## Warning: package 'rvest' was built under R version 4.0.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 4.0.3

``` r
library(xml2)
library(stringr)
faculty_web = "https://guide.wisc.edu/faculty/"
faculty = read_html(faculty_web)

# Use Selector Gadget from Chrome Extensions
info_chunk = html_nodes(faculty,"li p")

# convert xml_node to string
# CLEAN data
str_chunk_text = toString(info_chunk)
wi = unlist(strsplit(str_chunk_text, "</p>, "))
w1 = str_remove_all(wi,"<p>")

name = c()
position = c()
department = c()
degree = c()

# loop through data to add into df
for(i in 1:length(w1)){
    x = unlist(strsplit(w1[i], split = "<br>"))
    name[i] = x[1]
    position[i] = x[2]
    department[i] = x[3]
    degree[i] = x[4]
  }

# FINAL DF
df = data.frame(Name=name,
                 Position=position, 
                 Department=department, 
                 Degree_Information=degree)
```
