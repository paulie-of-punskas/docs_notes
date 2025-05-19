### **Back in a day (pre Java 8)**
```Java
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Labas.");
    }
};
```

### **Labiausiai paplite Functional Interfaces**
| **Interface** | **Funkcija** | **Aprasymas** | **Return** |
| ------------- | ------------ | ------------------------- | - |
| Predicate     | `test()`     | 1 argument, boolean valued function | True/False |
| Consumer      | `accept()`   | 1 argument, no result | No return, void |
| Supplier      | `get()`      | No argument, 1 result | |
| Function      | `apply()`    | 1 argument, 1 result| | |
| BiFunction<T, R> | `apply()` | 2 arguments, 1 result | |
| Runnable | | |

### **Pavyzdziai**
#### **Predicate**
```Java
Predicate<String> ss = (String s) -> s.equals("Labas");
System.out.println(ss.test("dziedas")); // false
System.out.println(ss.test("sudas")); // false
System.out.println(ss.test("Labas")); // true

Predicate<Integer> isEven = (Integer i) -> i % 2 == 0;
System.out.println(isEven.test(0)); // true
System.out.println(isEven.test(2)); // true
```

#### **Consumer**
```Java
Consumer<String> cc = message -> System.out.println(message);
cc.accept("Labas rytas is Kalabybiskiu rajono!");
System.out.println(LocalDateTime.now().getDayOfWeek());

List<String> names = Arrays.asList("John", "Freddy", "Samuel");
names.forEach(name -> System.out.println("Hello, " + name));

Map<String, Integer> ages = new HashMap<>();
ages.put("John", 25);
ages.put("Freddy", 24);
ages.put("Samuel", 30);

ages.forEach((name, age) -> System.out.println(name + " is " + age + " years old"));
```

#### **Supplier**
```Java
Supplier<Double> ss = () -> Math.random();
System.out.println(ss.get());
```

#### **Function**
```Java
Function<String, Integer> stringLength = str -> str.length();
System.out.println(stringLength.apply("Lambda")); // Output: 6
```

### **Nuorodos**
- https://dev.to/dhanush9952/mastering-lambda-expressions-in-java-8-a-comprehensive-guide-27bf
- https://devcookies.medium.com/a-complete-guide-to-lambda-expressions-in-java-0aea2e1cea42
- https://dev.to/be11amer/mastering-java-lambdas-a-deep-dive-for-java-developers-1df
