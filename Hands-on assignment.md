# Hands-on assignment

# THE TASK

#I wanted to find out how frequent the words 'roman' and 'romaani' have been in the Swedish-language and Finnish-language press, respectively, during the years 1820–1909.

# THE DATASET

# Since I wanted to find out how frequent the words 'roman' and 'romaani' have been in the Finnish press, I chose the Finnish newspapers digitized by the National Library as my dataset. I first tried to get the data I needed by using Jupyter and the Korp API, as we did on the lectures. For one reason or another, however, I couldn't get the code to work. Not wanting to disturb our dear teachers with my incompetence, I then decided to simply use the Korp GUI – which, as far as I can tell, is more than servicable enough if you simply want to compare the frequency of two words. 

# To break it down:

# I first used the Advanced Search in Korp to search for the baseform of ”romaani” [lemma=”romaani”] in all the Finnish newspapers from 1820–1909. The result:

# https://korp.csc.fi/#?corpus=klk_fi_1909,klk_fi_1908,klk_fi_1907,klk_fi_1906,klk_fi_1905,klk_fi_1904,klk_fi_1903,klk_fi_1902,klk_fi_1901,klk_fi_1900,klk_fi_1899,klk_fi_1898,klk_fi_1897,klk_fi_1896,klk_fi_1895,klk_fi_1894,klk_fi_1893,klk_fi_1892,klk_fi_1891,klk_fi_1890,klk_fi_1889,klk_fi_1888,klk_fi_1887,klk_fi_1886,klk_fi_1885,klk_fi_1884,klk_fi_1883,klk_fi_1882,klk_fi_1881,klk_fi_1880,klk_fi_1879,klk_fi_1878,klk_fi_1877,klk_fi_1876,klk_fi_1875,klk_fi_1874,klk_fi_1873,klk_fi_1872,klk_fi_1871,klk_fi_1870,klk_fi_1869,klk_fi_1868,klk_fi_1867,klk_fi_1866,klk_fi_1865,klk_fi_1864,klk_fi_1863,klk_fi_1862,klk_fi_1861,klk_fi_1860,klk_fi_1859,klk_fi_1858,klk_fi_1857,klk_fi_1856,klk_fi_1855,klk_fi_1854,klk_fi_1853,klk_fi_1852,klk_fi_1851,klk_fi_1850,klk_fi_1849,klk_fi_1848,klk_fi_1847,klk_fi_1846,klk_fi_1845,klk_fi_1844,klk_fi_1842,klk_fi_1841,klk_fi_1840,klk_fi_1839,klk_fi_1838,klk_fi_1837,klk_fi_1836,klk_fi_1835,klk_fi_1834,klk_fi_1833,klk_fi_1832,klk_fi_1831,klk_fi_1830,klk_fi_1829,klk_fi_1827,klk_fi_1826,klk_fi_1825,klk_fi_1824,klk_fi_1823,klk_fi_1822,klk_fi_1821,klk_fi_1820&search_tab=2&lang=en&hpp=50&cqp=%5B%5D&result_tab=1&search=cqp%7C%5Blemma%3D%22romaani%22%5D

# Korp sorts the hits by year automatically, and gives you the option of downloading the results as a csv-file. I did this. 

# I then did a similar search [lemma=”roman”] in the Swedish-language newspaper corpus, and combined the two csv-files into one. I now had a csv-file showing the absolute frequency of 'romaani' in Finnish-language newspapers and the absolute frequency of 'roman' in Swedish-language newspapers. This file (roman.csv) has been attached.

# CREATING A GRAPH

# While it would have been immensely easier to create the graph in Excel, I decided to try out RStudio. Having very little experience with codes and programming, it was quite challenging. But in the end, and thanks to much googling, I managed to create a passable graph (I think). I won't go into the many mistakes I made or the many things I didn't understand, I'll just show you how I – in the end – did it.

# First I imported the csv-file into Rstudio, turning it into a dataframe. I named this dataframe ”rom”. Then I created a basic line graph using this code:

> plot(rom$Year,rom$SvAbs,main="The word 'roman' in the Swedish-language press and \nthe word 'romaani' in the Finnish-language press 1820-1909",ylim=c(0,10000),type="l",col="red",xlab="Year",ylab="Frequency",las=2)

# To break it down:

> plot(rom$Year,rom$SvAbs)		

