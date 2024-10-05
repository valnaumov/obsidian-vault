# Материалы

> [!info] Learning materials overview | Kotlin  
> You can use the following materials and resources for learning Kotlin: Basic syntax - get a quick overview of the Kotlin syntax.  
> [https://kotlinlang.org/docs/learning-materials-overview.html](https://kotlinlang.org/docs/learning-materials-overview.html)  

> [!info] Migrating from Java to Kotlin: Strings | Kotlin  
> This guide contains examples of how to perform typical tasks with strings in Java and Kotlin.  
> [https://kotlinlang.org/docs/java-to-kotlin-idioms-strings.html#top](https://kotlinlang.org/docs/java-to-kotlin-idioms-strings.html#top)  

> [!info] Comparison to Java | Kotlin  
> Kotlin fixes a series of issues that Java suffers from: What Java has that Kotlin does not What Kotlin has that Java does not Learn how to perform typical tasks with strings in Java and Kotlin.  
> [https://kotlinlang.org/docs/comparison-to-java.html](https://kotlinlang.org/docs/comparison-to-java.html)  

> [!info] Introduction to the course - Introduction | Coursera  
>  
> [https://www.coursera.org/learn/kotlin-for-java-developers/lecture/1bpIV/introduction-to-the-course](https://www.coursera.org/learn/kotlin-for-java-developers/lecture/1bpIV/introduction-to-the-course)  

> [!info] Kotlin Playground: Edit, Run, Share Kotlin Code Online  
>  
> [https://play.kotlinlang.org/hands-on/Introduction%20to%20Coroutines%20and%20Channels/01_Introduction](https://play.kotlinlang.org/hands-on/Introduction%20to%20Coroutines%20and%20Channels/01_Introduction)  

# Интересное в языке

- [when](https://kotlinlang.org/docs/basic-syntax.html#when-expression)
- classes are final by default
- метод может быть определён выражением, не только блоком
- есть .with, it
- Generics: на type parameter, можно навесить два ограничения сверху. Например, Comparable **и** CharSequence
- [Inline classes](https://kotlinlang.org/docs/inline-classes.html#inline-classes-vs-type-aliases)
- [sealed classes](https://kotlinlang.org/docs/sealed-classes.html). есть в последних Java
- [extensions](https://kotlinlang.org/docs/extensions.html), которые можно использовать там, где они объявлены. хоть даже во всём модуле
- [Objects Expressions](https://kotlinlang.org/docs/object-declarations.html#creating-anonymous-objects-from-scratch). Как Expando, только типизированный. Или использовать их вместо анонимных классов.
    - [Можно объявлять Singelton](https://kotlinlang.org/docs/object-declarations.html#object-declarations-overview)
- [Companion Objects](https://kotlinlang.org/docs/object-declarations.html#companion-objects). Можно отделить некоторую функциональность в отдельный класс, но снаружи это не будет видно. Companion Object может быть наследником, это не просто отдельный static namespace.
    
    ```Kotlin
    interface Factory<T> {
        fun create(): T
    }
    
    class MyClass {
        companion object : Factory<MyClass> {
            override fun create(): MyClass = MyClass()
        }
    }
    
    val f: Factory<MyClass> = MyClass
    ```
    
- Lazy properties **and** local variables
- Check extension properties!
- Delegates
- Type aliases
- Указывая значения по умолчанию для функций, можно ссылаться на другие аргументы
- Лямбды в качестве последнего (дефолтного?) аргумента можно указывать вне скобок
- Named arguments, но не для функций, определенных в Java
- Spread operator
- Unit - это как void, и его можно пропустить при объявлении
- Infix functions: можно вызвать без точки и скобок, как в Groovy, но нужно это явно определить для функции
- Nested functions
- Tail recursive functions