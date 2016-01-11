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

# So my whole code ended up looking like this:

> plot(rom$Year,rom$SvAbs,main="The word 'roman' in the Swedish-language press and \nthe word 'romaani' in the Finnish-language press 1820-1909",ylim=c(0,10000),type="l",col="red",xlab="Year",ylab="Frequency",las=2)

> axis(side=1,at=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),labels=c("1820","1825","1830","1835","1840","1840","1850","1855","1860","1865","1870","1875","1880","1885","1890","1895","1900","1905","1910"),las=2)

> axis(side=2,at=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,10000),labels=c("0","1000","2000","3000","4000","5000","6000","7000","8000","9000","10000"),las=2)

> abline(h=c(0,1000,2000,3000,4000,5000,6000,7000,8000,9000,1000),v=c(1820,1825,1830,1835,1840,1845,1850,1855,1860,1865,1870,1875,1880,1885,1890,1895,1900,1905,1910),lty="dotted",col="lightgrey")

> lines(rom$Year,rom$FiAbs,type="l",col="blue")

# I also added a legend:

> legend(1820,9500,legend=c("Roman","Romaani"),col=c("red","blue"),lty=1)

# Finally, I printed the plot with the following command: 

> dev.print(pdf,"filename.pdf")






