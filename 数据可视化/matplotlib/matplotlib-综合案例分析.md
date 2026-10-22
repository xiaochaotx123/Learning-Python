### 分析案例：温度分析  

### 导入库
```python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import rcParams
rcParams["font.family"] = "SimHei"
plt.rcParams['axes.unicode_minus'] = False
```

### 导入数据
```python
df = pd.read_csv("Pandas_Study_Data/weather.csv")
df["date"] = pd.to_datetime(df["date"])
```

### 绘制一个气温（最高气温，最低气温，平均气温）的趋势变化图
```python
plt.figure(figsize = (15, 10))
plt.plot(df["date"], df["temp_max"],
         label = "最高气温")
plt.plot(df["date"], df["temp_min"],
         label = "最低气温")

df["temp_mean"] = (df["temp_max"] + df["temp_min"]) / 2
plt.plot(df["date"], df["temp_mean"],
         label = "平均气温")


plt.title("随机天气情况趋势变化图")
plt.xlabel("日期", fontsize = 14)
plt.ylabel("气温", fontsize = 14)
plt.ylim(-10, 20)
plt.legend(loc = "upper left")
plt.xticks(rotation = 30)
plt.grid(True, axis = "y", color = "blue", alpha = 0.3)

plt.show()
```

<img width="1250" height="894" alt="图片" src="https://github.com/user-attachments/assets/b4dd605d-fadf-4a6a-871d-1badbfd55d12" />




### 绘制一个降水量直方图 plt.hist()  
plt.hist() 是 Matplotlib 中用来绘制直方图（Histogram）的函数。它的核心作用是展示一组数据的分布情况（即数据集中在哪些范围，哪些范围的数据很少）。
- X 轴（横轴）：数据的“区间范围”。函数会自动找到这列数据的最小值和最大值，然后根据你设置的 bins=10，把这整个范围等分成 10 个区间（10 个“桶”）。
- Y 轴（纵轴）：数据的“频数（数量）”。柱子越高，说明落在这个区间里的数据（天数）越多。
 
```python
plt.hist(df["precipitation"], bins = 10)
```

<img width="553" height="413" alt="图片" src="https://github.com/user-attachments/assets/d543c356-85a3-4b86-a9bb-4e1d0d1a98db" />
