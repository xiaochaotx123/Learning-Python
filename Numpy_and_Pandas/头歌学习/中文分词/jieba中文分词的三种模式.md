```python
import jieba

text = input()

result_accurate = jieba.lcut(text)
print("【精确模式】", result_accurate)

result_full = jieba.lcut(text, cut_all=True)
print("【全模式】", result_full)

result_search = jieba.lcut_for_search(text)
print("【搜索引擎模式】", result_search)
```