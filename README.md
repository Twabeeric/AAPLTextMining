# Apple-Stock-Text-Mining
Daniel Schinder, Dylan Bates, Eric Ontieri
April 29, 2019

Text Mining Final Report

Objectives and Implications of the Analysis

The main goal for this analysis is to determine whether weekly news articles centering around a certain company can be used to predict a stock price increase or decrease.  The analysis focuses on changes each week in the stock price of Apple between the market close on Friday and opening on Monday. Specifically, the question is: can a positive vs. negative scrape of these types of reports lead to a statistically significant forecast on stock price?

If the answer to this question is yes, then this analysis can be repeated by investors to help make better investment decisions. Additionally, this practice could also  influence when may be best for people to buy or sell stocks.  If it turns out that this analysis can be repeated with statistical significance for any stock, then it may be worth it to wait until Monday morning or Sunday night to make stock buy vs. sell decisions.

The outcome of this analysis can also be used beneficially by companies as well. If each company knows how much these reports and overall public sentiment affects stock price, then the company can not only be prepared for stock price changes but it can have a better idea of how much of its resources to devote towards PR. For example, if a company is able to notice a large positive change in stock price anytime a positive Deutsche report is published, then it may want to spend more money to influence those reports or to generate similar reports within other outlets. 

Lastly, if there is a statistical significance of this analysis, investment software tools could use it as part of their overall algorithm to make recommendations to its users. These tools could advertise that they aggregate research sentiment and use this as a selling point to new potential users. If it is found that stock buy vs. sell decisions are best to make on Monday mornings, then this could influence the importance of being one of the first traders to get a transaction processed right as the market opens. Companies/tools that have an advantage in making the first transactions each morning would then be even more valuable for traders, especially short term ones.

Sentiment Analysis

Our sentiment analysis involves the use of unsupervised learning methods, both lexicon-based and domain-specific dictionaries  to categorise our data. 
The covered data includes:
Apple Financial Statements: We downloaded 10K and 10Q from the Apple investor relations website for the periods covering 2017-2018. These are preprocessed to remove exhibits, financial statements and risk disclosures. They are imported as word documents.
Deutsche Bank Weekly Research Reports: These are analyst reports obtained from ThomsonOne written by Sherri Scribner, a Deutsche Bank analyst who produces running commentary on weekly news articles that might affect the market for Apple stock. The reports available covered the time period from August 2017 to September 2018. These analyst reports are preprocessed to remove  tables, graphs and risk disclosures which would distort the analysis. They were imported as word documents.

Methodology - Sentiment Analysis

