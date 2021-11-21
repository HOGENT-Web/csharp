class: dark middle

# Enterprise Web Development C&#35;
> Chapter 8 - Suit up, wear a fancy Blazor

---
### Suit up, wear a fancy Blazor
# Table of contents
- [Workshop](#workshop)
- [Component Libraries](#component-libraries)
- [Sportstore example](#sportstore-example)
- [Exercises](#exercises)

---
name:workshop
### Suit up, wear a fancy Blazor
# Blazor Workshop

Follow the following tutorial:
- <a href="https://github.com/dotnet-presentations/blazor-workshop" target="_blank">Blazor Workshop</a>

---
class: dark middle
name:component-libraries
# Suit up, wear a fancy Blazor
> Component Libraries

---
### Component Libraries
# Introduction
Components can be shared in a Razor class library (RCL) across projects. Include components and static assets in an app from:
- Another project in the solution.
- A referenced .NET library.
- A NuGet package.

Just as components are regular .NET types, components provided by an RCL are normal .NET assemblies. Just like class libraries.

> More information about Razor Class Libraries can be found <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/class-libraries?view=aspnetcore-5.0&tabs=visual-studio">here</a>.

---
### Component Libraries
# Open source
A lot of components have already been created by the Blazor community and can be found on <a target="_blank" href="https://github.com/AdrienTorris/awesome-blazor#component-bundles">GitHub</a>.
Please note that:
- Some are pay-to-use
- Simply bad
- Outdated
- Duplicate

However, some are worth mentioning:
- <a target="_blank" href="https://github.com/Blazored">Blazored</a>, small but extenable
- <a target="_blank" href="https://github.com/MudBlazor/MudBlazor">MudBlazor</a>, full suite of components
- <a target="_blank" href="https://github.com/bUnit-dev/bUnit">bUnit</a>, testing library

> You can always implement and package your own components if you don't like any.

---
### Component Libraries
# Open source
The biggest pittfalls:
- Not reading the documentation
- Swashbuckling with how the library is setup
- Not doing research before you implement it in your project
  - Some are just wrappers around JavaScript and **really** slow
- The README of a GitHub repository is your documentation, use it
- If the documentation is bad, the package normally is too.
- Try not to use libraries which extensively use JavaScript, which can interfere with the virtual DOM of Blazor.

In this chapter, we'll use certain open source package, e.g.
- <a target="_blank" href="https://github.com/Blazored/Toast">Blazored.Toast</a>
- <a target="_blank" href="https://github.com/Append-IT/Blazor.Sidepanel">Append.Blazor.Sidepanel</a>
- <a target="_blank" href="https://github.com/Blazored/FluentValidation">Blazored.FluentValidation</a>

---
class: dark middle
name:sportstore-example
# Suit up, wear a fancy Blazor
> Sportstore

---
### Sportstore
# Flasback
In chapter 6, we created a `blazorwasm --hosted` application. We used fakers and Bogus to get some initial data in our `client`. The `Client` was runnable, since everything was done on the `Client` and the `Server` was not yet involved.

In chapter 7, we created our business logic in 2 libraries, `Domain` and `Services`, so we can easily use a console app to do our bidding. We exposed our Data Transfer Objects using a REST API and made it possible to call the Server using the REPL CLI.

---
### Sportstore
# Leap forward
In the following example we combined both applicaties so that:
- The `Server` serves the `Client`, which makes <a target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS">CORS</a> non-existent.
- The `Server` exposes REST API endpoints which are **partly** implemented.
    - You can navigate to `/swagger/index.html` to see the endpoints.
- The `Client` uses the <a target="_blank" href="https://bulma.io/">BULMA.io</a> CSS framework
    - It's like <a target="_blank" href="https://getbootstrap.com/">Bootstrap</a> but **without any JavaScript**
- The `Client` calls the REST API endpoints using the `(I)ProductService` and a `HTTPClient`.
- The `Client` has it's authentication / authorization mocked in the `FakeAuthenticationProvider`.
- The `Client` shows some functionality which is currently not working:
    - Filtering
    - Adding a product
    - Editing a product
    - ...

---
### Sportstore - As is
<img src="images/sportstore-as-is.gif" width="100%" class="center" />

<a href="images/sportstore-as-is.gif" target="_blank">Fullscreen</a>

---
class: dark middle
# Suit up, wear a fancy Blazor
> Sportstore - Going further

---
### Sportstore
# Going further
We'll implement the following:
- Possibility to delete a product
- Create a new product
- Edit an existing product
- Filter existing products based on certain criteria

> In a later chapter, we'll introduce real authentication and a real database, we'll be using the Fakers for now.

---
### Sportstore
# What we're building
<img src="images/sportstore-final-result.gif" width="100%" class="center" />

<a href="images/sportstore-final-result.gif" target="_blank">Fullscreen</a>

---
### Sportstore
# Start
1. Clone <a target="_blank" href="https://github.com/HOGENT-Web/csharp-ch-8-example-1">this GitHub Repository</a>
2. Run the project
3. Try to understand how the `Client` calls the `Server`

> All commits are done in the `solution` branch, which can be found <a href="https://github.com/HOGENT-Web/csharp-ch-8-example-1/tree/solution/src" target="_blank">here</a>.

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Add Project Files

---
### Sportstore
# Delete Product
Implement the Delete Functionality.

On the Details page, there is a button called "Verwijderen", make it call the `IProductService` to actually delete the Product and navigate back to the Product Index page.
- Create a `onclick` EventHandler to call a function called `DeleteProductAsync`
- In the `DeleteProductAsync`, use the `IProductService`
- Inject the `NavigationManager` in the Detail component and use it to `navigate` to the index page.
- Deleting something without a confirmation is **a big no-no**. Ask the user if he **really** wants to delete the product, if the answer is `yes`, delete else don't.

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Delete Confirmation

---
### Sportstore
# Create Product
Implement the Create Functionality.

- Create a new page with a code-behind file in the Client/Products folder called Create, with url `/product/create`.
- Make sure you can navigate from the `Toevoegen` knop in the index page.
- Use the <a target="_blank" href="https://github.com/Blazored/FluentValidation">Blazored.FluentValidation</a> library to create the form.
- Use the `ProductDto.Create` as model for the `EditForm`
- Use <a target="_blank" href="https://bulma.io/documentation/form/general/">BULMA's form components</a> to style the form accordingly
- After creation, navigate to the newly created product's detail page

> Form example on the next slide

---
### Sportstore
# Create Product
<img src="images/product-create.png" width="50%" class="center" />

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Create Product

---
### Sportstore
# Create Product (Sidepanel)
Sometimes the user experience can be better when rendering a small sidepanel to show the form, so that we're not actually navigating away from the index page.
- Investigate the <a target="_blank" href="https://github.com/Append-IT/Blazor.Sidepanel">Append.Blazor.Sidepanel</a> package on GitHub, especially the Forms functionality on the documentation website.
- Instead of navigating to the Product Create Page, use the Sidepanel component to show the form in.
   - Make sure to use version 1.0.1, since version 6.0.0 is for .NET 6.0

> Example on the next slide

---
### Sportstore - Create via Sidepanel
<img src="images/sportstore-create-sidepanel.gif" width="100%" class="center" />

<a href="images/sportstore-create-sidepanel.gif" target="_blank">Fullscreen</a>

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Create Product Via Sidepanel

---
### Sportstore
# Edit Product
Implement the Edit Functionality.

This time you're on your own, on the details page it should be possible to open a sidepanel which makes it possible to edit a product. Note that you should provide additional parameters to the sidepanel and a callback to refresh the details page once the edit is finished, since you'll be staying on the same page. Some help can be found <a target="_blank" href="https://github.com/Append-IT/Blazor.Sidepanel/blob/3da32a817e93bf28efa29053d510169f1d7ae196/docs/Pages/Callbacks.razor#L36">here</a>.

- Implement the `ProductService` functionality on both, the client and server side.
- Implement the `ProductController` with a `PUT` endpoint.
- Create or re-use DTO's, don't re-use `ProductRequest` nor `ProductResponse`
- You can test the back-end via Swagger.

> Example on the next slide

---
### Sportstore - Edit via Sidepanel
<img src="images/sportstore-edit-sidepanel.gif" width="100%" class="center" />

<a href="images/sportstore-edit-sidepanel.gif" target="_blank">Fullscreen</a>

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Edit Product Via Sidepanel

---
### Sportstore
# Filter Products
What we'll be building

<img src="images/sportstore-filter.gif" width="100%" class="center" />

<a href="images/sportstore-filter.gif" target="_blank">Fullscreen</a>

---
### Sportstore
# Filter Products
Implement the Filter Functionality. 

- How would you tackle this feature?
- Try to draw it on a piece of paper, since multiple components are working together and both of them require the same state.

In the Blazing Pizza tutorial you learned about <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/state-management?view=aspnetcore-6.0&pivots=webassembly#in-memory-state-container-service-wasm">State Management</a>. It might be a good idea to use it here. However you can still pass parameters from the `Index` page to the `ProductFilters` component.

> The categories are hard-coded for now, you can however create a new `Controller` and `Service` to make them dynamic.

---
### Sportstore
# Filter Products
Some guidance in implementing this feature:
- The concept is that the filter is a separate class with all filterable properties, which binds to the input elements of the `ProductFilters`.
- Each time a property is changed, the ProductFilter notifies the Index component that it did, therefore you need to have an event which the Index component can (un)subscribe to. Each time this happens, you'll have to fetch the products which are filtered based on all the properties that are passed as querystring parameters. The best part is, that it's filtered on the server-side and not on the client.

---
### Sportstore
# ProductFilter.cs
```
public class ProductFilter
{
*   public event Action OnProductFilterChanged;
    private string searchTerm;
*   private void NotifyStateChanged() => OnProductFilterChanged.Invoke();
    public string SearchTerm
    {
        get => searchTerm;
        set
        {
            searchTerm = value;
*           NotifyStateChanged();
        }
    }
    // Other properties / fields
}
```

---
### Sportstore
# Index.razor.cs
```
public partial class Index
{
    // Other stuff
*   private ProductFilter filter = new();
    protected override async Task OnInitializedAsync()
    {
*       filter.OnProductFilterChanged += FilterProductsAsync;
        // Other stuff
    }
    private async void FilterProductsAsync()
    {
        ProductRequest.GetIndex request = new()
        {
            MaximumPrice = filter.MaximumPrice,
            Category = filter.Category,
            MinimumPrice = filter.MinimumPrice,
            SearchTerm = filter.SearchTerm,
        };
        var response = await ProductService.GetIndexAsync(request);
        products = response.Products;
        StateHasChanged(); // Since it's not a UI-event.
    }
}
```

---
### Sportstore
# Index.razor.cs
Fixing the memory leak:
```
public partial class Index : `IDisposable`
{
    // Other stuff
    private ProductFilter filter = new();
    protected override async Task OnInitializedAsync()
    {
*       filter.OnProductFilterChanged += FilterProductsAsync;
        // Other stuff
    }
    private async void FilterProductsAsync()
    {
        // See previous slide
    }
*   public void Dispose()
*   { // If we don't do this, we'll have memory leaks.
*       filter.OnProductFilterChanged -= FilterProductsAsync;
*   }
}
```

---
### Sportstore
# Passing the Parameter down
Index.razor
```razor
    <ProductFilters `Filter="filter"` />
```

ProductFilters.razor.cs
```
public partial class ProductFilters
{
    [Parameter] public ProductFilter Filter { get; set; }
}
```
ProductFilters.razor

Binding the property to the `<input>`
```
<input `@bind="Filter.SearchTerm"` class="input" type="search" />
```

---
### Sportstore
# Passing querystring parameters
Client/ProductService.cs
```
public async Task<ProductResponse.GetIndex> GetIndexAsync
(ProductRequest.GetIndex request)
{
*   var queryParameters = request.GetQueryString();
    var response = await client.GetFromJsonAsync
    <ProductResponse.GetIndex>($"{endpoint}`?{queryParameters}`");
    return response;
}
```

Convert object to Query String parameters (name-value pairs)
```
public static string GetQueryString(this object obj)
{
    var properties = 
    from p in obj.GetType().GetProperties()
    where p.GetValue(obj, null) != null
    select p.Name + "=" + 
    HttpUtility.UrlEncode(p.GetValue(obj, null).ToString());
    return string.Join("&", properties.ToArray());
}
```


---
### Sportstore
# Back-end filtering
Services/ProductService.cs
```
public async Task<ProductResponse.GetIndex> GetIndexAsync
                        (ProductRequest.GetIndex request)
{
    ProductResponse.GetIndex response = new();
*   var query = products.AsQueryable();
*   if (!string.IsNullOrWhiteSpace(request.SearchTerm))
*       query = query.Where(x => x.Name.Contains(request.SearchTerm));
    // Don't forget case sensitivity
    if (request.MinimumPrice is not null)
        query = query.Where(x => x.Price.Value >= request.MinimumPrice);
    // Other filters here
    response.TotalAmount = query.Count(); // Used for paging
    query = query.Take(request.Amount).Skip(request.Amount * request.Page);
    query.OrderBy(x => x.Name);
    response.Products = query.Select(x => new ProductDto.Index
    {
        Id = x.Id,
        Name = x.Name,
        // Other mappings
    }).ToList();
    return response;
}
```

---
class: dark middle
# Suit up, wear a fancy Blazor
> 📝 Commit: Filter Products

---
name:exercises
class: dark middle
# Suit up, wear a fancy Blazor
> Exercises

---
### Exercises
# Add Paging
- Add a Previous and Next button on the Index.razor page (below the items), to make paging possible.
- Make previous disabled if it's the first page
- Make next disabled if there are no other pages.

> <a target="_blank" href="https://bulma.io/documentation/components/pagination/"> BULMA - Pagination</a> can help you for the layout.

---
### Exercises
# Add Shopping possibilities
- Make it possible to add products in a Shopping Cart.
- Make it possible to remove products from the  Shopping Cart.
- Only client side functionalities are currently required.
- What if the client on the same device and browser reloads, is the cart lost? Try using a LocalStorage package to keep state e.g. <a href="https://github.com/Blazored/LocalStorage" target="_blank">Blazored.LocalStorage</a>.

Tips:
- Render the Shoppingcart in the Sidepanel
- Use the <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/state-management?view=aspnetcore-6.0&pivots=webassembly" target="_blank">State Management article</a> to put the cart in a CartState class (memory) and in LocalStorage (browser storage).
