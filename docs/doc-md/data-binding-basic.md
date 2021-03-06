# TOC
* [Markup extensions for data binding](#markup-extensions-for-data-binding)
* [BindingContext](#binding-context)
* [Bind to other view property in same page](#bind-to-other-view-property-in-same-page)


## Markup extensions for data binding
| Markup extension | Property used in markup | Extension class |
|------------------|-------------------------|-----------------|
|<ul><li>`"{Binding ...}"` : Bind `SourceObject.Prop` to the view</li><li>`"{Binding}"` : `BindingContext` itself binds to the view</li></ul> | <ul><li>`Source`</li><li>`Path`</li><li>`Mode`</li><li>`StringFormat`</li><li>`Converter`</li><li>`FallbackValue`</li><li>`TargetNullValue`</li></ul> | [BindingExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.bindingextension) |
| <ul><li>`{x:Reference ...}` : Bind to other view property in same view</li></ul> | <ul><li>`Name`</li></ul> | [ReferenceExtension](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.xaml.referenceextension) |

**Notes:**
* Always set `Mode` (See: [BindingMode](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.bindingmode?view=xamarin-forms)) property explicitly to avoid unexpected behaviors from default value of `Mode`
* `Path` property can go down to property hierarchy (i.e. `Foo.Bar.Baz`) & can access element of indexer (i.e. `Foo.Bar.Baz[n]` where Baz is an indexer)
*  `StringFormat='... {0:xx}...'` single quote: '' is mandatory, use `&quot;` for double quote inside
* If `StringFormat` & `Converter` are both set, the value converter is invoked before the result is formatted as a string
* if `FallbackValue` & `TargetNullValue` are set directly, then single quote is needed (recommended: define as static resource => `Text="{Binding FooProp, FallbackValue={StaticResource fooDefault}}"`)
* It's not possible to set the `FallbackValue` &  `TargetNullValue` properties with a binding expression
* A defined value converter is not executed in a binding expression when the `FallbackValue` property is set
* String formatting is not applied in a binding expression when the `TargetNullValue` property is set


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
