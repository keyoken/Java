### Versioning RESTful Services Header amd Content Negotiation Approach 

```

package com.in28minutesKeyo.rest.webservices.restfulwebservices.versioning;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PersonVersioningController {

	@GetMapping("v1/person")
	public PersonV1  personV1() {
		return new PersonV1("keyo `"); //URi versioning
	}
	
	
	@GetMapping(value ="/person/param" , params = "version=1")
	public PersonV1  paramV1() {
		return new PersonV1("keyo `");
	}

	
	@GetMapping(value ="/person/param", params = "version=2")   //parameter versioning
	public PersonV2 paramV2() {
		return new PersonV2(new Name(" "," rojo"));
	}
	
	
	@GetMapping(value ="/person/header" , headers = "X-API-version=1")
	public PersonV1  headerV1() {
		return new PersonV1("keyo `");
	}

	
	@GetMapping(value ="/person/header", headers = "X-API-version=2") //headers versioning
	public PersonV2 headerV2() {
		return new PersonV2(new Name(" "," rojo"));
	}
	
	@GetMapping(value ="/person/produces" , produces = "application/vnd.commpany.app-v1+json")
	public PersonV1  producesV1() {
		return new PersonV1("keyo `");
	}

	
	@GetMapping(value ="/person/produces", produces = "application/vnd.commpany.app-v2+json") //Producer versioning
	public PersonV2  producesV2() {
		return new PersonV2(new Name(" "," rojo"));
	}
}




```
