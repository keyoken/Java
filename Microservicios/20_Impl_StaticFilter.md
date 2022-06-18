### Implementing Static filtring for Rest ful Service 

This is like static filter in the Bean

```
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

@JsonIgnoreProperties(value={"field2",""})
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



 ### This the Controller 

```

import java.util.Arrays;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;



@RestController
public class FilteringController {

	@GetMapping("/filtering")
	public SomeBean retievesSomeBean() {
		return new  SomeBean("value1", "value2", "value3");
	}
	
	@GetMapping("/filtering")
	public List<SomeBean> retievesListOfSomeBeans() {
		return Arrays.asList(new  SomeBean("value1", "value2", "value3"),
							new  SomeBean("value12", "value22", "value32"));
	}
}

```
