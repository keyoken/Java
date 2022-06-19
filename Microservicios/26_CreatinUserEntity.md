### Creating User Entiy and some test data 



Application propeerties
```
loggging.level.org.springframework = debug
spring.jackson.serialization.write-dates-as-timestamps= false
management.endpoints.web.exposure.include=*
spirng.security.user.name=username
spring.security.user.password=password



spring.datasource.url=jdbc:h2:mem:testdb;NON_KEYWORDS=USER
sprint.h2.console.enabled=true
sprint.jpa.defer-datasource-initialization=true
sprint.data.jpa-repositories.bootstrap-mode=default

***
spring.jpa.show-sql=true
spring.h2.console.enabled=true
***


```

Pom.xml

```
	<!-- H2 -->
		
		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
			<scope>runtime</scope>
		</dependency>
```



Bean Uaer

```

package com.in28minutesKeyo.rest.webservices.restfulwebservices.user;

import java.util.Date;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.validation.constraints.Past;
import javax.validation.constraints.Size;

//@ApiModel(description="all details about the user")
***@Entity***
public class User {

	***@Id
	@GeneratedValue ***
	private Integer id;
	
	@Size(min=2, message ="Name should have atleas 2 characters")
	//@ApiModelProperty(notes="Name should have atleas 2 characters")
	private String name;
	
	@Past
	//@ApiModelProperty(notes="date sould be in the past")
	private Date birthDate;
			
	protected User() {
	}
	
	public User(Integer id, String name, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.birthDate = birthDate;
	}
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public Date getBirthDate() {
		return birthDate;
	}
	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}
	@Override
	public String toString() {
		return "User [id=" + id + ", name=" + name + ", birthDate=" + birthDate + "]";
	}
}

```


