# 我的知识库

[github markdown 语法参考](https://docs.github.com/cn/free-pro-team@latest/github/writing-on-github/basic-writing-and-formatting-syntax#%E6%A0%87%E9%A2%98)

[gitbook markdown 语法参考](https://docs.gitbook.com/editing-content/markdown#quotes)

[markdown-preview-enhanced](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/?id=%e7%89%b9%e6%80%a7)

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

#### Advanced Java

- JDBC (Java Database Connectivity)
- Servlet
- JSP
- Popular Frameworks:

#### Spring (MVC, Core, JDBC, ORM, AOP)

- Hibernate ORM framework
- Struts
- JSF
- Web Services (SOAP & REST)

#### Other

- Design patterns and design questions related to your projects.

## 本地发布调整

```bash
gitbook serve
```

## 发布步骤

main分支编译生成静态文件

```bash
gitbook build
```

切换到gh-pages分支，把生成的文件推送到github pages

```bash
checkout out gh-pages

cp -r _book/* .
git add .
git commit -m "Publish book"
```

## 如何导出带UML图的pdf

Markdown Prewiew-> Chrome-> PDF

[参考gitbook集成文档](http://docs.flycloud.me/docs/gitbook/gitbook.com/config/github.html)
