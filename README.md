# trabalho.python.M2

#já estavam quando criei o notebook no Kaggle (até linha 21)

# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt 

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session





casas = pd.read_csv("/kaggle/input/housepriceprediction-cleaned-dataset/House-Price-Prediction-clean.csv")
#filtros de coluna
filtro = casas['YearBuilt'] % 2 == 0
filtro2 = casas['YearBuilt'] % 2 == 1

#Filtros de groupby
gbvenda = casas[filtro].groupby(by=['YearBuilt'])
contagempares = gbvenda['Id'].cont()
#gráfico número de casas construidas em anos pares ou impares
contagempares.plot()
plt.show()

gbvenda2 = casas[filtro2].groupby(by=['YearBuilt'])
contagemimpares = gbvenda2['Id'].cont()
contagempares.plot()
plt.show()

#fiiltro para casas vendidas a masid e 400000 por ano
mais400 = casas['SalePrice'] > 400000
vendascaras = casas[mais400].filter(['YrSold', 'SalePrice'])
print(vendascaras)
#save
vendascaras.to_csv("vendasmais400000.csv", index=False)
