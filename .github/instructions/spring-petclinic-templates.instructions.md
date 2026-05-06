---
description: "Use when editing Thymeleaf HTML templates in the Spring PetClinic project — owner forms, owner details, fragments. Covers th: attributes, fragment patterns and i18n usage in this codebase."
applyTo: "spring-petclinic/src/main/resources/templates/**/*.html"
---

# Convenções Thymeleaf — Spring PetClinic

## Fragments reutilizáveis
- **Campo de texto**: `<input th:replace="~{fragments/inputField :: input (#{chave}, 'nomeField', 'text')}" />`
- **Campo select**: `<select th:replace="~{fragments/selectField :: select (#{chave}, 'nomeField', ${opcoes})}" />`
- Todos os campos ficam dentro de `<div class="form-group has-feedback">`

## i18n
- Sempre use `th:text="#{chave}"` para labels — nunca texto hardcoded em inglês/português
- Chaves são definidas em `src/main/resources/messages/messages.properties`

## Campo Select para Enum (Gender)
Para renderizar um `<select>` com os valores do enum diretamente no template (sem fragment):
```html
<div class="form-group">
  <label class="col-sm-2 control-label" th:text="#{gender}">Gender</label>
  <div class="col-sm-10">
    <select th:field="*{gender}" class="form-control">
      <option th:each="g : ${T(org.springframework.samples.petclinic.owner.Owner.Gender).values()}"
              th:value="${g}" th:text="${g}"></option>
    </select>
    <span class="help-inline">
      <div th:if="${#fields.hasErrors('gender')}" th:errors="*{gender}"></div>
    </span>
  </div>
</div>
```

## ownerDetails.html
- Exibir campo com `<td th:text="*{nomeField}"></td>` dentro da tabela existente
- Rótulo com `<th th:text="#{chave}">Fallback</th>`

## Erros de validação
- Já tratados automaticamente pelo fragment `inputField`
- Para campos customizados: `<div th:if="${#fields.hasErrors('campo')}" th:errors="*{campo}"></div>`
