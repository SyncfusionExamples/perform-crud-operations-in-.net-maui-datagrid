# Perform the CRUD operations in .net maui datagrid

The .NET [MAUI DataGrid](https://www.syncfusion.com/maui-controls/maui-datagrid)(SfDataGrid) listens and respond to the CRUD operations such as add, delete and data update (property change) at runtime. DataGrid automatically refresh the UI when rows are added, deleted or cleared.

## C#
Implement the collection with [INotifyPropertyChanged](https://learn.microsoft.com/en-us/dotnet/api/system.collections.specialized.inotifycollectionchanged?view=net-7.0) interface.

```C#
    public class ViewModel : INotifyPropertyChanged
    {
        private ObservableCollection<OrderInfo> orderInfo;
        private ICommand buttonCommand;
        public ObservableCollection<OrderInfo> OrderInfoCollection
        {
            get { return orderInfo; }
            set { this.orderInfo = value; RaisePropertyChanged("OrderInfoCollection"); }
        }
        public ICommand ButtonCommand
        {
            get { return buttonCommand; }
            set { buttonCommand = value; }
        }

        public ViewModel()
        {
            this.OrderInfoCollection = new ObservableCollection<OrderInfo>();
            this.GenerateOrders();
            this.ButtonCommand = new Command(AddRecord);
        }

        public void GenerateOrders()
        {
            this.OrderInfoCollection.Add(new OrderInfo(1001, "Ana Trujillo", "Mexico", "ANATR"));
            this.OrderInfoCollection.Add(new OrderInfo(1002, "Ant Fuller", "Mexico", "ANTON"));
            this.OrderInfoCollection.Add(new OrderInfo(1003, "Thomas Hardy", "UK", "AROUT"));
        }

        private void AddRecord()
        {
            this.OrderInfoCollection.Add(new OrderInfo(1004, "Tim Adams", "Sweden", "BERGS"));
            this.OrderInfoCollection.Add(new OrderInfo(1005, "Hanna Moos", "Germany", "BLAUS"));
            this.OrderInfoCollection.Add(new OrderInfo(1006, "Andrew Fuller", "France", "BLONP"));
            this.OrderInfoCollection.Add(new OrderInfo(1007, "Martin King", "Spain", "BOLID"));
            this.OrderInfoCollection.Add(new OrderInfo(1008, "Lenny Lin", "France", "BONAP"));
            this.OrderInfoCollection.Add(new OrderInfo(1009, "John Carter", "Canada", "BOTTM"));
            this.OrderInfoCollection.Add(new OrderInfo(1010, "Laura King", "UK", "AROUT"));
        }

        #region INotifyPropertyChanged

        public event PropertyChangedEventHandler PropertyChanged;

        private void RaisePropertyChanged(string name)
        {
            if (PropertyChanged != null)
                this.PropertyChanged(this, new PropertyChangedEventArgs(name));
        }

        #endregion
    }
```

## XAML
Bind the ViewModel collection to the [ItemsSource](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataGrid.SfDataGrid.html#Syncfusion_Maui_DataGrid_SfDataGrid_ItemsSource) property and a new data to the ViewModel collection with a button click.

```XAML
 <StackLayout >
        <Button Command="{Binding ButtonCommand}" Text="AddRow"></Button>
        <syncfusion:SfDataGrid x:Name="dataGrid" AutoGenerateColumnsMode="None" VerticalOptions="FillAndExpand" ItemsSource="{Binding OrderInfoCollection}" DefaultColumnWidth="130" GridLinesVisibility="Both" HeaderGridLinesVisibility="Both">
            <syncfusion:SfDataGrid.Columns>
                <syncfusion:DataGridNumericColumn MappingName="OrderID" Format="D" HeaderText="ID"></syncfusion:DataGridNumericColumn>
                <syncfusion:DataGridTextColumn MappingName="Customer" HeaderText="Name"></syncfusion:DataGridTextColumn>
                <syncfusion:DataGridTextColumn MappingName="Country"></syncfusion:DataGridTextColumn>
            </syncfusion:SfDataGrid.Columns>
        </syncfusion:SfDataGrid>
    </StackLayout>
```
