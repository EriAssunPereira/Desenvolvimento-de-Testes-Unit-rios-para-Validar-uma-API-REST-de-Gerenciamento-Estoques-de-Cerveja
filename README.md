# Desenvolvimento-de-Testes-Unit-rios-para-Validar-uma-API-REST-de-Gerenciamento-Estoques-de-Cerveja

Desenvolver testes unitários é uma habilidade essencial para qualquer desenvolvedor de software, e a prática do TDD (Test-Driven Development) pode melhorar significativamente a qualidade do código. Aqui está um exemplo de como podemos começar a escrever testes unitários para uma API REST de gerenciamento de estoques de cerveja usando Spring Boot, JUnit e Mockito:

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.Mockito.when;

import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;

@SpringBootTest
public class BeerStockManagementTests {

    @MockBean
    private BeerRepository beerRepository;

    @InjectMocks
    private BeerService beerService;

    @Test
    public void whenBeerCreated_thenVerifySaved() {
        Beer beer = new Beer("Brahma", BeerType.LAGER, 10);
        when(beerRepository.save(beer)).thenReturn(beer);
        Beer createdBeer = beerService.createBeer(beer);
        assertEquals(beer.getName(), createdBeer.getName());
    }

    // Outros testes unitários podem ser adicionados aqui
}
```

Neste exemplo, estamos usando `@MockBean` para criar um mock do `BeerRepository`, que é uma interface para operações de banco de dados. Com `@InjectMocks`, estamos injetando as dependências necessárias no `BeerService`, que é a classe que contém a lógica de negócios. O teste `whenBeerCreated_thenVerifySaved` verifica se uma cerveja é salva corretamente.

Lembre-se de que este é apenas um ponto de partida. Você precisará desenvolver testes adicionais para cobrir todas as funcionalidades básicas, como listagem, consulta por nome e exclusão, além de seguir o TDD para novas funcionalidades. Boa sorte com seu desafio! 

Configurar o ambiente de testes para um projeto Spring Boot é essencial para garantir que suas funcionalidades sejam testadas de forma adequada. Vou explicar como você pode configurar o ambiente de testes para o seu projeto:

1. **Dependências Maven**:
   Primeiro, adicione as dependências necessárias ao seu arquivo `pom.xml`. As principais dependências para testes em Spring Boot são:

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-test</artifactId>
       <scope>test</scope>
   </dependency>
   <dependency>
       <groupId>com.h2database</groupId>
       <artifactId>h2</artifactId>
       <scope>test</scope>
   </dependency>
   ```

   O `spring-boot-starter-test` contém a maioria dos elementos necessários para seus testes. O H2 DB é um banco de dados em memória que elimina a necessidade de configurar e iniciar um banco de dados real para fins de teste.

2. **JUnit 4 (Opcional)**:
   A partir do Spring Boot 2.4, o mecanismo vintage do JUnit 5 foi removido do `spring-boot-starter-test`. Se você ainda deseja escrever testes usando o JUnit 4, adicione a seguinte dependência:

   ```xml
   <dependency>
       <groupId>org.junit.vintage</groupId>
       <artifactId>junit-vintage-engine</artifactId>
       <scope>test</scope>
       <exclusions>
           <exclusion>
               <groupId>org.hamcrest</groupId>
               <artifactId>hamcrest-core</artifactId>
           </exclusion>
       </exclusions>
   </dependency>
   ```

3. **Testes de Integração com `@SpringBootTest`**:
   Os testes de integração focam na integração entre diferentes camadas da aplicação e não envolvem mocks. Para configurar os testes de integração, utilize a anotação `@SpringBootTest`. Por exemplo:

   ```java
   import org.junit.jupiter.api.Test;
   import org.springframework.boot.test.context.SpringBootTest;
   import org.springframework.boot.test.mock.mockito.MockBean;
   import org.springframework.test.context.TestPropertySource;

   @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK, classes = Application.class)
   @AutoConfigureMockMvc
   @TestPropertySource(...)
   public class IntegrationTests {
       // Seus testes de integração aqui
   }
   ```

   Certifique-se de ajustar as configurações conforme necessário para o seu projeto.

Lembre-se de que essas são apenas diretrizes iniciais. Você precisará desenvolver testes adicionais para cobrir todas as funcionalidades básicas da sua API REST de gerenciamento de estoques de cerveja. 

https://github.com/rpeleias/beer_api_digital_innovation_one
