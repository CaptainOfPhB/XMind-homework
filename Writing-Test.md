---
Name: "戴江涛"
Date: "2022-06-18"
---

# Writing Test

1. What's the time complexity of the following code, and why?

    ```js
    var a = 0;
    for (var i = 0; i < N; i++) {
      for (var j = N; j > i; j--) {
        a = a + i + j;
      }
    }
    ```

    O(n^2)，因为外层的 for 循环执行 n 次，内部的 for 循环也执行了 n 次，因此复杂度为 O(n^2)。

2. Tell the differences between a byte, a character, and a string. Tell the differences between Unicode, UTF-8, UTF-16, GB2312, and GB18030.

    - bit: 计算机中存储最小单位，存储二进制
    - byte: 字节数据类型，是有符号型的，占 1 个字节，大小范围为 -128—127
    - char: 字符数据类型，是无符号型的，占 2 字节（Unicode码），大小范围是 0—65535，可以表示单个字符
    - string: 一串字符的组合

    - Unicode: 字符集，为每一个字符分配一个唯一的码点（code point）
    - UTF-8: 一套以 8 位为一个编码长度的可变长编码，是 Unicode 的一种编码规则
    - GB23112: 中国国家标准简体中文字符集，涵盖了大多数中文汉字，每个字符采用两个字节表示
    - GB18030: 中华人民共和国现时最新的内码字集，收录了更多的字符，采用了一二四字节变长编码

3. What are the mobile and desktop operating systems you use everyday? What applications do you use frequently? Can you name a few of them and tell how they can be improved or have bugs fixed?

    iOS & macOS。WebStorm、Chrome、iTerm2 等。WebStorm 可以在启动速度以及项目目录进行检查速度方面进行更多的优化。

4. What is the difference between Factory and Builder design patterns? What is the difference between Adapter and Decorator design patterns? Give an example for each above pattern.

    Factory design pattern:

    ```java
    // Factory
    static class FruitFactory {
        static Fruit create(name, color, firmness) {
            // Additional logic
            return new Fruit(name, color, firmness);
        }
    }

    // Usage
    Fruit fruit = FruitFactory.create("apple", "red", "crunchy");
    ```

    Builder design pattern:

    ```java
    // Builder
    class FruitBuilder {
        String name, color, firmness;
        FruitBuilder setName(name) {
            this.name = name;
            return this;
        }
        FruitBuilder setColor(color) {
            this.color = color;
            return this;
        }
        FruitBuilder setFirmness(firmness) {
            this.firmness= firmness;
            return this;
        }
        Fruit build() {
            return new Fruit(this); // Pass in the builder
        }
    }

    // Usage
    Fruit fruit = new FruitBuilder()
            .setName("apple")
            .setColor("red")
            .setFirmness("crunchy")
            .build();
    ```

    Decorator design pattern:

    ```java
    public interface Component {
        void operation();
    }

    // add some features to component
    abstract class Decorator implements Component {
        protected Component component;
        public abstract void operation();
        public void setComponent(Component component) {
            this.component = component;
        }
    }
    ```

    Adaptor design pattern:

    ```java
    public interface Target {
        String request();
    }

    public class Adaptee {
        public String specialRequest() {
            return "specialRequest";
        }
    }

    // enhance all instances created by Adapter 
    public class Adapter extends Adaptee implements Target {
        public String request() {
            return this.specialRequest();
        }
    }
    ```

5. What computer languages do you master? What're the pros and cons of each of them?

    JavaScript。优点是足够灵活，非常适合做脚本语言。缺点是缺少类型系统，以及各种数据的隐式转换。

6. Explain the differences between mutable and immutable objects.

    mutable 即为可变，例如在一个 plain object 上进行数据的增删改。immutable 即为不可变，数据一旦创建后将不能被增删改。例如：

    ```js
    // mutable
    const a = { name: 'abc' }
    a.name = 'def'
    console.log(a) // { name: 'def' }

    // immutable
    const b = Object.freeze({ name: 'abc' })
    b.name = 'def'
    console.log(b) // { name: 'abc' }
    ```

7. Use JavaScript to implement the 'reactive' and 'computed' functions so that the following code works as expected.

    ```js
    const node = reactive({ leftChildren: 1 })
    console.log(node.leftChildren, node.rightChildren) // 1 undefined
    const children = computed(() => node.leftChildren + (parseInt(node.rightChildren) || 0))
    console.log(children.value) // 1
    node.leftChildren = 10
    console.log(children.value) // 10
    node.rightChildren = 2
    console.log(children.value) // 12
    ```

    使用 Proxy 对数据进行代理即可。

    ```js
    function reactive(obj) {
      // use proxy or not
      return obj;
    }

    function computed(getter) {
      return new Proxy({}, {
        get(target, prop) {
          if(prop === 'value') {
            return getter()
          }
        }
      })
    }
    ```

8. Given a number of rectangles defined by their width, height, and location (x, y) of their top-left corners, how can we insert a new rectangle(with a fixed size) as close as possible to a desired target location, without making it intersect with any existing rectangles?

    没有明白题意。
