# java_myself

slug: java_myself
status: Published
tags: java
type: Post

[[toc]] ### 解析key值不固定的json

```
    JsonObject data = new Gson().fromJson(body, JsonObject.class);
    Set<Map.Entry<String, JsonElement>> entries = data.entrySet();
    // 动态获取key值
    Iterator<Map.Entry<String, JsonElement>> iterator = entries.iterator();//使用迭代器
    String list = "";
    while (iterator.hasNext()) {
        Map.Entry<String, JsonElement> obj = iterator.next();//获取key
        JsonElement value = obj.getValue();
        StockBean bean = new Gson().fromJson(value, StockBean.class);
        Double price = bean.getPrice();
    }
```

## 其他

- `补码`
    - 正数的补码与原码相同，而负数的补码是其对应正数的二进制反码加1
    - `Integer.toBinaryString(number)`
- `有符号整数` 可以表示正数、负数和零。它的表示方法通常使用补码来实现。在有符号整数中，最高位（最左边的位）用于表示符号，0 表示正数，1 表示负数。
## java_gui
- https://blog.csdn.net/mawei7510/article/details/89638126 可执行的jar桌面程序
- https://blog.csdn.net/weixin_42691149/article/details/119543370
