### Addeding dependency for validation  and Implementing Vlidations RESTFul Service 


## in the Pon.xml add the folowing dependency

```
	***	<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-validation</artifactId>
		</dependency> ***
```

## Iplementong 

```

import java.util.Date;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;
import com.in28minutesKeyo.rest.webservices.restfulwebservices.user.UserNotFoundException;

// apply all controllers
@ControllerAdvice
@RestController
public class CustomizedresponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
	
	@ExceptionHandler(Exception.class)
	public final ResponseEntity<Object> handleAllException(Exception ex, WebRequest request) {
		
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(),
						ex.getMessage(),request.getDescription(false));
		return new ResponseEntity(exceptionResponse, HttpStatus.INTERNAL_SERVER_ERROR);	
	}	

	@ExceptionHandler(UserNotFoundException.class)
	public final ResponseEntity<Object> handleUserNotFoundException(UserNotFoundException ex, WebRequest request) {
		
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(),
						ex.getMessage(),request.getDescription(false));
		return new ResponseEntity(exceptionResponse, HttpStatus.NOT_FOUND);		
	}
	
	***  @Override
	protected ResponseEntity<Object> handleMethodArgumentNotValid(
			MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(),
				"Validationv Faild", ex.getBindingResult().toString());		
		return new ResponseEntity(exceptionResponse, HttpStatus.BAD_REQUEST);
	} ***
}

```

##  User controller Validation

```
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

@RestController
public class UserResource {

	@Autowired
	private UserDaoService  userDaoService;
	
	//GET /users
	//retieveAllUsers
	@GetMapping("/users")
	public List<User> retieveAllUsers(){
		return userDaoService.finAll();
	}
		
	//GET /users/{id}
	//retieveUser(int id)
	@GetMapping("/users/{id}")
	public User retieveUser(@PathVariable int id) {
		User user =userDaoService.findOne(id);
		
		if(user == null) {
			throw new UserNotFoundException("id"+ id);
		}
		return user;
	}
	
	//CREATED POST
	// input - details of users
	//output - CREATED & Return the created URI
	
	@PostMapping("/users")
	public ResponseEntity<Object> createUser(***@Valid *** @RequestBody User user) {
		User savedUser =  userDaoService.save(user);
		
		///CREATED  POST 2001 for created Object and return the location /4
		// /user/{id}  savedUser.getId()
		
		URI location =ServletUriComponentsBuilder
		.fromCurrentRequest()
		.path("/{id}")
		.buildAndExpand(savedUser.getId()).toUri();
		
		
		 return ResponseEntity.created(location).build();
	}
	
	
		//DELETE /users/{id}
		//DELETEUser(int id)
		@DeleteMapping("/users/{id}")
		public void  deleteUser(@PathVariable int id) {
			User user =userDaoService.deleteById(id);
			if(user == null) {
				throw new UserNotFoundException("id"+ id);
			}			
		}
		
}


```




