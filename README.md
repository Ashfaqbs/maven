## Types of Jar's Created When Springboot : 

Executable JAR (Fat JAR or Uber JAR): This JAR contains not only your application code but also all the dependencies (like Spring Web, Apache POI, etc.). Maven packages all the required libraries inside the JAR, making it self-contained. In this case, when you run the JAR, you don't need to worry about external paths for dependencies because everything is bundled within the JAR. This is common in Spring Boot projects when you use the spring-boot-maven-plugin.

To generate this type of JAR, you typically use the following command:
```
mvn clean package

```

Standard JAR: This only contains your application's compiled classes and resources but not the dependencies. When you run this JAR, the external libraries (like Spring Web and Apache POI) must be available on the classpath, typically provided as part of a dependency directory or some other external path. This approach requires you to manage the dependencies separately.

What Happens with Your Libraries:
Executable JAR (Fat JAR): When you build the project with Maven and use the Spring Boot plugin, both the Spring Web and Apache POI dependencies will be included inside your application's JAR file. No need to refer to any external paths at runtime.

Standard JAR: If you're creating just the application JAR (without dependencies), you'll need to ensure that your external dependencies (Spring Web, Apache POI) are available in the classpath when running the application. This is less common in modern Spring Boot applications since the goal is often to make the JAR self-sufficient.

If you are using a Spring Boot Maven setup, it's very likely that you're creating an executable JAR (fat JAR) by default, meaning your dependencies will be inside your application JAR.

To check, look at your pom.xml for something like this:
```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>

```
This ensures your app will be packaged as an executable JAR with all dependencies included.

Key Points:
Fat JAR: Includes dependencies (Spring Web, Apache POI).
Standard JAR: Needs external dependencies at runtime.


## Just Maven : 
To make your Maven JAR into a fat JAR (which includes all dependencies like Spring Web and Apache POI), you'll need to configure your pom.xml to use the spring-boot-maven-plugin. This plugin packages your application and all its dependencies into a single JAR, so you can run the JAR without needing external libraries.

Here’s how to configure it:

Step-by-Step Process to Create a Fat JAR:
Ensure spring-boot-maven-plugin is in your pom.xml: Add or update the <build> section in your pom.xml to include the Spring Boot Maven plugin, which will package everything into a fat JAR.

```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <version>3.0.0</version> <!-- Use the correct version for your project -->
            <executions>
                <execution>
                    <goals>
                        <goal>repackage</goal> <!-- This will create the fat JAR -->
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

```

Make sure your dependencies are properly declared: In the <dependencies> section of your pom.xml, ensure that all the libraries (like Spring Web, Apache POI) are listed. This ensures they get included in the final JAR.

```
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>5.2.3</version> <!-- Example version -->
    </dependency>
</dependencies>

```

Build the project: Once the pom.xml is configured, you can build the fat JAR by running the following Maven command in the terminal and run the jar post build:
```
mvn clean package

```
