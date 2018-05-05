# 接口的默认方法

在接口中新增了default方法和static方法，这两种方法可以有方法体。

# Predicate接口

```
    public static void main(String[] args) {
        Predicate<String> predicate = (s) -> s.length() > 0;
        System.out.println(predicate.test("foo"));              // true
        System.out.println(predicate.negate().test("foo"));     // false
        Predicate<Boolean> nonNull = Objects::nonNull;
        Predicate<Boolean> isNull = Objects::isNull;
        Predicate<String> isEmpty = String::isEmpty;
        Predicate<String> isNotEmpty = isEmpty.negate();
        System.out.println(nonNull.test(null));
        System.out.println(isNull.test(null));
        System.out.println(isEmpty.test("sss"));
        System.out.println(isNotEmpty.test(""));
    }
```

# Function接口

```
        Function<String, Integer> toInteger = Integer::valueOf;
        System.out.println(toInteger.apply("123").getClass());
        Function<String, Object> toInteger2 = toInteger.andThen(String::valueOf);
        System.out.println(toInteger2.apply("123").getClass());
```


# Lambda

```
(int a, int b) -> {  return a + b; }
```

@FunctionalInterface用来标注接口可以使用lambda符号，该接口只能有一个方法。

```
@FunctionalInterface
public interface WorkerInterface {
    public void doSomeWork();
}
```

另外，java.util包中的类开始支持lambda符号。如：

```
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
list.forEach(n -> System.out.println(n));


list.forEach(System.out::println);
```

若将lambda函数当作函数的入参，则使用java.util.function.Predicate做为其类型。

```
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
list.stream().map((x) -> x*x).forEach(System.out::println);
```

使用匿名类与 Lambda 表达式的一大区别在于关键词的使用。对于匿名类，关键词 this 解读为匿名类，而对于 Lambda 表达式，关键词 this 解读为写就 Lambda 的外部类。

Lambda 表达式与匿名类的另一不同在于两者的编译方法。Java 编译器编译 Lambda 表达式并将他们转化为类里面的私有函数，它使用 Java 7 中新加的 invokedynamic 指令动态绑定该方法，关于 Java 如何将 Lambda 表达式编译为字节码，Tal Weiss 写了一篇很好的文章。

