### Implementing GET Methods for User Resource

```
import java.util.ArrayList;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

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
}

```
