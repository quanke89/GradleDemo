# Gradle 学习

## Groovy 相关知识
1. 以下示例内容来自[udacity](https://github.com/udacity/ud867)
1. 基础知识
    ```java
    // 常见示例，示例来源: 
    task groovy {}
    println "Hello Groovy!"

    // class
    class JavaGreeter {
    public void sayHello() {
        System.out.println("Hello Java!");
        }
    }
    JavaGreeter greeter = new JavaGreeter()
    greeter.sayHello()

    // 类型推断
    def foo = 6.5
    // 获取变量值，其他脚本语言中也常见
    println "foo has value: $foo"
    // {}中为表达式
    println "Let's do some math. 5 + 6 = ${5 + 6}"
    // 内置属性，获取class 类型
    println "foo is of type: ${foo.class} and has value: $foo"
    foo = "a string"
    println "foo is now of type: ${foo.class} and has value: $foo"

    // 函数，无需书写return，默认返回最后一个表达式的值
    def doubleIt(n) {
        n + n 
    }
    foo = 5
    println "doubleIt($foo) = ${doubleIt(foo)}"
    foo = "foobar"
    println "doubleIt($foo) = ${doubleIt(foo)}"

    // 无括号调用函数
    def noArgs() {
        println "Called the no args function"
    }

    def oneArg(x) {
        println "Called the 1 arg function with $x"
        x
    }

    def twoArgs(x, y) {
        println "Called the 2 arg function with $x and $y"
        x + y
    }

    oneArg 500 // Look, Ma! No parentheses!
    twoArgs 200, 300
    noArgs()
    //noArgs // Doesn't work
    //twoArgs oneArg 500, 200 // Also doesn't work as it's ambiguous
    twoArgs oneArg(500), 200 // Fixed the ambiguity
    ```

2. 闭包和对象
    ```java
    task groovy {}

    def foo = "One million dollars"
    // 定义闭包
    def myClosure = {
        println "Hello from a closure"
        println "The value of foo is $foo"
    }
    // 闭包传递
    myClosure()
    def bar = myClosure
    def baz = bar
    baz()

    // lambda
    def doubleIt = { x -> x + x}
    def applyTwice(func, arg){
        func(func(arg))
    }
    foo = 5
    def fooDoubledTwice = applyTwice(doubleIt, foo)
    println "Applying doubleIt twice to $foo equals $fooDoubledTwice"
    
    // list示例
    def myList = ["Gradle", "Groovy", "Android"]
    def printItem = {item -> println "List item: $item"}
    myList.each(printItem)

    // class 和 对象
    class GroovyGreeter {
        String greeting = "Default greeting"
        def printGreeting(){println "Greeting: $greeting"}
    }
    def myGroovyGreeter = new GroovyGreeter()
    myGroovyGreeter.printGreeting()
    myGroovyGreeter.greeting = "My custom greeting"
    myGroovyGreeter.printGreeting()

    // 委托
    def greetingClosure = {
        greeting = "Setting the greeting from a closure"
        printGreeting()
    }
    // greetingClosure() // This doesn't work, because `greeting` isn't defined
    greetingClosure.delegate = myGroovyGreeter
    greetingClosure() // This works as `greeting` is a property of the delegate
    ```


