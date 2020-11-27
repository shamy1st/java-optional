# Java Optional

### isPresent()
* we used the isPresent() method to check if there is a value inside the Optional object.
* a value is present only if we have created Optional with a non-null value.

        String str = null;
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.isPresent()); //false

        String str = "";
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.isPresent()); //true

### isEmpty()
* we can do the opposite with the isEmpty() method

        String str = null;
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.isEmpty()); //true

        String str = "";
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.isEmpty()); //false

### Optional.of() vs Optional.ofNullable()
* the argument passed to the **of()** method can't be null. Otherwise, we'll get a NullPointerException.
* but in case we expect some null values, we can use the **ofNullable()** method.

        String str = null;
        Optional<String> optional = Optional.of(str); //NullPointerException

### Condition

* instead of:

        if(name != null) {
            System.out.println(name.length());
        }

* use:

        String name = "ahmed";
        Optional<String> opt = Optional.ofNullable(name);
        opt.ifPresent(value -> System.out.println(value.length()));

### orElse()

        String maybeNull = null;
        String name = Optional.ofNullable(maybeNull).orElse("ahmed");
        System.out.println(name); //ahmed

        String maybeNull = "mohamed";
        String name = Optional.ofNullable(maybeNull).orElse("ahmed");
        System.out.println(name); //mohamed

### orElseGet()
* orElseGet() method is similar to orElse()
* however, instead of taking a value to return if the Optional value is not present
* it takes a supplier functional interface, which is invoked and returns the value of the invocation

        String maybeNull = null;
        String name = Optional.ofNullable(maybeNull).orElseGet(() -> "ahmed");
        System.out.println(name); //ahmed

        String maybeNull = "mohamed";
        String name = Optional.ofNullable(maybeNull).orElseGet(() -> "ahmed");
        System.out.println(name); //mohamed

### orElse() vs orElseGet()
* if the value presented the orElse() method is called, but orElseGet() will not.
* so, orElseGet() is more efficient.

        public class Main {
            public static String getDefaultName(String value) {
                System.out.println("call from: " + value);
                return "default-name";
            }

            public static void main(String[] args) {
                String name = "ahmed";
                String defaultName = Optional.ofNullable(name).orElseGet(() -> getDefaultName("orElseGet"));
                System.out.println(defaultName); // ahmed, getDefaultName() method not called
            }
        }

        public class Main {
            public static String getDefaultName(String value) {
                System.out.println("call from: " + value);
                return "default-name";
            }

            public static void main(String[] args) {
                String name = "ahmed";
                String defaultName = Optional.ofNullable(name).orElse(getDefaultName("orElseGet")); // call from: orElseGet
                System.out.println(defaultName); // ahmed, getDefaultName() is called
            }
        }

### orElseThrow()
* Instead of returning a default value when the wrapped value is not present, it throws an exception.

        String nullName = null;
        String name = Optional.ofNullable(nullName).orElseThrow(IllegalArgumentException::new);

* Java 10 introduced a simplified no-arg version of orElseThrow() method. 
* In case of an empty Optional it throws a NoSuchElelementException

        String nullName = null;
        String name = Optional.ofNullable(nullName).orElseThrow(); //NoSuchElementException

### get()
* return a value if the wrapped object is not null; otherwise, it throws a no such element exception

        Optional<String> opt = Optional.ofNullable(null);
        String name = opt.get(); //NoSuchElementException

### Ref
* https://www.oracle.com/technical-resources/articles/java/java8-optional.html
* https://www.baeldung.com/java-optional

