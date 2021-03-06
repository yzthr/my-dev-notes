# Json.NET 反序列化嵌套对象

有这么两个类：

``` C#
public class B
{
    public string MsgB { get; internal set; }
}

public class A
{
    public string MsgA { get; internal set; }
    public B B { get; internal set; }
}
```

A包含B类型的属性B，如何反序列化如下json？

``` JSON
{
    "b": {
        "msgB": "helloB"
    },
    "msgA": "helloA"
}
```

自定义一个反序列化B类的转换器，继承自 JsonConvertor

``` C#
public class BConvertor : JsonConvertor
{
    public override bool CanConvert(Type objectType)
    {
        return true;
    }

    // 反序列化时会触发此方法 （JSONText 转 对象）
    public override object ReadJson(JsonReader reader, Type objectType, object existingValue, JsonSerializer serializer)
    {
        // 如果对json的键值对信息不作任何修改，则直接返回当前读取到的对象的反序列化结果即可
        return serializer.Deserialize(reader, objectType);
    }

    // 序列化时会触发此对象（对象 转 JSONText）
    public override void WriteJson(JsonWriter writer, object value, JsonSerializer serializer)
    {
        serializer.Serialize(writer, value);
    }
}
```

然后在需要做转换的类上标上特性：

``` C#
public class B
{
    [JsonProperty("msgB", NullValueHandling = NullValueHandling.Ignore)]
    public string MsgB { get; internal set; }
}

public class A
{
    [JsonProperty("msgA", NullValueHandling = NullValueHandling.Ignore)]
    public string MsgA { get; internal set; }
    [JsonProperty("b", ItemConverterType = typeof(BConvertor))]
    public B B { get; internal set; }
}
```

此时，只需：

``` C#
string json = "{\"b\":{\"msgB\":\"helloB\"},\"msgA\":\"helloA\"}";
A a = JsonConvert.DeserializeObject(json, typeof(A)) as A;
```

即可完成序列化。

如图所示：

![img](data:image/png;base64,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)