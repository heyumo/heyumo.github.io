---
title: JSON的标准写法
categories:
	
date: 2019-08-4 10:32:32
notshow: true
---

JSON 是一种轻量级的数据交换格式

#### 只能用双引号

``` java
	
	{a:1,b:2,c:3} ×

	{"a":'1',"b":'文字'} ×

```

#### 所有的名字都必须用引号包起来

``` java

	{"a":1,"b":2,"c":"文字"} √
```

#### 简写方式

+ 名字和值相同,写一个就可以

``` java

let a = "中文"

let json = {a,"b":"中文"}

 
```

#### 对象方式

``` java

		{
            "user" : "zhiyu.he",

            "type" : "work",

            "team" : [{
                "city" : "BeiJing",
            }, {
                "city" : "GuangZhou",
            }]
        }

```
