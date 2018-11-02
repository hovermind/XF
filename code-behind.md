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
