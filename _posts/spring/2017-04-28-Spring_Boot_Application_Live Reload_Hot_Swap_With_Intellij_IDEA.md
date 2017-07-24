---
layout: post
comments: true
categories: spring
---


## Spring Boot Application Live Reload (Hot Swap) With Intellij IDEA
While developing Spring Boot Applications using Intellij IDEA, it was so annoying to restart the Spring Boot app after each and every change. Spring Boot provides live reload (hot swap) of application out of the box using the following dependency.
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```


But it didn't live reload the application/container, and the hot deployment didn't work for changes. Further researching found that following changes needed to be done in order the hot deployment to be worked correctly.

1. Open the Settings --> Build-Execution-Deployment --> Compiler

    and enable the Make Project Automatically.

2. Then press ctrl+shift+A and search for the registry. In the registry, make the following configuration enabled.

```
compiler.automake.allow.when.app.running
```

3. Reload Static content (html, css, js)

Add this configuration to your Spring Boot Maven Plugin:

```
<configuration>
    <addResources>true</addResources>
</configuration>
```


4. Restart the IDE.


That's it! Now the hot deployment works, and you don't have to restart manually after each and every change.