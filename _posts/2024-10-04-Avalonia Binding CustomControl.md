---
title: Avalonia Binding Inside Custom Control
date: 2024-10-04
categories: [dotnet, ui]
tags: [data-binding, dotnet, csharp]     # TAG names should always be lowercase
---

If you have experience with WPF (Windows Presentation Foundation), you will find that Avalonia shares many similarities with it. However, Avalonia offers several enhancements, particularly in its binding syntax. For instance, consider a scenario where you have a custom UserControl with a custom dependency property. Avalonia provides a more streamlined and efficient approach to implementing such features. 


```csharp
   public static readonly StyledProperty<string> TitleProperty =
            AvaloniaProperty.Register<TControl, string>(nameof(Title));
```

To bind to a custom property from your AXAML code, you can use the expression `$parent[model:TControl].Title`. This expression allows you to specify the type of your custom UserControl within the brackets `[]`, enabling access to your custom `Title` property.

However, it's important to note that if you are working within a `<DataTemplate>`, this approach will not be effective. In such cases, it's recommended to use a named expression like `#myControlName.Title` instead.

Below is an example of how you can implement this in your AXAML code for a custom user control.


```xml

<UserControl xmlns="https://github.com/avaloniaui"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             mc:Ignorable="d" d:DesignWidth="800" d:DesignHeight="450"
			 xmlns:model="using:Configurator.Controls"
			 x:Class="Configurator.Controls.TControl"
			 x:DataType="model:TControl">

	<Grid Margin="12" >

		<Border Grid.Row="0" BorderThickness="0,0,0,1">
			<TextBlock Text="{Binding $parent[model:TControl].Title}" Foreground="Aqua"
					   FontSize="16" FontWeight="Bold" Margin="10"/>
		</Border>
        ...
	</Grid>
</UserControl>

```

## References

[Avalonia Docs - Binding to controls](https://docs.avaloniaui.net/docs/guides/data-binding/binding-to-controls)