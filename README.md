# hello-world
  import pandas as pd
  import matplotlib.pyplot as plt
  import numpy as np
  import pylab
  def cm_to_inch(value):
    return value/2.54
    df = pd.read_excel('Налоги компании VW.xlsx')

i = 0
a = list()
while (i < 14):
    if (type(df.iat[2,i]) is str):
        a.append(df.iat[2,i])
    else:
        a.append(int(df.iat[2,i]))
    i = i + 1
i = 6
a5 = list()
while (i < 13):
    if (type(df.iat[2,i]) is str):
        a5.append(df.iat[2,i])
    else:
        a5.append(int(df.iat[2,i]))
    i = i + 1
df.columns = a
df = df.drop(df.index[:3])
df = df.drop(df.index[-1:])
df = df.drop(index = [34])
df_copy1 = df.copy()
i = 6
x5 = list()
while (i < 13):
    x5.append(df_copy1.iat[31,i])
    i = i + 1
#print (df)
x = list()
i = 2
while (i < 13):
    x.append(df.iat[31,i])
    i = i + 1
del a[0:2]
del df['Налог']
del df['Регион']
del df['Итого']
del a[11]
df_copy = df.copy()
del df_copy[2013]
plt.figure(figsize=(cm_to_inch(25), cm_to_inch(15)))
plt.xticks(rotation=45)
plt.plot(a5,x5)
plt.title('Динамика налогов Volkswagen Group Rus (в млн. руб)')
del df_copy[2010]
del df_copy[2011]
del df_copy[2012]


del df['9 мес. 2020']
del a[8]
df1 = pd.concat([df[1:2], df[10:11], df[12:13], df[17:18], df[19:20], df[22:23], df[24:25], df[26:27]])
x1 = df1.sum() 
plt.figure(figsize=(cm_to_inch(25), cm_to_inch(15)))
plt.plot(a,x1,label = 'Калужская обл.')
del df[2010]
del a[0:1]
df2 = pd.concat([df[3:4], df[14:15]])
x2 = df2.sum()
plt.plot(a,x2, label = 'Нижегородская обл.')
df3 = pd.concat([df[2:3], df[13:14], df[18:19], df[20:21], df[23:24], df[27:28]])
x3 = df3.sum()
del df[2011]
del df[2012]
del a[0:2]
plt.xticks(rotation=45)
plt.plot(a,x3, label = 'Москва')
del df[2013]
del a[0:1]
df5 = pd.concat([df[5:6], df[16:17]])
x5 = df5.sum()
plt.plot(a,x5, label = 'Санкт-Петербург')
del df[2014]
a1 = a.copy()
del a[0:1]
df4 = pd.concat([df[4:5], df[15:16], df[21:22], df[25:26]]) 
x4 = df4.sum()
plt.plot(a,x4, label = 'Московская обл.')
plt.legend(fontsize = 9,   
           facecolor = 'oldlace',    #  цвет области
           edgecolor = 'r',    #  цвет крайней линии
           title = 'Регионы',    #  заголовок
           title_fontsize = '13',    #  размер шрифта заголовка
           loc = 'best'
         )
plt.title('Налоги по регионам по годам (в млн. руб)')
kaluga = x1.sum()
niznov = x2.sum()
moscow = x3.sum()
saint_petersburg = x5.sum()
mosobl = x4.sum()
print (kaluga, niznov, moscow, saint_petersburg, mosobl)


df_profit = df_copy.iloc[0:7]
df_vot = df_copy.iloc[7:10]
df_excise = df_copy.iloc[10:12]
df_individ = df_copy.iloc[12:17]
df_insurance = df_copy.iloc[17:19]
df_recycling = df_copy.iloc[28:30]
df_customs = df_copy.iloc[30:31]
df_others = df_copy.iloc[19:28]
df_profit = df_profit.append(df_profit.sum(), ignore_index=True)
pr = df_profit.loc[7].sum()
df_vot = df_vot.append(df_vot.sum(), ignore_index=True)
vot = df_vot.loc[3].sum()
df_excise = df_excise.append(df_excise.sum(), ignore_index=True)
excise = df_excise.loc[2].sum()
df_individ = df_individ.append(df_individ.sum(), ignore_index=True)
individ = df_individ.loc[5].sum()
df_insurance = df_insurance.append(df_insurance.sum(), ignore_index=True)
insurance = df_insurance.loc[2].sum()
df_others = df_others.append(df_others.sum(), ignore_index=True)
others = df_others.loc[9].sum() + pr + insurance + individ
df_recycling = df_recycling.append(df_recycling.sum(), ignore_index=True)
recycling = df_recycling.loc[2].sum()
df_customs = df_customs.append(df_customs.sum(), ignore_index=True)
customs = df_customs.loc[1].sum()
all_taxes = vot + customs + excise + recycling + others
print (vot, customs, recycling, excise, others)
all_taxes


plt.figure(figsize=(cm_to_inch(25), cm_to_inch(15)))
labels = ['НДС','Таможенные пошлины','Акцизы','Утилизационные сборы за а/м','Остальные налоги']
values = [vot,customs,excise,recycling,others]
total = sum(values)
labels = [f"{n} ({v/total:.1%})" for n,v in zip(labels, values)]
colors = ['green','tan','red','gray','black']
plt.pie(values,colors=colors)
plt.legend(labels, loc="upper left")
plt.axis('equal')
plt.title('Распределение доль налогов от общего количества (начиная с 2014г.)')
plt.show()
