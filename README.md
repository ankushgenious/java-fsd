# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

1. Global Exception Handling:
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleException(Exception e) {
        // Log the exception
        return new ResponseEntity<>("An error occurred: " + e.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }

    // Add more methods for handling specific exceptions
}

2.Controller-specific Exception Handling: 

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseStatus;

@ControllerAdvice
public class MyControllerAdvice {

    @ExceptionHandler(MyCustomException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public ResponseEntity<String> handleCustomException(MyCustomException e) {
        // Log the exception
        return new ResponseEntity<>("Bad request: " + e.getMessage(), HttpStatus.BAD_REQUEST);
    }
}

3. Custom Exception Classes:

public class MyCustomException extends RuntimeException {
    public MyCustomException(String message) {
        super(message);
    }
}
4. Use @ResponseStatus:
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

5. Handle Validation Errors:
@ExceptionHandler(MethodArgumentNotValidException.class)
@ResponseStatus(HttpStatus.BAD_REQUEST)
public ResponseEntity<String> handleValidationException(MethodArgumentNotValidException e) {
    // Log the exception
    return new ResponseEntity<>("Validation error: " + e.getMessage(), HttpStatus.BAD_REQUEST);
}

6. Error Responses:
public class ErrorResponse {
    private String message;
    private int status;

    // Constructors, getters, setters
}
In your exception handler methods:
@ExceptionHandler(MyCustomException.class)
@ResponseStatus(HttpStatus.BAD_REQUEST)
public ResponseEntity<ErrorResponse> handleCustomException(MyCustomException e) {
    // Log the exception
    ErrorResponse errorResponse = new ErrorResponse(e.getMessage(), HttpStatus.BAD_REQUEST.value());
    return new ResponseEntity<>(errorResponse, HttpStatus.BAD_REQUEST);
}


#  Practice-Project 2
Step 1: Create a new Spring Boot Project
Step 2: Create a Model Class
public class User {
    private Long id;
    private String name;
    private String username;
    // getters and setters
}
Step 3: Create a Service to Consume the RESTful Web Service
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class UserService {

    private final String apiUrl = "https://jsonplaceholder.typicode.com/users";

    private final RestTemplate restTemplate;

    public UserService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public User getUserById(Long userId) {
        String url = apiUrl + "/" + userId;
        return restTemplate.getForObject(url, User.class);
    }
}
Step 4: Create a Controller
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users/{userId}")
    public User getUser(@PathVariable Long userId) {
        return userService.getUserById(userId);
    }
}
Step 5: Configure RestTemplate
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class AppConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
Step 6: Run your Application
Run your Spring Boot application, and it will expose an endpoint like http://localhost:8080/users/{userId}. You can make requests to this endpoint, and it will consume the RESTful web service and return the data.



# Practice Project 3

Step 1: Create a Spring Boot Project
https://start.spring.io/
Step 2: Create a File Storage Configuration
import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties(prefix = "file")
public class FileStorageProperties {

    private String uploadDir;

    public String getUploadDir() {
        return uploadDir;
    }

    public void setUploadDir(String uploadDir) {
        this.uploadDir = uploadDir;
    }
}
Step 3: Implement File Storage Service
import org.springframework.core.io.Resource;
import org.springframework.web.multipart.MultipartFile;

public interface FileStorageService {

    String storeFile(MultipartFile file);

    Resource loadFile(String fileName);
}
import org.springframework.core.io.Resource;
import org.springframework.core.io.UrlResource;
import org.springframework.stereotype.Service;
import org.springframework.util.StringUtils;
import org.springframework.web.multipart.MultipartFile;

import java.io.IOException;
import java.net.MalformedURLException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Objects;

@Service
public class FileStorageServiceImpl implements FileStorageService {

    private final Path fileStorageLocation;

    public FileStorageServiceImpl(FileStorageProperties fileStorageProperties) {
        this.fileStorageLocation = Paths.get(fileStorageProperties.getUploadDir())
                .toAbsolutePath().normalize();

        try {
            Files.createDirectories(this.fileStorageLocation);
        } catch (Exception ex) {
            throw new RuntimeException("Could not create the directory to upload files!", ex);
        }
    }

    @Override
    public String storeFile(MultipartFile file) {
        String fileName = StringUtils.cleanPath(Objects.requireNonNull(file.getOriginalFilename()));

        try {
            Path targetLocation = this.fileStorageLocation.resolve(fileName);
            Files.copy(file.getInputStream(), targetLocation);

            return fileName;
        } catch (IOException ex) {
            throw new RuntimeException("Could not store file " + fileName + ". Please try again!", ex);
        }
    }

    @Override
    public Resource loadFile(String fileName) {
        try {
            Path filePath = this.fileStorageLocation.resolve(fileName).normalize();
            Resource resource = new UrlResource(filePath.toUri());

            if (resource.exists()) {
                return resource;
            } else {
                throw new RuntimeException("File not found " + fileName);
            }
        } catch (MalformedURLException ex) {
            throw new RuntimeException("File not found " + fileName, ex);
        }
    }
}
Step 4: Create Controller for File Upload and Download
import org.springframework.core.io.Resource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

@Controller
@RequestMapping("/files")
public class FileController {

    private final FileStorageService fileStorageService;

    public FileController(FileStorageService fileStorageService) {
        this.fileStorageService = fileStorageService;
    }

    @PostMapping("/upload")
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        String fileName = fileStorageService.storeFile(file);
        return "redirect:/files/" + fileName;
    }

    @GetMapping("/{fileName:.+}")
    public ResponseEntity<Resource> downloadFile(@PathVariable String fileName) {
        Resource resource = fileStorageService.loadFile(fileName);

        return ResponseEntity.ok()
                .contentType(MediaType.parseMediaType("application/octet-stream"))
                .header(HttpHeaders.CONTENT_DISPOSITION, "attachment; filename=\"" + resource.getFilename() + "\"")
                .body(resource);
    }
}
Step 5: Configure File Storage Properties
file.upload-dir=uploads
Step 6: Create Thymeleaf Template for File Upload
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>File Upload</title>
</head>
<body>

<h2>File Upload</h2>

<form th:action="@{/files/upload}" method="post" enctype="multipart/form-data">
    <input type="file" name="file"/>
    <button type="submit">Upload</button>
</form>

</body>
</html>
Step 7: Run Your Application
Run your Spring Boot application. You can access the file upload form at http://localhost:8080/upload.

# practice project : 4
Option A: Using a Self-signed Certificate (For Testing Only)
keytool -genkeypair -alias myapp -keyalg RSA -keysize 2048 -keystore your_keystore_name.jks -validity 3650
Step 2: Configure Spring Boot for HTTPS
server.port=8443
server.ssl.key-store=classpath:your_keystore_name.jks
server.ssl.key-store-password=your_keystore_password
server.ssl.key-password=your_key_password

Step 3: Create a Controller to Display a Page
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "home";
    }
}
Step 4: Create a Thymeleaf Template
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Spring Boot HTTPS Example</title>
</head>
<body>

<h2>Hello, HTTPS!</h2>

</body>
</html>

Step 5: Run Your Application
Run your Spring Boot application, and it will be accessible over HTTPS at https://localhost:8080
