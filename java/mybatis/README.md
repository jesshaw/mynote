# Mybatis

## mybatis加载mappers文件有几种方式

有resource, url, class, package4种，package优先级最高。

## mybatis有几种执行器

有3种，分别是simple，reuse,  batch。

## SqlSession是线程安全的吗

本身不是线程安全的，但在Spring环境下是线程安全的。Spring通过ThreadLocal，确切的说是通过对象ThreadLocal<Map<SqlSessionFactory,SqlSessionHolder>>来实现线程安全。
