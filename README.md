# Netcool.HttpProxy

A http proxy for asp.net core 3.1 app.

Most of the codes comes from [aspnet/AspLabs](https://github.com/aspnet/AspLabs)

## Usage

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddProxy(options =>
    {
        options.MessageHandler = new HttpClientHandler
        {
            AllowAutoRedirect = false
        };
        
        options.PrepareRequest = (originalRequest, message) =>
        {
            message.Headers.Add("X-Forwarded-Host", originalRequest.Host.Host);
            return Task.FromResult(0);
        };
    });
}

public void Configure(IApplicationBuilder app)
{
    app.Map("/api", app => { app.RunProxy(new Uri("http://api.domain.com"); });
}

```

