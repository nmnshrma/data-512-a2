# A2: Bias in Data
DATA 512 A Au 19: Human-Centered Data Science

## Project Goal
The project aims to do some basic exploration of biases that exist in the english wikipedia pages. We use the publicly available wikipedia dataset about politicians from various countries along with [ORES](https://www.mediawiki.org/wiki/ORES), a machine learning web service, that 'rates' the articles on certain parameters and assigns it a list of probabilities as a score reflective of its [quality](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment#Grades), per the API. We use this and another publicly available data set, called the [world population datasheet](https://www.prb.org/international/indicator/population/table/) published by the Population Reference Bureau for better evaluation.

## Project Structure
```
.
├── LICENSE
├── README.md
├── hcds-a2-bias.ipynb
├── results-data
│   ├── quality-map.csv
│   └── wiki_page_merged.csv
└── source-data
    ├── WPDS_2018_data.csv
    └── page_data.csv
```

## Data Source

1. __Politicial Articles - English Wikipedia__

The Wikipedia politicians by country dataset is gathered from [Figshare](https://figshare.com/articles/Untitled_Item/5513449). Originaly, the data was extracted via the Wikimedia API using the associated code by Os Keyes. The fields in the data are:

1. "country", containing the sanitised country name, extracted from the category name;
2. "page", the unsanitised page title.
3. "rev_id", Unique identifier, refers to the the edit ID of the last edit to the page.

LICENSE: CC-BY-SA 4.0

2. __Population by country__

Drawn from the world population datasheet published by the [Population Reference Bureau](https://www.prb.org/international/indicator/population/table/)

Explicit license info not available on the website.

## Results Generated

We consider two major metrics to investigate the bias in the English Wikipedia pages: 
1. Coverage: The percentage of articles-per-population
2. Relative Quality: The proportion of articles that were rated either 'FA' or 'GA' by the ORES service 

Final results generated:

1. __Top 10 countries by coverage__: 10 highest-ranked countries in terms of number of politician articles as a proportion of country population
2. __Bottom 10 countries by coverage__: 10 lowest-ranked countries in terms of number of politician articles as a proportion of country population
3. __Top 10 countries by relative quality__: 10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
4. __Bottom 10 countries by relative quality__: 10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
5. __Geographic regions by coverage__: Ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population
6.__Geographic regions by coverage__: Ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality_

## API Documentation

The key APIs used in the project is the [Wikimedia ORES API](https://www.mediawiki.org/wiki/ORES)

The ORES service is build to deliver article and edit quality grades, as stated in the wiki content assessment [page](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment#Grades). It contains the quality score, in the form of probabilities, for all articles at a given point in time.

Note: The ORES API contains the article quality data, but the API service may not serve quality score for all revision IDs. The project considers article scored as {'FA' , 'GA'} as good.

ORES API Response Object:
```
{'enwiki': {'models': {'wp10': {'version': '0.8.1'}},
  'scores': 
  {'806503132': {'wp10': {'score': {'prediction': 'Start',
      'probability': {'B': 0.08366287323596852,
       'C': 0.17744300684057873,
       'FA': 0.005809853264138301,
       'GA': 0.01580210415313383,
       'Start': 0.6655620827086284,
       'Stub': 0.05172007979755225}}}},
   '806503196': {'wp10': {'score': {'prediction': 'Start',
      'probability': {'B': 0.030833538536049584,
       'C': 0.05191350351802135,
       'FA': 0.0039232070356563,
       'GA': 0.006332520745605151,
       'Start': 0.7767308522691304,
       'Stub': 0.1302663778955373}}}}}}}
```

ORES API Article quality reference, listed best to worse:

1. FA - Featured article
2. GA - Good article
3. B - B-class article
4. C - C-class article
5. Start - Start-class article
6. Stub - Stub-class article


## License

By using Wikimedia ORES API, you agree to [Wikimedia's Terms of Use](https://wikimediafoundation.org/wiki/Terms_of_Use/en) and [Privacy Policy](https://wikimediafoundation.org/wiki/Privacy_policy)

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/nmnshrma/data-512-a1/blob/master/LICENSE) file for details
