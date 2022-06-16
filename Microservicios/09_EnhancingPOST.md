### Enhancing POST method to return correct HTTP status and location

```
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
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
		return userDaoService.findOne(id);
	}
	
	//CREATED POST
	// input - details of users
	//output - CREATED & Return the created URI
	
	@PostMapping("/users")
	public ResponseEntity<Object> createUser(@RequestBody User user) {
		User savedUser =  userDaoService.save(user);
		
	***	///CREATED  POST 2001 for created Object and return the location /4
		// /user/{id}  savedUser.getId()
		
		URI location =ServletUriComponentsBuilder
		  .fromCurrentRequest()
		  .path("/{id}")
		  .buildAndExpand(savedUser.getId()).toUri();		
		
		 return ResponseEntity
      .created(location).build();  ***
	}
}
```
