# API Response Skill

Use a shared generic API response wrapper across DMRoot.

## Location

`Core/Common/ApiResponse.cs`

## Implementation

```csharp
namespace DMRoot.Core.Common;

public class ApiResponse<T>
{
    public bool Success { get; set; }
    public string Message { get; set; }
    public T? Data { get; set; }
    public object? Errors { get; set; }

    public ApiResponse(
        bool success,
        string message,
        T? data = default,
        object? errors = null)
    {
        Success = success;
        Message = message;
        Data = data;
        Errors = errors;
    }

    public static ApiResponse<T> Ok(
        T data,
        string message = "Success")
        => new(true, message, data);

    public static ApiResponse<T> Ok(
        string message = "Success")
        => new(true, message);

    public static ApiResponse<T> Fail(
        string message,
        object? errors = null)
        => new(false, message, default, errors);
}