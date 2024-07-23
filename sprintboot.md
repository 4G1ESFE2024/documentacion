# Controlador basico en  sprint boot con las acciones de get, create, put, delete
```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/example")
public class ExampleController {

    @GetMapping
    public String getAll() {
        // Implementación para obtener todos los recursos
        return "example/list";
    }

    @GetMapping("/{id}")
    public String getOne(@PathVariable Long id) {
        // Implementación para obtener un recurso específico
        return "example/details";
    }

    @PostMapping
    public String create(@RequestBody ExampleDto dto) {
        // Implementación para crear un nuevo recurso
        return "redirect:/example";
    }

    @PutMapping("/{id}")
    public String update(@PathVariable Long id, @RequestBody ExampleDto dto) {
        // Implementación para actualizar un recurso existente
        return "redirect:/example/{id}";
    }

    @DeleteMapping("/{id}")
    public String delete(@PathVariable Long id) {
        // Implementación para eliminar un recurso
        return "redirect:/example";
    }
}
```
# Los principales atributos th que se pueden usar en Thymeleaf:

![image](https://github.com/user-attachments/assets/20b3ab20-a284-41be-b901-c939b5829cf6)


![image](https://github.com/user-attachments/assets/d7709b23-7c1c-421a-a49a-50d72f0a0a8a)

![image](https://github.com/user-attachments/assets/dc50f4e7-5e73-409b-b0d6-f4f33724409e)
![image](https://github.com/user-attachments/assets/4c88da86-13da-4850-8412-fd25ce1f8e88)
![image](https://github.com/user-attachments/assets/2ecc2f9b-d605-4d16-88d9-cc788adc4284)
![image](https://github.com/user-attachments/assets/13814774-143d-4501-b1ee-b933697f5d3d)
![image](https://github.com/user-attachments/assets/86938a6f-2242-42e6-a43e-54510a33299d)


# Enviar datos desde el controlador hacia la vista

```java

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/example")
public class ExampleController {

    @GetMapping
    public String example(Model model) {
        String message = "Hello, World!";
        model.addAttribute("message", message);
        return "example";
    }
}

```

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Example Page</title>
</head>
<body>
    <h1 th:text="${message}">Default Message</h1>
</body>
</html>
```

# Ejemplo de cómo sumar dos números en Spring Boot utilizando un controlador para recibir los datos desde la vista

En el Controlador (SumController.java):

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class SumController {

    @GetMapping("/sum")
    public String showSumForm(Model model) {
        model.addAttribute("num1", 0);
        model.addAttribute("num2", 0);
        model.addAttribute("result", 0);
        return "sum";
    }

    @PostMapping("/sum")
    public String performSum(@RequestParam("num1") int num1, @RequestParam("num2") int num2, Model model) {
        int result = num1 + num2;
        model.addAttribute("num1", num1);
        model.addAttribute("num2", num2);
        model.addAttribute("result", result);
        return "sum";
    }
}

```
En este controlador, tenemos dos métodos:

showSumForm(): Este método se invoca cuando se accede a la URL "/sum" mediante una solicitud GET. Inicializa los valores de num1, num2 y result en el modelo, y devuelve el nombre de la vista "sum".

performSum(): Este método se invoca cuando se envía el formulario de suma mediante una solicitud POST. Obtiene los valores de num1 y num2 a través de los parámetros @RequestParam, calcula el resultado de la suma y lo agrega al modelo. Luego, devuelve el nombre de la vista "sum" para mostrar los resultados.

En la Vista (sum.html):

```html

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Sum Calculator</title>
</head>
<body>
    <h1>Sum Calculator</h1>
    <form th:action="@{/sum}" method="post">
        <label for="num1">Number 1:</label>
        <input type="number" id="num1" name="num1" th:value="${num1}"><br>

        <label for="num2">Number 2:</label>
        <input type="number" id="num2" name="num2" th:value="${num2}"><br>

        <button type="submit">Calculate</button>
    </form>

    <p th:if="${result != 0}">
        The result of <span th:text="${num1}"></span> + <span th:text="${num2}"></span> is <span th:text="${result}"></span>.
    </p>
</body>
</html>

```





