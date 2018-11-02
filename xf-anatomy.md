# TOC
* [xml namespace in `MainPage.xaml`](/xf-anatomy.md#xml-namespace-in-mainpagexaml)
* [code behind (`MainPage.xaml.cs`)](/xf-anatomy.md#code-behind)
* [ios specific code](/xf-anatomy.md#ios-specific-code)
* [android specific code](/xf-anatomy.md#android-specific-code)

## xml namespace in `MainPage.xaml`
`MainPage.xaml`
```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:FooApp"
             x:Class="FooApp.MainPage">

    <StackLayout>
        <Label Text="Welcome to Xamarin Forms!" VerticalOptions="Center" HorizontalOptions="Center" />
    </StackLayout>

</ContentPage>
```
#### `xmlns="http://xamarin.com/schemas/2014/forms"` (default namespace)
* means that tags defined within the XAML file with no prefix refer to classes in Xamarin.Forms i.e. `ContentPage`, `Label`

#### `xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"` (prefix x)
* used for several elements and attributes that are intrinsic to XAML itself (belonging naturally)
* `x:Class` attribute can only appear in the root element of a XAML file

#### `xmlns:local="clr-namespace:FooApp"`
* allows you to access other classes from the .NET Standard library project

## Code behind
`MainPage.xaml.cs`
```c#
using Xamarin.Forms;

namespace FooApp
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();
            MainPage = new MainPage();
        }
    }
}
```
* Code behind partial class: `MainPage.xaml.cs`
* `xaml` parsed partial class: `FooApp.MainPage.xaml.g.cs`
* `FooApp.MainPage.xaml.g.cs` partial class contains `InitializeComponent()` definition
* both partial class are merged to create main page
* MainPage property initialied to set inital page (launcher activity in Android)

## ios specific code
```c#
namespace FooApp.iOS
{
    [Register ("AppDelegate")]
    public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
    {
        public override bool FinishedLaunching (UIApplication app, NSDictionary options)
        {
            global::Xamarin.Forms.Forms.Init ();
            LoadApplication (new App ());
            return base.FinishedLaunching (app, options);
        }
    }
}
```
* **`global::Xamarin.Forms.Forms.Init()`** => loads iOS-specific implementation of Xamarin.Forms
* **`LoadApplication (new App())`** => loads application
* **`new App()`** => App class of .NET Standard library
* **App class constructor** => instantiates MainPage (`MainPage = new Mainpage()`)
* **MainPage class constructor** => calls InitializeComponent(), which then calls the `LoadFromXaml()` method that extracts the XAML file (or its compiled binary) from the .NET Standard library
* **`LoadFromXaml()`** => initializes all the objects defined in the XAML file

## android specific code
```c#
namespace FooApp.Droid
{
    [Activity(Label = "FooApp", 
              Icon = "@mipmap/icon", 
              Theme = "@style/MainTheme", 
              MainLauncher = true,
              ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        internal static MainActivity Instance { get; private set; }

        protected override void OnCreate(Bundle bundle)
        {
            TabLayoutResource = Resource.Layout.Tabbar;
            ToolbarResource = Resource.Layout.Toolbar;

            base.OnCreate(bundle);
            Instance = this;
            global::Xamarin.Forms.Forms.Init(this, bundle);
            LoadApplication(new App());
        }
    }
}
```
* **`global::Xamarin.Forms.Forms.Init(this, bundle)`** => loads Android-specific implementation of Xamarin.Forms
* `Instance = this` => local context (used by other classes in Andoid project only) 
* **`LoadApplication (new App())`** => loads application
* **`new App()`** => App class of .NET Standard library
* **App class constructor** => instantiates MainPage (`MainPage = new Mainpage()`)
* **MainPage class constructor** => calls InitializeComponent(), which then calls the `LoadFromXaml()` method that extracts the XAML file (or its compiled binary) from the .NET Standard library
* **`LoadFromXaml()`** => initializes all the objects defined in the XAML file

## Relationship between classes, properties, and XML
A Xamarin.Forms class (such as ContentPage or Label) appears in the XAML file as an XML element. Properties of that class—including Title on ContentPage and seven properties of Label—usually appear as XML attributes.
