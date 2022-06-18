### Implementing Dynamic filtering for RESTful service 


```

import java.util.Arrays;
import java.util.List;

import org.springframework.http.converter.json.MappingJacksonValue;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.fasterxml.jackson.databind.ser.FilterProvider;
import com.fasterxml.jackson.databind.ser.impl.SimpleBeanPropertyFilter;
import com.fasterxml.jackson.databind.ser.impl.SimpleFilterProvider;



@RestController
public class FilteringController {

	/// filed1, field2
	@GetMapping("/filtering")
***	public MappingJacksonValue retievesSomeBean() {
		SomeBean someBean = new  SomeBean("value1", "value2", "value3");		
		SimpleBeanPropertyFilter filter = SimpleBeanPropertyFilter.filterOutAllExcept("filed1", "field2");		
		FilterProvider filters = new SimpleFilterProvider().addFilter("SomeBeanFilter", filter);		
		MappingJacksonValue mapping = new  MappingJacksonValue(someBean);
		mapping.setFilters(filters);
		return mapping;
	}
	
	
	
	/// filed2, field3
	@GetMapping("/filtering")
***	public MappingJacksonValue retievesListOfSomeBeans() {
		List<SomeBean>  list = Arrays.asList(new  SomeBean("value1", "value2", "value3"),
							new  SomeBean("value12", "value22", "value32"));		
		SimpleBeanPropertyFilter filter = SimpleBeanPropertyFilter.filterOutAllExcept("filed2", "field3");
		FilterProvider filters = new SimpleFilterProvider().addFilter("SomeBeanFilter", filter);
		MappingJacksonValue mapping = new  MappingJacksonValue(list);
		mapping.setFilters(filters);		
		return mapping;***
	}
}



```


Bean class

```

package com.in28minutesKeyo.rest.webservices.restfulwebservices.filtering;

import com.fasterxml.jackson.annotation.JsonFilter;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

@JsonIgnoreProperties(value={"field2",""})
***@JsonFilter("SomeBeanFilter")***
public class SomeBean {

	private String field1;
	private String field2;
	
	//Is like not see/excluded password
	@JsonIgnore
	private String field3;
	
	public SomeBean(String field1, String field2, String field3) {
		super();
		this.field1 = field1;
		this.field2 = field2;
		this.field3 = field3;
	}

	public String getField1() {
		return field1;
	}

	public void setField1(String field1) {
		this.field1 = field1;
	}

	public String getField2() {
		return field2;
	}

	public void setField2(String field2) {
		this.field2 = field2;
	}

	public String getField3() {
		return field3;
	}

	public void setField3(String field3) {
		this.field3 = field3;
	}
	
	
	
}

```
