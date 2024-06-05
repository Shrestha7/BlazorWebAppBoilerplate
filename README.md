# Blazor Web App BoilerPlate

A quick startup template with Blazor server and client including Admin portal.

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
 * Here is the explaination of how I have setup Routes:
 1. Cascading Value: The CascadingValue component provides the CheckLayout function's result to the child components rendered by the RouteView.

2. CheckLayout Function: This function determines the appropriate layout based on the route and returns a LayoutComponentBase instance.

3. RouteView: The RouteView component now uses the default layout specified (@typeof(MainLayout)). It renders the matched component, and that component receives the layout information from the cascading value.

4. Child Components: When a child component is rendered, it checks the cascading value to determine which layout to use. If the CheckLayout function returns typeof(AdminLayout), the component will be rendered within the AdminLayout; otherwise, it will use the MainLayout.

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