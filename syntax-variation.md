## Attribute syntax
```xaml
<Label Text="Hello, XAML!"
       FontSize="Large"
       TextColor="Aqua" />
```

## Element syntax
```xaml
<Label>
    <Label.Text>
        Hello, XAML!
    </Label.Text>
    <Label.FontSize>
        Large
    </Label.FontSize>
    <Label.TextColor>
        Aqua
    </Label.TextColor>
</Label>
```

## When to use element syntax
* when the value of a property is too complex to be expressed as a simple string for example:  
RowDefinitions and ColumnDefinitions of the Grid
```xaml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
        <RowDefinition Height="100" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="100" />
    </Grid.ColumnDefinitions>
    ...
</Grid>
```