Our methodology involves three approaches:
VADER lexicon: VADER (Valence Aware Dictionary and sEntiment Reasoner) is a lexicon and rule-based sentiment analysis tool that is specifically attuned to sentiments expressed in social media but works for other domains.
McDonald Dictionary: Leveraging the work of Prof. Bill McDonald, we import his finance domain-specific dictionary by the name Loughran-McDonald Sentiment Word Lists. It contains a repository of positive words and negative words from a financial context. (https://sraf.nd.edu/)
Bing Liu Dictionary: Leveraging the Hu and Liu, KDD-2004 paper on opinion analysis, we import their 6800 repository of positive and negative opinion words without a specific domain..(https://www.cs.uic.edu/~liub/FBS/sentiment-analysis.html)

We use these three approaches to see if the lexicon model will outperform dictionary models and if domain specific dictionaries outperform general dictionaries.

We began by creating consistency across the date columns for our three data sets: Apple Financial Statements, Deutsche Bank reports and Apple (AAPL) stock data. The date column for all three are formatted for consistency. The text data for the financial reports and analyst reports is normalized; stemming and lemmatization. They are then processed for lower case, punctuation, special characters, contractions, stop words  and splitting of words.

For the VADER lexicon, we parse the each financial statement and report through the model and record the compound, positive and negative scores. Our sentiment score here will be represented by the positive score because all the compound scores are close to 1.0.

For the dictionary models, we parse each word into both the positive words  dictionary and negative words dictionary and calculate a count of each. Our sentiment will be represented by the proportion of positive words to the total of positive words and negative words.
We then create a graph to compare the three sentiment scores through time. We created graphs to compare sentiment scores to the AAPL stock price for all three models across time. Lastly, we created graphs to compare sentiment scores to the AAPL traded volume for all three models.

Advantages:
Relatively simple analysis making model interpretation and inference easy.
We assume that there aren’t other extemporaneous reasons that would move the stock price outside of company specific news.
Efficient market hypothesis assumes that public information is already reflected in the stock price and therefore our reports present news that are not public information(at least for the financial statements)
Given the voluminous nature of analyst reports around blue-chip stocks, it might be an efficient way of reviewing numerous reports.

Disadvantages:
We are limited to unigrams as we don’t have a dictionary for bigrams or comparative phrases across all the models.
Sentiment Analysis in finance is still premature and the requisite tools are still being developed.
Our volume analysis does not segment according to purchases and sales making it difficult to ascertain the direction of volume on any sentiment score spike.
We are dependant on the lexicons and dictionaries to be accurate in their depiction of what qualifies as domain-specific words and the sentiment or context.

Methodology - Topic Modeling

We mined the text to find topics that were correlated with weekend changes in stock prices. To do this, the DeutscheBank analyst statements and the Apple financial statements were normalized and converted into two 10,000 feature bag of words datasets. Latent Dirichlet Allocation was used to identify topics on each of these datasets. The DeutscheBank model was fit using 3 topics and 1000 iterations. The Apple model was fit using just 2 topics and 1000 iterations.

In order to find meaningful divisions in topics, several words needed to be removed from each dataset. When initially testing topic numbers, these words appeared prevalently in all topics, making it hard to distinguish any difference between the topics regardless of how many topics were modeled. The words that were removed from the DeutscheBank data include apple, iphone, share, sale, and market. From the Apple financial statements, the words company, month, december, april, and condensed were removed. Removing these words helped us view differences in topics.

The number of topics was chosen through trial and error. For the Deutsche model, the coherence score was estimated for an LDA model with 1 to 5 topics. The best score was achieved with 4 topics, however, we ended up using 3 topics in the final model. The reason for this is that the 4th topic used almost all the same words as on of the other topics, so it felt redundant. Using 3 topics seemed to yield the most useful separation of words. A similar process happened with the Apple financial statements. Once again, a model with 4 topics had the best coherence score but when viewed the topics seemed redundant. Additionally, when looking at topic dominance for each financial statement a third and fourth topic were almost never represented in any document. For this reason, 2 was chosen to be the number of topics to best represent the Apple financial statement data.

Finally, after building the two models, the topic results were compared to weekend price changes. This was accomplished through linear regression with price change as the dependent variable and the document’s association with each topic as the independent variables. A separate regression was run for each of the datasets. Since each document was released on a Friday, it could be matched to the change in prices from that day to the following Monday.

Results - Topic Modeling

DeutscheBank Analyst Statements
The DeutscheBank data was modeled using 3 topics. The first topic included words like ‘homage’, ‘iconic’, ‘enhancement’ and ‘buzz’. The second topic included ‘home’, ‘google’, ‘amazon’. The third topic included ‘new’, ‘smartphone’, and ‘growth’. From these words, it seems like the first topic is related to product design and how new products are marketed and received. The second topic seems clearly to be about competitors. The third is trickier to understand but seems to be related to the health of the company going forward. Below, you can see the top 10 words of each topic.

          word_0	 word_1	word_2	word_3	word_4	word_5	word_6	word_7	word_8	word_9
          
## Table
Topic_0	 homage	ionic	authenticate	enhancement	curve	touchid	buzz	surprise	replaces	macos
Topic_1	 home	device	google	amazon	smart	vpa	company	assistant	user	year
Topic_2	 com	new	include	smartphone	growth	www	accord	company	news	risk




These 3 topics had different levels of relevance to each document. Topic 2 was the dominant topic in most of the documents, followed by Topic 1. Topic 0 never dominated but had a small association with each of the documents. The regression results indicate that topic association is not highly related to weekend price changes. While all of the topics had positive coefficients, none of these coefficients were statistically different than 0. 

Apple Financial Statements
The Apple financial statements were modeled using 2 topics. It was hard to find a number of topics that resulted in very different groupings of words. Since only 2 topics yielded associations that were meaningful, we decided to use 2 topics. However, trying to figure out the difference between the 2 topics proved somewhat useless. Both topics mainly used words like ‘product’, ‘net’, ‘sale’, ‘tax’, and other words related to financial accounting. Further along in the word importance, some small differences did appear. Topic 0 included the word ‘billion’ and ‘end’. Topic 1 included the word ‘apple’, ‘service’ and ‘september’. These differences hardly make it any easier to discern the real meaning behind the two topics. The top 10 words of each topic are shown in the table below.



        word_0	word_1	word_2	word_3	word_4	word_5	word_6	word_7	word_8	word_9       
 ## Table       
Topic_0	product	net	sale	may	tax	financial	end	include	could	billion
Topic_1	product	sale	net	tax	financial	include	apple	service	september	may


Topic 0 was the dominant topic in all but 2 of the 8 documents in this case. When matching these documents to the change in weekend price, it turns out there were only 3 that matched with any non-zero change. With such a small sample, regression is unlikely to tell us anything about the relationship between these documents and stock price. However, the changes that did exist were small and the sign of the change did not depend on topic dominance. Those changes are shown in the table below.

## Table
doc_title	    Topic_0	Topic_1	dominant_topic	date	Price Change
02022018.docx	0.9201	0.0799	0	              2/2/2018	-0.87%
06022018.docx	0.9535	0.0465	0	              6/2/2018	0.73%
11032017.docx	0.1886	0.8114	1	              11/3/2017	-0.08%



Results - Sentiment Analysis:

Exhibit 2 and Exhibit 3 shows the scaled comparison between the three sentiment scores. Bing Liu sentiment and McDonald sentiment are closely correlated though Bing Liu has larger distortions. Correlation is lower between the dictionary models and the VADER lexicon.

Exhibit 4, 8 and 12 comparing the sentiment models of the Deutsche Bank Reports to the AAPL price show the stock reacts overwhelmingly on positive sentiment and has a muted response to a decrease in positive sentiment.

Exhibit 5,9 and 13 comparing the sentiment scores of the Deutsche Bank Reports to the AAPL volume, show the expected increase in volume for a spike in positive sentiment. The correlation looks positive though more research is required to discern what the ratios are between purchases and sales.

The Deutsche Bank reports appear to add better color to the price and volume movement of the stock than the periodic financial statements. This is expected due to the higher number of data points available from the Deutsche Bank reports.

Overall, we can see the market impact of positive sentiment on the traded volume of Apple stock however, more research is needed to filter out the impact of positive sentiment on the price of the stock.




Sentiment Analysis Recommendations:
Our analysis shows that AAPL stock price relatively overreacts to positive news and under reacts to negative news. There needs to be a plausible explanation to this effect.
Our analysis would be better served if we had volume segmented into purchases versus sales volume so that we can cross compare to positive news versus negative news. Currently, we see a spike in volume for every spike in positive sentiment but cannot ascertain if they are purchases or take-profit sales.
The only way to compare across models would be to test their predictive power, however we are not sure what approach to take.

Sentiment Analysis Shortcomings:
Apple Financial statements might contain bias from the author, given that they are prepared by Apple.
Deutsche Bank research report might contain bias as Deutsche bank routinely does business on behalf of Apple.
A better comparison would be to news articles generated from financial journals of record like the Wall Street Journal or Bloomberg.
VADER compound score for all reports is close to 1.0, indicating possible errors.

Conclusion

Topic modeling did not reveal any relevant correlations between the analyzed texts and weekend stock price changes. Furthermore, topics in these texts were very difficult to discover. It is possible that these texts do not lend themselves to topic analysis due to their highly specialized purpose. It is likely that the humans creating these documents did not intend to cover multiple topics, and searching for more than one via algorithm is meaningless. We believe this is especially the case with the Apple financial statements, which basically cover the same topics with updated information in each release. One weakness of our analysis is that linear regression is a limited way to find relationships in any dataset. It is possible that the topics discovered here may be useful predictors in a more advanced machine learning model, but that is outside of the scope of this paper. For now, we have found little evidence that topic modeling of DeutscheBank analyst reports and Apple financial statements are predictive of very short term stock performance.

## Exhibit 1
 Exhibit 1: Apple Stock Price and Volume
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevVolume.png">
## Exhibit 2
Exhibit 2: Comparison between VADER, McDonald and Bing Liu Sentiment Scores for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/VADERvsMcDonaldvsBingLiuDeutscheReports.png">
## Exhibit 3
Exhibit 3: Comparison between VADER, McDonald and Bing Liu Sentiment Scores for Apple Financial  Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/VADERvsMcDonaldvsBingLiuAppleFinancialReports.png">
## Exhibit 4
Exhibit 4: Comparison between AAPL Price and McDonald sentiment score for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsMcDonaldDeutscheReports.png">
## Exhibit 5
Exhibit 5: Comparison between AAPL Volume and McDonald sentiment score for Deutsche Bank 
Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsMcDonaldDeutscheReports.png">
## Exhibit 6
Exhibit 6: Comparison between AAPL Price and McDonald sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsMcDonaldAppleFinancialReports.png.png">	
## Exhibit 7
Exhibit 7: Comparison between AAPL Volume and McDonald sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsMcDonaldAppleFinancialReports.png">
## Exhibit 8
Exhibit 8: Comparison between AAPL Price and Bing Liu  sentiment score for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsBingDeutscheReports.png.png">
## Exhibit 9
Exhibit 9: Comparison between AAPL Volume and Bing Liu  sentiment score for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsBingDeutscheReports.png">
## Exhibit 10
Exhibit 10: Comparison between AAPL Price and Bing Liu  sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsBingAppleFinancialReports.png">
## Exhibit 11
Exhibit 11: Comparison between AAPL Volume and Bing Liu  sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsBingAppleFinancialReports.png">
## Exhibit 12
Exhibit 12: Comparison between AAPL Price and VADER sentiment score for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsVADERDeutscheReports.png">
## Exhibit 13
Exhibit 13: Comparison between AAPL Volume and VADER sentiment score for Deutsche Bank Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsVADERDeutscheReports.png">
## Exhibit 14
Exhibit 14: Comparison between AAPL Price and VADER sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLVolumevsVADERAppleFinancialReports.png">
## Exhibit 15
Exhibit 15: Comparison between AAPL Volume and VADER sentiment score for Apple Financial Reports
<img width="800" src="https://github.com/Twabeeric/Apple-Stock-Text-Mining/blob/master/AAPLPricevsVADERAppleFinancialReports.png">








