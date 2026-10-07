创建一个包含10名学生数学成绩的Series，成绩范围在50-100之间。计算平均分、最高分、最低分，并找出高于平均成绩的学生人数。
```python
import pandas as pd
import numpy as np

# 生成随机成绩
np.random.seed(42)
scores_value = np.random.randint(50, 101, 10)
scores_index = ["学生" + str(i) for i in range(1, 11, 1)]
scores = pd.Series(scores_value, scores_index)

print(f"平均分：{round(scores.mean(), 3)}")
print(f"最高分：{round(scores.max(), 3)}")
print(f"最低分：{round(scores.min(), 3)}")
print(f"高于平均成绩的学生人数：{len(scores[scores > scores.mean()])}")
# 或者 scores[scores > scores.mean()].count()
```
