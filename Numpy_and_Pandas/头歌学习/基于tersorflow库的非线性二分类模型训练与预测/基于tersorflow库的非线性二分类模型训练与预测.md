# 接收控制台输入：第一个值为第一层隐藏层神经元数量，第二个值为训练轮数
num, epochs = eval(input())

# ===================== 1. 数据读取与预处理 =====================
# 导入pandas库，取别名pd,用于读取csv数据和数据处理
import pandas as pd

# 读取当前目录下的 data.csv 数据文件
data = pd.read_csv("data.csv")

# 提取特征数据 X: 用loc[]选取 x1、x2 两列作为模型输入特征
X = data[['x1', 'x2']]

# 提取标签数据 y: 用loc[]选取 y 列作为模型输出标签
Y = data['y']

# ===================== 2. 数据集划分 =====================
# 导入sklearn.model_selection库中数据集划分工具 train_test_split
from sklearn.model_selection import train_test_split

# 将数据划分为训练集和测试集
X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size=0.33, random_state=10)

# ===================== 3. 构建神经网络模型 =====================
# 导入tensorFlow深度学习框架
import tensorflow

# 导入序贯模型（Sequential），用于逐层搭建神经网络
from tensorflow.keras.models import Sequential

# 导入全连接层 Dense 和输入层 Input (注意：需从 layers 中导入)
from tensorflow.keras.layers import Dense, Input

# 构建多层感知机（MLP）模型
mlp = Sequential([
    Input(shape = (2,)),
    Dense(num, activation='relu'),          # 第一层隐藏层：神经元数量由输入变量 num 决定，激活函数 relu
    Dense(32, activation='relu'),           # 第二层隐藏层：32 个神经元，激活函数 relu
    Dense(1, activation='sigmoid')          # 输出层：1 个神经元，sigmoid 激活函数输出 0~1 概率（二分类任务）
])

# ===================== 4. 模型编译 =====================
# 编译模型：配置优化器、损失函数、评估指标。
mlp.compile(
    optimizer='adam',                       # 优化器：使用 adam 自适应优化算法
    loss='binary_crossentropy',             # 损失函数：二分类交叉熵
    metrics=["accuracy"]                    # 训练过程中评估指标：准确率
)

# ===================== 5. 模型训练 =====================
# 使用训练集训练模型
mlp.fit(
    X_train, y_train,                       # 传入训练特征和标签
    epochs=epochs,                          # 训练轮数由输入变量决定
    batch_size=8,                           # 每批次使用 8 个样本更新权重
    verbose=2                               # 训练时输出简洁日志 (注意拼写是 verbose)
)

# ===================== 6. 模型预测与评估 =====================
# 导入准确率计算工具
from sklearn.metrics import accuracy_score

# 模型对测试集进行预测，输出预测概率 (0~1之间的小数)
y_test_predict_prob = mlp.predict(X_test)

# 将预测概率转为 0/1 类别：概率大于 0.5 判为 1，否则为 0，并展平为一维数组 (注意是 0.5 不是 0,5)
y_test_predict = (y_test_predict_prob > 0.5).astype(int).flatten()

# 计算测试集准确率
accuracy_test = accuracy_score(y_test, y_test_predict)

# ===================== 7. 保存准确率，不要修改以下代码 =====================
# 打开 output.txt 文件（若无则自动创建），以写入模式保存
f = open('output.txt', 'w', encoding='utf8')
# 将准确率保留 4 位小数写入文件
f.write(f'{accuracy_test:.4f}')
# 关闭文件，完成保存
f.close()