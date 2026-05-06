---
description: "Generate or update unit tests for OwnerControllerTests after adding email and gender fields to Owner entity"
name: "Gerar Testes Owner"
argument-hint: "Deixe em branco para gerar todos os testes necessários"
agent: "agent"
tools: [read, edit, search]
---

Leia o arquivo `spring-petclinic/src/test/java/org/springframework/samples/petclinic/owner/OwnerControllerTests.java` completo.

Em seguida, faça as seguintes alterações:

## 1. Atualizar @BeforeEach
No método de setup do `owner` válido, adicionar:
```java
owner.setEmail("john@example.com");
owner.setGender(Owner.Gender.MALE);
```

## 2. Adicionar testes de validação de Email

```java
@Test
void testInitCreationFormWithInvalidEmail() throws Exception {
    mockMvc.perform(post("/owners/new")
            .param("firstName", "Joe")
            .param("lastName", "Bloggs")
            .param("address", "123 Caramel Street")
            .param("city", "London")
            .param("telephone", "0167452525")
            .param("email", "invalid-email")
            .param("gender", "MALE"))
        .andExpect(status().isOk())
        .andExpect(model().attributeHasFieldErrors("owner", "email"))
        .andExpect(view().name("owners/createOrUpdateOwnerForm"));
}

@Test
void testInitCreationFormWithBlankEmail() throws Exception {
    mockMvc.perform(post("/owners/new")
            .param("firstName", "Joe")
            .param("lastName", "Bloggs")
            .param("address", "123 Caramel Street")
            .param("city", "London")
            .param("telephone", "0167452525")
            .param("email", "")
            .param("gender", "MALE"))
        .andExpect(status().isOk())
        .andExpect(model().attributeHasFieldErrors("owner", "email"))
        .andExpect(view().name("owners/createOrUpdateOwnerForm"));
}
```

## 3. Adicionar teste de validação de Gender

```java
@Test
void testInitCreationFormWithMissingGender() throws Exception {
    mockMvc.perform(post("/owners/new")
            .param("firstName", "Joe")
            .param("lastName", "Bloggs")
            .param("address", "123 Caramel Street")
            .param("city", "London")
            .param("telephone", "0167452525")
            .param("email", "joe@example.com"))
        .andExpect(status().isOk())
        .andExpect(model().attributeHasFieldErrors("owner", "gender"))
        .andExpect(view().name("owners/createOrUpdateOwnerForm"));
}
```

## 4. Verificar imports
Garantir que estejam presentes:
- `import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.model;`
- `import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.view;`

Após editar, informe os testes adicionados e indique para executar:
```bash
cd spring-petclinic && ./mvnw test -Dtest=OwnerControllerTests -q
```
