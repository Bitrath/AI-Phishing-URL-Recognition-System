# Phishing URL Recognition System
**Course**: AI for Cybersecurity - Project, Academic Year 2024/2025 

In today’s digital age, cybersecurity is more critical than ever. Among the various types of cyberattacks, phishing remains the most prevalent and effective. In fact, phishing is responsible for over 36% of all data breaches in 2025 alone, making it a top threat across industries. According to the latest TechMagic report, phishing attacks caused global damages exceeding $12.5 billion in 2024, marking a 25% year-over-year increase. And not only that, AI is enabling faster, more personalized data-stealing malware, spear phishing emails, and phishing sites. By 2027, AI is predicted to be involved in 17% of cyberattacks.

These attacks are not just increasing in frequency, they're becoming more sophisticated. Hoxhunt's 2025 phishing trends report has revealed that attackers are now leveraging AI to craft hyper-realistic messages and domains, drastically increasing click-through and deception rates. In fact, phishing emails are now intercepted every 42 seconds, and 66% of all phishing emails are specifically targeted at business users.

It becomes natural to ask ourselves, why does phishing matter more now than ever? And we can list some reasons:
* **Rapid evolution of phishing tactics**: Attackers now use AI to personalize messages, making them nearly indistinguishable from legitimate sources.
* **Business Email Compromise (BEC)**: Targeted attacks impersonating executives are increasingly common, with financial losses often exceeding millions of dollars.
* **Economic and reputational damage**: The average cost of a phishing-related breach in the U.S. reached $4.9 million in 2024 [source].
And last, but not least...
* **AI vs. AI**: As threat actors adopt AI tools, we must deploy intelligent countermeasures, in fact this project is designed as a proactive shield, not a reactive patch.
## Authors 
* Nicolò Zarulli @[Bitrath]()
* Nicola Cavaletti @[nicolacava01](https://github.com/nicolacava01)

## Goal
To address the steadily growing threat of phishing, we wanted to develop a **live phishing URL recognition system** using machine learning models for **URL classification**. We also had the goal to provide a solution that by design could be easily embedded within browsers, email clients, or enterprise-grade cybersecurity tools, and that could possibly be used to expand the dataset to obtain an extended and much more fine-grained classifier to tackle the increasing complexity and evolution of phishing tactics.

## Specifics
To achieve this goal, we used a dataset that was constructed based on a [research group paper](https://eprints.hud.ac.uk/id/eprint/24330/6/MohammadPhishing14July2015.pdf) published by University of Huddersfield, which highlights and explains the reasoning behind important features that can be extracted from URLs to be able to detect phishing behavior.

## Data Acquisition and Exploration
* **Dataset Overview**: The data was acquired in .ARFF format, consisting of 11,055 rows (instances) and 31 columns (features).
* **Categorical Values**: The data relies on three main categorical values: -1 for Phishing, 1 for Legitimate, and 0 for Suspicious characteristics.
* **Target Distribution**: The dataset contains roughly 5,000 phishing instances and 6,000 legitimate instances.
* **Preprocessing**: The data was split into an 80/20 ratio for training and testing. To prepare for cross-validation, a 10-fold Stratified K-Fold approach was established.
* **Feature Selection** : By utilizing a Cramér's V Heatmap to calculate categorical feature association, we identified a highly correlated feature pair (0.939) between Favicon and popUpWidnow. Consequently, the popUpWidnow feature was dropped to optimize the dataset.

## Model Processing and Evaluation
The project evaluated four different classifiers, split into two comparative groups:

### Decision Tree vs. Random Forest
* **Decision Tree Classifier**: Achieved a test accuracy of 0.96 and a cross-validated accuracy of 0.9631.
* **Random Forest Classifier**: Outperformed the Decision Tree with a test accuracy of 0.97 and a cross-validated accuracy of 0.9717. Random Forest was selected as the first candidate for the best classifier.

### Naïve Bayesian vs. Logistic Regression (with OneHot Encoding)
To evaluate these models, a OneHot Encoding pipeline was applied, increasing the number of attributes from 30 to 66 by binarizing the values.
* **Naïve Bayesian Classifier**: Achieved a test accuracy of 0.93 and a cross-validated accuracy of 0.9288.
* **Logistic Regression**: Outperformed Naïve Bayesian with a test accuracy of 0.94 and a cross-validated accuracy of 0.9400. Logistic Regression was selected as the second candidate.

## Best Classifier Validation
* To definitively choose the best model, a Paired T-Student test was conducted between Random Forest and Logistic Regression metrics.
* The T-test on F1 Scores yielded a t-statistic of 28.5339 and a p-value of 0.0000000072.
* Because the t-statistic is strictly greater than the near-zero p-value, there is a substantial statistical difference confirming that Random Forest is the superior model.

## Live URL Analyzer
We developed a live analyzer utilizing the trained Random Forest model.
* **Functionality**: It features a custom URL feature extractor that parses URLs in real-time, extracting data such as IP address usage, URL length, shortening services, @ symbol usage, and domain age.
* **Performance**: The analyzer is highly accurate, consistently distinguishing between complex phishing links and legitimate sites like https://www.google.com.

## Incremental Feature Cross-Validation (Bonus)
An experimental test was run to evaluate Random Forest performance by incrementally increasing the number of features utilized (two by two per fold).

* **Result**: Interestingly, the absolute highest performance was found at 22 features (Accuracy: 0.9756, F1-macro: 0.9752), marginally outperforming the full 30-feature set.

## Next Steps
* Improvement of the Dataset.
* Training and testing on other ML Classification Models.
* Direct implementation of the Analyzer in real-life apps and/or situations.
* Extend the detection scope from just URLs to full E-Mails
