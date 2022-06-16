### Enhancing the Hello World with Palt Variable 



```
//hello-world-bean/path-variable/in28Minutes

@GetMapping(path = "/hello-world/path-variable/{name}")
 public HelloWorldBean helloWorldPathVariable(@PathVariable String name) {
			return new  HelloWorldBean (String.format("Hello World, %s", name));
		}    
    
```    
