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
