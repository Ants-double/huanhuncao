##  MD5如何生成的
[百度百科](https://baike.baidu.com/item/MD5)

![md5](../images/md5.png)

##  生成MD5

### 1.通过摘要生成MD5

``` java
 MessageDigest md = MessageDigest.getInstance("MD5");
        md.update(input.getBytes(StandardCharsets.UTF_8));
        byte[] hashBytes = md.digest();
        StringBuilder sb = new StringBuilder();
        for (byte b : hashBytes) {
            sb.append(String.format("%02x", b));
        }
        return sb.toString();
```

### 2.使用Google的Guava生成MD5

- 添加依赖

``` xml
            <dependency>
              <groupId>com.google.guava</groupId>
              <artifactId>guava</artifactId>
              <version>28.1-jre</version>
          </dependency>
```
- 生成代码

 ``` java
   // com.google.common.hash.Hashing.md5()
          // If you must interoperate with a system that requires MD5, then use this method, despite its deprecation. But if you can choose your hash function, avoid MD5, which is neither fast nor secure. As of January 2017, we suggest:
          // For security: Hashing.sha256() or a higher-level API.
          // For speed: Hashing.goodFastHash(int), though see its docs for caveats.
          HashFunction hashFunction = Hashing.md5();
  
          HashCode hash = hashFunction.hashString(input, StandardCharsets.UTF_8);
          return hash.toString();
 ```

### 3.使用Appach的commons生成MD5

- 添加依赖

``` xml
<dependency>
            <groupId>commons-codec</groupId>
            <artifactId>commons-codec</artifactId>
            <version>1.13</version>
        </dependency>
```
- 生成代码

``` java
   String md5 = DigestUtils.md5Hex( input );
          return md5;
```

  

## 加盐MD5

