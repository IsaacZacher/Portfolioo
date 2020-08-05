# Stats Examples 

### Here are some examples of stats that I have coded 
 
---

## Paired t-Test 


```python
from scipy.stats import ttest_rel
ttestpair_Simon = ttest_rel(simon_congru, simon_in_congru, nan_policy='omit')
print(ttestpair_Simon)

```

## Two Way ANOVA


```python
import statsmodels as sm
formula = 'rt ~ simon + flankers + simon:flankers'
model = sm.formula.ols(formula, data= data).fit()

aov_table = sm.stats.anova_lm(model, typ=2)
```
