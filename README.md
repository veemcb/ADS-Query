# ADS-Query

The idea with this project was to determine the number of publishing astronomers on the African continent, and to see how the number of publications with African affiliations has increased over he recent past.

The data we used to make these figures were gathered by querying [NASA's Astrophysics Data System](http://adsabs.harvard.edu/) for peer-reviewed astronomy articles in which any of the authors had affiliations that linked to one of the 54 countries in Africa. The search was further restricted by including only publications between 2013 and 2018.

## Running the query
The query used the new [ADS API](https://github.com/adsabs/adsabs-dev-api) and the [Python wrapper for this API](https://ads.readthedocs.io/en/latest/)

For ADS query syntax see [this link](https://adsabs.github.io/help/search/search-syntax).

For each country in our list, the query output is parsed to search for that specific country in each affiliation. We then keep track of the Author, DOI, bibcode and date for each article.

We convert the lists into a _pandas_ DataFrame and then drop any duplicate authors.

The Jupyter notebook containing the query and an initial 

### Idiosyncracies

1. The ADS query returns a maximum of around 2800 lines, even if you set the number of rows larger than this. For that reason, we've had to run separate queries for South Africa (for each year). 

2. The _pandas_ `drop_duplicates` command will not drop all duplicates, e.g. _Carignan, C_ and _Carignan, Claude_ will be viewed as different authors. We had to implement a final, manual check for duplicates.
