# mypButtons
mypButtons routine creates one CSV (mgstat and Windows Performance are shown in one line) from multiple pButtons HTML files. This routine works only for Windows.

# Background
InterSystems IRIS family has a nice utility **^SystemPerformance** (as known as **^pButtons** in Caché and Ensemble) which outputs the database performance information into a readable HTML file. When you run ^SystemPerformance on IRIS for Windows, a HTML file is created where both our own performance log *mgstat* and Windows performance log are included.

It's a great report, however, you need to extract log sections manually from a HTML file and paste them to a spreadsheet editor like Excel to create a performance visual graph. Many developers already share useful tips and utilities to do it [here](https://community.intersystems.com/post/intersystems-data-platforms-capacity-planning-and-performance-series-index "InterSystems Data Platforms Capacity Planning and Performance Series Index").

Now I introduce a new utiltiy **^mypButtons**!

# What's new compared to other tools
* **^mypButtons** combines mgstat and Windows performnace logs in one line. For instance, you can create a graph includes both "PhyWrs" (mgstat) and "Disk Writes/sec" (Win perfmon) in the same time frame.
* **^mypButtons** generates a single CSV file into your laptop so it's much easier to crete your graph as you like.
* **^mypButtons** generates a CSV and it includes columns which *I* strongly recommend to check as the first step to see the performance of InterSystems product. So everyone can enjoy a peformance graph with this utility so easily.

# How to run
> do readone^mypButtons("C:\temp\dir\myserver_IRIS_20230522_130000.html","^||naka")

It reads one SystemPerformance HTML file and store the information into a given global. In this sample, it reads *myserver_IRIS_20230522_130000.html* and store it into *^||naka*.

> do readdir^mypButtons("C:\temp\dir\","^||naka")

It reads all of SystemPerformance HTML files under a given folder and store the information into a given global. In this sample, it reads all HTML files under *C:\temp\dir\* and store it into *^||naka*.

> do writecsv^mypButtons("C:\temp\csv\","^||naka")

It generates the following three csv files under a given folder from a given global. 
* mgstat.csv
* perfmon.csv
* mypButtons.csv

Here, mypButtons.csv includes these columns by default, which I strongly recommend to check the performance:
* mgstat:  Glorefs, PhyRds, Gloupds, PhyWrs, WDQsz, WDphase
* perfmon: Available MBytes, Disk Reads/sec, Disk Writes/sec, % Processor Time
