## Java: Java 序列化中如果有些字段不想进行序列化，怎么办

方法一：将类实现类Externalizabel，使得不能自动序列化，需要自己写序列化规则，并且在writeExternal()中对所需要的部分进行反序列化。

可以使用Externalizable接口，代替实现Serializable接口。Externalizable继承了Serializable接口，并且添加了writeExternal()和readExtrenal()方法，会在序列化和反序列化的时候被调用。可以在writeExternal()和readExternal()当中自定义序列方式，可以实现不希望序列化那么多字段的需求。



方法二：使用transient配合Serializable接口的自动序列化，使用transient可以关闭字段的序列化。使用transient配合Serializable接口，将不想要序列化的属性前面加上transient，那这序列化对象的时候，这个属性就不会序列化指定的目的地当中。

transient只能修饰变量，不能修饰方法和类，如果变量为本地新建类，则该类需要实现Serializable接口。