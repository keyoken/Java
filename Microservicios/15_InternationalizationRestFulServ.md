### Internationalization for RESTful Services


```
import java.util.Locale;
import org.apache.logging.log4j.message.Message;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.MessageSource;
import org.springframework.context.i18n.LocaleContextHolder;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestHeader;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

//Controller
@RestController 
public class HelloWorldController {

	
***	@Autowired
	private MessageSource messageSource; ***
	
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
	
	//hello-world-bean/path-variable/in28Minutes
		@GetMapping(path = "/hello-world/path-variable/{name}")
		public HelloWorldBean helloWorldPathVariable(@PathVariable String name) {
			return new  HelloWorldBean (String.format("Hello World, %s", name));
		}
		

	***	@GetMapping(path = "/hello-world-Internationalized")
		public String helloWorldInternationalized(
			//@RequestHeader(name ="Acept-Languaje", required= false) Locale locale
				) {
			
			return messageSource.getMessage("good.morning.message", null, "Default message",
					//locale);
					LocaleContextHolder.getLocale());
			//return "Hello World";
		}***
		
}

```



