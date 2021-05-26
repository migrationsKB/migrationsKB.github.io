## Introduction

**MigrationsKB** is a public RDF corpus of anonymized data for a collection of **Migration** related **annotated** tweets. 
The dataset currently contains over **170 thousand** tweets, spaning over 7 years (January 2013 to December 2020), 
filtered with 11 European countries of *United Kingdom, Germany, Spain, Poland, France, Sweden, Austria, Hungary, Switzerland, Netherlands and Italy*.
**Metadata** information about the tweets, such as geo information (**place name**, **coordinates**, **country code**), 
and the extracted **entities**, **sentiments**, **hate speeches**, **topics**, **hashtags**, _encrypted user mentions_ are stored in RDF, 
based on and extended the displayed RDF/S vocabularies from [**TweetsKB**](https://data.gesis.org/tweetskb/).
Moreover, to associate the potential economic and social factors driving the migration flows, the external databases such as 
[**eurostat**](https://ec.europa.eu/eurostat/web/main/home), [**statista**](https://www.statista.com/) are used. The extracted 
**economic indicators**, such as GDP Growth Rate, are connected with each Tweet in RDF using geographical and temporal dimensions.
The user ids and the tweet texts are encrypted for privacy, while the tweet IDs are reserved for reproducibility of this study.

Paper
 
[Code](https://github.com/migrationsKB/MGKB) 

[Documentation of RDF Model](migrationsKB/documentation.html)
## Purpose
* Provide query-able resource about public attitudes on social media towards migration
* Provide an insight into which factors in terms of economic indicators are the driving factors of that attitude.

## Geo Map of The Tweets
<iframe width="100%" height="520" frameborder="0" src="https://migrationskb.carto.com/builder/69edca56-f1b1-4add-9b2d-ef1ab1e6cf58/embed" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
[Download `MapOfTweets`](data/MapOfTweets.carto)

## Statistics of the EU countries with the most first time asylum applicants
* [source](https://ec.europa.eu/eurostat/databrowser/view/tps00191/default/table?lang=en) 

  |Country | 2013 | 2014 | 2015 |	2016  | 2017 |	2018 |	2019 |	2020 |	SUM | 
  | ---  | --- | ---  | ---     | ---   | ---    | ---  | ---   | ---  |---|
  | Germany |	126705 |	202645 |	476510 | 745160 |	222565 |	184180 |	165615 |	121955 |	2245335 |
  | Spain	| 4485  |	5615 |	14780 |	15755 |	36610  | 54050  |	117800 |	88530 |	337625 |
  | Poland | 15240 |	8020 |	12190 |	12305 |	5045 |	4110 |	4070 |	2785 |	63765 |
  | France 	| 66265 | 64310 | 76165 |	84270 |	99330 | 137665 | 151070 |	93470 | 772545 |
  |Sweden	| 54270 |	81185  | 162450 | 28795 | 26330 | 21560 | 26255 | 16225  | 417070 | 
  | United Kingdom  | 	30585  | 32785 | 40160 | 39735 | 34780	| 38840 |	46055 |	36041 |	298981 |
  | Austria |	17500 |	28035 |	88160 |	42255  | 24715 |  13710 |	12860 | 14180 | 241415 | 
  | Hungary	| 18895 |	42775 | 177135  |	29430 |	3390  | 670	 | 500  |	115	 | 272910 | 
  | Switzerland	| 21305	 | 23560 | 39445 |	27140 |	18015 |	15160 |	14195 |	10990 |	169810 |
  | Netherlands	| 13065 | 24495  |	44970 | 20945 |	18210|24025 |	25200 |	15255 |	186165 |
  | Italy |	26620 |	64625|	83540 |	122960 |	128850|	59950|	43770 |	26535 |	556850 |	 


## Overall Framework
![](images/overall-framework.png)


## RDF/S Model
### Overall Schema
![](images/migrationKB_schema.png)

## Correlations of the Negative Public Attitudes and The Economic Indicators
More [plots for each destination country](stats.md)
![](images/stats/percentage_correlations/ALL.png)

## Sparql Queries
The dump for [MigrationsKB](data/migrationsKB_05222021_235316.tar.xz)

Download and run [blazegraph](blazegraph.md)

* Prefixes:
```sparql
prefix mgkb: <https://migrationskb.github.io/MGKB#> 
prefix dc: <http://purl.org/dc/elements/1.1/> 
prefix fibo_fnd_arr_asmt: <https://spec.edmcouncil.org/fibo/ontology/FND/Arrangements/Assessments/> 
prefix fibo_fnd_arr_rep: <https://spec.edmcouncil.org/fibo/ontology/FND/Arrangements/Reporting/> 
prefix fibo_fnd_dt_fd: <https://spec.edmcouncil.org/fibo/ontology/FND/DatesAndTimes/FinancialDates/> 
prefix fibo_fnd_rel_rel: <https://spec.edmcouncil.org/fibo/ontology/FND/Relations/Relations/> 
prefix fibo_fnd_utl_alx: <https://spec.edmcouncil.org/fibo/ontology/FND/Utilities/Analytics/> 
prefix fibo_ind_ei_ei: <https://spec.edmcouncil.org/fibo/ontology/IND/EconomicIndicators/EconomicIndicators/> 
prefix nee: <http://www.ics.forth.gr/isl/oae/core#> 
prefix onyx: <http://www.gsi.dit.upm.es/ontologies/onyx/ns#> 
prefix owl: <http://www.w3.org/2002/07/owl#> 
prefix prov: <https://www.w3.org/TR/prov-o/#> 
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> 
prefix rdf: <https://www.w3.org/1999/02/22-rdf-syntax-ns#> 
prefix schema: <http://schema.org/> 
prefix sioc: <http://rdfs.org/sioc/ns#> 
prefix sioc_t: <http://rdfs.org/sioc/types#> 
prefix wna: <http://www.gsi.dit.upm.es/ontologies/wnaffect/ns#> 
prefix xsd: <http://www.w3.org/2001/XMLSchema#>
```
* The following query retrieve a list of all the entitiy labels which contain "refugee" and its frequency of detected entity mentions.
```sparql
SELECT ?entityLabel (count(?entityLabel) as ?numOfEntityMentions)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?entityLabel. FILTER( regex(?entityLabel, "refugee", "i") || lcase(str(?entityLabel))="refugee").
 }GROUP BY ?entityLabel ORDER BY DESC(?numOfEntityMentions) LIMIT 10
```




* The following query retrieves a list of emotion categories (neutral/positive/negative sentiment, 
  and hate speeches/offensive/normal) of tweets where the labels of detected entity mentions containing "refugee camp".
```sparql
SELECT ?EmotionCategory (count(?tweet) as ?numOfTweets)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?x.  FILTER( regex(?x, "refugee camp", "i") || lcase(str(?x))="refugee camp").
  	?tweet onyx:hasEmotionSet ?y.
  	?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  	?z a onyx:Emotion; onyx:hasEmotionCategory ?EmotionCategory.
 } GROUP BY ?EmotionCategory
```





* The following query requests the top-10 hashtags co-occuring with the entity label containing "refugee".

```sparql
SELECT ?hastagLabel (count(distinct ?tweet) as ?num) WHERE {
  ?tweet schema:mentions ?entity .
  ?entity a nee:Entity ; nee:hasMatchedURI ?uri .
  ?uri a rdfs:Resource; rdfs:label ?x.  FILTER( regex(?x, "refugee", "i") || lcase(str(?x))="refugee").

  ?tweet schema:mentions ?hashtag.
  ?hashtag a sioc_t:Tag ; rdfs:label ?hastagLabel 
} GROUP BY ?hastagLabel ORDER BY DESC(?num) LIMIT 10
```

[comment]: <> (![]&#40;images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee.png&#41;)

* The following query retrieves GDPR indicator values and the number of tweet hate speeches in United Kingdom.
```sparql
SELECT  ?year ?IndicatorValue (count(?tweet) as ?numOfTweets) where {
  ?tweet fibo_fnd_rel_rel:isCharacterizedBy ?gdpr.
  ?gdpr a fibo_ind_ei_ei:GrossDomesticProduct.
  ?gdpr schema:addressCountry "GB". 
  ?gdpr dc:date ?year.
  ?gdpr fibo_ind_ei_ei:hasIndicatorValue ?IndicatorValue.
  ?tweet onyx:hasEmotionSet ?y.
  ?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  ?z a onyx:Emotion; onyx:hasEmotionCategory wna:hate.
 }GROUP BY ?year ?IndicatorValue ORDER BY DESC(?year)
```



* The following query retrieve a list of all the entity labels which contain "refugee camp" and its frequency of detected entity mentions.
```sparql
SELECT ?x (count(?x) as ?num)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?x. FILTER( regex(?x, "refugee camp", "i") || lcase(str(?x))="refugee camp").
 }GROUP BY ?x ORDER BY DESC(?num)
```


* The following query retrieve emotions regarding the hashtags containing "refugee".
```sparql
SELECT ?EmotionCategory (count(?tweet) as ?numOfTweets)   where{
	?tweet schema:mentions ?hashtag.
  	?hashtag a sioc_t:Tag; rdfs:label ?x. FILTER( regex(?x, "refugee", "i") || lcase(str(?x))="refugee").
  	?tweet onyx:hasEmotionSet ?y.
  	?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  	?z a onyx:Emotion; onyx:hasEmotionCategory ?EmotionCategory.
 } GROUP BY ?EmotionCategory
```


* The following query retrieves GDPR indicator values and the number of negative sentiment tweets in United Kingdom.
```sparql
SELECT  ?year ?IndicatorValue (count(?tweet) as ?numOfTweets) where {
  ?tweet fibo_fnd_rel_rel:isCharacterizedBy ?gdpr.
  ?gdpr a fibo_ind_ei_ei:GrossDomesticProduct.
  ?gdpr schema:addressCountry "GB". 
  ?gdpr dc:date ?year.
  ?gdpr fibo_ind_ei_ei:hasIndicatorValue ?IndicatorValue.
  ?tweet onyx:hasEmotionSet ?y.
  ?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  ?z a onyx:Emotion; onyx:hasEmotionCategory wna:negative-emotion.
 }GROUP BY ?year ?IndicatorValue ORDER BY DESC(?year)
```




* The following query requests the top-10 hashtags co-occuring with the entity label containing "refugee camp".

```sparql
SELECT ?hastagLabel (count(distinct ?tweet) as ?num) WHERE {
  ?tweet schema:mentions ?entity .
  ?entity a nee:Entity ; nee:hasMatchedURI ?uri .
  ?uri a rdfs:Resource; rdfs:label ?x.  FILTER( regex(?x, "refugee camp", "i") || lcase(str(?x))="refugee camp").

  ?tweet schema:mentions ?hashtag.
  ?hashtag a sioc_t:Tag ; rdfs:label ?hastagLabel 
} GROUP BY ?hastagLabel ORDER BY DESC(?num) LIMIT 10
```



* The following query retrieves a list of emotion categories (neutral/positive/negative sentiment, 
  and hate speeches/offensive/normal) of tweets where the labels of detected entity mentions containing "refugee camp".

```sparql
SELECT ?EmotionCategory (count(?tweet) as ?numOfTweets)   where{
	?tweet schema:mentions ?hashtag.
  	?hashtag a sioc_t:Tag; rdfs:label ?x. FILTER( regex(?x, "refugee camp", "i") || lcase(str(?x))="refugee camp").
  	?tweet onyx:hasEmotionSet ?y.
  	?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  	?z a onyx:Emotion; onyx:hasEmotionCategory ?EmotionCategory.
 } GROUP BY ?EmotionCategory

```


* The following query retrieves the number of tweets about a particular refugee camp "zaatari refugee camp".
```sparql
SELECT (count(?tweet) as ?num)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?x. FILTER(  lcase(str(?x))="zaatari refugee camp").
 }
```


## About

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
