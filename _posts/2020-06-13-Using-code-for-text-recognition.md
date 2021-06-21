---
layout: post
title: "Using a combination of VBScipt and RegEx to read text from forms"
date: 2020-06-13
---
This was my job for 4 months, I was helping to create templates for invoices, so that software can read the vital information
 and save it to a database. <br /><br />
 The way they did this was to use a custom peice of software that allowed you to view the invoice and select information for tagging
  and a selection offset from that tag that gives the value of the information.<br />
Whilst the majority of this templating only required a basic knowledge of the program, (setting an invoice start period date 
capture to stop when it gets to a "-") some of it required a bit more RegEx knowledge. <br />
For instance where the period of service dates were in a paragraph, perhaps like "Charge for the period 04 March 2019 to 04 June 2010"
   I would need to write a regex like this:<br />
   <pre><code>if instr(D1.P1.Value, "Charge for the period") then  
     startdate = filterIn(D1.P1.Value, "[\d]{1,2}\s[A-Za-z]+\s[\d]{4}(?= to)")
     enddate = filterIn(D1.P1.Value, "[\d]{2}\s[A-Za-z]+\s[\d]{4}(?! to)")
   End if
</code></pre>
So this would use VBScript to check if there was the text "Charge for the period" in the section, then uses a regular expression to 
select the information. [\d]<span style="color:red;">a number</span>{1,2}<span style="color:red;">1 or 2 of them</span>\s<span style="color:red;">a space</span>
[A-Za-z]+<span style="color:red;">1 to unlimited amount of letters in a word beginning with a capital letter</span>\s[\d]{4}<span style="color:red;">a space followed by 4 digits</span>
(?= to)<span style="color:red;">This looks ahead, if " to" is present, then the string is verified</span><br />
the (?! to) means that if there is not " to" after the string then it is captured.<br /><br />
There are several other small bits like this that can need doing, often an invoice will say "For the month of May", so I'd need to 
use the dateadd function enddate = dateadd("D",-1,dateadd("M",1,startdate.value)) which would first add a month (01 Jun 2020) then
 remove a day (31 May 2020). A more complicated example I came across the other day, the invoice had been encoded in an odd way, resulting in
  numbers being displayed in their hexidecimal form, but 29 characters further along the list (similar to a Caesar Cypher). I had to first seperate all the hexadecimal
   numbers into an array, then iterate through the array to remove the square brackets. Then used a pre written piece of code to 
   move them 29 places and convert them back to regular decimals. Then I had to put them back together again!<br /><br />
   Once all this was completed, the template can be set to that invoice account in an SQL field, and automatically used to pull the information
    from any future invoices connected to that account. <br />
    

