---
description: "Implement email and gender fields on Spring PetClinic Owner — runs all 6 steps: entity, schemas, i18n, form template, details template, unit tests"
name: "Adicionar Email e Gênero ao Owner"
argument-hint: "Deixe em branco para executar todos os passos, ou informe um passo específico (ex: 'apenas entity', 'apenas testes')"
agent: "agent"
tools: [read, edit, search, execute]
---

Implemente o desafio do hackathon: adicionar campos **Email** e **Gênero** ao Owner do Spring PetClinic.

## Contexto
- Projeto em: `spring-petclinic/`
- Rodar testes ao final: `cd spring-petclinic && ./mvnw test -Dtest=OwnerControllerTests -q`

## Passos (execute em ordem)

### Passo 1 — Owner.java
Leia `spring-petclinic/src/main/java/org/springframework/samples/petclinic/owner/Owner.java` e adicione:

```java
public enum Gender {
    MALE, FEMALE, OTHER
}

@Column
@NotBlank
@Email
private String email;

@Column
@Enumerated(EnumType.STRING)
@NotNull
private Gender gender;
```
Com getters e setters para ambos. Adicionar imports: `jakarta.validation.constraints.Email`, `jakarta.persistence.EnumType`, `jakarta.persistence.Enumerated`.

### Passo 2 — Schemas SQL
Nos 3 arquivos (`db/h2/schema.sql`, `db/mysql/schema.sql`, `db/postgres/schema.sql`), adicionar na tabela `owners`:
```sql
email     VARCHAR(100),
gender    VARCHAR(10)
```

### Passo 3 — messages.properties
Adicionar em `src/main/resources/messages/messages.properties`:
```
email=Email
gender=Gender
```

### Passo 4 — Formulário HTML
Em `createOrUpdateOwnerForm.html`, após o campo `telephone`, adicionar:
```html
<input th:replace="~{fragments/inputField :: input (#{email}, 'email', 'text')}" />
```
E o select de gender conforme instrução `spring-petclinic-templates.instructions.md`.

### Passo 5 — ownerDetails.html
Adicionar duas linhas `<tr>` na tabela de informações do owner (após telephone):
```html
<tr>
  <th th:text="#{email}">Email</th>
  <td th:text="*{email}"></td>
</tr>
<tr>
  <th th:text="#{gender}">Gender</th>
  <td th:text="*{gender}"></td>
</tr>
```

### Passo 6 — Testes
Atualizar `OwnerControllerTests.java`:
1. No `@BeforeEach`, adicionar `owner.setEmail("john@example.com")` e `owner.setGender(Owner.Gender.MALE)`
2. Adicionar teste de email inválido retorna erro
3. Adicionar teste de gender nulo retorna erro

### Validação Final
```bash
cd spring-petclinic && ./mvnw test -Dtest=OwnerControllerTests -q 2>&1 | tail -20
```
