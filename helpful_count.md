<a href="https://IsaacZacher.github.io/Portfolio/">Home</a>

# Fun Codes 
---


## Transcipt Counter
Used to count how many times the word 'help' was said in a demo I made 

---

```python
count_helpful = 0      # Varibles that I will use to count
count_help = 0
count_helped =0

text = open("Isaac_transcrip.txt")
#print(text)
for line in text:             # definite loop to go through all lines to find desierd words
    line = line.lower()       # will help count if starts sentence
    #print(line)
    line = line.rstrip()      # removes whitespce
    words = line.split()      # splits words into list
    count_helpful = count_helpful + words.count("helpful")
    count_help = count_help + words.count('help')
    count_helped = count_helped + words.count("helped")

total = count_help + count_helped + count_helpful

print('You said Helpful ' + str(count_helpful) + " times. ")
print('You said Help ' + str(count_help) + " times. ")
print('You said Helped ' + str(count_helped) + " times. ")
print()
print('In total you used the base word "Help"', str(total), "times in your demo_1 video.")

```

    You said Helpful 6 times. 
    You said Help 1 times. 
    You said Helped 3 times. 
    
    In total you used the base word "Help" 10 times in your demo_1 video.



```python

```
