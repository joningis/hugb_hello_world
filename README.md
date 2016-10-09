hugb_hello_world
================
(T-303-HUGB, Hugbúnaðarfræði, 2016-3)

Sample program used to show students Gradle in action.


What was done
===========

####NOTE: I used gradle 3.1 in the lecture.

## Create project


- Git clone hugb_hello_world project
- Run ``` gradle init --type java-library ``` to create basic folder structure.
- Run ``` gradle check ``` to check if everything is working as it should.

## Project content


- **build.gradle** (The gradle build file that we use)
- **gradle** (Folder containing the gradle wrapper)
- **gradlew** (Linux/Unix script to run the gradle wrapper)
- **gradlew.bat** (Windows script to run the gradle wrapper)
- **settings.gradle** (Settings file for gradle, not used in our example, can for example contain definitions if we have multiple projects)
- **src** (Source folder for our code)


## Show basic gradle tasks

- Checkout list of gradle tasks (```./gradlew tasks``` if we use the wrapper,  ```gradle tasks``` if using the gradle install on the machine)

## Create basic code

- Navigate to src/main/java and delete Library.java (just a demo file that we do not use)
- Navigate to scr/test/java and delete LibraryTest.java.
- Create folders for code under src/main/java (```mkdir -p com/bangsapabbi/helloworld```)
- Navigate to the new folder and create HelloWorld.java

```java
package com.bangsapabbi.helloworld;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world");
    }
}
```

- Check if everything builds.
- Add the **application plugin*** to run the program.

```java
apply plugin: 'application'

mainClassName = "com.bangsapabbi.helloworld.HelloWorld"
```

- Extract the "Hello World!" message to **World** class to be able to show basic unit tests.

```java
package com.bangsapabbi.helloworld;

public class HelloWorld {
    public static void main(String[] args) {
        World world = new World();
        System.out.println(world.greet());
    }
}
```

```java
package com.bangsapabbi.helloworld;

public class World {
    public String greet() {
        return "Hello world!";
    }
}
```


## Testing

- Navigate to src/test/java 
- Create folder structure (```mkdir -p com/bangsapabbi/helloworld```)
- Add **WorldTest.java** file.

```java
package com.bangsapabbi.helloworld;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class WorldTest {

    @Test
    public void greetResultsInHello() {
        World world = new World();
        assertEquals("Hello world!", world.greet());
    }

}
```



- Run tests using ``` gradle test ```
- Change test and see the build fail.
- Open ```build/reports/test``` to view detailed test report.


## bin folder
- Create bin folder
- Create clean script
- chmod +x on the clean file.

```bash
#!/bin/bash

./gradlew clean
```



## Gson (Not part of the project in git)
- Goto http://search.maven.org/
- Search for gson
- Click the version number
- Here we can find the dependency string that we need.
```groovy
compile 'com.google.code.gson:gson:2.3'
```

### Refactoring World class to include gson output.
```
package com.bangsapabbi.helloworld;

import com.google.gson.Gson;

public class World {

    private String greeting = "Hello world!";

    public String greet() {
        return greeting;
    }

    public String jsonGreet() {
        return new Gson().toJson(this);
    }
}
```

- Add the following line to ***HelloWorld.java*** to output json.

```
System.out.println(world.jsonGreet());

```

