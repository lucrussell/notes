---
post_title: Attempting to Retrieve JSON Opens up the response as if it was a file download
author: Luc
post_date: 
layout: post
---
## Problem 
Attempting to Retrieve JSON Opens up the response as if it was a file download
## Solution 
See [this link](http://stackoverflow.com/questions/4516702/json-object-returned-as-file-download-spring-mvc/) for more information.

Essentially, you have to let jQuery know to expect a JSON response back from the
server, i.e. use the `$getJSON` function for a GET, or something like this
for a POST: 

    $.post(url, $("#myForm").serialize(), function(data) {
        alert('data'); 
    }, "json");
    

