# Java and SpringBoot

## What is Java
- Java is a high-level, strongly typed object-oriented programming (OOP) language
- Java is Platform Independent. WORA (write once, run anywhere). It is also a compiled and interpreted language
- Unlike C which compile to binary and can only excute code for a particular machine, Java convert code into Java Bytecode and sent to Java Virtual mechine which resides in the RAM of any operating system. JMV recognizes its platform and convert that bytecode into that platform native machine code

## What is JRE / JDK / JVM?
- JVM (Java Virtual Machine): Enables a computer to run Java programs. It essentially behaves like an interpreter or just-in-time compiler (JIT) which takes bytecode and translate it to something the computer can understand.
	- We have different implementations of the JVM for different operating systems: Linux, Windows, Mac, etc..
	- The important thing to take away from this is that this allows you to run the same bytecode on any operating system (platform independence)
- JRE (Java runtime environment): Contains the JVM and core libraries that our code may be calling and using. If the only thing we need to do is run Java programs, all we need to install is the JRE.
- JDK (Java development kit): contains the JRE (which of course contains the JVM) + developer tools like the compiler (javac), debugger, documentation tools (javadoc), and other command-line utilities

## What are annotations?
- Provide the extra information of a method source code
- Ex: @override (override a method with the same name from a parent class)

## Java Collection
Map is not inherit from Collection interface, but it is a Java collection also
![Screenshot]\([https://i.ytimg.com/vi/gtBS7HKfy-k/maxresdefault.jpg](https://facingissuesonitcom.files.wordpress.com/2019/07/java-collection-framework-hierarchy.jpg?w=1024)) 

# Maven
## What is Maven?
- Maven is a dependency manager and build automation tool for Java programs. Maven project configuration and dependencies are handled using the Project Object Model, which is defined in a file called the `pom.xml` file

## Where does Maven retrieve dependencies from?
- Maven retrieve its dependencies from a Maven repository
- 3 type of Maven repositories: Local, Central, Remote
  - Local – Folder location on the local Dev machine. The default local repository is located at  C:\Users\<User_Name>\.m2 (indow). Custom Local Repository in .m2/settings.xml
  - Central – Repository provided by Maven community
  - Remote – Organization owned custom repository
  
  # Spring
  
  ## What is Spring
- Spring an umbrella term for a family of frameworks which can be utilized to rapidly create loosely coupled Java applications (lossly coupled = low or weak coupling: two or more hardware and software components are attached or linked together to provide two services that are not dependent on one another)
- Spring start out as an inversion of control container for Java(IoC Container)
- Spring enables developers to build java applications utilizing a POJO design pattern, and applying enterprises services, as needed.

  ##  What is IOC and what does the IOC Container do?
- IoC stands for Inversion of Control. It is a principle which is all about inverting the control to achieve loose coupling between classes. It implemented using DI - Dependency injection
- IOC Container is a framework used to manage automatic dependency injection throughout the application without creating them
- We cannot achieve loosely coupled classes by using IoC alone. Along with IoC, we also need to use DIP, DI and IoC container.
- Process: Tigtly Coupled Class -> Implement IoC using Factory Pattern -> Implement DIP by creating abstraction -> Implement DI -> Use IoC Container -> Loosely Coupled classes
- Note: it is used together with DIP, Dependency Inversion Principle, the 5th one fron SOLID OOP design principle which states that states that the high-level module must not depend on the low-level module, but they should depend on abstractions.
	- Principle: IoC, PIP
	- Pattern: DI
	- Framwork: IoC Container
  
  ##  What are Spring Projects and Spring Modules? 
https://springtutorials.com/spring-ecosystem/
- Before Spring 3 came out, the entire Spring Framework can be download as one big jar. But then they stop that because of the module conflict of different jars version
- **Spring Project**:
	- Developed on top of Spring Framework
	- Contains 1 or more module
	- A Spring project will bring all its dependency together
	- Ex: Spring Boot, Spring Cloud, Spring Security, Spring Data, Spring LDAP, Spring Web Flow
- **Spring Module**:
	- It is the building blocks of Spring project and Framework. It exists from day 1
	- A Spring Module is a complete and independent feature with minimal dependency on other external libraries and projects
	- Ex: Spring JDBC, Spring Web, and Spring MVC, Spring AOP
  
  ## What is dependency injection and what are some of the benefits of using dependency injection?
- Dependency injection is a design pattern which implements the IoC principle to invert the creation of dependent objects. It sharing one single object across the application

  ## What is Spring Bean
- It is a POJO that managed by the Spring IoC container

  # Spring Boot
- Spring Boot is one of the most popular framework to develop microservices today. Spring Boot makes it easy to develop applications quickly
## Boot?
- Come from Bootstrap, means self-starting

## What's in SpringBoot
- SpringBoot is an extension of Spring Framework
- Automatic configuration
- Starter dependency
- CLI
- Actuator

##  How is Spring Boot different from legacy Spring applications? What does it mean that it is opinionated?
- **Spring Boot** is an extension of the Spring framework, which eliminates the boilerplate configurations required for setting up a Spring application
- Spring Boot takes an opinionated view of the Spring platform, which paves the way for a faster and more efficient development ecosystem
- **Unlike Spring**, Spring Boot requires only 1 dependency to get a web application running. That is the spring-boot-starter-web from org.springframework.boot
- **Spring Boot opinionate** because it follows the opinionated default configuration that reduces developer efforts to configure the application
    
##  What does convention over configuration mean?
- Convention over configuration is a software design paradigm which is used by many modern software frameworks that attempts to decrease the number of decisions that a developer can made without necessarily losing flexibility
- It takes a lot of burden away from developers
    
##  What annotation would you use for Spring Boot apps? What does it do behind the scenes?
- For all Spring Core Spring MVC Spring Boot annotation: https://www.javatpoint.com/spring-boot-annotations
- **@SpringBootApplication**: It is the combination of 3 annotation: @EnableAutoConfiguration, @ComponentScan and @Configuration
- @SpringBootConfiguration: replace @Configuration and annotate the class as a SpringBoot configuration
- @EnableAutoConfiguration: a Spring Boot Annotation, enable the application to add the beans using classpath definitions. You can tell Spring to disable certain auto-configuration classes.  (i.e.  ```@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})``` )
- @ComponentScan: This annotation tells the spring to look for where the bean is and inject it, configurations and services in the specified path.
- When using Spring MVC, we have to configure these ourself: component scan, dispatcher servlet, view resolver, web jars, others

## How to mark a class as a bean so the IOC  can inject it
- @Component (@Service, @Configuration, and @Controller are meta-annotations of @Component)
- @Repository (use for database access layer)
- @Bean is a **method level** annotation. It tells that a method produces a bean to be managed by the Spring container
- Ex of @Bean:
```
@Configuration
public class HelloWorld {
    @Bean
    public TweetUserSevice tweetUserSevice() {
        return new TweetUserSeviceImpl();
    }      
}
```
##  What is the significance of the Spring Boot starter POM?
- SpringBoot uses convention over configuration. It takes away some choices at first but save time for developers. Developers can always override the undesired configuration later
- All Spring Boot projects use spring-boot-starter-parent as a parent in pom.xml file
- The spring-boot-starter-parent is a special starter that provides useful Maven defaults. It also provides a dependency-management section so that you can omit version tags for “blessed” dependencies.
- Ex:
```
dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

## SpringBoot project diagram
![Screenshot]\(https://i.ytimg.com/vi/gtBS7HKfy-k/maxresdefault.jpg) 






