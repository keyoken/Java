### Versioning RESTful Services Basic Approacha with URis


Beans

```
package com.in28minutesKeyo.rest.webservices.restfulwebservices.versioning;

public class PersonV1 {
	
	private String name;

	
	public PersonV1() {
		super();
	}


	public PersonV1(String name) {
		super();
		this.name = name;
	}


	public String getName() {
		return name;
	}


	public void setName(String name) {
		this.name = name;
	}
}

```

Bean

```
package com.in28minutesKeyo.rest.webservices.restfulwebservices.versioning;

public class PersonV2 {
	
	private Name name ;
	
	

	public PersonV2() {
		super();
	}

	public PersonV2(Name name) {
		super();
		this.name = name;
	}

	public Name getName() {
		return name;
	}

	public void setName(Name name) {
		this.name = name;
	}
	
}


```

Bean 

```
package com.in28minutesKeyo.rest.webservices.restfulwebservices.versioning;

public class Name {

	private String firstName;
	private String lastName;
	
	
	
	public Name() {
		super();
		
	}
	
	public Name(String firstName, String lastName) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
	}
	public String getFirstName() {
		return firstName;
	}
	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
	
}


```


Controller

```

package com.in28minutesKeyo.rest.webservices.restfulwebservices.versioning;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PersonVersioningController {

	@GetMapping("v1/person")
	public PersonV1  personV1() {
		return new PersonV1("keyo `");
	}
	
	@GetMapping("v2/person")
	public PersonV2 personV2() {
		return new PersonV2(new Name(" "," rojo"));
	}
}

```
