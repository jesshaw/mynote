# 我的知识库

[github markdown 语法参考](https://docs.github.com/cn/free-pro-team@latest/github/writing-on-github/basic-writing-and-formatting-syntax#%E6%A0%87%E9%A2%98)

[gitbook markdown 语法参考](https://docs.gitbook.com/editing-content/markdown#quotes)


#### Concepts from core Java:

- OOPS concepts (Data Abstraction, Encapsulation, Inheritance, Polymorphism)
- Basic Java constructs like loops and data types
- String handling
- Collection framework
- Multithreading
- Exception handling
- Generics
- Synchronisation
- Serialisation & De-serialisation
- Concurrent collection

#### Advanced Java:

- JDBC (Java Database Connectivity)
- Servlet
- JSP
- Popular Frameworks:

#### Spring (MVC, Core, JDBC, ORM, AOP)
- Hibernate ORM framework
- Struts
- JSF
- Web Services (SOAP & REST)

#### Other:

- Design patterns and design questions related to your projects.

## 本地发布调整

```
gitbook serve
```

## 发布步骤

main分支编译生成静态文件
```
gitbook build
```

切换到gh-pages分支，把生成的文件推送到github pages
```
checkout out gh-pages

cp -r _book/* .
git add .
git commit -m "Publish book"
```

[参考gitbook集成文档](http://docs.flycloud.me/docs/gitbook/gitbook.com/config/github.html)
