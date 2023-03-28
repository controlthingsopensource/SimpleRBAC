# Simple role-based access control for .NET
## About
This is a sample project that can be used for quickly adding RBAC to your .NET project.
All user information is stored in the configuration file so there is not need for adding
support for a database system.

## Run
You can run the sample code by running from the `SimpleRBAC` folder:

```
dotnet run
```

If you log in a user you can observe that access is denied wheen you try to access `http://localhost:5247/Home/Admin`

## Using it in your project

You need to copy in your project the `Account` controller and the corresponding views. You need also to add the following lined in your
`Program.cs`:

```
builder.Services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        options.LoginPath = "/Account/Login";

    });

builder.Services.AddAuthorization(options =>
{
    options.FallbackPolicy = new AuthorizationPolicyBuilder()
        .RequireAuthenticatedUser()
        .Build();
});
...
app.UseAuthentication();
app.UseAuthorization();
```

Finally, add user accounts in you configuration file (see for example the provided `appsettings.Development.json` file).

## More information
You can read [my blog post](https://respected-professor.blogspot.com/2023/03/a-simple-role-based-access-control.html). Open an issue if you need
support. 
