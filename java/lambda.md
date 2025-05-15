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
| Predicate     | `test()`     | 1 input, test a condition | True/False |
| Consumer      | `accept()`   | 1 input, nieko negrazina  | void |
| Supplier      | `get()`        | 1 input, 1 output         | |

- Function
- BiFunction<T, R>
- Runnable

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

### **Nuorodos**
- https://dev.to/dhanush9952/mastering-lambda-expressions-in-java-8-a-comprehensive-guide-27bf
- https://devcookies.medium.com/a-complete-guide-to-lambda-expressions-in-java-0aea2e1cea42
- https://dev.to/be11amer/mastering-java-lambdas-a-deep-dive-for-java-developers-1df
