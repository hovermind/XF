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
