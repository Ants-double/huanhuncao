# fastjson 
## 介绍
- 阿里巴巴FastJson是一个Json处理工具包，包括“序列化”和“反序列化”两部分，它具备如下特征：
速度最快，测试表明，fastjson具有极快的性能，超越任其他的Java Json parser。包括自称最快的JackJson；
- 官网
https://github.com/alibaba/fastjson
## 使用
- 相关类型的序列化与反序列化
``` java
@Test
    public void testJson() {

        //测试空
        Person person = new Person();
        Object json = JSON.toJSONString(person, SerializerFeature.WriteNullStringAsEmpty);
        System.out.println(json);
        //测试对象
        Person person1 = new Person(1, "lyy");
        System.out.println(JSON.toJSONString(person1, SerializerFeature.WriteClassName));
        // System.out.println(JSON.toJSONBytes(person1, SerializerFeature.config(0,)));
        //时间
        String dateJsonNoFeature = JSON.toJSONString(new Date());
        System.out.println(dateJsonNoFeature);
        String dateJson = JSON.toJSONString(new Date(), MyJsonUtils.FEATURES);
        System.out.println(dateJson);
        //list
        List<Person> list = new ArrayList<Person>();
        list.add(person);
        list.add(person1);
        System.out.println(JSON.toJSON(list));
        String jsonList = JSON.toJSONString(list, MyJsonUtils.FEATURES);
        System.out.println(jsonList);
        //map
        HashMap<Integer, Person> map = new HashMap<Integer, Person>();
        map.put(0, person);
        map.put(1, person1);
        System.out.println(JSON.toJSON(map));
        String mapJson = JSON.toJSONString(map, MyJsonUtils.FEATURES);
        System.out.println(mapJson);
        //byte
        byte[] bytes = JSON.toJSONBytes(map, MyJsonUtils.FEATURES);
        System.out.println(bytes.toString());


        //反序
        System.out.println("反序");
        System.out.println(JSON.parse(dateJson));
        //list
        System.out.println(JSON.parse(jsonList));
        // 把JSON文本parse成JSONArray
        System.out.println(JSON.parseArray(jsonList, Person.class));
        //map
        System.out.println(JSON.parse(mapJson));
        // 把JSON文本parse成JSONObject
        Map<Integer, Person> map1 = JSON.parseObject(mapJson, new TypeReference<Map<Integer, Person>>() {
        });
        System.out.println(map1);
        System.out.println(map1.get(1));

        //bytes
        Object parse = JSON.parse(bytes, Feature.AllowArbitraryCommas);
        System.out.println(parse);
    }

    public class Person {

    private  long id;
    private String name;

    public Person() {
    }

    public Person(long id, String name) {
        this.id = id;
        this.name = name;
    }

    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
public class MyJsonUtils {
    public static  final SerializerFeature[] FEATURES={
            SerializerFeature.WriteMapNullValue,
            SerializerFeature.WriteNullListAsEmpty,
            SerializerFeature.WriteNullBooleanAsFalse,
            SerializerFeature.WriteNullNumberAsZero,
            SerializerFeature.WriteNullStringAsEmpty,
            SerializerFeature.WriteDateUseDateFormat
    };
}
```   
运行代码参考右上角github->learn-all->learn-fastjson
> http://kimmking.github.io/2017/06/06/json-best-practice/  

> https://github.com/alibaba/fastjson/wiki
