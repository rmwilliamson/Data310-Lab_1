
# Question 2
#### Write a Python code to import the data file 'L1data.csv' (introduced in Lecture 1) and code an imputation for replacing the NaN values in the "Age" column with the median of the column. The NaN instances are replaced by



```markdown
import pandas as pd
import numpy as np
from google.colab import drive
drive.mount('/content/drive')
pwd()
cd drive
cd MyDrive
cd Colab Notebooks

data = pd.read_csv('L1Data.csv')

from sklearn.impute import SimpleImputer
imp = SimpleImputer(missing_values=np.nan,strategy='median')
imp.fit(data.loc[:,["Age"]])
data.loc[:,["Age"]] = imp.transform(data.loc[:,["Age"]])
```
#### Median = 21.0


# Question 5
#### Assume that during a pandemic 15% of the population gets infected with a respiratory virus while about 35% of the population has some general respiratory symptoms such as sneezing, stuffy nose etc. Assume that approximately 30% of the people infected with the virus are asymptomatic. What is the probability that someone who has the symptom actually has the disease?

```markdown
p = ((1-0.3) * 0.15)/0.35
```
#### probability = 0.3

# Question 8
#### Assume we play a slightly bit different version of the original Monte Hall problem such as having four doors one car and three goats. The rules of the game are the same, the contestant chooses one door (that remains closed) and one of the other doors who had a goat behind it is being opened. The contestant has to make a choice as to stick with the original choice or rather switch for one of the remaining closed doors. Write a Python code to approximate the winning probabilities, for each choice, by the means of Monte Carlo simulations. The probability that the contestant will ultimately win by sticking with the original choice is closer to

```markdown
%matplotlib inline
%config InlineBackend.figure_format = 'retina'
import matplotlib as mpl
mpl.rcParams['figure.dpi'] = 150

import random
import matplotlib.pyplot as plt

doors = ["goat","goat", "goat", "car"]

# approximated results
switch_win_probability = []
stick_win_probability = []

plt.axhline(y=0.66, color='red', linestyle='--')
plt.axhline(y=0.33, color='green', linestyle='--')

def monte_carlo(n):

  switch_wins = 0
  stick_wins = 0

  for i in range(n):
     random.shuffle(doors)

     k = random.randrange(4)

     if doors[k] != 'car':
       switch_wins +=1
    
     else:
       stick_wins +=1
    
     switch_win_probability.append(switch_wins/(i+1))
     stick_win_probability.append(stick_wins/(i+1))
    
  plt.plot(switch_win_probability,label='Switch')
  plt.plot(stick_win_probability,label='Stick')
  plt.tick_params(axis='x', colors='navy')
  plt.tick_params(axis='y', colors='navy')
  plt.xlabel('Iterations',fontsize=14,color='DeepSkyBlue')
  plt.ylabel('Probability of Winning',fontsize=14,color='green')
  plt.legend()
  print('Winning probability if you always switch:', switch_win_probability[-1])
  print('Winning probability if you always stick to your original choice:', stick_win_probability[-1])

monte_carlo(3000)
```
#### Winning probability if you always switch: 0.7403333333333333
#### Winning probability if you always stick to your original choice: 0.25966666666666666
