# How to enable compiled binding for Xamarin.Forms ListView (SfListView)

To reduce the CPU cycles Xamarin.Forms has introduced compiled bindings and boost performance when using data binding.

You can enable [compiled binding](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/compiled-bindings?WT.mc_id=compiledbindings-xamarinblog-jamont) by using the special **x:DataType** attribute on any [VisualElement](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.visualelement) in Xamarin.Forms [SfListView](https://help.syncfusion.com/xamarin/listview/overview).

You can also refer to the following document regarding compiled bindings in Xamarin.Forms,

[https://devblogs.microsoft.com/xamarin/compiled-bindings-xamarin-forms/](https://devblogs.microsoft.com/xamarin/compiled-bindings-xamarin-forms/)

You can also refer the following article 

https://www.syncfusion.com/kb/11807/how-to-enable-compiled-binding-for-xamarin-forms-listview-sflistview

**XAML**

Define namespace of the ViewModel and set [BindingContext](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.bindableobject.bindingcontext#Xamarin_Forms_BindableObject_BindingContext) for the [ContentPage](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.contentpage).

```xml
<ContentPage xmlns:viewModel="clr-namespace:ListViewXamarin.ViewModel"
             x:DataType="viewModel:ContactsViewModel">
    <ContentPage.BindingContext>
        <viewModel:ContactsViewModel/>
    </ContentPage.BindingContext>
    <ContentPage.Content>
        <StackLayout>
            <syncfusion:SfListView x:Name="listView" ItemSize="60" ItemsSource="{Binding ContactsInfo}">
            </syncfusion:SfListView>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```
You need to set up complied binding for the [DataTemplate](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.datatemplate) by using **x:DataTye** , if you are using template control like **SfListView**.

``` xml
<ContentPage xmlns:model="clr-namespace:ListViewXamarin.Model">
    <syncfusion:SfListView x:Name="listView" ItemSize="60" ItemsSource="{Binding ContactsInfo}">
        <syncfusion:SfListView.ItemTemplate>
            <DataTemplate x:DataType="model:Contacts">
                <Grid x:Name="grid">
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="70" />
                        <ColumnDefinition Width="*" />
                    </Grid.ColumnDefinitions>
                    <Image Source="{Binding ContactImage}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="50" WidthRequest="50"/>
                    <Grid Grid.Column="1" RowSpacing="1" Padding="10,0,0,0" VerticalOptions="Center">
                        <Label LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ContactName}"/>
                        <Label Grid.Row="1" Grid.Column="0" TextColor="#474747" LineBreakMode="NoWrap" Text="{Binding ContactNumber}"/>
                    </Grid>
                </Grid>
            </DataTemplate>
        </syncfusion:SfListView.ItemTemplate>
    </syncfusion:SfListView>
</ContentPage>
```

For [SfListView.GroupHeaderTemplate](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~GroupHeaderTemplate.html), [BindingContext](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.bindableobject.bindingcontext#Xamarin_Forms_BindableObject_BindingContext) of **GroupHeaderTemplate** will be [GroupResult](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.DataSource.Portable~Syncfusion.DataSource.Extensions.GroupResult.html) which can be accessed from the [Syncfusion.DataSource.Extensions](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.DataSource.Portable~Syncfusion.DataSource.Extensions_namespace.html) of [Syncfusion.DataSource](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.DataSource.Portable~Syncfusion.DataSource_namespace.html).

``` xml
<ContentPage xmlns:result="clr-namespace:Syncfusion.DataSource.Extensions;assembly=Syncfusion.DataSource.Portable">
    <syncfusion:SfListView x:Name="listView" ItemSize="60" ItemsSource="{Binding ContactsInfo}">
        <syncfusion:SfListView.GroupHeaderTemplate>
            <DataTemplate x:DataType="result:GroupResult">
                <Grid BackgroundColor="#E4E4E4">
                    <Label Text="{Binding Key}" FontSize="18" FontAttributes="Bold" VerticalOptions="Center" HorizontalOptions="Start" Margin="20,0,0,0" />
                </Grid>
            </DataTemplate>
        </syncfusion:SfListView.GroupHeaderTemplate>
    </syncfusion:SfListView>
</ContentPage>
```
**Output**

![CompiledBindingGroupHeaderTemplate](https://github.com/SyncfusionExamples/compiled-binding-listview-xamarin/blob/master/ScreenShot/CompiledBindingGroupHeaderTemplate.png)
