# RestAssured_API_Framework

# REST API Testing with RestAssured

## 📌 Introduction
This guide will help you set up a **REST API Testing Framework** using **RestAssured in Java**. The framework covers end-to-end API testing scenarios, including **GET, POST, PUT, DELETE** operations, JSON validation, and CI/CD integration.

---

## 📂 Project Structure
```
API-Testing-RestAssured/
│-- src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── com/api/base/BaseTest.java
│   │   │   ├── com/api/tests/GetRequestTest.java
│   │   │   ├── com/api/tests/PostRequestTest.java
│   │   │   ├── com/api/tests/PutRequestTest.java
│   │   │   ├── com/api/tests/DeleteRequestTest.java
│   │   │   ├── com/api/utils/ConfigReader.java
│   ├── resources/
│   │   ├── config.properties
│   ├── test/
│   │   ├── java/
│-- pom.xml
│-- testng.xml
```

---

## 🚀 Setup Instructions
### 1️⃣ Prerequisites
Ensure you have the following installed:
- **Java JDK (11 or later)**
- **Maven**
- **RestAssured**
- **TestNG**

---

### 2️⃣ Clone the Repository
```sh
git clone https://github.com/YourRepo/API-Testing-RestAssured.git
cd API-Testing-RestAssured
```

---

### 3️⃣ Add Dependencies to `pom.xml`
```xml
<dependencies>
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <version>4.4.0</version>
    </dependency>
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.4.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

### 4️⃣ Base Test Setup
```java
package com.api.base;

import io.restassured.RestAssured;
import org.testng.annotations.BeforeClass;
import java.util.Properties;
import com.api.utils.ConfigReader;

public class BaseTest {
    static Properties properties = ConfigReader.getProperties();

    @BeforeClass
    public static void setup() {
        RestAssured.baseURI = properties.getProperty("baseURI");
    }
}
```

---

### 5️⃣ Implementing API Tests
#### **GET Request Test**
```java
package com.api.tests;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.Test;

public class GetRequestTest {
    @Test
    public void testGetRequest() {
        Response response = RestAssured.get("/users");
        Assert.assertEquals(response.getStatusCode(), 200);
    }
}
```

#### **POST Request Test**
```java
package com.api.tests;

import io.restassured.RestAssured;
import io.restassured.http.ContentType;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.Test;
import java.util.HashMap;
import java.util.Map;

public class PostRequestTest {
    @Test
    public void testPostRequest() {
        Map<String, Object> requestBody = new HashMap<>();
        requestBody.put("name", "John Doe");
        requestBody.put("job", "Software Engineer");

        Response response = RestAssured.given()
            .contentType(ContentType.JSON)
            .body(requestBody)
            .post("/users");
        
        Assert.assertEquals(response.getStatusCode(), 201);
    }
}
```

#### **PUT Request Test**
```java
package com.api.tests;

import io.restassured.RestAssured;
import io.restassured.http.ContentType;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.Test;
import java.util.HashMap;
import java.util.Map;

public class PutRequestTest {
    @Test
    public void testPutRequest() {
        Map<String, Object> requestBody = new HashMap<>();
        requestBody.put("name", "John Doe");
        requestBody.put("job", "Tech Lead");

        Response response = RestAssured.given()
            .contentType(ContentType.JSON)
            .body(requestBody)
            .put("/users/2");
        
        Assert.assertEquals(response.getStatusCode(), 200);
    }
}
```

#### **DELETE Request Test**
```java
package com.api.tests;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.testng.Assert;
import org.testng.annotations.Test;

public class DeleteRequestTest {
    @Test
    public void testDeleteRequest() {
        Response response = RestAssured.delete("/users/2");
        Assert.assertEquals(response.getStatusCode(), 204);
    }
}
```

---

### 6️⃣ Running Tests with TestNG
Execute the tests using:
```sh
mvn test
```
OR run the **`testng.xml`** file:
```xml
<suite name="API Test Suite">
    <test name="API Tests">
        <classes>
            <class name="com.api.tests.GetRequestTest"/>
            <class name="com.api.tests.PostRequestTest"/>
            <class name="com.api.tests.PutRequestTest"/>
            <class name="com.api.tests.DeleteRequestTest"/>
        </classes>
    </test>
</suite>
```

---

## 🎯 Conclusion
Congratulations! 🎉 You have successfully set up an **API Testing Framework with RestAssured**. This framework allows you to validate REST API responses efficiently and integrate it with CI/CD pipelines. 🚀

📫 Feel free to **contribute, improve, and customize** this framework for your needs!