# Draws a graph of the values that are in the columns ”Year” and ”SvAbs”. (The csv-file that I had made and imported had three columns: Year, SvAbs and FiAbs.)

> main="The word 'roman' in the Swedish-language press and \nthe word 'romaani' in the Finnish-language press 1820-1909"

# Draws the title of the graph. \n splits the title on two rows

> ylim=c(0,10000)

# Determines the limits of the y-axis (I wanted it to go from 0 to 10000).

> type="1"

# Determines the type of graph that is being drawn. Type 1 is an ordinary line graph.

> col="red"

# Determines the color of the line.

> xlab="Year"
> ylab="Frequency (absolute)"

# Determines the labels on the x- and y-axis.

> las=2

# Turns the tick mark labels on the x-axis vertical.

# When you draw graphs with R, you are given ”tick marks” automatically. Since the tick marks that R gave me didn't seem optimal (R had placed them at 1820, 1840, 1860, 1880 and 1900) I wanted to remove them and add my own tick marks. I found some helpful code for this on stackoverflow.com:

# "You can suppress the drawing of the axis altogether and add the tick marks later with axis().
To suppress the drawing of the axis use plot(... , xaxt = "n"). Then call axis() with side, at, and labels: axis(side = 1, at = v1, labels = v2). With side referring to the side of the axis (1 = x-axis, 2 = y-axis), v1 being a vector containing the position of the ticks (e.g., c(1, 3, 5) if your axis ranges from 0 to 6 and you want three marks), and v2 a vector containing the labels for the specified tick marks (must be of same length as v1, e.g., c("group a", "group b", "group c"))."

# Since I wanted to place the tick marks on the x-axis at 5-year intervals (1820, 1825, etc), I used this code:

> axis(side=1,at=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),labels=c("1820","1825","1830","1835","1840","1840","1850","1855","1860","1865","1870","1870","1880","1885","1890","1895","1900","1905","1910"),las=2)

# I also added some tick markers on the y-axis:

> axis(side=2,at=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,10000),labels=c("0","1000","2000","3000","4000","5000","6000","7000","8000","9000","10000"),las=2)

# I realized that the graph would look better with a grid. I googled for a code and found this:

> grid(nx=NA,ny=NULL,col="lightgray",lty="dotted")

# However, this only placed the grid on the automatically generated tick marks, not the tick marks I had created myself. So I kept googling and ended up using another code, abline().

> abline(h=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,1000),v=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),lty="dotted",col="lightgrey")

# When I had drawn a graph showing the frequency of 'roman' in Swedish-language newspapers, I wanted to add a line showing the frequency of 'romaani' in Finnish-language newspapers. You can add lines to a graph by using lines(). I used the following code:

> lines(rom$Year,rom$FiAbs,type="l",col="blue")

# I also added a legend:

> legend(1820,9500,legend=c("Roman","Romaani"),col=c("red","blue"),lty=1)

# So my whole code ended up looking like this:

> plot(rom$Year,rom$SvAbs,main="The word 'roman' in the Swedish-language press and \nthe word 'romaani' in the Finnish-language press 1820-1909",ylim=c(0,10000),type="l",col="red",xlab="Year",ylab="Frequency",las=2)

> axis(side=1,at=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),labels=c("1820","1825","1830","1835","1840","1840","1850","1855","1860","1865","1870","1875","1880","1885","1890","1895","1900","1905","1910"),las=2)

> axis(side=2,at=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,10000),labels=c("0","1000","2000","3000","4000","5000","6000","7000","8000","9000","10000"),las=2)

> abline(h=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,1000),v=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),lty="dotted",col="lightgrey")

> lines(rom$Year,rom$FiAbs,type="l",col="blue")

> legend(1820,9500,legend=c("Roman","Romaani"),col=c("red","blue"),lty=1)

# Finally, I printed the plot with the following command: 

> dev.print(pdf,"filename.pdf")

# PLEASE NOTE: Since I couldn't figure out how to upload images to GitHub, I haven't attached the final graph itself. You should nevertheless be able to re-create the graph by using the csv-file and the code above.

# INTERPRETATION

