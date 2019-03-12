---
layout: default
title:  "How to run, let, also, apply in Kotlin"
date:   2019-03-12 23:44:36 +0700
categories: blog
---
**How to run, let, also, apply in Kotlin**

A short summary on Kotlin standard library functions: run, let, also, apply 



If you decide to write Kotlin code, eventually you will see a lot of usage of the following 4 functions from standard library: `run`, `let`, `also` and `apply`.

After doing a lot of research, I show simple examples of how to use them here.

First, a helper `class Student`.

```Kotlin
class Student(name: String, age: Int, stuNum: String) {

    var name = name
        private set

    var age = age
        private set

    var stuNum = stuNum
        private set

    fun increaseAge() {
        age++
    }

    fun nameToUpperCase() {
        name = name.toUpperCase()
    }

    override fun toString(): String {
        return "($name, $age, $stuNum)"
    }
}
```

We can group the 4 functions into 2 groups: `transformation functions` and `mutation functions`.

***Transformation functions***

This means that the function takes an A and returns a B.

`run` and `let` belongs in this group.

```Kotlin
val student = Student("Bob", 19, "1234")

// Takes a student and returns its name, Student -> String

val name = student.run {
    println(this)
    name
}

val name1 = student.let {
    println(it)
    it.name
}
```

***Mutation functions***

This means that the function takes an A, mutate its state, and return it back.

`apply` and `also` belongs in this group.

```Kotlin
val student = Student("Bob", 19, "1234")

val result = student.apply {
    increaseAge()
    nameToUpperCase()
}
                
val result1 = student.also {
    it.increaseAge()
    it.nameToUpperCase()
}
```

So when trying to choose from these 4 functions, think in terms of transformation and mutation, NOT the four function names (the names are terrible in my opinion).

Another thing is that I cannot figure out when to used which function inside each group, to me they are pretty much interchangable. If someone has a good explanation, please let me know.


**From**
*   [How to run, let, also, apply in Kotlin](https://www.lvguowei.me/post/kotlin-run-let-also-apply/){:target="_blank"}