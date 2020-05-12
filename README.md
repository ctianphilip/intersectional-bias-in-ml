# intersectional-bias-in-ml


**Intersectional Bias in Hate Speech and Abusive Language Datasets**

- Slides: https://slides.com/jaeyeonkim/intersectional-bias-in-hate-speech-and-abusive-language-datasets/fullscreen

## Motivation

Algorithms are widely applied to detect hate speech and abusive language in popular social media platforms such as YouTube, Facebook, Instagram, and Twitter. Using algorithms helps identify, at scale, which posts contain socially undesirable content. This computational method is efficient but not perfect. Most algorithms are trained with labeled data. What if the training data, used to detect bias in social media, were itself *biased*?


## Research design

For transparency and reproducibility, we only used publicly available datasets. [The annotated Twitter dataset (N = 99,996)](https://www.dropbox.com/sh/4mapojr85a6sc76/AABYMkjLVG-HhueAgd0qM9kwa?dl=0) on hate speech and abusive language was created by a crowd-sourcing platform and its quality has been ensured by several rounds of validations. (The dataset is also part of the public data shared for [the first International Conference on Web and Social Media data challenge](https://sites.google.com/view/icwsm2020datachallenge). In the data wrangling process, we discovered that 8,045 tweets were duplicates and removed them. Consequently, the size of the final dataset was reduced to 91,951 tweets.) Founta et al. (2018), who generated the aforementioned dataset, defined abusive language as “any strongly impolite, rude, or hurtful language using profanity” and hate speech as “language used to express hatred towards a targeted individual or group” (5). We followed their definitions.

The Twitter dataset does not contain any information on the racial, gender, or partisan identities of the authors of these tweets. We utilized additional public datasets to classify and fill in the missing information. Our primary interest was the interaction between race and gender and whether that generated a biased distribution of hateful and abusive labels. Such an underlying data distribution would generate uneven false positive and negative rates for different groups. However, human annotators could be biased not only in terms of race and gender but also in terms of political affiliation. This is likely true if annotators were recruited in the United States, where political polarization is extreme. For this reason, we also classified party identification, the degree to which a person identifies with a particular political party. To be clear, what we classified were not the actual racial, gender, or partisan identities of the authors of these tweets. The objective was to classify whether the language features expressed in a tweet were closer to the ones commonly expressed by one racial/gender/partisan group than those of other groups.

- Race classification [[Jupyter Notebook](https://github.com/jaeyk/intersectional-bias-in-ml/blob/master/code/race_classification/code/race_classification_Santiago_Ortiz_Kim_reviewed.ipynb)]
- Gender classification [[Jupyter Notebook](https://github.com/jaeyk/intersectional-bias-in-ml/blob/master/code/gender_classification_Nam_Kim_reviewed.ipynb)]
- Party identification Classification [[Jupyter Notebook](https://github.com/jaeyk/intersectional-bias-in-ml/blob/master/code/party_ID_classification_Datta_Kim_reviewed.ipynb)]

The data analysis was correlational and thus, descriptive. We first described the bivariate relationship between race and gender and then added uncertainty about the measures using bootstrapping. We further investigated how the interaction between race and gender influences the distribution of hateful and abusive labels using logistic regression models. By taking a statistical modeling approach, we estimated the partial effect of the interaction bias on the outcomes while controlling for partisan bias.

## Hypotheses

**Racial bias**: The first hypothesis is about between-group differences. Consistent with the prior research, we expect that tweets more closely associated with African American than White English language features would be more likely to be labeled as abusive and hateful.

**Intersectional bias**: The second hypothesis is about within-group differences. Influenced by broad social science literature, we argue that tweets more closely associated with African American males than other groups' language features are more likely to be labeled as hateful.

## Results [[R Markdown](https://github.com/jaeyk/intersectional-bias-in-ml/blob/master/code/modeling_visualization_Kim.Rmd)]


## Conclusion

- This study provides the first systematic evidence on intersectional bias in datasets of hate speech and abusive language. More importantly, the finding that African American men are closely associated with hate speech is consistent with broad social science research on the criminalization of African American men.
- Many caveats exist.
  - The statistical model could be incomplete. The multivariate regression model is naive and likely to be underspecified. Missing variables in the model may cause selection bias. A better approach would be to design an experiment in which researchers could manipulate the source of biases---different types of language features---and directly examine their causal effects.
  - The data could be inaccurate. This problem is particularly concerning because the magnitude of the intersectional bias is small. All of the key predictor variables were not directly observed but were based on machine-enabled text classification. Uncertainty in the data may not destabilize inference if the effect size is large enough; an increase of up to 3.7 times due to racial bias is difficult to remove. By contrast, an increase of up to 77% due to intersectional bias could be sensitive to measurement error.
- The findings reported here should not be taken at their face value and should be followed up with further investigation.
