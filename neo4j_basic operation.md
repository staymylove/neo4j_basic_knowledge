# neo4j_basic_knowledge
neo4j图形数据库基础语法
**查询操作：**
1.查询整个图形数据库
```python
match(n)  return n;
```

2.查询具有特殊属性的节点

```python
match(n{name:'xxxx'})  #这个{}类似与json里的  所以查询到属性也可以这样
return n;  #{}里面写要查询的属性
```
通过id查询
```python
MATCH (n) WHERE id(n)=251 RETURN n
```

3.查询指定label的节点

```python
match(n:course) 
return n;
```

4.关系查询
*Cypher语言规定，关系分为三种：
（1）符号“--”，表示有关系，忽略关系的类型和方向；
（2）符号“-->”表示有方向的关系
（3）符号“<--”表示有方向的关系；*


查询所以节点及关系
```python
match(n) return n;
```
 
返回与  m：xxx标签   有关系的所有节点

```python
match(n)--(m:course)
return n;
```

查询有向关系的节点
这个意思是：查询所有指向   course标签   对应的    电子电路基础   的所有  下一级节点
```python
match(:course{name:'电子电路基础'})-->(course)
return course
```


通过[r]为关系定义一个变量名，通过函数type获取关系的类型
这个意思是：查询所有指向   course标签   对应的    电子电路基础   的所有  下一级节点，，并通过type获取类型

```python
match(:course {name:'电子电路基础'})-[r] ->(course)
return r,type(r)
```

**删除节点**

删除指定id的节点及其所有的关系
```python
match (r)
where id(r) = xxx
detach delete r
```
清空所有数据

```python
MATCH (n)
OPTIONAL MATCH (n)-[r]-()
DELETE n,r
```
批量删除节点

```python
match (n) where n.ranker Contains 'xxx' delete n
```
批量删除节点以及关系

```python
match ()-[r]-(n) where n.ranker Contains 'xxx' delete n,r
```
**修改节点属性**

```python
match (r)
WHERE id(r) =xxx
SET r.name = "xxx"
```



**新增节点属性**

```python
match (r)
match (n) where exists(n.leve) set n.level=4
```


**删除节点属性**

```python
match (n) where exists(n.leve) remove n.leve
```
