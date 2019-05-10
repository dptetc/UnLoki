# UnLoki
Swollen utility for effectively killing Java through reflections.

## What can it do?
1. Edit enums;
2. Edit modifiers;
3. Edit values;
4. And so on.

**Example 1:**
```java
EnumList editor = new EnumList(Drink.class);

editor.add("TEA", 23);
editor.add(1, "COFFEE", 42);
editor.add(0, "WHISKY", 65);
editor.remove(3);

System.out.println(Arrays.deepToString(Drink.values())); // [WHISKY, WATER, COFFEE, JUICE, TEA]

Drink juice = (Drink) editor.get(3);
System.out.println(juice); // JUICE
System.out.println(juice.ordinal()); // 3
```

```java
enum Drink {
    WATER(8),
    MILK(15),
    JUICE(16);

    private final int _price;

    Drink(Integer price) {
        this._price = price;
    }

    public int getPrice() {
        return this._price;
    }
}
```

**Example 2:**
```java
DuckBypass magic = new DuckBypass(); // Yes, it works with OpenJDK 13

magic.getValue(Enemy.class, "walrus"); // Crutch: You must turn to the field before working with it
magic.setValue(Enemy.class, "walrus", false);

Enemy.say(); // I Am the Egg Man
```

```java
class Enemy {
    public static final Boolean walrus = true;

    public static void say() {
        System.out.println(walrus ? "I Am the Walrus" : "I Am the Egg Man");
    }
}
```

## What can't it do?
- Work with primitives.
- ...and String?

## What versions of Java are supported?
Java 6 and above (including Java 12).

## Licence
Licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

## List of used information sources
1. http://java-performance.info/updating-final-and-static-final-fields/
2. https://www.niceideas.ch/roller2/badtrash/entry/java_create_enum_instances_dynamically
3. https://blog.gotofinal.com/java/diorite/breakingjava/2017/06/24/dynamic-enum.html
4. https://blog.gotofinal.com/java/breakingjava/2017/11/08/reflections-in-java-9.html
