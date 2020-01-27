---
layout: post
title: "Creating a basic time counter with Java"
date: 2020-01-27
---
<a href="https://github.com/TomParr/JavaCounter">Java Counter</a><br />
A few years ago whilst I was using BlueJ for an Open University module (M250) I found out the till printers at work
will produce a reem of diagnostic information, one of the peices of data was how many hours it had been on for,
often numbering in the tens of thousands. This got me thinking if there was an easier way of displaying this information. <br />
When I got home later that day I fired up <a href="https://www.bluej.org/">BlueJ</a> and went about producing a small program 
that would take 5 inputs - hours, days, weeks, months and years. It then recompiles these figures to simplify the output as much as possible.<br />
 For instance an input of 46 hours would output as 0 years, 0 months, 0 weeks, 2 days and 2 hours. <br /><br />
 The main problem with this project at the time was that obviously the length of a month varies depending on the month! 
 I do address this in the readme, but I basically just assume a month is 30 days. 
 I use the amount of days to calculate the amount of years (365) to avoid confusion about week and month length. <br />
 <pre><code>while (this.getD() >= 365)
      {
         this.Y = this.getY() + 1;
         this.D = this.getD() - 365;
      }
</code></pre><br />
A small snippet showing how the Y object is incremented by 1 for every 365 D objects.<br />
I found this project much harder to polish off than to think up the basic code due to the decrepencies between the objects
(days in months could be 28, 30 or 31, weeks in months could be 5 or 6, weeks and years, etc) so it isn't entirely accurate! 
I do like how small it is a program though, there is only one class. <br />
Now I find another problem, I have long since uninstalled BlueJ, and the Java Development Kit it relies on
(going from the code in the file it was an Open University kit) so I cannot test it easily!.
