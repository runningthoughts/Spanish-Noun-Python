# Spanish Noun Statistics Python Learner Scripts
I'm new to Python and needed a simple, first project to do. I hate Hello Worlds if I can do something a bit more useful.  As I am taking Spanish, now at the B2 level after 2+ years of study, I decided to do a gender analysis of the most common nouns.  I found a site that listed the Top 2000 nouns from this site (https://frequencylists.blogspot.com/2015/12/the-2000-most-frequently-used-spanish.html), and set about writing a scraper plus a stats script once the scraped CSV file was created.  It consists of the following (which are also in the Jupyter Notebooks as comments):

## Web Scraper
This is a dead simple app that is simply meant to help me learn basic Python capabilities.  I am enlisting Claude to help wtih this module as well to serve as a teacher and accelerator.  Hence, everything in here is hard-coded.

### Purpose
The purpose of this module is simply to extract a list of the top 2000 nouns and their gender in Spanish from a blog entry I found. In the next module, I will run statistics on that to generate some simple statistics.  The output will go into a CSV file.

### Trimming
The hard-coded site above has specific formatting that needs to be dealt with.  First we need to trim off lines that are not useful to us, some before and some after.

### Parsing
The Parse_Entry function is the main part here.  There are four main formats for the list that need to be dealt with.  The author of the blog article was not totally consistent in the way they conveyed the data.  Four formats capture more than 99% of the list.  The remainder amount to a few entries, so rather than code up every last permutation, we'll just throw those out, as it will have an insignificant effect on the statistics we will generate later.

#### Supported Formats
1.  ``word - palabra - gender``
2.  ``word - palabra - gender / palabra - gender``
3.  ``word - palabro/palabra - masculine/feminine``
4.  ``word - palabro/a - masculine/feminine``

The first one accounts for the bulk of the entries.  The remaining three are mostly variations of the same thing- words that change slightly in spelling for the other gender.  Typically, in Spanish, nouns ending in "o" are masculine and words ending in "a" are feminine.  But not always.  *While "palabro" is not a word, but is meant to show that when it is used in these last two formats, the word ending in "o" is always masculine in these cases.*

In all cases, the English word is discarded as we only want to run stats on the Spanish words.  The result is that the output will always be for these formats:

``word - palabra- gender                        ``&rarr;`` palabra,gender``\
*The gender may be masculine, feminine or masculine/feminine. In the latter case, gender will be set to "both"*

``word - palabra - gender / palabra - gender  |``\
``word - palabro/palabra - masculine/feminine | ``&rarr;`` | palabro,gender``\
``word - palabro/a - masculine/feminine       |     | palabra,gender``

with the latter formats resulting in splitting into two outputs lines.

Remaining formats number less than 20 lines and will be discarded.

## Spanish Gender Stats
This is a simple practice at some very basic data analysis and plotting.  In a separate Python script- FinalScraper, I scraped a basic list of the most popular 2000 nouns.  That scraper was very messy due to inconsistent formatting on the source page.  A few of the 2000 were discarded as "not worth the hassle" to accommodate every single format variant.  98% were covered with 5 formats there.  And some words were "doubled up" with a special o/a or word/word nomenclature, and those were split to 2 lines.

The net result was a CSV file in a very simple word,gender format.  Genders are masculine, feminine, and both (for things like Professions).

I generate 3 representations of data below:
1. Total distribution of m/f/both nouns
2. -o (normally masculine) excpetions and -a (normally feminine) exceptions
3. A table listing the exceptions for each, as well as a list of the words that are both genders in the 3rd column.

As said, simple stuff.  This is for me to learn with.

