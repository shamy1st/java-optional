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





