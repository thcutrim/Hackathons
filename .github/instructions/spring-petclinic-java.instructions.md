---
description: "Use when editing Java files in the Spring PetClinic project — Owner entity, controllers, repositories, validators and tests. Covers JPA annotations, Bean Validation, Spring MVC patterns used in this codebase."
applyTo: "spring-petclinic/src/**/*.java"
---

# Convenções Java — Spring PetClinic

## Entidades JPA
- Toda entidade herda de `Person` (para Owner) ou `NamedEntity` / `BaseEntity`
- Campos persistidos usam `@Column` + constraints de Bean Validation (`@NotBlank`, `@Email`, `@Pattern`)
- Mensagens de erro via chave i18n: `message = "{chave.no.messages.properties}"`
- Enum para tipos fixos (ex: Gender) — declarar dentro da própria entidade como `public enum`

## Validação
- `@NotBlank` para campos obrigatórios de texto
- `@Email` para e-mail (jakarta.validation.constraints)
- `@NotNull` para campos enum obrigatórios

## Controller Pattern
- Anotações: `@Controller`, `@RequestMapping`
- Model attributes via `@ModelAttribute`
- Redirect após POST: `return "redirect:/owners/{ownerId}"`
- Erros de binding checados com `result.hasErrors()`

## Testes (OwnerControllerTests)
- Usa `@WebMvcTest(OwnerController.class)` + `MockMvc`
- Mock do repository com `@MockitoBean`
- Setup de owner válido no `@BeforeEach` com todos os campos obrigatórios preenchidos
- Assertions com `MockMvcResultMatchers.model()` e `.status()`
- Para novos campos obrigatórios: adicionar cenários de validação (campo ausente → erro, campo inválido → erro, campo válido → redirect)

## Pacote
`org.springframework.samples.petclinic.owner`
