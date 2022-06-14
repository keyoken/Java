### Code

## 03_Hello-World.java

```
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

//Controller
@RestController 
public class HelloWorldController {

	//GET
	//URL  /hello-world
	//Method - "hello world"
	//@RequestMapping(method=RequestMethod.GET, path= "/hello-world")

@GetMapping(path = "/hello-world")
	public String helloWorld() {
		return "Hello World";
	}
	
}

```


## 04_Enhancing Hello-World Service to return Bean

```

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

//Controller
@RestController 
public class HelloWorldController {

	//GET
	//URL  /hello-world
	//Method - "hello world"
	//@RequestMapping(method=RequestMethod.GET, path= "/hello-world")	
  @GetMapping(path = "/hello-world")
	public String helloWorld() {
		return "Hello World";
	}
	
	//hello-world-bean  
  @GetMapping(path = "/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		return new  HelloWorldBean ("Hello World");
	}
}



///Using a Bean Constructor
package com.in28minutesKeyo.rest.webservices.restfulwebservices;

public class HelloWorldBean {
	private String message;
	public HelloWorldBean(String message) {
		// TODO Auto-generated constructor stub
		this.message = message;
	}
  public String getMessage() {
		return message;
	}
  public void setMessage(String message) {
		this.message = message;
	}
	@Override
	public String toString() {
		return "HelloWorldBean [message=" + message + "]";
	}
}


```
