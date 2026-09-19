# DMRoot — DTO & Validation Skill

## Goal

Create consistent DTOs and keep **request validation in one place only**.

---

## 1. DTO Naming

Always use operation-specific names.

```text
SignInRequestDTO
SignInResponseDTO

UpdateProfileRequestDTO
UpdateProfileResponseDTO
```

Never use generic names like:

```text
UserDTO
RequestDTO
ResponseDTO
```

---

## 2. DTO Location

Keep DTOs inside the relevant Application module.

```text
DMRoot.Application/
└── Auth/
    ├── DTOs/
    │   ├── SignInRequestDTO.cs
    │   └── SignInResponseDTO.cs
    └── Validators/
        └── SignInRequestDTOValidator.cs
```

---

## 3. Validation

Use **FluentValidation**.

Every request DTO that needs validation gets a matching validator:

```text
SignInRequestDTO
        ↓
SignInRequestDTOValidator
```

Example:

```csharp
public sealed class SignInRequestDTOValidator
    : AbstractValidator<SignInRequestDTO>
{
    public SignInRequestDTOValidator()
    {
        RuleFor(x => x.Email)
            .NotEmpty()
            .EmailAddress()
            .MaximumLength(254);

        RuleFor(x => x.Password)
            .NotEmpty()
            .MinimumLength(8);
    }
}
```

---

## 4. Single Validation Point

Validation rules must **not** be duplicated in:

* Controllers
* Services
* Repositories
* DTOs
* SQL

Flow:

```text
Request
  ↓
Request DTO
  ↓
Validator
  ↓
Application Service
```

Controllers should never manually validate fields.

---

## 5. Business Rules

FluentValidation handles **request/input validation**.

Business rules stay in the Application/Core layer.

Example:

```text
Email is required       → Validator
Password minimum length → Validator

User is suspended       → Application logic
Subscription is active → Application logic
```

---

## 6. Response DTOs

Response DTOs normally do not need validators.

```csharp
public sealed record SignInResponseDTO
{
    public string AccessToken { get; init; } = string.Empty;
    public string RefreshToken { get; init; } = string.Empty;
}
```

---

## 7. Rules

For every new request:

1. Create `{Operation}RequestDTO`
2. Create `{Operation}RequestDTOValidator`
3. Put all input validation in the validator
4. Never duplicate validation elsewhere
5. Keep controllers thin
6. Never expose database models directly as API DTOs
7. Use PostgreSQL constraints separately for database integrity

**Principle:**

> One request DTO → One authoritative validator → One validation path.
