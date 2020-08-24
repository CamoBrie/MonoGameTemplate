# MonoGameTemplate

https://www.reddit.com/r/monogame/comments/cst49i/the_ultimate_guide_to_getting_started_with/

## prerequisites

#### Prerequisites Part 1:

Download and install the latest versions of the following:

1. Visual Studio Code

2. MonoGame for Visual Studio (we only need the pipeline tool)

3. .NET Core SDK

#### Prerequisites Part 2:

NOTE: You only need to run the following commands once.

Install NUnit templates for writing unit tests:

> dotnet new -i NUnit3.DotNetNew.Template

Install MonoGame project templates.

> dotnet new -i MonoGame.Template.CSharp



## Step-by-Step guide:

### If you get errors, most of the time it can be solved using this or restarting vscode.
    dotnet restore


### 1. Create the solution and the app.
    dotnet new sln
    dotnet new mgdesktopgl -o <MyProject>
    dotnet sln add <MyProject>/<MyProject>.csproj

### 2. Edit the \<MyProject>/\<MyProject>.csproj file 
   <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
         <OutputType>WinExe</OutputType>
         <!-- Set to "netcoreapp" plus the first 2 digits of your .NET Core SDK version. -->
         <TargetFramework>netcoreapp3.0</TargetFramework>
         <TargetLatestRuntimePatch>true</TargetLatestRuntimePatch>
     </PropertyGroup>

     <ItemGroup>
         <MonoGameContentReference Include="**\*.mgcb" />
     </ItemGroup>

     <ItemGroup>
         <PackageReference Include="MonoGame.Content.Builder" Version="3.7.0.4" />
         <PackageReference Include="MonoGame.Framework.DesktopGL.Core" Version="3.7.0.7" />
     </ItemGroup>

     <!-- Actually cleans your project when you run "dotnet clean" -->
     <Target Name="SpicNSpan"  AfterTargets="Clean">
         <!-- Remove obj folder -->
         <RemoveDir Directories="$(BaseIntermediateOutputPath)" />
         <!-- Remove bin folder -->
         <RemoveDir Directories="$(BaseOutputPath)" />
     </Target>

 </Project>
 
 ### 3. Add a folder for the tests.
       └── <MyProject>
          ├── <MyProject>.sln
          ├── <MyProject>
          |   └── <MyProject>.csproj
          └── <MyProject>.Tests

### 4. Add the references and the Test to the solution.
    cd ./<Myproject>.Tests
    dotnet new nunit
    dotnet add reference ../<MyProject>/<MyProject>.csproj
    cd ..
    dotnet sln add ./<MyProject>.Tests/<MyProject>.Tests.csproj

### 5. in \<MyProject>.Tests/\<Package>/\<MyClassTests>.cs 
    using NUnit.Framework;
 
     namespace <MyProject>.Tests.<Package>
     {
      [TestFixture]
     public class <MyClassTests>
     {
     
         [SetUp]
         public void SetUp()
         {
             // Code here will be run once before every test.
         }
         
         [TearDown]
         public void TearDown()
         {
             // Code here will be run once after every test.
         }
         
         [Test]
         public void FunctionBeingTested1_Condition_ExpectedResult()
         {
             // Write some test code.
             // e.g. Assert.AreEqual(expectedValue, actualValue);
         }
         
         [Test]
         [Repeat(100)]
         public void FunctionBeingTested2_Condition_ExpectedResult()
         {
             // Tests can also be repeated N times.
             // Here, this test will be repeated 100 times.
             
             // Write some test code.
             // e.g. Assert.AreEqual(expectedValue, actualValue);
         }
     }
    }
 
 ### 6. Useful commands
    dotnet test //for running the tests
    dotnet clean //for clean the folders
    dotnet build //for building the app
    
### 7. Create an executable
    Windows:
     dotnet clean
     dotnet build
     dotnet publish -r win-x64 -c release

    Mac:
     dotnet clean
     dotnet build
     dotnet publish -r osx-x64 -c release

    Linux:
     dotnet clean
     dotnet build
     dotnet publish -r linux-x64 -c release
     
