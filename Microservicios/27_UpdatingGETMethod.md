### Updating GET Methods on BEAN User Resource to use JPA


Bean UserJPA Repo


```
package com.in28minutesKeyo.rest.webservices.restfulwebservices.user;

import java.net.URI;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import javax.validation.Valid;

import static org.springframework.hateoas.server.mvc.WebMvcLinkBuilder.*;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.hateoas.EntityModel;
import org.springframework.hateoas.server.mvc.WebMvcLinkBuilder;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

@RestController
public class UserJPAResource {

	
	@Autowired
	private UserDaoService  userDaoService;
	
	***@Autowired
	private UserRepository userRepository; ***
	
	
	//GET /users
	//retieveAllUsers
	@GetMapping("/jpa/users")
	public List<User> retieveAllUsers(){
***		return userRepository.findAll();***
	}
		
	//GET /users/{id}
	//retieveUser(int id)
	@GetMapping("/jpa/users/{id}")
	public EntityModel<User> retieveUser(@PathVariable int id) {
		***Optional<User> user = userRepository.findById(id);
		
		if(!user.isPresent()) {
			throw new UserNotFoundException("id"+ id);
		}
		EntityModel<User> model = EntityModel.of(user.get());
		
		WebMvcLinkBuilder  linkToUsers =
				linkTo(methodOn(this.getClass()).retieveAllUsers());
		
		model.add(linkToUsers.withRel("all-users"));
		return model;
	}***
	
	//CREATED POST
	// input - details of users
	//output - CREATED & Return the created URI
	
	@PostMapping("/jpa/users")
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
		@DeleteMapping("/jpa/users/{id}")
		public void  deleteUser(@PathVariable int id) {
			User user =userDaoService.deleteById(id);
			if(user == null) {
				throw new UserNotFoundException("id"+ id);
			}			
		}
}


```
