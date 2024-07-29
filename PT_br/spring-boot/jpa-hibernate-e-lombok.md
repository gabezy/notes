## O que é Java Persistence API (JPA)?

É uma especificação Java EE para persistência de dados que é padronizada para desenvolvimento de aplicações, descrevendo como deve ser implementado (produto final).

## O que é Hibernate?

No caso o Hibernate é uma Object Ralational Mapping (ORM) que implementa a especificação JPA, sendo o mais famosos entre as ORMs Java.

### Configurar o Data Source e propriedades do JPA

```yaml
spring:
    datasource:
        url: jdbc:postgresql://localhost:5432/{database_name} # utilizado o postgreSQL como exemplo
        username: admin
        password: secret
    jpa:
        show-sql: true
    properties:
        hibernate:
            format_sql: true
            dialect: # Especificar o dialeto que o DB irar usar
    gererate-ddl: true # inicializa o schema quando a aplicação startar
    hibernate:
        ddl-auto: create # cria o schema e deleta as informações anteriores

```

## Mapeamento de Entidades

Para mapear as entidades, o JPA utiliza anotações para definir o objeto, linhas e campos.

- `@Entity` para mapear a entidade que serve como a coluna no banco de dados.
- `@Table(name = "")` para especificar o nome da table caso for diferente da classe.
- `@Id` para mapear o atributo que servirá como a coluna de PRIMARY KEY
- `@GeneratedValue(strategy = )` especificar a estratégia utilizada para gerar os valores da coluna
    - `GenerationType.IDENTITY` deixa o banco de dados decidir a forma de geração dos valores 
    - `GenerationType.AUTO`
    - `GenerationType.SEQUENCE`
    - `GenerationType.TABLE`
    - `GenerationType.UUID`
- `@Column(name = "", nullable = false)` para especificar o nome da coluna caso for diferente do atributo e for NOT NULL

## JPA

### Métodos para consultar, criar, alterar e deletar entidade no banco de dados

[Artigo sobre JPA](https://blog.algaworks.com/tutorial-jpa/)
```java
import com.gabezy.foodnow.domain.entity.Cuisine;
import jakarta.persistence.EntityManager;
import jakarta.persistence.PersistenceContext;
import org.springframework.stereotype.Component;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Component
public class CuisineRegister {

    @PersistenceContext // Anotação para instanciar o manager do banco de dados 
    private EntityManager entityManager; 

    public List<Cuisine> list(){
        return this.entityManager.createQuery("from Cuisine", Cuisine.class).getResultList();
    }

    public Cuisine buscar(Long id){
        return this.entityManager.find(Cuisine.class, id);
    }
    // Quando a query faz alguma modificação (INSERT or DELETE) 
    // é necessário fazer dentro de uma transação
    @Transactional 
    // O método save pode ser tanto para criar ou alterar a entidade
    public Cuisine save(Cuisine cuisine) {  
        return this.entityManager.merge(cuisine);
    }

    @Transactional  
    public void delete(Cuisine cuisine) {
        Cuisine cuisineToDelete = buscar(cuisine.getId());
        this.entityManager.remove(cuisineToDelete);
    }
}
```

### Relacionamentos

- `@ManyToOne` mapea um relacionamento de muitos para um. Por padrão cria uma coluna da tabela coluna Objeto_id.
- `@JoinColumn`Para espeficar os propriedades (nome, nullable) da coluna da FK.
- `@OneToMany`


## Lombok

O Lombok é uma dependêcia gerado de código boilerplate, como setter, getter e construtores da classe.

- `@Setter` gera os setters das propriedades da classe. 
- `@Getter` gera os getters das propriedades da classe.
- `@EqualsAndHasCode` gera o equals e hashCode da classe.
- `@RequiredArgsConstructor`
- `@Data` é uma shortcut para gerar os @Setters (apenas em propriedades non-final), @Getters, @EqualsAndHashCode e @RequiredArgsConstructor


