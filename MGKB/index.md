# MigrationsKB


## Introduction

**MigrationsKB(MGKB)** is a public Knowledge Base of anonymized **Migration** related **annotated** tweets.
The MGKB currently contains over **200 thousand** tweets, spanning over 9 years (January 2013 to July 2021),
filtered with 11 European countries of *the United Kingdom, Germany, Spain, Poland, France, Sweden, Austria, Hungary, Switzerland, Netherlands and Italy*.
**Metadata** information about the tweets, such as Geo information (**place name**, **coordinates**, **country code**).
**MGKB** contains **entities**, **sentiments**, **hate speeches**, **topics**, **hashtags**, _encrypted user mentions_ in RDF format.
The schema of **MGKB** is an extension of TweetsKB for migrations related information.
Moreover, to associate and represent the potential economic and social factors driving the migration flows such as [**eurostat**](https://ec.europa.eu/eurostat/web/main/home), 
[**statista**](https://www.statista.com/), etc. FIBO ontology was used. The extracted **economic indicators**,
such as GDP Growth Rate, are connected with each Tweet in RDF using geographical and temporal dimensions.
The user IDs and the tweet texts are encrypted for privacy purposes, while the tweet IDs are preserved.


## RDF/S Model
### Overall Schema
![](images/migrationKB_schema.png)

### Schema for Economic Indicators and Provenance Information
![](images/fibo-schema.png)
<details>
<summary> <b> Financial Industry Business Ontology (FIBO)</b> representing  <b>Economic Indicators of EU</b></summary>
<ul>
<li>The class <tt>fibo-ind-ei-ei:GrossDomesticProduct</tt> represents the GDPR of the country of the tweet in a certain year, 
which are specified by the properties <tt>schema:addressCountry<\tt> 
and  <tt>dc:date</tt>from DCMI, and the value of this indicator is represented by
<tt>fibo-ind-ei-ei:hasIndicatorValue</tt> </li>

<li>
The class <tt>fibo-ind-ei-ei:UnemploymentRate</tt> represents the unemployment rate in the country of
the tweet in a certain year, represented with the help of the same properties, 
i.e.,  <tt>schema:addressCountry</tt>, <tt>dc:date</tt>, and <tt>fibo-ind-ei-ei:hasIndicatorValue</tt>.</li>

<li>The class <tt>fibo-ind-ei-ei:UnemployedPopulation</tt> is used to specify the population of the unemployment rate. </li>
<li>The class <tt>fibo-fnd-dt-fd:ExplicitDate</tt> represents the date when the statistics are last updated as a literal with the help of the property <tt>fibo-fnd-dt-fd:hasDateValue</tt>.</li>
<li>The property <tt>fibo-fnd-rel-rel:isCharacterizedBy</tt>  is used to associate a tweet with the economic indicators.</li>
</ul>
</details>

<details>
<summary>
<b>PROV-O</b> representing <b>Provenance Information</b>

<p>To represent the provenance information about the economic indicators, i.e., Eurostat, Statista, UK parliament, and Office of National Statistics, PROV-O is used. The class <tt>prov:Activity</tt> defines an activity that occurs over a period of time and acts upon entities, which are defined by the class <tt>prov:Entity<\tt>. The class <tt>fibo-fnd-arr-asmt:AssessmentActivity</tt> represents an assessment activity involving the evaluation and estimation of the economic indicators, which is a subclass of the class <tt>prov:Activity</tt>.
The class  <tt>prov:Organization</tt> represents a governmental organization or a company that is associated with the assessment activity, which is a subclass of the class <tt>prov:Agent</tt>. </p>
</summary>
</details>

<details>
<summary>Further extensions</summary>
<ul>
<li><tt>dc:subject</tt> represents a topic of a tweet resulting from topic modeling.</li>
<li> <tt>wna:neutral-emotion</tt>  represents the neutral sentiment of the tweet by applying sentiment analysis.</li>
<li> <tt> wna:hate</tt>, <tt>mgkb:offensive</tt> and <tt> mgkb:normal</tt> represent the hate speeches, offensive speeches and normal speeches from hate speech detection of the tweets.</li>
<li> <tt>schema:ReplyAction</tt> represents the action of reply regarding a tweet.</li>
<li> <tt>mgkb:EconomicIndicators</tt> represents the economic indicators, which has the subclasses <tt>fibo-ind-ei-ei:GrossDomesticProduct</tt> and <tt>fibo-ind-ei-ei:UnemploymentRate</tt>.</li>
<li><tt>t mgkb:YouthUnemploymentRate</tt> and <tt>mgkb:TotalUnemploymentRate</tt> represent the unemployment rates with respect to the population, i.e., the youth unemployment population and the total unemployed population.</li>
</ul>
</details>


:clipboard: [Documentation of RDF Model](migrationsKB/documentation.html)

:pencil: [Codes](https://github.com/migrationsKB/MGKB) 

:open_file_folder: [Data](https://zenodo.org/record/5206820#.YRqF1nUza0o)

:question: [SPARQL endpoint](https://mgkb.fiz-karlsruhe.de/sparql/)

:page_with_curl: [Technical Report (arXiv)](https://arxiv.org/pdf/2108.07593.pdf) 

## Overall Framework
![](images/overall-framework.png)



## Purpose
* Provide query-able resource about public attitudes on social media towards migration
* Provide an insight into which factors in terms of economic indicators are the driving factors of that attitude.

## Geo Map of The Tweets
<iframe width="100%" height="520" frameborder="0" src="https://migrationskb.carto.com/builder/55b7655b-30de-41c9-9e09-2ab30284c225/embed" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
[Download `MapOfTweets`](data/MapOfTweets.carto)

## Statistics and Plots

### 1. Statistics of the EU countries with the most first time asylum applicants
[source](https://ec.europa.eu/eurostat/databrowser/view/tps00191/default/table?lang=en) 

<details>
<summary>Table</summary>

<table>
<thead>
<tr>
<th>Country</th>
<th>2013</th>
<th>2014</th>
<th>2015</th>
<th>2016</th>
<th>2017</th>
<th>2018</th>
<th>2019</th>
<th>2020</th>
<th>SUM</th>
</tr>
</thead>
<tbody>
<tr>
<td>Germany</td>
<td>126705</td>
<td>202645</td>
<td>476510</td>
<td>745160</td>
<td>222565</td>
<td>184180</td>
<td>165615</td>
<td>121955</td>
<td>2245335</td>
</tr>
<tr>
<td>Spain</td>
<td>4485</td>
<td>5615</td>
<td>14780</td>
<td>15755</td>
<td>36610</td>
<td>54050</td>
<td>117800</td>
<td>88530</td>
<td>337625</td>
</tr>
<tr>
<td>Poland</td>
<td>15240</td>
<td>8020</td>
<td>12190</td>
<td>12305</td>
<td>5045</td>
<td>4110</td>
<td>4070</td>
<td>2785</td>
<td>63765</td>
</tr>
<tr>
<td>France</td>
<td>66265</td>
<td>64310</td>
<td>76165</td>
<td>84270</td>
<td>99330</td>
<td>137665</td>
<td>151070</td>
<td>93470</td>
<td>772545</td>
</tr>
<tr>
<td>Sweden</td>
<td>54270</td>
<td>81185</td>
<td>162450</td>
<td>28795</td>
<td>26330</td>
<td>21560</td>
<td>26255</td>
<td>16225</td>
<td>417070</td>
</tr>
<tr>
<td>United Kingdom</td>
<td>30585</td>
<td>32785</td>
<td>40160</td>
<td>39735</td>
<td>34780</td>
<td>38840</td>
<td>46055</td>
<td>36041</td>
<td>298981</td>
</tr>
<tr>
<td>Austria</td>
<td>17500</td>
<td>28035</td>
<td>88160</td>
<td>42255</td>
<td>24715</td>
<td>13710</td>
<td>12860</td>
<td>14180</td>
<td>241415</td>
</tr>
<tr>
<td>Hungary</td>
<td>18895</td>
<td>42775</td>
<td>177135</td>
<td>29430</td>
<td>3390</td>
<td>670</td>
<td>500</td>
<td>115</td>
<td>272910</td>
</tr>
<tr>
<td>Switzerland</td>
<td>21305</td>
<td>23560</td>
<td>39445</td>
<td>27140</td>
<td>18015</td>
<td>15160</td>
<td>14195</td>
<td>10990</td>
<td>169810</td>
</tr>
<tr>
<td>Netherlands</td>
<td>13065</td>
<td>24495</td>
<td>44970</td>
<td>20945</td>
<td>18210</td>
<td>24025</td>
<td>25200</td>
<td>15255</td>
<td>186165</td>
</tr>
<tr>
<td>Italy</td>
<td>26620</td>
<td>64625</td>
<td>83540</td>
<td>122960</td>
<td>128850</td>
<td>59950</td>
<td>43770</td>
<td>26535</td>
<td>556850</td>
</tr>
</tbody>
</table>


</details>

### 2. Statistics of Tweets before and after ETM

#### Selecting Migration-related Tweets
<details>
<summary>Detail</summary>
<p>
Green referes to migration-related topics, and orange refers to other topics. 
MGPS refers to the maximal migration-related topic probaiblity score.

<a href="images/tm_filter/tweet_filtering.png">
<img src="images/tm_filter/tweet_filtering.png" alt="tweet filtering">
</a>

The tweets are then refined based on topic embeddings.
For each topic, the  <a href="https://bit.ly/2SZgpKb">top 20 words</a> (ranked by their probability) are 
selected as representatives of the topic. 
These words are then manually verified based on their relevance to the topic 
of migration, accordingly, <a href="https://bit.ly/30z25wp">the migration-related topics</a> are 
chosen. 
The migration-related tweets are chosen with the help of the probabilities 
associated to all the topics. Regarding the chosen topics, 
the maximal probability score for each tweet is extracted. 

For this tweet, it has the **maximal migration-related topic probability score (MGPS)** 0.8.

By manual evaluation, the threshold for reserving the tweets by the maximal probability score is set to 0.45. Hence, 
the tweet showed in the Figure is reserved for further analysis.
</p>
</details>



<details>
<summary>The distribution of maximal probability scores of tweets regarding migration-related topics before filtering</summary>
<a href="images/tm_filter/dist_topic_max_scores_50.png">
<img src="images/tm_filter/dist_topic_max_scores_50.png" alt="dist_before_filtering">
</a>
</details>

<details>
<summary>The distribution of maximal probability scores of tweets regarding migration-related topics after filtering</summary>
<a href="images/tm_filter/dist_topic_max_scores_50_t4.5.png">
<img src="images/tm_filter/dist_topic_max_scores_50_t4.5.png" alt="dist_after_filtering">
</a>
</details>


### 3. Correlations of the Negative Public Attitudes and The Economic Indicators
More [plots for each destination country](stats.md)

To learn the potential cause of the negative public attitudes towards migrations, the factors such as unemployment
rate including youth unemployment rate and totla unemployment rate, and gross domestic product growth rate (GDPR) were studied.
This data was collected from [Eurostat](https://ec.europa.eu/eurostat), [Statista](https://www.statista.com/),
[UK Parliament](https://www.parliament.uk/), and [Office for National Statistics](https://www.ons.gov.uk/).

The following figure shows the comparison between the factors (such as youth unemployment rate, total unemployment rate,
and real GDPR) and the negative attitudes (i.e., negative sentiment and hate speech) in all the extracted
tweets. On average in all 11 destination countries, the percentages of hate speech and negative sentiment of the public
towards immigration are negatively correlated with the real GDPR and positively correlated with total/youth
unemployment rate, from 2013 to 2018 and from 2019 to 2020. In 2019, the percentages of hateful tweets and negative tweets
are rapidly increased by about 2% and 1% respectively compared to 2018.

<details>
<summary>Figure</summary>
<a href="images/stats/percentage_correlations/ALL.png">
<img src="images/stats/percentage_correlations/ALL.png" alt="percentage_coorelations">
</a>
</details>



## Sparql Queries
* **Online SPARQL endpoint Query [example](virtuoso.md)**.

* Locally 
  * Download `nt` file for **MGKB** on [Zenodo](https://zenodo.org/record/5206820#.YRqF1nUza0o). 
  * Download and run [blazegraph](blazegraph.md)


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

* The following query retrieve a list of top 20 hashtags which contain "refugee" or "immigrant".
```sparql 
SELECT ?hashtagLabel (count(distinct ?tweet) as ?num) WHERE {
  ?tweet schema:mentions ?hashtag.
  ?hashtag a sioc_t:Tag ; rdfs:label ?hashtagLabel.  FILTER( regex(?hashtagLabel, "refugee", "i") || lcase(str(?hashtagLabel))="refugee" ||  regex(?hashtagLabel, "immigrant", "i") || lcase(str(?hashtagLabel))="immigrant").
} GROUP BY ?hashtagLabel ORDER BY DESC(?num) LIMIT 20
```

[comment]: <> (<img src="images/sparql_query_results/top20_hashtags_refugee_immigrant.png" alt="hashtags" width="200" />)

[comment]: <> (![]&#40;images/sparql_query_results/top20_hashtags_refugee_immigrant.png&#41;)

<details>
<summary> Answer </summary>
<a href="images/sparql_query_results/top20_hashtags_refugee_immigrant.png">
<img src="images/sparql_query_results/top20_hashtags_refugee_immigrant.png" alt="top20_hashtags_refugee_immigrant">
</a>
</details>


* The following query retrieve a list of top 10 the entity labels which contain "refugee" and its frequency of detected entity mentions.
```sparql
SELECT ?entityLabel (count(?entityLabel) as ?numOfEntityMentions)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?entityLabel. FILTER( regex(?entityLabel, "refugee", "i") || lcase(str(?entityLabel))="refugee").
 }GROUP BY ?entityLabel ORDER BY DESC(?numOfEntityMentions) LIMIT 10
```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/entity_mentions_containing_refugee.png">
<img src="images/sparql_query_results/entity_mentions_containing_refugee.png" alt="entity_mentions_containing_refugee">
</a>
</details>

[comment]: <> (<img src="images/sparql_query_results/entity_mentions_containing_refugee.png" width="400px"/>)


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

<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/emotions_entity_containing_refugee_camp.png">
<img src="images/sparql_query_results/emotions_entity_containing_refugee_camp.png" alt="emotions_entity_containing_refugee_camp">
</a>

</details>

[comment]: <> (<img src="images/sparql_query_results/emotions_entity_containing_refugee_camp.png" width="400px" />)

* The following query requests the top-10 hashtags co-occurring with the entity label containing "refugee".

```sparql
SELECT ?hastagLabel (count(distinct ?tweet) as ?num) WHERE {
  ?tweet schema:mentions ?entity .
  ?entity a nee:Entity ; nee:hasMatchedURI ?uri .
  ?uri a rdfs:Resource; rdfs:label ?x.  FILTER( regex(?x, "refugee", "i") || lcase(str(?x))="refugee").

  ?tweet schema:mentions ?hashtag.
  ?hashtag a sioc_t:Tag ; rdfs:label ?hastagLabel 
} GROUP BY ?hastagLabel ORDER BY DESC(?num) LIMIT 10
```

<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee.png">
<img src="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee.png" alt="top10_coocur_hashtags_with_entity_refugee">
</a>
</details>

[comment]: <> (<img src="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee.png" width="400px" />)

[comment]: <> (![]&#40;images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee.png&#41;)

* The following query retrieves GDPR indicator values and the number of tweet hate speeches in the United Kingdom.
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

<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/gdpr_hate_speech_GB.png">
<img src="images/sparql_query_results/gdpr_hate_speech_GB.png" alt="gdpr_hate_speech_GB">
</a>
</details>

[comment]: <> (<img src="images/sparql_query_results/gdpr_hate_speech_GB.png" width="400px" />)

* The following query retrieves average GDPR indicator values and the number of tweet hate speeches 
  in 11 destination countries.
```sparql
SELECT  ?year (AVG(?IndicatorValue) AS ?avgIndicatorValue) (count(?tweet) as ?numOfTweets) where {
  ?tweet fibo_fnd_rel_rel:isCharacterizedBy ?gdpr.
  ?gdpr a fibo_ind_ei_ei:GrossDomesticProduct.
  ?gdpr dc:date ?year.
  ?gdpr fibo_ind_ei_ei:hasIndicatorValue ?IndicatorValue.
  ?tweet onyx:hasEmotionSet ?y.
  ?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  ?z a onyx:Emotion; onyx:hasEmotionCategory wna:hate.
 }GROUP BY ?year ORDER BY DESC(?year)
```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/avgRGDPR_hate.png">
<img src="images/sparql_query_results/avgRGDPR_hate.png" alt="avgRGDPR_hate">
</a>

</details>

[comment]: <> (<img src="images/sparql_query_results/avgRGDPR_hate.png" width="400px" />)

* The following query retrieve a list of all the entity labels which contain "refugee camp" and its frequency of detected entity mentions.
```sparql
SELECT ?EntityLabel(count(?EntityLabel) as ?NumberOfMentions)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?EntityLabel. FILTER( regex(?EntityLabel, "refugee camp", "i") || lcase(str(?EntityLabel))="refugee camp").
 }GROUP BY ?EntityLabel ORDER BY DESC(?NumberOfMentions)
```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/num_of_entities_refugee_camp.png">
<img src="images/sparql_query_results/num_of_entities_refugee_camp.png" alt="num_of_entities_refugee_camp">
</a>

</details>

[comment]: <> (<img src="images/sparql_query_results/num_of_entities_refugee_camp.png" width="400px" />)



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
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/emotion_category_hashtag_containing_refugee.png">
<img src="images/sparql_query_results/emotion_category_hashtag_containing_refugee.png" alt="emotion_category_hashtag_containing_refugee">
</a>
</details>

[comment]: <> (<img src="images/sparql_query_results/emotion_category_hashtag_containing_refugee.png" width="400px" />)

* The following query retrieves GDPR indicator values and the number of negative sentiment tweets in the United Kingdom.
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
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/negative-emotion-gdpr-GB.png">
<img src="images/sparql_query_results/negative-emotion-gdpr-GB.png" alt="negative-emotion-gdpr-GB">
</a>
</details>

[comment]: <> (<img src="images/sparql_query_results/negative-emotion-gdpr-GB.png" width="400px" />)


* The following query requests the top-10 hashtags co-occurring with the entity label containing "refugee camp".

```sparql
SELECT ?hastagLabel (count(distinct ?tweet) as ?num) WHERE {
  ?tweet schema:mentions ?entity .
  ?entity a nee:Entity ; nee:hasMatchedURI ?uri .
  ?uri a rdfs:Resource; rdfs:label ?x.  FILTER( regex(?x, "refugee camp", "i") || lcase(str(?x))="refugee camp").

  ?tweet schema:mentions ?hashtag.
  ?hashtag a sioc_t:Tag ; rdfs:label ?hastagLabel 
} GROUP BY ?hastagLabel ORDER BY DESC(?num) LIMIT 10
```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee_camp.png">
<img src="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee_camp.png" alt="top10_coocur_hashtags_with_entity_refugee_camp">
</a>

</details>

[comment]: <> (<img src="images/sparql_query_results/top10_coocur_hashtags_with_entity_refugee_camp.png" width="300px" />)

* The following query retrieves a list of emotion categories (neutral/positive/negative sentiment, 
  and hate speeches/offensive/normal) of tweets where the labels of detected entity mentions containing "refugeecamp".

```sparql
SELECT ?EmotionCategory (count(?tweet) as ?numOfTweets)   where{
	?tweet schema:mentions ?hashtag.
  	?hashtag a sioc_t:Tag; rdfs:label ?x. FILTER( regex(?x, "refugeecamp", "i") || lcase(str(?x))="refugeecamp").
  	?tweet onyx:hasEmotionSet ?y.
  	?y a onyx:EmotionSet; onyx:hasEmotion ?z.
  	?z a onyx:Emotion; onyx:hasEmotionCategory ?EmotionCategory.
 } GROUP BY ?EmotionCategory

```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/emotion_categories_hashtag_refugee_camp.png">
<img src="images/sparql_query_results/emotion_categories_hashtag_refugee_camp.png" alt="emotion_categories_hashtag_refugee_camp">
</a>

</details>

[comment]: <> (<img src="images/sparql_query_results/emotion_categories_hashtag_refugee_camp.png" width="400px" />)


* The following query retrieves the number of tweets about a particular refugee camp "zaatari refugee camp".
```sparql
SELECT (count(?tweet) as ?num)   where{
	?tweet schema:mentions ?entity.
  	?entity a nee:Entity; nee:hasMatchedURI ?uri. 
	?uri a rdfs:Resource; rdfs:label ?x. FILTER(  lcase(str(?x))="zaatari refugee camp").
 }
```
<details>
<summary>Answer</summary>
<a href="images/sparql_query_results/num_of_tweets_entity_zaatari.png">
<img src="images/sparql_query_results/num_of_tweets_entity_zaatari.png" alt="num_of_tweets_entity_zaatari">
</a>

</details>


[comment]: <> (<img src="images/sparql_query_results/num_of_tweets_entity_zaatari.png" width="400px" />)

## Citation
```
@misc{chen2021migrationskb,
      title={MigrationsKB: A Knowledge Base of Public Attitudes towards Migrations and their Driving Factors}, 
      author={Yiyi Chen and Harald Sack and Mehwish Alam},
      year={2021},
      eprint={2108.07593},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```


## Acknowledgement
This work is a part of [ITFlows project](https://www.itflows.eu). This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement No 882986.


## License

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
