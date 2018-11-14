## `StaticResource` Markup Extension
* Used to access `xaml` resource from resource dictionary (returns an object from resource dictionary)
* `StaticResource` markup extension is supported by XAML implementations that define a resource dictionary

## `x:Static` Markup Extension
* `x:Static` is an intrinsic part of XAML (as the x prefix reveals)
* `x:Static` accesses one of the following:
  * a public static field
  * a public static property
  * a public constant field
  * an enumeration member

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:Foo">

    <StackLayout>
       <Label Text="Name"
              TextColor="{x:Static local:AppConstants.FooColor}" />

    </StackLayout>
</ContentPage>
```
