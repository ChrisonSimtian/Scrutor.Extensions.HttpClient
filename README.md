# Scrutor.Extensions.HttpClient
A solution for https://github.com/khellang/Scrutor/issues/180 baked into a Nuget Package

## Usage

1. Inject your Http Client as a named Client
2. Make sure that all your Api Clients are assignable to a common interface
3. Register all your Api Clients with Scrutor.Extensions.HttpClient

```csharp
/* Inject named HttpClient */
services.AddHttpClient("MyHttpClient", client =>
{
	client.BaseAddress = new Uri("https://api.example.com");
});

/* Inject all implementations of IMyHttpApiClient */
services.Scan(scan => scan
        .FromCallingAssembly()
        .AddClasses(classes => classes.AssignableTo<IMyHttpApiClient>())
        .AsMatchingInterface()
        .AsHttpClient("MyHttpClient")
        );
```