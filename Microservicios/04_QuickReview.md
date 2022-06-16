### Quick Review Spring Boot Auto Configuration and Dispacher Servlet

This happend when there are not getter in the principal class in this case HelloWorldBean

## Questions to Answer


What is Dispacher servlet?  
    - I found dispacher servlet at org.springframework.web.servlet.DispacherServlet and this is configurable as a servlet is for Spring Boot auto-configuration

who is configuration DS?
    - "Spring boot auto-configuration" in this one are all the jars which are avalible on the classpath that try diferents configurations

what does DS do?
     - Spring Boot auto Configuration 

How does the HelloWorldBean object get converted to JSON?
     -its also because of Spring boot auto configuration the message convertors and the Jacson beans are geting initialized   
     
Who is configuring the error maping? 
    - Spring Boot Auto Configuration and it create a default error page for us.
    
    
 
 
 --Mapping servlet: 'dispatcherServlet' to [/]  dispachtech servlet is handling all the request
 --DispachetServlet is a key roll,  also maping all the reques [GET,POST,PUT,DELETE, ERROR] to this method
