## Common markup entensions
| markup extension | purpose |
|------------------|---------|
| `{Binding ...}` | data binding (with [`BindingContext`] or [`Source` & `Path`]) |
| `{StaticResource ...}` | XAML resources with `x:key` |
| `{x:Static ...}` | Accesses one of the following: <ul> <li>a public static field</li> <li>a public static property</li> <li>a public constant field</li> <li>an enumeration member</li> </ul> |
| `{x:Reference ...}` <br /> `{x:Reference Name=...}` | Refers control (view i.e. Label) with `x:Name` |
| `"{Binding Value, StringFormat='... {x:x} ...'}"` <br /> `StringFormat=''` => `''` is important |
| `{x:Type someClass}` | target type |
| `{x:Array ...}` | arrays in XAML |
| `{x:Null}` | to set `null` |
