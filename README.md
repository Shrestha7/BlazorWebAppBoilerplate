# Blazor Web App BoilerPlate (Blazor Server | Blazor Client(WebAssembly) | BlazorAdminPortal)

A quick startup template with Blazor Server and Blazor Client including Blazor Admin portal.

## Description

This is a quick startup boilerplate template for Blazor Developers. This project include Blazor Server, Blazor Client and Blazor Admin portal ready-made setup.So, that you don't have to waste your time to create and setup while creating a project.

Here you will get a choice to use Blazor Server/ Blazor Client with or without Blazor Admin portal.

## Getting Started

### Dependencies

<!-- * Describe any prerequisites, libraries, OS version, etc., needed before installing program.
* ex. Windows 10 -->

### Installing

<!-- * How/where to download your program
* Any modifications needed to be made to files/folders -->

### Executing program
<!-- 
* How to run the program
* Step-by-step bullets
```
code blocks for commands
```
 -->
 **Here is the explaination of how I have setup Routes:**
 * Cascading Value: The CascadingValue component provides the CheckLayout function's result to the child components rendered by the RouteView.

* CheckLayout Function: This function determines the appropriate layout based on the route and returns a LayoutComponentBase instance.

* RouteView: The RouteView component now uses the default layout specified (@typeof(MainLayout)). It renders the matched component, and that component receives the layout information from the cascading value.

* Child Components: When a child component is rendered, it checks the cascading value to determine which layout to use. If the CheckLayout function returns typeof(AdminLayout), the component will be rendered within the AdminLayout; otherwise, it will use the MainLayout.

**So, what is the difference between using typeof(App).Assembly and typeof(Program).Assembly?**

In Blazor, the AppAssembly attribute within the Router component determines which assemblies to search for routable components (pages and components with @page directives). Let's break down the difference between using typeof(App).Assembly and typeof(Program).Assembly with additional assemblies:
```
AppAssembly="@typeof(App).Assembly"
```
* Common Use: This is the default configuration when you create a new Blazor project. It instructs the router to look for routable components within the assembly that contains the App component (App.razor).
*  Simplicity: This approach is straightforward and suitable for smaller projects where all your components reside in the same project as the App component.
* Limitations: If you have multiple projects (e.g., a shared UI library) containing routable components, this won't work because the router won't search those assemblies.
```
AppAssembly="@typeof(Program).Assembly" AdditionalAssemblies="new[] { typeof(Client._Imports).Assembly }"
```
* Multiple Projects: This is used when your Blazor application has multiple projects (often in a Blazor WebAssembly hosted solution).
* Client-Side Components: typeof(Client._Imports).Assembly refers to the assembly containing client-side components in your Blazor WebAssembly project. This tells the router to also search for components in the client-side project.
* Flexibility: This approach offers greater flexibility for structuring your Blazor solution across multiple projects.
* Additional Assemblies: You can add more assemblies to the AdditionalAssemblies array if you have other projects containing routable components.

**How to Choose:**

* Single Project: If all your Blazor components are in one project, use typeof(App).Assembly.

* Multiple Projects: If you have multiple projects (e.g., Blazor WebAssembly hosted in ASP.NET Core), use typeof(Program).Assembly and add the necessary assemblies to AdditionalAssemblies.

* _Imports.razor: In each project containing routable components, make sure the _Imports.razor file has the @using Microsoft.AspNetCore.Components.Routing directive. This ensures the @page directive is recognized.

**Understanding App and Program:**

* App.razor: This is the root component of your Blazor application. It typically sets up routing, error handling, and provides a layout for your pages.

* Program.cs (Blazor WebAssembly): This is the entry point for your Blazor WebAssembly app. It bootstraps the application, configures services, and starts the runtime.

**Key Points:**

>Both configurations tell the router where to find the components to display for specific routes.
Choose the configuration that best suits your project structure and organization.

* Uncomment and Use this if you dont need Admin portal and want to use server and client only:
```
    <!-- Routes.razor -->
    
    <Router AppAssembly="typeof(Program).Assembly" AdditionalAssemblies="new[] { typeof(Client._Imports).Assembly }">
    <Found Context="routeData">
        <RouteView RouteData="routeData" DefaultLayout="typeof(Layout.MainLayout)" />
        <FocusOnNavigate RouteData="routeData" Selector="h1" />
    </Found>
</Router>
```

* Use this if you want Admin portal with Blazor server and Blazor client.
```
<!-- Routes.razor -->

<Router AppAssembly="@typeof(Program).Assembly" AdditionalAssemblies="new[] { typeof(Client._Imports).Assembly }">
    <Found Context="routeData">
        <CascadingValue Value="CheckLayout(routeData)">
            <RouteView RouteData="@routeData" DefaultLayout="@typeof(Layout.MainLayout)" />
        </CascadingValue>
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(Layout.MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>



@code {
   
    LayoutComponentBase CheckLayout(RouteData routeData)
    {
        var page = routeData.PageType;
        var layoutType = page.Namespace.Contains("Admin") ? typeof(Layout.AdminLayout) : typeof(Layout.MainLayout);
        return (LayoutComponentBase)Activator.CreateInstance(layoutType)!;
    }

   }
```
<!-- ## Help
 
Any advise for common problems or issues.
```
command to run if program contains helper info
```  -->

<!-- ## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie) -->

## Version History

<!-- * 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()-->
* 0.1
    * Initial Release 

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details
<!--
## Acknowledgments

 Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46) -->