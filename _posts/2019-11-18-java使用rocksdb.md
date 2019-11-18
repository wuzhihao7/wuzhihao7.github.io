---
layout: page
title: 第一篇博客
---
# 介绍

rocksdb是facebook开源的一个嵌入式kv存储引擎，key 和 value 是任意字节流。使用c++语音编写，基于Google的LevelDB，但提高了扩展性可以运行在多核处理器上，可以有效使用快速存储，支持IO绑定、内存和一次写负荷。

它具有以下四个特点：

- 高性能：RocksDB使用一套日志结构的数据库引擎，为了更好的性能，这套引擎是用C++编写的。 Key和value是任意大小的字节流。
- 为快速存储而优化：RocksDB为快速而又低延迟的存储设备（例如闪存或者高速硬盘）而特殊优化处理。 RocksDB将最大限度的发挥闪存和RAM的高度率读写性能。
- 可适配性：RocksDB适合于多种不同工作量类型。从像MyRocks这样的数据存储引擎，到应用数据缓存,甚至是一些嵌入式工作量，RocksDB都可以从容面对这些不同的数据工作量需求。
- 础和高级的数据库操作，RocksDB提供了一些基础的操作，例如打开和关闭数据库。对于合并和压缩过滤等高级操作，也提供了读写支持。

# 使用

## 依赖

```gradle
implementation 'org.rocksdb:rocksdbjni:6.3.6'
```

## 示例

RocksDB底层实现了AutoCloseable接口，因此可以使用try-with-resources打开资源。

Options类包含一组可配置的DB选项，它们决定数据库的行为。

通过open工厂方法，可以返回一个RocksDB实例，使用该实例即可进行Get(key) ，Put(key) ，Delete(key) 和 Scan(key)等操作。

部分代码如下：

```java
       try(final Options options = new Options().setCreateIfMissing(true)) {
            try(final RocksDB db = RocksDB.open(options, "rocksdb_data")){
                db.put("hello".getBytes(), "world".getBytes());
                byte[] bytes = db.get("hello".getBytes());
                System.out.println(new String(bytes));
            }
        }catch (RocksDBException e){
            e.printStackTrace();
        }
```



参考：

https://sdk.cn/news/6686

https://www.orchome.com/938