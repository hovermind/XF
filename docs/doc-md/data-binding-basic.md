# TOC
* [Markup extensions for data binding](#markup-extensions-for-data-binding)
* [BindingContext](#binding-context)
* [Bind to other view property in same page](#bind-to-other-view-property-in-same-page)


## Markup extensions for data binding
| Markup extension | Property used in markup | Purpose | Extension class |
|------------------|-------------------------|---------|-----------------|
| `"{Binding ...}"` | <ul><li>`Source`</li><li>`Path`</li><li>`Mode` (See: [BindingMode](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.bindingmode?view=xamarin-forms))</li></ul> | Bind `SourceObject.Prop` to the view | [BindingExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.bindingextension) |
| `"{x:Reference ...}"` | <ul><li>`Name`</li></ul> | Bind to other view property in same view | [ReferenceExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.referenceextension) |

**Note:** Always set `Mode` property explicitly to avoid unexpected behaviors from default value of `Mode` 

#### BindingContext and Syntax
| `BindingContext` | Syntax |
|------------------|--------|
| **not set** | `"{Binding Source={StaticResource fooViewModel}, Path=fooProp}"` |
| **set** | `"{Binding Path=fooProp}"` |

#### Syntactic sugar
| Syntactic sugar | Full syntax |
|-----------------|-------------|
| `"{Binding fooProp}"` | `"{Binding Path=fooProp}"` |
| `"{Binding fooProp, Source={StaticResource fooViewModel}}"` | `"{Binding Source={StaticResource fooViewModel}, Path=fooProp}"` |
| `"{Binding Value, Source={x:Reference viewName}}"` | `"{Binding Source={x:Reference viewName}, Path=Value}"` |

#### Alternative element syntax:
```
<Label.Scale>
	<Binding Path="Value">
		<Binding.Source>
			<x:Reference Name="viewName" />
		</Binding.Source>
	</Binding>
</Label.Scale>
```

## Binding Context
The setting of the `BindingContext` property is inherited through the visual tree - means if you set `BindingContext` property of parent view, all child views will inherit that `BindingContext`.

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

#### Use properties of ViewModel in markup extension
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
