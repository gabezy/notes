# Spring Rest

## Spring VS Jakarta EE (Java EE)

Jakarta é o novo nome do Java EE quando o Eclipse Foundation ficou responsável pelo projeto que criaram a especificação JPA e com a implementação pelo Hibernate

## Spring VS Spring Boot

Spring é um <strong>framework modularizado e flexível</strong>, onde é possível criar aplicações como APIs, Web Services e etc. Ele é composto por diversos módulos que compõem o framework, <strong>não sendo obrigatório utilizar todos</strong>, como exempĺos abaixo, porém é necessário realizar as configurações prévias para utilizar suas funcionalidades:

- <strong>Spring Security</strong> para implementar segurança.
- <strong>Spring Data</strong> para persistência de dados.
- <strong>Spring MVC</strong> para criação de Rest API e MVC.
- [Entre outros](https://spring.io/projects/spring-framework)


Já o Spring Boot é uma ferramenta do Spring que já configuração esse módulos para serem utilizado, sendo feito a configuração e convenções definidas pela própria desenvolvedora da ferramenta, não gerando código. O Spring Boot utiliza os Starters para agrupar as dependências necessária para utilizar os módulos pré-configurado, como exemplo o spring-boot-starter-web que utiliza o Spring MVC e configura para criar Web Services.:


Use o [Spring Initializr]() para  

![Spring Initalizr interface](https://codingjump.com/_next/image?url=%2Fstatic%2Fimages%2Fposts%2Fspring-boot%2Fcreate-spring-boot-app%2Fspring-initializr.png&w=3840&q=75)

Caracteristicas:

- Group: Como se fosse uma pacote Java, geralmente usa o dômino da empresa/pessoal ao contrário (com.exemplo).
- Artifact: 
- Package: Pacote inicial que será criado para o projeto.


## 2.6 Maven, pom.xml e estrutura do projeto

Maven é uma ferramenta de gerenciamento do dependências e de Build para Java.

- Pasta src/test/java -> Classes de teste.
- Pasta src/main/java -> Código fonte da aplicação.
- Pasta src/main/resources -> Código de configuração (application.properties/yml), imagens, HTML, Database Migrations e etc.
- Pasta raiz do projeto é criado o pom.xml (Project Object Model) onde é armazenado os configurações, dependências do Maven.
- mnvw.cmd e mnvw são arquivos (Maven Wrapper) para windows e Linux que permitem executar o Maven sem está instalado local na máquina.

### Comandos Maven 
```bash
mvn package # Empacota o projeto para formato .jar na pasta target
java -jar project-name-SNAPSHOT.jar # executa o jar
mvn clean # remove (limpar) os arquivos de build na pasta target
mvn dependency:tree # informa a árvore as dependências do projeto 
mvn dependency:resolve # informa as dependências resolvidas
mvn help:effective-pom # gera o pom.xml efetivo:
```


### Dev Tools

Para a aplicaçã restartar todas vez que salvar um arquivo é necessário adicionar a dependência Dev tools no pom.xml e siga o [passo a passo](https://bitstogigs.com/how-to-auto-start-spring-boot-application-after-code-changes-in-intellij-idea/)</br>

```xml
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
</dependency>
```

## Inversão de Controle (IoC) e Injeção de Dependências

A inversão de controle é um princípio onde controle de como o objeto é criado e gerenciado é invertido, não cabendo mais o objeto (classe) decidir como será instanciado, passando essa responsabilidade para a aplicação.</br>

```Java
// Sem utilizar o princípio da inversão de controle
public class Driver {
    private Car car;

    public Driver() {
        this.car = new Car();
    }
}


// Utilizando o princípio da inversão de controle
public class Driver {
    private Car car;

    public Driver(Car car) {
        this.car = car;
    }
}
```

A injeção de dependência é uma forma de implementar o IoC, onde as dependências que a objeto necessita para operar são passadas para ele invés do próprio objeto instancia-lás internamente.
Existe várias forma de injeção de dependências;

1. Injeção via construtor (mais utilizada)
2. Injeção via Setter
3. Injeção via Campo por meio de uma anotação (@Autowired no Spring)

```java
public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        Driver driver = new Driver(car); // Passando a dependência que a classe Driver necessita via construtor
    }
}
```
As vantagens de utilizar IoC e injeção de dependências são:
- Baixo acoplamenta
- Simplifca a evolução/alteração do código
- Facilita os mocks para teste


## Spring IoC Container 

É a implementação de injeção de dependêncais, também conhecido como <strong>Spring/application Context</strong>.
Ao iniciar uma aplicação Spring, o container é inicializado e começa a instanciar os Beans da aplicação
que ele deve gerenciar. Bean é o nome dado para objetos gerenciados, instanciado e configurado pelo container do Spring,
podendo também ser injentado em outros Beans (dependências)

## Definindo beans com @Component



## Injeção de dependência

A injeção de dependência é utilziada no Spring principalmente através do construtor (melhor para teste) e do atributo
utilizando o @Autowired, porém é possíve utilizar via Setter.

```java
// pelo construtor
public class Driver {
    private Car car;

    public Driver(Car car) {
        this.car = car;
    }
}

// pelo atributo
public class Driver {

    @Autowired(required = true) // quando for falsa, o Spring tratará a dependência como opcional
    private Car car;
}

// pelo Setter
public class Driver {
    private Car car;

    @Autowired
    public void setCar(Car car) {
        this.car = car;
    }
}
```

### Ambiguidade de Beans e lista de Beans

A ambiguidade de beans pode ocorrer quando mais de um @Component implementa uma interface ou estende uma classe abstrada
e essa é utilizada como dependência em outra classe, assim por padrão, o Spring não sabe definir qual dependência usar.

```java
public interface Notificador {
    void notificar(String mensagem);
}

@Component
public class NotificadorEmail implements Notificador {
    
    @Override
    public void notificar(String mensagem) {
        //
    }
}

@Component
public class NotificadorSMS implements Notificador {

    @Override
    public void notificar(String mensagem) {
        //
    }
}

public class ServiceExamplo {
    @Autowirde
    private Notificador notificador; // irar apresentar erro de ambiguidade
}
```
Para solucinar esse erro, é possível implementar a seguintes soluções:
- Passar uma lista da interface/classe abstrata para variável (List<Notificador>).
- Usar o @Primary no bean desejado para prioriza-ló quando houver mais de um bean
- Usar o @Qualifier("") no bean e na classe que utiliza o bean
- Usar uma anotação customizada utilizando o @Qualifier e @Retetion(ReterionPolicy.RUNTIME)

## Spring Profiles
Através do Spring profiles é possível alterar o comportamento e separqar componentes da aplicação que serão disponibilizados
em determinados ambientes. Em suma, através desse parâmetro, que é passado na inicialização da aplicação, é possível alterar o comportamento
dependendo do ambiente que é passado (Ex.: Local, hml, test, prod). É possível, por exemplo, mudar o banco de dados que cada ambiente
utilizado.

```java
@Profile("prod") // Roda apenas no ambiente de produção
@Component
public class NotificadorEmail implements Notificador {
    
    @Override
    public void notificar(String mensagem) {
        //
    }
}

@Profile("local") // Roda apenas no ambiente local AKA Dev
@Component
public class NotificadorEmailMock implements Notificador {

    @Override
    public void notificar(String mensagem) {
        //
    }
}
```
Para utilizar o perfil desejado é necessário colocar spring.profiles.active={"profile"} no
application.properties ou passando por parâmetro quando executar a aplicação

