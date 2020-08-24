<a href="https://IsaacZacher.github.io/Portfolio/">Home</a>

# Stats Examples 

### Here are some examples of stats that I have coded 
 
---

## Paired t-Test 

Example 1
```python
from scipy.stats import ttest_rel
ttestpair_Simon = ttest_rel(simon_congru, simon_in_congru, nan_policy='omit')
print(ttestpair_Simon)

```
Example 2 - *developed with Arlene jiang
```python
# Initialize time window names
time_windows = ['N400','P600']

# Format output
report = "Time: {time}, Contrast: {contrast}; t({df})={t_val:.3f}, p={p:.3f}" 
print("\nTargeted Statistical Test Results:")
print('==================================')

# Loop through time windows
for time in time_windows:

    # Loop through contrasts
    for con in contrasts.keys():
        #cond_1,cond_2 = contrasts[contrast]  #makes tuples from the dict to be used in selfecting the df for array to go into t-test

        # Slice DataFrame for relevant time and conditions
        A = test_1[(test_1['t_window'] == time) & (test_1['condition'] == contrasts[con][0])]['value']
        B = test_1[(test_1['t_window'] == time) & (test_1['condition'] == contrasts[con][1])]['value']

        # Conduct pairwise t-test
        test, p = stats.ttest_rel(A, B)

        # Display results
        format_dict = dict(time=time, contrast=con,  df=199, t_val=test, p=p)
    
        print(report.format(**format_dict))
    print()
```

    
    Targeted Statistical Test Results:
    ==================================
    Time: N400, Contrast: WPtn-Ctrl; t(199)=-64.117, p=0.000
    Time: N400, Contrast: RplusS-Ctrl; t(199)=-42.514, p=0.000
    Time: N400, Contrast: RnotS-Ctrl; t(199)=-52.587, p=0.000
    Time: N400, Contrast: RplusS-RnotS; t(199)=5.163, p=0.000
    
    Time: P600, Contrast: WPtn-Ctrl; t(199)=4.223, p=0.000
    Time: P600, Contrast: RplusS-Ctrl; t(199)=9.686, p=0.000
    Time: P600, Contrast: RnotS-Ctrl; t(199)=7.214, p=0.000
    Time: P600, Contrast: RplusS-RnotS; t(199)=3.005, p=0.003
    

## Two Way ANOVA


```python
import statsmodels as sm
formula = 'rt ~ simon + flankers + simon:flankers'
model = sm.formula.ols(formula, data= data).fit()

aov_table = sm.stats.anova_lm(model, typ=2)
```
