### Implementing HATEOAS (Hypermedia as the Engine of Application State) for RESTFUL Service 


in  POM.xml

```
	<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-hateoas</artifactId>
		</dependency>
		
```


```
import java.net.URI;
import java.util.ArrayList;
import java.util.List;
import javax.validation.Valid;
***import static org.springframework.hateoas.server.mvc.WebMvcLinkBuilder.*; ***
import org.springframework.beans.factory.annotation.Autowired;
***import org.springframework.hateoas.EntityModel;***
***import org.springframework.hateoas.server.mvc.WebMvcLinkBuilder;***
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
	public EntityModel<User> retieveUser(@PathVariable int id) {
		User user =userDaoService.findOne(id);		
		if(user == null) {
			throw new UserNotFoundException("id"+ id);
		}
	***	EntityModel<User> model = EntityModel.of(user);		
		WebMvcLinkBuilder  linkToUsers =
				linkTo(methodOn(this.getClass()).retieveAllUsers());
		
		model.add(linkToUsers.withRel("all-users"));
		return model; ***
	}
	
	//CREATED POST
	// input - details of users
	//output - CREATED & Return the created URI	
	@PostMapping("/users")
	public ResponseEntity<Object> createUser(@Valid @RequestBody User user) {
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
