# phoneloc
手机号归属地信息库

## phone.dat文件格式

```
        | 4 bytes |                     <- phone.dat 版本号（如：2001即20年01月）
        ------------
        | 4 bytes |                     <-  第一个索引的偏移
        -----------------------
        |  offset - 8            |      <-  记录区
        -----------------------
        |  index                 |      <-  索引区
        -----------------------
```

* 头部为8个字节，版本号为4个字节，第一个索引的偏移为4个字节(`<4si`)。
* 记录区 中每条记录的格式为"<省份>|<城市>|<邮编>|<长途区号>\0"。 每条记录以'\0'结束。
* 索引区 中每条记录的格式为"<手机号前七位><记录区的偏移><卡类型>"，每个索引的长度为9个字节(`<iiB`)。

phone type沿用源数据的定义：

* 1: 移动
* 2: 联通
* 3: 电信
* 4: 电信虚拟运营商
* 5: 联通虚拟运营商
* 6: 移动虚拟运营商


### 数据相关操作

```
dc = DataConverter()
dc.unpack()  # 生成csv文件
```
