## Violin Plots 
---

```python
# Violin plot of flankers and Simon conditions
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')

fig2 = sns.violinplot(x='flankers', y='rt',  hue='simon',order=["congruent", "incongruent"], data=data,split=True, scale="count", inner="quartile")

fig2.set_title('Flanker and Simon Condition Interactions (Figure 2)', fontsize=18)
fig2.set_xlabel('Flankers', fontsize=15)
fig2.set_ylabel('RT(ms)', fontsize=15)
fig2.set_xticklabels(['Congruent', 'Incongruent'], fontsize=12)
h, l = fig2.get_legend_handles_labels()
labels=['Congruent', 'Incongruent']
fig2.legend(h, labels, title='Simon')

plt.savefig("Violin_plot.png")

```

![violin plot (figure 2)](Violin_plot.png)
## Box Plots 
---



```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_style('whitegrid')

fig1 = sns.boxplot(x='flankers', y='rt', hue='simon', order=["congruent", "incongruent"], data=data)

fig1.set_title('Flanker and Simon Condition Interactions (Figure 1)', fontsize=18)
fig1.set_xlabel('Flankers', fontsize=15)
fig1.set_ylabel('RT(ms)', fontsize=15)
fig1.set_xticklabels(['Congruent', 'Incongruent'], fontsize=12)
plt.legend(title='Simon', labels=['Congruent', 'Incongruent'])
h, l = fig1.get_legend_handles_labels()
labels=['Congruent', 'Incongruent']
fig1.legend(h, labels, title='Simon')

plt.savefig("Boxplot.png")
```
![boxplots (Figure 1)](Boxplot.png)
