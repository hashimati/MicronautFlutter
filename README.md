[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/P5P411AKC)
<a href="https://www.buymeacoffee.com/hashimati"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=hashimati&button_colour=BD5FFF&font_colour=ffffff&font_family=Cookie&outline_colour=000000&coffee_colour=FFDD00"></a>
# Micronaut + Flutter Web App

A Simple demo app that demostrates configuring a Flutter Web App in a Micronaut application. 


The Basic Steps:
1. Create a flutter application
2. Enable Web 
```shell  
 flutter configu --enable-web
```
3. Build Web App 
```shell
flutter build web
```
4. Generate Micronaut Application that has Thymeleaf feature. 
5. copy index.html from the Flutter Project's build flolder to "/main/resources/views" folder of the Micronaut Project. 
6. copy the rest of the files from the Flutter Project's build flolder to "/main/resources/static" folder of the Micronaut project.
7. Create a controller that produces a view from index.html. 

```java 
package io.hashimati;


import io.micronaut.http.HttpResponse;
import io.micronaut.http.annotation.Controller;
import io.micronaut.http.annotation.Get;
import io.micronaut.views.View;

@Controller
public class IndexController {

    @View("index")
    @Get("/")
    public HttpResponse<?> index()
    {
        return HttpResponse.ok();
    }
}

```

8. Configure static resources

```yaml
micronaut:
  application:
    name: micronautFlutterService
  router:
    static-resources:
      default:
        mapping: "/**"
      '*':
        paths:
          - "classpath:static"
        enabled: true
```
9. Run the below command to launch the Micronaut app. 

```shell
gradlew clean run
```
10. open http://localhost:8080/
