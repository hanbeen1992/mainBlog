---
title: Decision Tree
date: 2021-11-04 15:00:00
categories:
- python
- Decision Tree
tags:
- python
- Decision Tree
---
# 결정트리(Decision Tree)
<li>분류와 회귀에 사용되는 지도학습 방법</li>
<li>데이터 특성으로부터 추론된 결정 규칙을 통해 값을 예측</li>
<li>if-then-else 결정규칙을 통해 데이터 학습</li>
<li>트리의 깊이가 깊을 수록 복잡한 모델</li>
<br>
<li>결정 트리 장점</li>
  1.이해와 해석이 쉽다.<br>
  2.시각화가 용이하다<br>
  3,많은 데이터 전처리가 필요하지 않다.<br>
  4.수치형과 범주형 데이터 모두를 다룰수 있다.<br>

단점
1. 데이터를 잘 일반화하지 못하고 복잡한 트리를 만들 수 있다.
2. 1번과 같은 것을 과적합이라고 하며, 알고리즘 성능이 떨어진다.이를  극복하기 위해 트리의 크기를 사전에 제한하는 튜닝이 필요하다.

사이킷런은 결정트리 알고리즘을 구현한 **DecisionTreeClassifier** 와**DecisionTreeRegressor**클래스를 제공한다. **DecisionTreeClassifier**는 분류를 위한 클래스이며,  **DecisionTreeRegressor** 는 회귀를 위한 클래스이다.

## DecisionTreeClassifier
분류를 위한 클래스를 알아보자.


```python
from sklearn import tree
X = [[0,0],[1,1]]
Y = [0,1]
clf = tree.DecisionTreeClassifier()
clf = clf.fit(X, Y)
```

모델을 사용하여 표본의 클래스를 예측할 수 있다.



```python
clf.predict([[2.,2.]])
```




    array([1])



결정트리 분류 클래스는 이진[-1,1]분류와 다중 클래스 (라벨이[0,...,k-1]인경우)분류를 모두 수행할 수 있다.


```python
clf.predict_proba([[2.,2.]])
```




    array([[0., 1.]])



iris 데이터를 활용하여 다음과 같이 트리를 구성할수 있다.


```python
from sklearn.datasets import load_iris
from sklearn import tree
iris = load_iris()
X, y = iris.data, iris.target
clf = tree.DecisionTreeClassifier()
clf = clf.fit(X,y)
```


```python
tree.plot_tree(clf)
[...]
```




    [Ellipsis]



![](/images/Decision_Tree(결정트리)/output_11_1.png)

    


이를 export_graphviz를 활용하여 결정트리 알고리즘이 어떠한 규칙을 가지고 트리를 생성하는지 시각적으로 보여줄 수 있다. 


```python
import graphviz
dot_data = tree.export_graphviz(clf, out_file=None)
graph = graphviz.Source(dot_data)
graph.render("iris")
```




    'iris.pdf'






```python
dot_data = tree.export_graphviz(clf, out_file=None,
                                feature_names=iris.feature_names,
                                class_names=iris.target_names,
                                filled=True, rounded=True,
                                special_characters=True)
graph = graphviz.Source(dot_data)
graph
```




    
![svg](/images/Decision_Tree(결정트리)/output_15_0.svg)
    


