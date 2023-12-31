---
layout: post
title: "Text Mining with R: Romeo and Juliet"
author: "Ben Gonzalez"
date: "December 14 , 2018"
bigimg: /img/Text.PNG

---

### First things first, install the correct libraries in R. 


````
    packages<-c("Rcampdf","tm","wordcloud","ggplot2","biclust","igraph")
    install.packages(packages, dependencies = T)

````

### Next we need to load our libraries to use them. 

````
    {r setup, include=FALSE}
    library(Rcampdf)
    library(tm)
    library(wordcloud)
    library(ggplot2)
    library(biclust)
    library(igraph)
````

### Set the file path for the documents to be inspected
We will want to set up the file path one level above where our document is located. This will allow us to pick and choose which **.txt** we would like to use in our text analysis. 

````
    actone <- ("C:/Users/stlgonzb/Desktop/texts")   
    actone 
````
### Sets the directory to arbitrary name in ()

```` 
    dir(actone) 
```` 

````
    library(tm)   
    
    docs <- Corpus(DirSource(actone))   
````
### Summary of the docs object
````
    summary(docs)  
    
    inspect(docs[1])
    
    docs <- tm_map(docs, tolower) 

    docs
    
```` 

### Removes the whitespace in the document being inspected
````
    docs <- tm_map(docs, stripWhitespace)
````

### fix(docs)

````
    docs <- tm_map(docs, PlainTextDocument) 
````

````
    dtm <- DocumentTermMatrix(docs)   
    
    dtm
    
````

### Finds the frequency of the terms in a text document
````
    findFreqTerms(dtm,10)
````

### Finds term correlations with other terms
````
    findAssocs(dtm, "gun", 0.4)
````
### Removes sparse terms from a document

````
    inspect(removeSparseTerms(dtm, 0.6))

    tdm <- TermDocumentMatrix(docs)   
    tdm 

    freq <- colSums(as.matrix(dtm))   
    length(freq) 

    ord <- order(freq) 

    m <- as.matrix(dtm)   
    dim(m)   
    write.csv(m, file="dtm.csv") 
    
````

````
    dtms <- removeSparseTerms(dtm, 0.1)    
    
    inspect(dtms) 
````

````
    freq[head(ord)] 

    freq[tail(ord)]  


    head(table(freq), 20) 

    tail(table(freq), 20) 
    
````

````
    freq <- colSums(as.matrix(dtms))   
    
    freq  
    
    knitr::opts_chunk$set(echo = FALSE)
````

Romeo and Juliet- Word appears 10 times


### Plots the minimum number (frequency) of words in color
````
    set.seed(142)   
    wordcloud(names(freq), freq, min.freq=10, scale=c(5, .1), colors=brewer.pal(6, "Dark2"))  

````

### Romeo and Juliet- Word appears 30 times

````
    set.seed(142)   
    
    wordcloud(names(freq), freq, min.freq=30, scale=c(5, .1), colors=brewer.pal(6, "Dark2")) 
````

### Romeo and Juliet- Word appears 50 times

````
    set.seed(142)   
    
    wordcloud(names(freq), freq, min.freq=50, scale=c(5, .1), colors=brewer.pal(6, "Dark2")) 
    
````

### Romeo and Juliet- Word appears 75 times

````
    set.seed(142)   
    
    wordcloud(names(freq), freq, min.freq=75, scale=c(5, .1), colors=brewer.pal(6, "Dark2")) 
````

### Romeo and Juliet- Word appears 100 times

````

    set.seed(142)   
    
    wordcloud(names(freq), freq, min.freq=100, scale=c(5, .1), colors=brewer.pal(6, "Dark2")) 
    
````

