# IA 626 Final Project, NYC Arrests Data and NYC COVID Data

 # Table of contents
1. [Introduction](#introduction)
2. [What Data and Why?](#paragraph1)
3. [Parsing and Joining my Data](#paragraph2)
    1. [Getting Comfortable With My Data](#subparagraph1)
    2. [Subsetting My Data](#subparagraph2)
    3. [Joining My Data](#subparagraph3)
4. [Analyzing My Data](#paragraph3)
    1. [Arrests vs Cases](#subparagraph4)
    2. [Arrests vs Deaths](#subparagraph5)
    
## Introduction <a name="introduction"></a>
The follwoing project outlines the procces finding my data, and why I chose the data sets I did. I will also outline the necessary steps I needed to take to filter my data sets inorder to join them as well as the process I took to join them. Lastly I will discuss what my newly joined data showed and the analysis I created.

## What Data and Why? <a name="paragraph1"></a>
Understanding that my realistic ability to take two super complex data sets and filter them to something that allowed me to join them was limited, I decided to focus on one thing first, what kind of data would make for a good join? Throughout the semester I felt as though we had done a lot with dates, whther change the structure of them, finding MIN and MAX dates within data or creating subsets based of specific dates. Thus I decided my data should at least have dates in both of them, as I knew I could match their structures up to join as well as filter uneeded data if one set contained too much. Second, I wanted the data to be something relevent to our current life and interesting to me, and whats more current and interesting than COVID? Not much right now, so with that I started to look for my forst dataset, at first I started at a national scale and had found some decent sets but then I started to think about what I would join that to, and another relevent thing to everyone is crime, so I started looking into national crime datasets, but that became such a large scope and size that it seemed a bit unreasonable. Knowing COVID and Crime would be a good route to go I just shrunk my scope a bit and focused on states and decided to use New York and obviously the first thing that popped up when I searched "NY COVID Data", was the city. Because theres no such thing as New York outside the city apparatenly. So I rolled with it and found a nice NYC COVID data set, so next was arrest data and I was able to find a 1,1 million kb dataset about essentially all arrest made in NYC with quite a few variables. The two sets both had dates, and I was entrigued to see how COVID impacted the number of arrests, as well as other atributes like age groups, sex, race, and types of crime.


## Parsing and Joining My Data <a name="paragraph2"></a>

### Getting Comfortable with my Data <a name="subparagraph1"></a>
After dowloading my data I used a csv reader to read it into python and jupyter lab, once that was done I printed the first two lines of my data sets to see what the headers were and see how the actual data points looked as well as how they where formated. Again both datasets contained dates and they were both formated in the same way mm/dd/yyyy the only difference was that my arrest data contained multiple of the same dates as multiple arrests happen on the same day, my COVID data had unique dates as it recorded cases, deaths, and so on once for every day. This is was an important thing to remeber when formating my join later. I then found the MIN and MAX dates of my Arrest data and found that the MIN date was 1/1/2006 and the Max date was 12/31/2020, for my Covid data it was 2/28/2020 and 11/7/21.
### Subsetting My Data <a name="subparagraph2"></a>
Onece I realized that my Arrest Data was just too large and outside the scope I was looking for I decided to make two subsets of the data one for 2019 as a "control" and then my 2020 data that I would join my COVID to. Again this was something we had done in class where I isolated the column or 'row' that contained my dates, split it by the "/" and then selected my years. I then used that to reference a variable that would be 2019 or 2020 depending on the data sat I created and saif if the year in the data set is equal the the variable then write the row. once completed I had a set with all 2019 arrests and one with all 2020 arrests
### Joining My Data <a name="subparagraph3"></a>
With my new subset arrest data that matched up with with my Covid data I now had to join them together off my dates. Referencing back to my earlier comment about unique dates and repeated dates, it was important to think about how I would join the two sets together. Meaning, I couldn't join my arrest data "TO" my Covid data because for every one row of COVID data there where multiple rows of Arrest data because again, covid dates are unique and arrest dates are not. Thus I had to make sure I joined my covid data "TO" my arrest data such that for every row for arrest date there would be the same repeated row of COVID data that shared the same date. With that in mind I created a function similar to that as in class where if I typed print(lookup_datecsv['03/27/2020']), it would print out that row with all the info in it. I then created my joined file and created the first row on my own, making spefic columns and naming them. I chose to only join specific parts of each data set as I felt some of the fields were unecessary and irrelevent to my project. Once, choosinf and lbeleing which columns to include I then set up the writer to write the date and use the function to write the data from the shared covid file and the data from the the arrest file. once completed I now had a csv file that showed 2020 arrest data as well as covid data for those dates. It is also important to not that it only joined on dates where there were boths arrests and COVID information, meaning for January and February before COVID was tracked there are no joined rows.

## Analyzing My Data <a name="paragraph3"></a>
With my new csv file I was able to open it into excel and create pivot tables. excel is where I am a bit more well versed so I was able to work out a few kinks with the data. Meaning it wasnt as simple as picking the dates as a row and then cases and arrests as my values. What I ended up doing was taking the unique arrest key and counting each key, now my output would be the count of unique arrest keys which tranlates to total arrests, then for covid cases or covid death is was a bit more tricky, what I had to do was take the average cases for each date and then just sum the averages to get my month and total. This was all thing I was able to do in the setting within the pivot table, but I know through excel I could do it and that it would take less time and prevent me from making mistakes rather than trying to use python to count for me. Once I had this figured out I was able to make some comparrisons between covid deaths and cases vs different arrest information.
### Arrests vs COVID Cases <a name="subparagraph4"></a>
This comparison was initially the main one I though about when starting this project. To be honest I thought there would be a more direct comparison. Initially there was a pretty strong correlation between the number of cases and the effect it had on the number of arrests made. I ran a regression on the first 3 months of data as well as the whole 10 months. The first 3 months vs arrests had a Multiple R of .89 but when compared to the whole time frame it drops down to .13. This to me shows that at first covid cases did effect the number of arrests made when cases went up crime went down and when cases dropped back down arrest went back up, but as time went on the correlation dissapeared and cases didnt effect arrests as much or nearly at all.

Regression for the first 3 months: <br>
y=(-.06)x + 15836<br>
<br>
![regression 3 months](images/arrests.vs.cases.regression.3months.JPG "regression 3 months")
<br>
<br>
Regression for the 10 months:<br>
y=0.008x+10408<br>
<br>
![regression whole time](images/arrests.vs.cases.regression.JPG "regression whole time")
### Arrests vs COVID Deaths <a name="subparagraph5"></a>