<img src="https://fynydd.com/images/carbide-icon.png" width="100" />

# Carbide

Carbide is a set of classes that provide Umbraco developers with additional high-level functionality. This API requires no commercial third party components.

**This project uses the newer project file "PackageResource" configuration for NuGet packages.** This means that Carbide's NuGet packages are downloaded to your user folder, and used much like assemblies in the GAC, so they won't interfere with the /packages folder in the root of your project if you're using the standard (default) packages.config method in your solution.

## Requirements
Currently, Carbide is built on .NET CLR 4.6.1, and references UmbracoCMS.Core 7.10.x. Depending on your use case, you could keep it at this version even with a newer Umbraco CMS version, provided there are no real incompatibilities with Core. Ideally, you want to keep the versions in lock-step. So any Carbide solutions should be updated frequently, which is generally a good practice from a security standpoint.

**NOTE: Turn on 64-bit IIS Express** in Visual Studio, or you won't be able to debug unless you set all projects to x86. This is due to *SharpScss* detecting which binary is being used based on compilation flags. It will default to x64 for "Any CPU" configurations. This shouldn't affect deployments to IIS, provided the app pool for the site isn't set to use 32-bit mode.

## Usage
Simply include the git repo as a submodule in your Umbraco solution, and add a project reference to it in any other projects. You can also place the project into your solution, but you'll lose the benefit of a single source for Carbide updates.

Once you add the project to your solution, be sure to reference it in your code where applicable:

<pre><code>using Fynydd.Carbide;</code></pre>
or in Razor views...
<pre><code>@using Fynydd.Carbide</code></pre>

## Carbide Methods and Enhancements
Following are the methods and other enhancements available in Carbide.

### Fynydd.Carbide.ConfigurationHelpers
These are static methods to use for retrieving web.config data.

### Fynydd.Carbide.EmailHelpers.Mailer
Instantiate this class to create and send email using the Send() methods.

### Fynydd.Carbide.ContentHelpers
These are static methods to use for retrieving (and scouring) content with as little code as possible.

### Fynydd.Carbide.ContextHelpers
These are static methods to use for ensuring an Umbraco context is available, as in class libraries, for example.

### Fynydd.Carbide.ExtensionMethods
These extension methods enhance existing Umbraco types, like IPublishedContent, to provide simple ways of retrieving and manipulating content.

### Fynydd.Carbide.RestHelper
Instantiate this class to make REST calls..

### SEO Helpers
Following are features to help with SEO and site indexing.

1. #### RobotsTxt
   If you add the following to your web.config, instances of {HTTP_HOST} in a robots.txt file at the root of your site will be swapped for the actual domain of the current site and served dynamically.
   
   ```
   <system.webServer>
     <handlers>
        <add name="RobotsTxt" path="/robots.txt" verb="*" type="Fynydd.Carbide.RobotsTxt" resourceType="Unspecified" preCondition="integratedMode" />
   ```

### Fynydd.Carbide.StorageHelpers
This is a static class with methods for reading and writing files to and from disk, dynamically building SCSS, creating cache busters for web file links, and more.

### Fynydd.Carbide.TemporalHelpers
This is a static class with methods for formatting dates and times, and performing date calculations. There is also a stopwatch class.

### Validators
Additional MVC model and client-side validators for your forms. To use client-side validation, be sure to include the scripts:

```
<script src="@Html.Raw(Url.Content("~/umbraco/api/carbidesupport/scripts/?file=FormValidationHelpers"))"></script>
```
1. #### MinimumFileSizeValidator
   ##### Model usage:
   Where # is the number of megabytes.
   
   ```
   [MinimumFileSizeValidator(#)]
   ```

2. #### MaximumFileSizeValidator
   ##### Model usage:
   Where # is the number of megabytes.
   
   ```
   [MaximumFileSizeValidator(#)]
   ```

3. #### ValidFileTypeValidator
   ##### Model usage:
   Accepts a string array list of valid file extensions, without leading periods.
   
   ```
   [ValidFileTypeValidator(new string[] { "pdf", "docx" })]
   ```

## WebAPI/Controller Endpoints
Following are the endpoints provided by Carbide.

1. **/umbraco/api/carbidesupport/scripts/**   
   Use this URL to generate a path to a JavaScript resource for client-side validation support, etc.

2. **/umbraco/api/carbidesupport/rebuildcache/**   
   Rebuild the content cache and Examine indexes, and refresh the content cache. 

   **/umbraco/api/carbidesupport/rebuildcachestatus/**   
   Get the current status of a rebuild.

   **/umbraco/api/carbidesupport/rebuildcachestatushistory/**   
   Get the last status of a rebuild.

## Developers
If you'd like to help make this library better through bug fixes or code additions, let me know through the usual means.

_Carbide is published into the open source community by Fynydd._

__License and Disclaimer__: Carbide is licensed under the MIT Open Source license, which can be read in the included file "LICENSE.txt".
