### **Info**
1. Sukuriam pagrindine klase/record'a su `private final` atributais. Pvz. `Book()`.
    - kiekvienam atributui sukuriam getter'us
    - sukuriam konstruktoru `private Book()`, kurio atributas bus tik `Builder builder`, t.y.

```Java
Book(Builder builder) {
    this.title = builder.title;
}
```

2. Sukuriam klase `public static class Builder`:
    - surasom tuos pacius atributus ka praeitam punkte, su tais paciais keywords (pvz. `private`), bet ne `final`
    - kiekvienam atributui, parasom funkcija su atributo pavadinimu, bet klase turi but `Builder`.
    Papildomai, funkcija turi sugrazit ta atributa (pvz. `this.title = title`) ir `return this`
    ```Java
    public Builder title(String title) {
        this.title = title;
        return this;
    }
    ```
    - sukuriam funkcija `build()` su tipu `BookBuilder`, kuri return'uoja nauja objekta `BuilderBooks(this)`:
    ```Java
    public Book build() {
        return new Book(this);
    }
    ```
    - (optional) sukuriam konstruktoru `Builder()`

### **Pilnas kodas**
```Java
public class Book {
    private final String title;
    private final String author;

    private Book(Builder builder) {
        this.title = builder.title;
        this.author = builder.author;
    }

    public String getTitle() {
        return this.title;
    }

    public String getAuthor() {
        return this.author;
    }

    public static class Builder {
        private String title;
        private String author;

        public Builder title(String title) {
            this.title = title;
            return this;
        }

        public Builder author(String author) {
            this.author = author;
            return this;
        }

        public Book build() {
            return new Book(this);
        }
    }
}
```

### **Kada naudojamas**
    - norim sukurt objekta viena karta
    - zinom, kad objektas ir jo atributai nesikeis

### **Links**
- https://blogs.oracle.com/javamagazine/post/exploring-joshua-blochs-builder-design-pattern-in-java
