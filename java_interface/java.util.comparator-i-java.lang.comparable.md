# java.util.Comparator и java.lang.Comparable

В Java для задания порядка объектов используются два интерфейса: **`Comparable`** и **`Comparator`**. Оба они применяются для сортировки объектов, но имеют разные подходы и случаи использования.

## 1. Интерфейс **`Comparable`**

`Comparable` — это интерфейс, который определяет естественный порядок объектов одного типа. Он содержится в пакете `java.lang` и требует от класса, который его реализует, определить один метод:

{% tabs %}
{% tab title="Метод 'int compareTo(T s)'" %}
{% hint style="info" %}
**`int compareTo(T s)`**
{% endhint %}

Этот метод сравнивает текущий объект с объектом, переданным в качестве параметра **`s`**. \
Он возвращает:

* отрицательное число, если текущий объект меньше объекта **`s`**,
* 0, если они равны,
* положительное число, если текущий объект больше объекта **`s`**.

### Применение:

* `Comparable` <mark style="background-color:blue;">используется, когда вы хотите, чтобы объекты вашего класса имели</mark> <mark style="background-color:blue;"></mark><mark style="background-color:blue;">**естественный порядок**</mark>, который может быть применен, например, при использовании методов `Collections.sort()` или `Arrays.sort()`.
{% endtab %}

{% tab title="Пример использования:" %}
```java
class Person implements Comparable<Person> {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age); // Сравнение по возрасту
    }

}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("John", 25);
        Person p2 = new Person("Alice", 30);
        
        int result = p1.compareTo(p2);
        
        System.out.println(result); // Вывод: -1, так как p1 младше p2
    }
}
```
{% endtab %}
{% endtabs %}

## 2. Интерфейс **`Comparator`**

`Comparator` — это функциональный интерфейс, который позволяет определять несколько способов сравнения объектов, не изменяя их исходный класс. Он содержится в пакете `java.util` и предлагает гибкий способ сортировки объектов.

{% tabs %}
{% tab title="Метод 'int compare(T o1, T o2)'" %}
{% hint style="info" %}
**`int compare(T o1, T o2)`**
{% endhint %}

Сравнивает два объекта **`o1`** и **`o2`**. Возвращает:

* отрицательное число, если `o1` меньше чем `o2`,
* 0, если они равны,
* положительное число, если `o1` больше чем `o2`. &#x20;
{% endtab %}

{% tab title="Пример использования:" %}
```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

}

class AgeComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return Integer.compare(p1.age, p2.age);
    }
}

class NameComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.name.compareTo(p2.name);
    }
}

public class Main {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("John", 25));
        people.add(new Person("Alice", 30));

        Collections.sort(people, new AgeComparator());
        Collections.sort(people, new NameComparator());
    }
}
```
{% endtab %}

{% tab title="Приме с анонимным классом" %}
<pre class="language-java"><code class="lang-java">class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

}

Comparator&#x3C;Person> byAge = new Comparator&#x3C;Person>() {
    @Override
    public int compare(Person p1, Person p2) {
        <a data-footnote-ref href="#user-content-fn-1">return Integer.compare(p1.age, p2.age);</a>
    }
};

class NameComparator implements Comparator&#x3C;Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.name.compareTo(p2.name);
    }
}

public class Main {
    public static void main(String[] args) {
        List&#x3C;Person> people = new ArrayList&#x3C;>();
        people.add(new Person("John", 25));
        people.add(new Person("Alice", 30));

        Collections.sort(people, new AgeComparator());
        Collections.sort(people, new NameComparator());
    }
}
С анонимным классом
// Компаратор без лямбды, используя анонимный класс

</code></pre>
{% endtab %}

{% tab title="Пример использования с лямбдой:" %}

{% endtab %}
{% endtabs %}

[^1]: В методе:\
    **`compare(Person o1, Person o2)`** используется конструкция:\
    `return`` `<mark style="color:orange;">`Integer.compare(o1.age, o2.age);`</mark>\
    для сравнения двух объектов типа `Person` по полю `age`. Давайте разберем, почему именно так.\
    ![](<../.gitbook/assets/Снимок экрана 2024-09-29 в 20.30.25.png>)

    ![](<../.gitbook/assets/Снимок экрана 2024-09-29 в 20.31.12.png>)

    #### Заключение

    Таким образом, `return Integer.compare(o1.age, o2.age);` — это:

    1. Компактный способ сравнения двух целых чисел.
    2. Более безопасный и читаемый подход по сравнению с ручной реализацией через `if-else`.
    3. Принятый стандарт в Java для сравнения примитивных типов, таких как `int`.

    #### Заключение

    Таким образом, `return Integer.compare(o1.age, o2.age);` — это:

    1. Компактный способ сравнения двух целых чисел.
    2. Более безопасный и читаемый подход по сравнению с ручной реализацией через `if-else`.
    3. Принятый стандарт в Java для сравнения примитивных типов, таких как `int`.

    #### Заключение

    Таким образом, `return Integer.compare(o1.age, o2.age);` — это:

    1. Компактный способ сравнения двух целых чисел.
    2. Более безопасный и читаемый подход по сравнению с ручной реализацией через `if-else`.
    3. Принятый стандарт в Java для сравнения примитивных типов, таких как `int`.
