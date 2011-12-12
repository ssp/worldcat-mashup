# Project at WorldCat Mashathon 2011 in Frankfurt

For comments and questions get in touch with [Sven-S. Porst](mailto:porst@sub.uni-goettingen.de) at SUB Göttingen.

This projects starts off with a standard pazpar2 search because I usually work with that environment, know my way around it and it is a quick and easy way for me to get hold of search results.

## Description
The project consists of two parts:
1. For a result with an ISBN, when opening the full record view by clicking on the record:
	1. use the [xISBN](http://oclc.org/developer/documentation/xisbn/using-api) service to determine other editions of the »same« book and add those as »Other Editions« to the result, then
	2. use the WorldCat Search service to determine the library nearest to the user(’s IP address) holding that book and add that to each of the »Other Editions«
2. When doing an extended search and typing into the »Person, Author« field:
	1. [VIAF](http://oclc.org/developer/documentation/xisbn/using-api) is queried for autocompletion suggestions and the top 10 suggestions are displayed
	2. If a suggestion is clicked, the person’s full VIAF record is loaded, all the alternate name forms are collected and turned into a big OR query for person names


## Possible improvements
* It would be great to use the xOCLCNumber instead of the xISBN service as it should be able to cover books without ISBN as well. Unfortunately the results of xOCLCNumber aren’t as rich as those of xISBN, making it impossible to do that without many extra queries.
* xISBN does not seem to support searching for all »same but different« books at a certain library. Doing that would be great to help people discover other editions that are available locally when local data is not FRBRised.
* The display of the closest library is pretty useless for all practical purposes. It could be considered to use this information to check for availability at a particular library.
* Displaying the closest library requires one query per item checked. These queries can add up very quickly if many alternate editions exist. Being able to do all of them in a single query would be great.
* VIAF suggestion data does not include the canonical form of a found person’s name. Having that would be useful to display  more informative suggestions.
* VIAF data, particularly the subset thereof sent in suggestions, usually does not include a person’s occupation, which can be very useful for disambiguating several people with the same name.

## Example xISBN
1. Go to my [test page](http://vlib.sub.uni-goettingen.de/demo/wm/viaf.html)
2. Start a search for »Krabat«
3. Click the second result (»Krabat, Roman. Otfried Preußler«)

After clicking the result it will expand to the full display and shortly after »Other Editions« will be added. Subsequently information about the »Next Copy« appears after each item of the list if the user’s location can be determined based on the IP address.

![Alternate Editions and the nearest copy as provided by xISBN and WorldCat](worldcat-mashup/raw/master/screenshots/xISBN-Krabat.png)


## Example VIAF
1. Go to my [test page](http://vlib.sub.uni-goettingen.de/demo/wm/viaf.html)
2. Open the extended search form
3. Start typing into the »Person, Author« field: »gesse, german« (This is an alternate spelling for the name of Hermann Hesse)
4. Click the item »Gesse, German, 1877-1962« that appears

During and after step 3. completion suggestions for the name appear beneath the »Person, Author« search field:

![Completion suggestions for the Author name](worldcat-mashup/raw/master/screenshots/VIAF-Gesse.png)

After clicking the first suggestion, the complete VIAF record is downloaded and an OR query for all alternate forms of the name is created and started.

![ORed query for all alternate name forms, along with results](worldcat-mashup/raw/master/screenshots/VIAF-Gesse-2.png)

As a result we see that even though we started typing the alternate spelling 'Gesse', we end up finding results in the spelling 'Hesse' as well. As the alternate forms include »Hesse, H.«, we also get results from other authors with the same initial.