# Does this graph actually tell us anything interesting, then? Well, it mostly tells us that the word ”romaani” entered Finnish-language newspapers somewhat later than the word ”roman” entered Swedish-language newspapers. In the Finnish-language newspapers, the word ”romaani” started to be used in the 1880s – before that it was more or less nonexistent. In the Swedish-language newspapers, however, the word has been used consistently (more than 100 times per year) since at least the 1840s.

# More surprisingly: after the year 1905 the absolute frequency of the word ”romaani” in the Finnish newspapers rises sharphly. It is hard to say what lies behind this development, but there are at least a couple of historical factors one can point to. First, as Toivo Nygård points out in Suomen lehdistön historia 2 (1987), the Finnish press expanded strongly in the years 1905–1908. After the parliamentary reform in 1906, the political parties were eager to reach out to the public. This resulted in a multitude of new newspapers, especially Finnish-language newspapers. (Toivo Nygård, ”Sanomalehdistön yleispiirteet 1906–1917”, Päiviö Tommila (päätomittaja), Suomen lehdistön historia 2 : sanomalehdistö suurlakosta talvisotaan, Kustannuskiila Oy, Kuopio 1987, s. 16.) This drastic expansion is also reflected in the newspaper corpus itself:

# Finnish-language newspapers in Korp: number of tokens per year

# Year    Number of tokens
# 1909      258,643,730 
# 1908      249,949,036 
# 1907      233,414,790 
# 1906      202,405,976 
# 1905      152,047,147 
# 1904      124,892,321 
# 1903      123,835,330
# 1902      110,773,624 
# 1901      114,239,738 
# 1900      126,352,523 

# Also, as we can see in Korp, the Swedish-language press didn't grow nearly as much: from 78 million tokens in 1900 to 90 million in 1909.

# Another probable reason for the increased frequency of the word ”romaani” are the commercials. As a quick glance at the search results in Korp will tell you, many – if not most – hits are from bookstore and publisher commercials. And as Nygård points out, the amount of commercials published in newspapers also increased in 1906: ”Lähes kaikissa lehdissä kaupallisiin ilmoituksiin myyty tekstiala kasvoi vuodesta 1906 vuoteen 1910. Tämän jälkeen kehitys taittui laskuun.” (Nygård 1987, s. 142.)

# These two factors – an increased amount of newspapers and an increased amount of commercials (which, of course, were reprinted many times in many different newspapers) – might explain why the word ”romaani” becomes so frequent in Finnish newspapers after 1905.

# FINAL REMARKS

# There are some caveats to this study that should be pointed out.

# First, the OCR of the newspapers in the National Digital Library is far from perfect. This means that a search for ”romaani” will not find all the occurences of the word in the corpus. Second, the lemmatization has been done automatically, by machine, which means that there are mistakes. For example, a search for the baseform ”romaani” also returns the following hits:

# "Tawallisesti kun puhutaan amerilalaisista tarkoitetaan niillä Pohjois-Nmerikan anglosak » silaista r « wa ja tiekin muistetaan että koto Etelä^Amerita ja osa pohjoisesta » kin on toista heimoa , nimittäin romaanilaista, espanjalaisia ja portugalilaisia."

# "Ensimmäiseen luuluu : itämainen kirjallisuus , klassillinen kirjallisuus , manha kristillinen ja ja keskiajan latinankielinen lirjallisuus ; toiseen osaan : romaanilainen lirjallisuus ( Italia , Espansa , Portugali , Ranska , Nnmania ) ; kolmanteen osaan : germamlaincn kirjallisuus ( Englanti , Alankomaat , Belgia , Salsa , Skandinamilaiset maat ) , suomalainen lirjallisuus -a muiden Euroopan kansojen lirjallisnus ."

# Because of these factors, the results of this study should be taken with a grain of salt. While the general trend shown in the graph is most likely true, the frequencies that the graph is based on should be thought of as approximate rather than exact.

# It should also be pointed out that the corpus doesn't include all Finnish newspapers from 1820–1909. The newspaper collection of the National Library is not complete: some numbers of some journals are missing. This is not likely to change the big picture, but it still needs to be pointed out.

# Finally, while absolute frequencies are interesting in themselves, relative frequencies can be even more interesting. Absolute frequencies can tell us when a word first appears in a corpus, and give us a rough idea of how common it has been at certain points in time. However, when comparing different corpora of different sizes (such as the Finnish-language newspaper corpus and the Swedish-language newspaper corpus) it makes more sense to study relative frequencies. 




