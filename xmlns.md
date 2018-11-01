## MainPage.xaml
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
