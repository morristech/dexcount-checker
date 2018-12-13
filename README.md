# dexcount-checker
See how dex method count increases in Android coding

## So how it works

### Variables
* Normal variable doesn't increase count, for eg: `String x = 1`.
* Static final variable doesn't increase count, for eg: `static final boolean dev = false`.
* Static Non final variable increase method count by 1, for eg: `static boolean dev = false`.

### Interface class
* Interface definition doesn't increase count.
    ```
    public interface TestInterface1 {
        // No method count for this.
    }
    ```
* Interface implementation increase count by 1.
    ```
    private TestInterface1 testInterface1 = new TestInterface1() {
        // 1 method count for this.
    };
    ```
* Each method definition will increase method count by 1.
    ```
    public interface TestInterface2 {
         public void test(); // 1 method count for this.
     }
    ```

### Abstract Class
* Abstract Definition increments count by 1.
    ```
    public abstract class TestAbstract {
        // 1 method count for this.
    }
    ```
* Each method definition (abstract/non-abstract) will increase method count by 1.
    ```
    public abstract class TestAbstract1 {
         public abstract void test(); // 1 method count for this.
    }
    ```
* Each Abstract class implementation will take extra 1.
    ```
    private TestAbstract testAbstract = new TestAbstract() {
        // 1 method count for this.
    };
    ```
* Each method abstract/non-abstract overridden method will take extra 1.
    ```
    private TestAbstract1 abstract1 = new TestAbstract1() {
         @Override
         public void test() {
            // 1 method count for this.
         }
    };
    ```

     or

     ```
     private TestAbstract2 abstract2 = new TestAbstract2() {
          @Override
          public void test() {
             // This will take method count.
          }

          @Override
          public void test2() {
              super.test2();
              // This will take another method count.
          }

     };
     ```
### Regular Class
* Each class definition increase count by 1.
    ```
    public class RegularClass {
        // This will take method count.
    }

    ```
* Each method definition will increase count by 1.
    ```
    public class RegularClass1 {
        public void test() {
            // This will take method count.
        }
    }
    ```
* Empty class implementation doesn't increase count.
    ```
    // No affect.
    private RegularClass regularClass = new RegularClass();
    ```
* Non Empty (with methods) class implementation takes extra 1.
    ```
    private RegularClass1 regularClass1 = new RegularClass1() {
        // This will take method count.
    };
    ```
* Each overridden method will also increase count by 1.
    ```
    private RegularClass1 regularClass2 = new RegularClass1() {
            @Override
            public void test() {
                super.test();
                // This will take another method count.
            }
        };

    ```
    
    
## Conclusion, so far

* Avoid unnecessary new interfaces and extra methods.
* Avoid more unnecessary new abstract classes and extra methods, 
    since both definition and implementation of class and override takes extra count.
* Same for Regular class as Abstract classes.