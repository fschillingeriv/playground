# Backend Languages

You can use passwordless.dev with any programming language by implementing calls to the passwordless.dev API, but this document will provide some code examples, guidelines, and other help integrating passwordless.dev with popular languages.

## ASP.NET Core <Badge text="example" type="warning"/>

This ASP.NET Core implementation uses .NET5 and some JavaScript for a simple passwordless.dev implementation. A [register](api/#register-token) function might look something like:

```csharp
public async Task<ActionResult<string>> GetRegisterToken(string alias)
        {

            string userId = Guid.NewGuid().ToString();

            var json = JsonSerializer.Serialize(new
            {
                userId = userId,
                username = alias,
                DisplayName = "Mr Guest"
            });

            var request = await _httpClient.PostAsync("register/token", new StringContent(json, Encoding.UTF8, "application/json"));
            request.EnsureSuccessStatusCode();
            var token = await request.Content.ReadAsStringAsync();

            try
            {
                var aliasJson = JsonSerializer.Serialize(new
                {
                    userId = userId,
                    aliases = new string[] { alias }
                });
                var aliasRequest = await _httpClient.PostAsync("alias", new StringContent(aliasJson, Encoding.UTF8, "application/json"));
                aliasRequest.EnsureSuccessStatusCode();
            }
            catch(Exception) {
                throw;
            }

            return token;
        }
```


[See more sample code](https://github.com/passwordless/passwordless-dotnet-example).

## Node.js <Badge text="example" type="warning"/> <Badge text="demo" type="tip"/>

This Node.js implementation is done in only a few lines of code. A [register](api/#register-token) function might look something like:

```js
const apiKey = "demobackend:public:c203e65b581443778ea4823b3ef0d6af";
 const backendUrl = "https://demo-backend.passwordless.dev";

 async function Register(alias) {
   const p = new Passwordless.Client({ apiKey });
   const myToken = await fetch(backendUrl + "/create-token?alias=" + alias).then((r) => r.text());
   await p.register(myToken);
   console.log("Register succeeded");
 }
```

[See more sample code](https://github.com/passwordless/passwordless-nodejs-example).

Alternatively, check out our demo application, which you can use by adding your [API key](concepts)'s secret to `index.html` and `app.js`. [See our demo](https://demo-backend.passwordless.dev/).

## PHP

Coming Soon.

## Python

Coming Soon.
