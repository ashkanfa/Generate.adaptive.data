# Generate adaptive treatment regime artificial data
Inspired by  [dynamic treatment regime (DTR)](https://en.wikipedia.org/wiki/Dynamic_treatment_regime) or adaptive treatment strategy, the linear association (causal relationship) in the artificial data at each time slot are created, as shown by causal diagram in the following figure.

![alt text](https://github.com/ashkanfa/Generate.adaptive.data/blob/master/Causal_relation.PNG)
 
 Here, the first goal of modeling is to capture the closest to true causal features. Lets explain the sequential logic of generating the artificial data.
 1. Let 𝑋𝑂 denote covariates associated with outcome, 𝑋𝑂𝑇 predictors of both treatment and outcome as confounders, 𝑋𝑇 the predictors of exposure (treatment), and finally 𝑋𝑆 nuisance or spurious covariates. All the covariates are correlated with a designated correlation matrix and generated by a modified version of the [BinNor package in R](https://cran.r-project.org/web/packages/BinNor/index.html). If we divide covariate (treatment) space into true(causal) predictors(treatment) and spurious(non-causal) variable(treatments), then we can define a complex correlation structure as in the following figure where upper diagnoal is depicted:
 
![alt text](https://github.com/ashkanfa/Generate.adaptive.data/blob/master/Correlation%20structure.png)
 
 which controls not only the magnitude of the correlation within true predictors (causal treatments) but also controls the intensity      of the correlation between true predictors (causal treatments) and spurious variables(non-causal treatments). This gives the researcher to  monitor the strength of different methodology in differentiating "causation from correlation".
 
 2. Having covariates now, we can obtain the probability of each binary treatment by association with some controlled selection of 𝑋𝑂𝑇, 𝑋𝑇, the past treatments and the previous outcome by the following Eq:
 
 ![alt text](https://github.com/ashkanfa/Generate.adaptive.data/blob/master/eq1.PNG)
 
 Then by predefined correlation matrix as explained above and approximate multivariate normal, correlated binary treatments are created. The algorithm divides the data in two groups: effective and non-effective treatments.
 
 3. Finally, the outcome at the end of time slot 𝑡 is created by the following linear association with the effective treatment, 𝑋𝑂, 𝑋𝑂𝑇 and the previous outcome and some interaction terms. 
