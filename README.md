# data2-Philanthropy

This is a project about 20 Cultural Institutions' philanthropy data in New York City. We tried to find out the cross giving, which a board member of museum A donates to museum B, and the board member of museum B donates back. The project is initiated in the class of Mark Hansen's data II in Columbia University. 

[Download Full Story Here](story-use%20data/Philanthropy_Final_Project.docx?raw=true)

<h3>Data</h3>
We collected the data from the following 20 Institutions, said to be the richest institutions based on ranking by Crain’s New York.

- Carnegie Hall 
- Lincoln Center
- The Metropolitan Museum of Arts
- The Metropolitan Opera
- Museum of Modern Art
- New York Philharmonic
- American Museum of Natural History
- Museum of Arts and Design
- Brooklyn Public Library
- Frick Collection
- New York Public Library 
- 9/11 memorial
- Cooper Hewitt/Smithsonian
- New York Transit Museum 
- The Morgan Library and Museum
- WNET (Thirteen, WLIW, etc.)
- 92 Street Y
- Roundabout Theatre Company
- WNYC 
- Brooklyn Academy of Music

We extracted donor names and amounts from their annual report, by using an online service [pdftable](https://pdftables.com/), and turned them into a 42,955 rows csv file.


<h3>Tools</h3>
- R
- Python
- d3.js
- Gephi


<h3>Some Results</h3>


![Percentage of Board Member's donation](story-use%20data/images/bar-chart.jpg "Each bar represents the percentage of an institution's total donation income that was provided by other institution's board members.")

*Each bar represents the percentage of an institution's total donation income that was provided by other institution's board members. Lincoln Center benefited most from cross-giving.*


![Donors connections](story-use%20data/images/graph-1.png "")

*Each cluster represents an institution. The inner group of circles at the center of each institution represents the institution's board members. Blue arrows represent donations. The outer circles of each cluster represent the institution's most powerful donors. The red arrows call attention to donors who appear in multiple clusters--donors who donate to multiple institutions. This network shows how big each institution's donor network is and which institution's share similar donor bases*


![Cross Giving Chart](story-use%20data/images/graph-3.png "")

*Institutions are along the circumference according to the percentage of board members who donated to them. Colored chords connecting two institutions represent reciprocal relationships (the institutions have donated to each other through their board members). Gray chords connecting two institutions represent non-reciprocal relationships (one institution gave to the other, but the other did not give back). Lincoln Center, 9/11 Memorial and Mets are the largest player in the backscratching game*


![Institution Board Member Donation](story-use%20data/images/graph-2.png "")

*Each large orange circle represents an institution. The smaller circles clustered around it are that institution's board members. The blue arrows represent donations that board members made to institutions other than the one to which they belong. These donations are made in the board member's name. The green arrows represent donations from an organization, foundation, company or other group affiliated with a board member made to an institution to which the board member does not belong."
*


###Code

#####Python/Parse pdf to csv
[File](https://github.com/mw10104587/data2-Philanthropy/blob/master/Python/ParsePDF2CSV.py)

<pre lang="text"><code>python ParsePDF2CSV.py file.csv stackType Year Institution [Fund Type]</code></pre>

<p> We extract donors data with pdf table, and download excel from the website. Some times when the names of donors are long, like: Jackie Harris Hochberg and Robert J Hochberg, it often turns into two row. </p>

|Donors                |
|----------------------|
|Jackie Harris Hochberg|
|and Robert J Hochberg |


We manually move the second half of the data back to the first row, for all of these long donor names, and use this ParsePDF2CSV.py file to make it a csv file, adding year, institution and fund type into the data, trying reduce manual effort for journalists.

|Year|Donor                   |Amount       |Type|Institution  |
|---:|-----------------------:|------------:|---:|------------:|
|2013|The Starr Foundation    |"$25,000,000"|    |9/11 Memorial|
|2013|Bank of America         |"$20,000,000"|    |9/11 Memorial|
|2013|Bloomberg Philanthropies|"$15,000,000"|    |9/11 Memorial|
|2013|JPMorgan Chase Co       |"$15,000,000"|    |9/11 Memorial|


This is a command line tool that tackles with three kind of format.

1. par: the amount donation of each donor is listed parrallel to the donors name
2. stack: the amount of donation of each donors is stacked on the same column
3. stack-with-fundtype: the amount of donation is stacked with donors, and the fund type is parrallel to donors list.


#####Python/Amount Parser
[File](https://github.com/mw10104587/data2-Philanthropy/blob/master/Python/AmountParser.py)

<p> Different institutions have different way of showing the amount of donation in their annual reports. We parse different format of donation amount into an upper bound and a lower bound (some of them are ranges). We also classify them into 5 classes according to their amoun of donation to simplify our visualization. </p>

|Class |Amount      |
|-----:|-----------:|
|1     |  1,000,000+|
|2     |   750,000 +|
|3     |   500,000 +| 
|4     |   250,000 +|
|5     |   249,999 -|


#####Python/ Generate Node Graph Data
[File](https://github.com/mw10104587/data2-Philanthropy/blob/master/Python/GenerateNodeGraphData.py)

<pre lang="text"><code>python GenerateNodeGraphData.py donors-list.csv boards.csv smallest_donation_class></code></pre>

<p> This file takes the a donor list of 20 institutions and a list of all board members, and outputs two file for plotting a node graph, one node.csv and a edge.csv. The class for amount of donations to be taken into consideration should also be specified in the command. The classes are mentioned in the last paragraph.
</p>


### Future Plan

1. Currently there are a lot of donors who donate together, like **Jackie Harris Hochberg and Robert J Hochberg**, but we still take them as one person. We plan to parse them and split them into different rows in the future.
2. Currently there are similar names for companies and people, we plan to implement Fuzzy String matching.
3. Visualize data into web portable format. (Now on Gephi)
4. We plan to interview members of several boards, and philanthropy experts to understand more insight about this phenomenon.

