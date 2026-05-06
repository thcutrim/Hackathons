---
name: petclinic-challenge
description: "Complete guide for the Spring PetClinic hackathon challenge — adding email and gender fields to Owner. Use when implementing the challenge, stuck on a specific step, need to understand which files to change, or want to verify the implementation. Covers entity, schema, templates, i18n and unit tests."
argument-hint: "Descreva onde está travado ou o que precisa implementar"
---

# Spring PetClinic — Desafio Hackathon Microsoft/Vivo

## O Desafio
Adicionar **E-mail** e **Gênero** ao cadastro e visualização do `Owner` (dono do pet).

### Critérios de Aceite
- **Email**: obrigatório, validação de formato (ex: `example@domain.com`), exibido na tela de detalhes
- **Gênero**: obrigatório, campo select (enum), exibido na tela de detalhes
- Ambos salvos no banco de dados
- Testes unitários cobrindo validação dos novos campos

---

## Mapa de Arquivos

| Arquivo | O que mudar |
|---|---|
| `src/main/java/.../owner/Owner.java` | Adicionar enum `Gender`, campos `email` e `gender` com validações |
| `src/main/resources/db/h2/schema.sql` | Adicionar colunas `email` e `gender` na tabela `owners` |
| `src/main/resources/db/mysql/schema.sql` | Idem |
| `src/main/resources/db/postgres/schema.sql` | Idem |
| `src/main/resources/messages/messages.properties` | Adicionar chaves `email`, `gender` |
| `src/main/resources/templates/owners/createOrUpdateOwnerForm.html` | Adicionar inputs de email e gender |
| `src/main/resources/templates/owners/ownerDetails.html` | Adicionar linhas na tabela de info |
| `src/test/java/.../owner/OwnerControllerTests.java` | Atualizar setup + adicionar testes de validação |

---

## Passo a Passo

### 1. Owner.java — Entidade
```java
// Enum dentro da classe Owner
public enum Gender {
    MALE, FEMALE, OTHER
}

// Campos
@Column
@NotBlank
@Email
private String email;

@Column
@Enumerated(EnumType.STRING)
@NotNull
private Gender gender;

// Getters e Setters
public String getEmail() { return this.email; }
public void setEmail(String email) { this.email = email; }
public Gender getGender() { return this.gender; }
public void setGender(Gender gender) { this.gender = gender; }
```

**Imports necessários:**
```java
import jakarta.validation.constraints.Email;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
```

### 2. Schemas SQL
Adicionar em **todos os 3** arquivos de schema, na tabela `owners`:
```sql
-- H2
email     VARCHAR(100),
gender    VARCHAR(10)

-- MySQL / Postgres: mesmo padrão
```

### 3. messages.properties
```properties
email=Email
gender=Gender
```

### 4. createOrUpdateOwnerForm.html
Após o campo `telephone`:
```html
<input th:replace="~{fragments/inputField :: input (#{email}, 'email', 'text')}" />
<div class="form-group">
  <label class="col-sm-2 control-label" th:text="#{gender}">Gender</label>
  <div class="col-sm-10">
    <select th:field="*{gender}" class="form-control">
      <option th:each="g : ${T(org.springframework.samples.petclinic.owner.Owner.Gender).values()}"
              th:value="${g}" th:text="${g}"></option>
    </select>
    <div th:if="${#fields.hasErrors('gender')}" th:errors="*{gender}" class="help-inline"></div>
  </div>
</div>
```

### 5. ownerDetails.html
Após a linha do `telephone` na tabela:
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

### 6. OwnerControllerTests.java
No `@BeforeEach`, adicionar ao owner válido:
```java
owner.setEmail("john@example.com");
owner.setGender(Owner.Gender.MALE);
```

Adicionar testes: email inválido, email vazio, gender ausente (ver prompt `generate-owner-tests`).

---

## Executar e Validar

```bash
# Rodar só os testes do Owner
cd spring-petclinic && ./mvnw test -Dtest=OwnerControllerTests -q

# Rodar todos os testes
cd spring-petclinic && ./mvnw test -q

# Subir a aplicação localmente
cd spring-petclinic && ./mvnw spring-boot:run
```
Acesse: http://localhost:8080

## Checklist Final
- [ ] Owner.java com `email` e `gender` (com validações)
- [ ] Os 3 schemas SQL atualizados
- [ ] messages.properties com as chaves
- [ ] Formulário com os 2 campos novos
- [ ] ownerDetails com os 2 campos exibidos
- [ ] Testes unitários passando (`OwnerControllerTests`)
- [ ] Aplicação sobe sem erro
- [ ] Demo funcional: criar owner com email + gender → ver na tela de detalhes
