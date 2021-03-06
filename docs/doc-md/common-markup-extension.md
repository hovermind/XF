# Syntax
`Property="{ markup_extension_here }"`

# Common markup entensions
| markup extension | purpose |
|------------------|---------|
| `{Binding ...}` <br />`{Binding ..., Converter={StaticResource ...}}` <br />(you can add `ConverterParameter`) | data binding (with [`BindingContext`] or [`Source` & `Path`]) |
| `{StaticResource ...}` | XAML resources with `x:key` |
| `{DynamicResource ...}` | Respond to changes in objects in a resource dictionary |
| `{TemplateBinding ...}` | Performs data binding from a control template |
| `{x:Static ...}` | Accesses one of the following: <ul> <li>a public static field</li> <li>a public static property</li> <li>a public constant field</li> <li>an enumeration member</li> </ul> |
| `{x:Reference ...}` <br /> `{x:Reference Name=...}` | Refers control (view i.e. Label) with `x:Name` |
| `{Binding Value, StringFormat='... {x:x} ...'}` <br /> (`StringFormat=''` => `''` is important) | String value converter <br /> `String.Format` will be called with format `{x:x}` |
| `{x:Type someClass}` | target type |
| `x:DataType="..."` <br /> `<DataTemplate x:DataType="local:FooViewModel">` | Compiled binding |
| `{x:Array ...}` | arrays in XAML |
| `{x:Null}` | to set `null` |   


Details: [Consuming XAML Markup Extensions](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/xaml/markup-extensions/consuming)
