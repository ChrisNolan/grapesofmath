---
layout: post
title:  "Benford's Law"
date:   2014-10-05 17:00:00
categories: chapter2
---
Chapter Two introduces us to an interesting distribute of leading digits of numbers which we learn is now known as [Benford's Law] (p 30) but could have been known as the Law of Anomalous Numbers.

I wanted to reproduce the example using data from the [Doomsday Book], but after looking around for a few minutes I couldn't find a public version of it available -- only ones behind pay walls or government logins.  Next I thought I'd do a text input so you could just paste in whatever you wanted... but Khan Academy doesn't have that type of input.  Ok, multiline string?  Now, that doesn't work well either.  So find some text you want to do the count on, put it into a text editor that handles special characters and search and replace all tabs (\t) and newlines (\n) and returns (\r) to spaces and paste it into the program as the var myText.

The program will then go through and count up the first digits of any numbers it finds, figure out the percentage distribution of those numbers, and then graph the result.

The excepted result is shown in this image: ![benford graphic][benford_graphic]

The distribution should be 1: 30.1% / 2: 17.6% / 3: 12.5% / 4: 9.7% / 5: 7.9% / 6: 6.7% / 7: 5.8% / 8: 5.1% / 9: 4.6%  

The example text I pulled from wikipedia on [Demographics in Toronto][Demographics of Toronto] doesn't fit the curve exactly.  Too small a sample?

<h3><a href="http://www.khanacademy.org/cs/gom-benfords-law/4661942277111808">GOM: Benford&#x27;s Law</a></h3> <script src="http://www.khanacademy.org/cs/gom-benfords-law/4661942277111808/embed.js?editor=yes&amp;buttons=yes&amp;author=no&amp;embed=yes"></script>

For more Khan Academy content on [Benford's Law], start with [Vi and Sal's chat] about it.

Here is the source code for reference

{% highlight javascript %}
// More info @ http://grapesofmath.chrisnolan.ca/chapter2/Benford%27s%20Law.html

// Input text - change this text to change the output

var myText = "Toronto population by year, within present boundaries    Year  City  Urban  CMA  GTA  GTHA  GH  GGH  1861    65,085[6]  &#8212;  193,844[6]  &#8212;  &#8212;  &#8212;  &#8212;    1901  238,080[6]  &#8212;  440,000[6]  &#8212;  &#8212;  &#8212;  &#8212;    1931  856,955  &#8212;  810,000[7]  &#8212;  &#8212;  &#8212;  &#8212;    1941  951,549  &#8212;  900,000[7]  &#8212;  &#8212;  &#8212;  &#8212;    1951  1,176,622  &#8212;  1,262,000[7]  &#8212;  &#8212;  &#8212;  &#8212;    1961  1,824,481  &#8212;  1,919,000[7]  &#8212;  &#8212;  &#8212;  &#8212;    1971  2,089,729[8]  &#8212;  2,628,045[9]  &#8212;  &#8212;  &#8212;  &#8212;    1976  2,124,291[8]  &#8212;  2,803,101[9]  &#8212;  &#8212;  &#8212;  &#8212;    1981  2,137,395[8]  &#8212;  2,998,947[9]  &#8212;  &#8212;  &#8212;  &#8212;    1986  2,192,721[10]  &#8212;  3,427,170[9]  3,733,085[10]  &#8212;  &#8212;  &#8212;    1991  2,275,771[10]  &#8212;  3,893,933[11]  4,235,756[10]  &#8212;  &#8212;  &#8212;    1996  2,385,421[12]  &#8212;  4,263,759[12]  4,628,883[13]  5,096,682[14]  5,500,186[14]  6,935,499[14]    2001  2,481,494[15]  4,375,899[16]  4,682,897[15]  5,081,826[13]  5,572,104[14]  5,982,678[14]  7,532,246[14]    2006  2,503,281[15]  4,732,361[17]  5,113,149[15]  5,555,912[18]  6,060,471[19]  6,487,892[19]  8,164,593[19]    2011  2,615,060[20]  5,132,794[17]  5,583,064[20]  6,054,191[21]  6,574,140[21]  7,005,486[21]  8,759,312[21]   The last complete census by Statistics Canada estimated there were 2,615,060 people living in Toronto,[20] making it the largest city in Canada,[22] and the fifth most populous municipality in North America.[23]  City of Toronto  (2011 census)  2,615,060  Toronto Census Metropolitan Area  (2011 census)  5,583,064  Annual Growth Rate  0.9%   Population growth studies have projected the City of Toronto&apos;s population in 2020 to reach 3,000,000, and the Greater Toronto Area would reach a population of roughly 7.5 million in 2025. Toronto&apos;s population grew by 1.0% from 2001 to 2006, with an annual growth rate of 0.2%. As of 2001, 17.5% of the population was 14 years and under, and 13.6% was 65 years and over; the median age was 36.9 years. Most recent studies show this has dropped to around 35.4 years of age, and the growth rate has increased to 0.4%.   2011 Census population data for the City of Toronto are to found readily aggregrated at a finer level than the city as a whole at i. the electoral district (riding) level (2003 redistribution)[21] and ii. the neighbourhood level.[24] The three ridings with the largest increase in population between 2006 and 2011 in the City of Toronto have been Trinity-Spadina (25.5%), Etobicoke-Lakeshore (7.3%), and Toronto Centre (7.3%); actually, the following four (4) ridings in the GTA have had a higher population increase even than Trinity-Spadina, and along with the aforementioned City of Toronto riding constitute the five (5) Ontario ridings with the highest increase in population: Oak Ridges-Markham (35.5%), Halton (33.9%), Vaughan (27.1%), and Bramalea-Gore-Malton (25.8%). On the contrary, the population in the Davenport riding actually decreased (-2.2%), whereas in Scarborough-Agincourt (+0.2%) and Toronto-Danforth (+0.3%) it only marginally increased (these are the lowest figures for the GTA at large too).   The neighbourhoods in the City of Toronto that experienced the highest increase in population from 2001 to 2011 are:       Toronto: Waterfront Communities-The Island (133.6%), Niagara (83.4%), Bay Street Corridor (37.7%), Church-Yonge Corridor (29.6%), Mount Pleasant West (25.4%), Moss Park (24.3%), Junction Area (15.5%), Cabbagetown-South St. James Town (13.7%), Casa Loma (12.3%), University (11.4%)      North York: Willowdale East (66.7%), Bayview Village (42.4%), Willowdale West (31.6%), Lansing-Westgate (24.4%), Banbury-Don Mills (16.7%), Bathurst Manor (15.2%), Newtonbrook West (12.5%), Englemount-Lawrence (10.1%)      Scarborough: Rouge (59.6%), Clairlea-Birchmount (24.0%), Bendale (21.4%)      Etobicoke: Islington-City Centre West (20.9%), Kingsway South (11.9%)      East York: Thorncliffe Park (15.7%)   It is in the neighbourhoods of Corso Italia-Davenport (-12.8%), Greenwood-Coxwell (-11.9%), Regent Park (-11.3%), and Little Portugal (-10.3%) in the old city of Toronto; and Caledonia-Fairbank (-10.4%) and Beechborough-Greenbrook (-10.0%) in York that population has declined the most.   Visible minority and Aboriginal population[28][29][30]  Population group  Population (2011)   % of total population (2011)  Population (2006)   % of total population (2006)  White  1,292,365  50.2%  1,300,330  52.5%  Visible minority group  South Asian  317,100  12.3%  298,370  12%  Chinese  278,390  10.8%  283,075  11.4%  Black  218,160  8.5%  208,555  8.4%  Filipino  132,445  5.1%  102,555  4.1%  Latin American  71,205  2.8%  64,855  2.6%  Arab  28,920  1.1%  22,485  0.9%  Southeast Asian  46,825  1.8%  37,495  1.5%  West Asian  50,235  2%  42,755  1.7%  Korean  37,225  1.4%  34,220  1.4%  Japanese  12,315  0.5%  11,965  0.5%  Visible minority, n.i.e.  33,670  1.3%  25,195  1%  Multiple visible minorities  37,920  1.5%  31,100  1.3%  Total visible minority population  1,264,395  49.1%  1,162,630  46.9%  Aboriginal group  First Nations  12,990  0.5%  9,130  0.4%  M&#233;tis  4,875  0.2%  3,650  0.1%  Inuit  305  0%  195  0%  Aboriginal, n.i.e.  920  0%  485  0%  Multiple Aboriginal identities  180  0%  145  0%  Total Aboriginal population  19,265  0.7%  13,605  0.5%  Total population  2,576,025  100%  2,476,565  100% ";
var words = myText.split(" ");

var getLeadingDigit = function(n) {
    var number = "" + parseInt(n, 10);
    return number.charAt(0);
};

var leadingDigit = 0;
var leadingDigits = [];
var leadingDigitsPercentage = [];
var total = 0;
// init the array filled with zeroes ; should be a better way
for (var i=1; i<10; i++){
    leadingDigits[i]=0;
    leadingDigitsPercentage[i]=0;
}

// Add up the counters per digit
for (var i=0; i<words.length; i++) {
    leadingDigit = getLeadingDigit(words[i]);
    if (leadingDigit !== "0") {
        leadingDigit = leadingDigits[leadingDigit]++;
        total++;
    }
}

// Calculate the percentages
for (var i=1; i<10; i++) {
    leadingDigitsPercentage[i] = round((leadingDigits[i]/total)*1000)/10;
}

// Display the counts
text("Leading Digits", 10, 10);
fill(35, 54, 161);
for (var i=1; i<10; i++) {
    text(i + ": " + leadingDigits[i] + " ("+leadingDigitsPercentage[i]+"%)", 5, 30*i);
}

// Graph the percentages
textSize(9);
for (var i=1; i<10; i++) {
    fill(35, 54, 161);
    rect(30*i+60, 350, 20, -leadingDigitsPercentage[i]*4);
    fill(0, 0, 0);
    text(leadingDigitsPercentage[i]+"%", 30*i+60, 345-leadingDigitsPercentage[i]*4);
    text(i, 30*i+67, 365);
}
{% endhighlight %}

[Doomsday Book]: http://en.wikipedia.org/wiki/Domesday_Book
[benford_graphic]: http://upload.wikimedia.org/wikipedia/commons/4/46/Rozklad_benforda.svg
[Demographics of Toronto]: http://en.wikipedia.org/wiki/Demographics_of_Toronto
[Benford's Law]: http://en.wikipedia.org/wiki/Benford%27s_law
[Vi and Sal's chat]: https://www.khanacademy.org/math/algebra2/logarithms-tutorial/logarithmic-scale-patterns/v/vi-and-sal-talk-about-the-mysteries-of-benford-s-law