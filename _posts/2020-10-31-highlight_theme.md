---
layout: post
title: 测试代码高亮
categories: 代码
description: 测试代码高亮
keywords: 测试代码高亮，
# topmost: true
---

```python
#!/usr/bin/env python
# coding: utf-8
import numpy as np
import matplotlib.pyplot as plt
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import Ridge


class MyLGMode(object):
    """
    自定义回归模型
    """
    def __init__(self, degree=1, alpha=0.0005):
        self.degree = degree  # 阶数
        self.alpha = alpha  # 正则化
        self.theta_ = ""  # theta
        # self.coef__ = ""  # 特征权重
        # self.intercept__ = ""  # 偏值项

    def fit(self, x, y):
        """
        使用最小二乘法求解(推导公式求解theta)
        :param x:
        :param y:
        :return:
        """
        # 正则化项
        identity_matrix = np.identity(self.degree+1)
        reg_item = self.alpha * identity_matrix

        x_b = np.ones((len(x), 1))  # 偏值项b的权重
        for i in range(1, self.degree + 1):
            x_b = np.c_[x ** i, x_b]  # 添加i次多项式
        theta_best = np.linalg.inv(x_b.T.dot(x_b) + reg_item).dot(x_b.T).dot(y)

        self.theta_ = theta_best

    def predict(self, x_new):
        """
        预测结果
        :param x:
        :param degree:
        :param alpha:
        :return:
        """
        x_b = np.ones((len(x_new), 1))  # 偏值项b的权重
        for i in range(1, self.degree + 1):
            x_b = np.c_[x_new ** i, x_b]  # 添加i次多项式
        y_predict = x_b.dot(self.theta_)

        return y_predict

    def coef_(self):
        """
        特征权重
        :return:
        """
        return self.theta_.reshape(-1)[:-1]

    def intercept_(self):
        """
        偏值项
        :return:
        """
        return self.theta_.reshape(-1)[-1]


def real_func(x):
    """
    目标函数
    :param x:
    :return:
    """
    return np.sin(2*np.pi*x) 


def plot_model(model_class, degree, alphas, **model_kargs):
    """使用不同的 polynomial 值对某个线性数据进行训练的几种模型"""
    for degree, style in zip(degree, ("y--", "g--", "b--")):
        if model_class == "MyLGModel":
            model = MyLGMode(degree, alphas)
        else:
            model = model_class(alphas, **model_kargs)
            model = Pipeline([
                # 对数据进行扩展
                ("poly_features", PolynomialFeatures(degree=degree, include_bias=False)),
                # 进行缩放
                # ("std_scaler", StandardScaler()),
                # 将岭回归模型用于结果特征
                ("regul_mode", model)
            ])

        model.fit(x, y)
        y_predict_regul = model.predict(x_points)

        plt.plot(x_points, y_predict_regul, style, label=r"degree={}".format(degree))
        title_name = "My_mode" if model_class == "MyLGModel" else "Ridge"
        plt.title(r"{}_alpha={}".format(title_name, alphas), fontsize=14)

        if alphas == 0.0005 and degree == 3 and model_class != "MyLGModel":
            print("\n岭回归模型求解theta===== alpha={}, degree={}".format(alphas, degree))
            print("coef_(特征权重): ", model[1].coef_.reshape(-1)[::-1])
            print("intercept_(偏置项): ", model[1].intercept_)
        elif alphas == 0.0005 and degree == 3 and model_class == "MyLGModel":
            print("\n自定义模型求解theta===== alpha={}, degree={}".format(alphas, degree))
            print("coef_(特征权重): ", model.coef_())
            print("intercept_(偏置项): ", model.intercept_())

    plot_curve(x, y, x_points)


def plot_curve(x_noise, y_noise, x_points):
    """
    绘制曲线
    :param x_noise: 噪声点 x
    :param y_noise: 噪声点 y
    :param x_points: 数据点 x
    :return:
    """
    plt.plot(x, y, "ro", label="noise")
    plt.plot(x_points, real_func(x_points), "r-", label="real")
    # plt.ylabel("y", fontsize=14)
    plt.legend(loc="upper right")
    # plt.show()


if __name__ == '__main__':
    np.random.seed(42)
    # 构建数据集，这里用十个点
    x = np.linspace(0, 1, 10).reshape(10, 1)
    x_points = np.linspace(0, 1, 1000).reshape(1000, 1)
    # 加上正态分布噪音的目标函数（Ground-Truth）的值
    y_ = real_func(x)
    y = [np.random.normal(0, 0.2) + y1 for y1 in y_]

    plt.figure(figsize=(12, 8))
    # 绘制Ridge模型曲线--alphas=0
    plt.subplot(221)
    plot_model(Ridge, degree=(1, 3, 9), alphas=0, random_state=42)
    plt.ylabel("$y$", fontsize=14)
    # plt.xlabel("$x$", fontsize=14)
    # 绘制Ridge模型曲线--alphas=0.001
    plt.subplot(222)
    plot_model(Ridge, degree=(1, 3, 9), alphas=0.0005, random_state=42)
    # plt.xlabel("$x$", fontsize=14)

    # 绘制自定义回归模型曲线
    plt.subplot(223)
    plot_model("MyLGModel", degree=(1, 3, 9), alphas=0)
    plt.ylabel("$y$", fontsize=14)
    plt.xlabel("$x$", fontsize=14)
    plt.subplot(224)
    plot_model("MyLGModel", degree=(1, 3, 9), alphas=0.0005)
    plt.xlabel("$x$", fontsize=14)
    plt.savefig("Ridge_MyModel.png")
    plt.show()



```