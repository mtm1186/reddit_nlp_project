# Classifying Investing Advice: A Look Into The World of A Bogle Head

##### Matthew Malone https://git.generalassemb.ly/mtm1186

## Problem Statement
Investing for the people is a non profit organization started by a former employee of John Bogle, the founder of Vanguard. John Bogle had a simple investing style recommending people buy mutual funds or ETFs that try to mimic the entire stock market. When buying these funds, they pay special attention to fees, and only invest in funds with low fees and expenses. Taxes are also a huge consideration. To maximize tax efficiency, investment vehicles like 401ks and IRAs are the preferred mediums.

Investing for the people is looking to spread John Bogles investing advice to more people especially those who are new to investing. The executives at Investing for the people have asked their data science time to build a model that uses natuarl language processing to identify websites and message boards that share John Bogle's investing advice. Once a message or website has been identified as including the core principles of Bogle investing, Investing for the people will add it to it's approved list of financial websites.

The team has been asked to test their model on Reddit where there is no dearth of investing advice. The executives want to see the model perform well before funding the roll out of the program. They want to see the model can differentiate between traditional investing advice, which can be found on r/Investing and the advice of John Bogle which can be found on r/Bogleheads. An accuracy rate of 85% has been set as the goal for the target for the team to meet.


## Executive Summary
Initially the team assumed it would be easy to distinguish between the two as in general r/Bogleheads focuses more on index funds or exchange traded funds (ETFs). These types of funds are essentially a basket of individual stocks that are selected to match or track the components of financial market index. Subscribers of r/Bogleheads usually reference the stock ticket symbols associated with these funds (VTI, VOO, VTSAX). We observed these symbols when looking at top occurences of words during the EDA process. Retirement Accounts such as IRA, Roth IRA and 401k also jumped out when looking at r/Bogleheads. With both of fund categories and retiremnt categories being distinguishing features of r/Bogleheads we were confident we cold acheive the target accuarcy rate of 85%.

Three models were selected for production, they included a Logistic Regression Classification model and two Naive Bayes Models (Multinomial & Gaussian). The thought process here was to a have at least one model for interpreation and one for prediction. We also wanted to compare two Naive Bayes models to see which one performed better. We would include the transformers CountVectorizer and TfidfVectorizer on each of the models to generate more results as we wanted to see which combinations would work best. Including pipelines allowed us to apply a number of transformers and a final estimator. We then used GridSearchCV to test a number of different values and combinations of hyper-parameters. This would help us identify the best possible score of our models.

Since the data we pulled from reddit using reddit's API we created a baseline model that was essentially 50%. We were confident our models would outperform this baseline score. Initially scoring results were in the 80%-85% and continued to climb as we adjusted the parameters of the model. However, we weren't hitting the desired goal of 85% accuracy as we were observing too many incorrect predictions. We attributed this to many of the same words and investing terms in both subreddits. There was a lot of overlap and if posts were short and only included one or two features that had a high coefficient from the other subreddit it would result in a misclassification.

Our approach was to create simple models and increase the complexity as we went while tuning the parameters. This resulted in us observing an inscrease in model performance. However, we also started to observe higher variance in our models which caused us to scale back on complexity to find an ideal bias variance tradeoff.


## Data Collection
The data was collected from r/Bogleheads and r/Investing using the Reddit API. Because r/Ivesting is a considerably larger subreddit with over a million subscribers we only needed to pull data on two months of data to acheive our desired result of 1000 posts. r/Bogleheads is a much smaller and less popular subreddit and we had to pull data from a greater scope date. 

# Modeling
Model preparation included creating a baseline model in order to have an initial result from our data set to compare the other models we will be using. Before modeling we perfomed a train/test split on our dataset. We will be create a pipeline using either CountVectorizer or TfidfVectorizer as a transformer. The models that will be used include Logistic Regression, Gaussian Naive Bayes, and Multinomial Naive Bayes. A gridsearch will be performed on each model in attempt to identify the best parameters. Models will be assessed on their accuracy score on testing data. 

# Model Evaluation
The Models will be evaluated based on their accurarcy scores. We want to determine what model is making the most accurate predictions. 

# Conclusion
Unfortunately we did not achieve the goal of 85% accuracy for our model. In hindsight it was naive to think r/Bogleheads offered investing advice that was that much different than r/Investing. Investing can be complicated and there are many differnent terms and investment products that could differentiate investing styles but for the most part investors are going to simliar asset classes (stocks, bonds, commodities) to invest their money. Many investment products (VTI, VTSAX) are extremely popular for the average investor and not just bought by a niche group of investors who follow specific investing advice. In preprocessing we took the necessary steps to remove frequently occuring words by identifying these words and adding them to the standard stop words list. This was in attempt to to reduce their affect on the model. However, when looking at the model performance we did not observe consistency in the model using this as the ideal parameter. Sometimes the model used the stopword list other times it did not. This did not seem to have as big of an impact we had originally thought. The best performing model was the Logistic Regression Model + TfidfVectorizer which achieved an accuracy score of 85%. This model was observed to be low variance as it had less than a 2% difference between the training score and testing score. However, this score was close but not good enough and we will have to review our workflow from the beginning to see if any improvements can be made that will achieve a better result. 

# Recommendations 
The reduced scope date when pulling data from r/Investing most likely helped in our performance. This is due to a higher occurence of words on short term market activity. Coronavirus appered high in the coefficients for r/investing because this has been an ongoing topic and it is greatly affecting the stock market. If we had equal scope dates we most likely we observe a decrease in the occurence of this word dating back to last year. Do work toward a better performing model we should take scope date of data into consideration. We did not need to attempt to have balanced classes as this is not how data exists in the real world. Create more models, a limited approach was taking this time and we were unable to compare the models we used to other models such as KNN, Random Forest, or Decision Tree. This limited our results and we may have had a better performing model if we used something else. 

# References 
Investopdiea, James Chenn, Jan,2016 https://www.investopedia.com/terms/j/john_bogle.asp


..