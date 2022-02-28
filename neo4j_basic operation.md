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
