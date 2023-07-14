
# Initial Install of .Net6 core in your Terminal (CLI)
```csharp
    dotnet tool install --global dotnet-ef
```
#
## Commands to run hereafter :
- dotnet restore
- dotnet run
- dotnet watch run
- dotnet new console
- dotnet new console -o Myproject
- dotnet new web --no-https -o Myproject
- dotnet new mvc --no-https -o Myproject
- dotnet add package Pomelo.EntityFrameworkCore.MySql --version 6.0.1
- dotnet add package Microsoft.EntityFrameworkCore.Design --version 6.0.3
- dotnet ef migrations add FirstMigration
- dotnet ef database update
- dotnet ef migrations add FirstMigration -v
# Starter Code
**Static Function**
```csharp
 static void SayHello()
{
    Console.WriteLine("Hello how are you doing today?");
}
```
**Fields**
```csharp
 class Dog
 {
     string Name;
     string Breed;
     string FurColor;
 }
```
**Properties**
```csharp
public string FurColor {get; set;}
```
**Override**
```csharp
    public override void ShowInfo()
    {
        Console.WriteLine($"Name: {Name}");
        Console.WriteLine($"Diet: {Diet}");
        Console.WriteLine($"Mammal: {IsMammal}");
        Console.WriteLine($"Fur Type: {FurType}");
    }
```
**Static Classes**
```csharp
public static class Calculator
{
   public static double Add(double FirstValue, double SecondValue)
   {
      return FirstValue + SecondValue;
   }
}
```
**Controller.cs**
```csharp
return RedirectToAction("Here");
```
```csharp
// Surrounding registration code
HttpContext.Session.SetInt32("UserId", newUser.UserId);
return RedirectToAction("SomeAction");
// Surrounding registration code
```
```csharp
using Microsoft.AspNetCore.Mvc.Filters;
```
**.cshtml/.html**
```csharp
<form action="process" method="post">    
    <input asp-for="name" type="text" name="name"/>    
    <input asp-for="NumberField type="number" name="NumberField"/>    
    <button type="submit">Submit</button>
</form>
```
```csharp
<form action="process" method="post">    
    <input type="text" name="TextField"/>    
    <input type="number" name="NumberField"/>    
    <button type="submit">Submit</button>
</form>
```
```csharp
public IActionResult FunctionName(type name)
{
    // Code goes here
}
```
***pragma...***
```csharp
#pragma warning disable CS8618
```
***using...***
```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
```
***namespace...***
```csharp
namespace Myproject.Controllers;
namespace Myproject MyModel.Models;
```
**Program.cs**
```csharp
using Microsoft.EntityFrameworkCore;
using CRUDelicious.Models;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllersWithViews();
builder.Services.AddHttpContextAccessor();  
builder.Services.AddSession();  

var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");

builder.Services.AddDbContext<MyContext>(options =>
{
    options.UseMySql(connectionString, ServerVersion.AutoDetect(connectionString));
});

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
}
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.UseSession();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```
***MyContextModel.cs***
```csharp
#pragma warning disable CS8618
// We can disable our warnings safely because we know the framework will assign non-null values 
// when it constructs this class for us.
using Microsoft.EntityFrameworkCore;
namespace Login_And_Registration.Models;
// the MyContext class represents a session with our MySQL database, allowing us to query for or save data
// DbContext is a class that comes from EntityFramework, we want to inherit its features
public class MyContext : DbContext 
{   
    // This line will always be here. It is what constructs our context upon initialization  
    public MyContext(DbContextOptions options) : base(options) { }
    // We need to create a new DbSet<Model> for every model in our project that is making a table
    // The name of our table in our database will be based on the name we provide here
    // This is where we provide a plural version of our model to fit table naming standards    
    public DbSet<User> Users { get; set; } 
}
```
***[Http] & [Route]...***
```csharp
[HttpGet("")]
[HttpPost("")]
[Route("")]
// The name we gave our class minus "Attribute"
[SessionCheck]
[HttpGet("someRoute")]
// The rest of the code
```
***validation...***
```csharp
[Required]
[Required(3, ErrorMessage="Something is required")]
[MinLength(3)]
[MinLength(3, ErrorMessage="This was suppose to be so many characters long")]
[MaxLength(45)]
[MaxLength(45, ErrorMessage="This was not suppose to exceed this many characters")]
[DataType(DataType.EmailAddress)]
[RegularExpression(@"\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*", ErrorMessage = "Invalid email format")]
[RegularExpression(@"^[a-zA-Z0-9.+_-]+@[a-zA-Z0-9._-]+\.[a-zA-Z]+$", ErrorMessage = "Invalid email format")]
*must include a span element in your .cshtml file
<span asp-for="name"></span>
```
***razor @foreach & @if...***
```csharp
    @foreach(string word in StringList)    
    {        
        <div>            
            <p>@word</p>
            @if(word.Length < 4)            
            {                 
                <p>@word is a short word</p>            
            }       
        </div>    
    }
```
**ViewBag/ProjectController**
```csharp
// Other code 
[HttpGet("")]
public IActionResult Index()
{    
    // Here we assign the value "Hello World!" to the key .Example    
    // Key names can be whatever you like    
    ViewBag.Example = "Hello World!";    
    return View();
}
```
***appsettings.json***
```csharp
{  
    "Logging": {    
        "LogLevel": {      
            "Default": "Information",      
            "Microsoft.AspNetCore": "Warning"    
        }  
    },
    "AllowedHosts": "*",    
    "ConnectionStrings":    
    {        
        "DefaultConnection": "Server=localhost;port=3306;userid=root;password=root;database=**CHANGE ME TO NEW DB NAME**;"    
    }
}
```
***Tailwind***
```csharp
npm install -D tailwindcss
npx tailwindcss init

change config file
content: ["./Views/**/*.cshtml"]

add src/input.css
@tailwind base;
@tailwind components;
@tailwind utilities;

npx tailwindcss -i ./src/input.css -o wwwroot/css/site.css --watch

```
#
**many-to-many example**
```csharp
#pragma warning disable CS8618
namespace YourProjectName.Models;
using System.ComponentModel.DataAnnotations;
public class User
{    
    [Key]    
    public int UserId { get; set; }       
    public string Name { get; set; } 
    public string Email { get; set; }
    public DateTime CreatedAt { get; set; } = DateTime.Now;
    public DateTime UpdatedAt { get; set; } = DateTime.Now;
}
* updated to this for a many-to-many
#pragma warning disable CS8618
namespace YourProjectName.Models;
using System.ComponentModel.DataAnnotations;
public class User
{    
    [Key]    
    public int UserId { get; set; }       
    public string Name { get; set; } 
    public string Email { get; set; }
    public DateTime CreatedAt { get; set; } = DateTime.Now;
    public DateTime UpdatedAt { get; set; } = DateTime.Now;
    // Our navigation property to track the many Posts our user has made
    // Be sure to include the part about instantiating a new List!
    public List<Post> AllPosts { get; set; } = new List<Post>();
}
```
```csharp
#pragma warning disable CS8618
namespace YourProjectName.Models;
using System.ComponentModel.DataAnnotations;
public class Post
{    
    [Key]    
    public int PostId { get; set; }
    public string Content { get; set; }
    public DateTime CreatedAt { get; set; } = DateTime.Now;
    public DateTime UpdatedAt { get; set; } = DateTime.Now;
    // This is the ID we will use to know which User made the post
    // This name should match the name of the key from the User table (UserId)
    public int UserId { get; set; }
}
#pragma warning disable CS8618
namespace YourProjectName.Models;
using System.ComponentModel.DataAnnotations;
public class Post
{    
    [Key]    
    public int PostId { get; set; }
    public string Content { get; set; }
    public DateTime CreatedAt { get; set; } = DateTime.Now;
    public DateTime UpdatedAt { get; set; } = DateTime.Now;
    public int UserId { get; set; }
    // Our navigation property to track which User made this Post
    // It is VERY important to include the ? on the datatype or this won't work!
    public User? Creator { get; set; }
}
```



