## O que é REST?

REpresentational State Transfer (REST) é um modelo arquiteturial (especificação) utilizado para comunicação entre componentes de softwares via web, como APIs. Entre as vantagens de desenvolver utilzando a especifação REST, são:

- Seperação entre cliente (consumidor) e servidor (provedor).
- Escalabilidade;
- Independência de linguagem e plataforma.
- Geralmente simples e intuitivo de utilizar.

### Melhores praticas (Constrains)

- Cliente-servidor
- Stateless (sem estado/sessão)
    - Exemplo: o servidor não pode guadar a sessão do usuário, sendo necessário autenticar o usuário a cada requisição
- Cache
- Interface uniforme (URI)
- Repostas de requisições (reponse) uniformes
- Sistemas em camadas
- Código sob demanda (opcional e pouco utilizada)


### RESTFul

É o termo utilizado para softwares (APIs) que seguem estritamente todas as constrains descritas na arquitetura REST

### URI

Significa Uniform Resource Identifier e serve para identificar recursos na aplicação, por exemplo: //localhost:8080/users/1, que identificar o usuário de id 1. A URI é um tipo de URL (Uniform Resource Location) que além de localizar, identifica.

### @Controller vs @RestController

Em Spring Framework, `@Controller` e @`RestController` são duas anotações usadas para definir controladores, mas elas servem a propósitos ligeiramente diferentes. O `@Controller`  podem lidar com solicitações web e retornar vistas (JSP, Thymeleaf, etc.). Geralmente, você usa @Controller em aplicações web tradicionais onde o servidor renderiza o HTML para o cliente. 

Já a anotação `@RestController` uma combinação de `@Controller` e `@ResponseBody`. Ela é usada para criar serviços RESTful. Quando usada, os métodos retornam diretamente os dados JSON ou XML (ou outros formatos) em vez de renderizar uma vista.

```java
@Controller
public class ViewController {
    
    @GetMapping("/view")
    public String viewPage(Model model) {
        model.addAttribute("message", "Hello from ViewController");
        return "view"; // renderiza view.html
    }
}

@RestController
public class ApiController {
    
    @GetMapping("/api")
    public String getApiResponse() {
        return "Hello from ApiController"; // retorna "Hello from ApiController" em JSON
    }
}
```
## Protocolo HTTP

### Requisição (Request)

<img src="https://www.webdevdrops.com/http-desenvolvedores-frontend/images/http-br-2-1024x461.png"/>


### Resposta (Response)

<img src="https://mazer.dev/pt-br/http/introducao-protocolo-http/http-headers-response.png"/>
