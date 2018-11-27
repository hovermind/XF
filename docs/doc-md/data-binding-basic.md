# TOC
* [Markup extensions for data binding](#markup-extensions-for-data-binding)
* [BindingContext](#binding-context)
* [Bind to other view property in same page](#bind-to-other-view-property-in-same-page)


## Markup extensions for data binding
| Markup extension | Property used in markup | purpose | Extension class |
|------------------|-------------------------|---------|-----------------|
| `"{Binding ...}"` | <ul><li>`Source`</li><li>`Path`</li></ul> | Bind source object.prop to the view | [BindingExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.bindingextension) |
| `"{x:Reference Name=... }"` | <ul><li>`Name`</li></ul> | Bind to other view property in same view | [ReferenceExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.referenceextension) |

## Binding Context
#### Set `BindingContext` in code behind
```
public partial class FooPage : ContentPage
{
    public FooPage()
    {
        InitializeComponent();
        BindingContext = new FooViewModel(...); // BindingContext for the entire page
    }
}
```
**Note:**
* setting `BindingContext` in code behind is preferred because ViewModel can be instantiated with constructor that accepts parameters
* while setting `BindingContext` in xaml, the ViewModel must have parameterless constructor and can't instantiate ViewModel with parameter

#### Use properties of `FooViewModel` in markup extension
```
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Demo.FooPage"
             Title="Data Binding Basic">
             
    <StackLayout Padding="10, 0">
        <Label Text="{Binding FooViewModelProp}" />
    </StackLayout>
    
</ContentPage>
```

## Bind to other view property in same page
Use: `x:Reference` markup extension
```
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Demo.FooPage"
             Title="Data Binding Basic">
             
    <StackLayout Padding="10, 0">

        <Slider x:Name="fooSlider"
                Maximum="360"
                VerticalOptions="CenterAndExpand" />
    
        <Label Text="Foo"
               BindingContext="{x:Reference Name=fooSlider}"
               Rotation="{Binding Path=Value}" />
               
    </StackLayout>
</ContentPage>
```
