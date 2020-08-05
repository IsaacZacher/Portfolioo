## Violin Plots 


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


```python

```
