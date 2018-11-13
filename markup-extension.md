# TOC

## Markup extension
* XAML markup extensions are not extensions of XML (XAML is entirely legal XML). They’re called “extensions” because they are backed by code in classes that implement IMarkupExtension
* You can write your own custom markup extensions
* Markup extension are important for data-binding
```xaml
    <StackLayout>
        <Button Text="Submit"
                Command = {Binding SubmitCommand} />

    </StackLayout>
```
`BingdingContext` is set in code behind:
```c#

```
