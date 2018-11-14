# TOC

## Markup extension
* XAML markup extensions are not extensions of XML (XAML is entirely legal XML). They’re called “extensions” because they are backed by code in classes that implement IMarkupExtension
* You can write your own custom markup extensions
* Markup extension are important for data-binding
* Example: `{Binding ...}`, `{StaticResource ...}`
```xaml
<StackLayout>

    <Entry Text="{Binding FooInput}" />

    <Button Text="Add"
            Command = "{Binding AddCommand}" />

</StackLayout>
```
`BingdingContext` is set in code behind:
```c#
public class FooContentPage : ContentPage {

    public FooContentPage(){
        BindingContext = new FooViewModel();
    }
}

public class FooViewModel {
    string FooInput {get; set}
    ICommand AddCommand {get; set}
}
```
