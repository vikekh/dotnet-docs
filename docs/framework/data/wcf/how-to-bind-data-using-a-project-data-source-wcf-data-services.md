---
title: "How to: Bind Data Using a Project Data Source (WCF Data Services)"
ms.date: "03/30/2017"
dev_langs:
  - "csharp"
  - "vb"
helpviewer_keywords:
  - "data binding, WCF Data Services"
  - "WCF Data Services, data binding"
ms.assetid: 2477af0a-676f-44f7-b73d-e66208785509
---
# How to: Bind Data Using a Project Data Source (WCF Data Services)

You can create data sources that are based on the generated data objects in an WCF Data Services client application. When you add a reference to a data service by using the **Add Service Reference** dialog, a project data source is created along with the generated client data classes. One data source is created for each entity set that the data service exposes. You can create forms that display data from the service by dragging these data source items from the **Data Sources** window onto the designer. These items become controls that are bound to the data source. During execution, this data source is bound to an instance of the <xref:System.Data.Services.Client.DataServiceCollection%601> class, which is filled with objects that are returned by a query to the data service. For more information, see [Binding Data to Controls](binding-data-to-controls-wcf-data-services.md).

 The examples in this topic use the Northwind sample data service and autogenerated client data service classes. This service and the client data classes are created when you complete the [WCF Data Services quickstart](quickstart-wcf-data-services.md).

## Use a project data source in a WPF window

1. In Visual Studio, in a WPF project, add a reference to the Northwind data service. For more information, see [How to: Add a Data Service Reference](how-to-add-a-data-service-reference-wcf-data-services.md).

2. In the **Data Sources** window, expand the `Customers` node in the **NorthwindEntities** project data source.

3. Click the **CustomerID** item, select **ComboBox** from the list, and drag the **CustomerID** item from the **Customers** node to the designer.

     This creates the following object elements in the XAML file for the window:

    - A <xref:System.Windows.Data.CollectionViewSource> element named `customersViewSource`. The <xref:System.Windows.FrameworkElement.DataContext%2A> property of the top-level <xref:System.Windows.Controls.Grid> object element is set to this new <xref:System.Windows.Data.CollectionViewSource>.

    - A data-bound <xref:System.Windows.Controls.ComboBox> named `CustomerID`.

    - A <xref:System.Windows.Controls.Label>.

4. Drag the **Orders** navigation property to the designer.

     This creates the following additional object elements in the XAML file for the window:

    - A second <xref:System.Windows.Data.CollectionViewSource> element named `customersOrdersViewSource`, the source of which is the `customerViewSource`.

    - A data-bound <xref:System.Windows.Controls.DataGrid> control named `ordersDataGrid`.

5. (Optional) Drag additional items from the **Customers** node to the designer.

6. Open the code page for the form and add the following `using` statements (`Imports` in Visual Basic):

     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersusingwpf)]

7. In the partial class that defines the form, add the following code that creates an <xref:System.Data.Objects.ObjectContext> instance and defines the `customerID` constant.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersdefinitionwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf2.xaml.vb#customersordersdefinitionwpf)]

8. In the designer, select the window.

    > [!NOTE]
    > Make sure that you select the window itself, rather than selecting content that is within the window. If the window is selected, the **Name** text box near the top of the **Properties** window should contain the name of the window.

9. In the **Properties** window, select the **Events** button.

10. Find the **Loaded** event, and then double-click the drop-down list next to this event.

     Visual Studio opens the code-behind file for the window and generates a <xref:System.Windows.FrameworkElement.Loaded> event handler.

11. In the newly created <xref:System.Windows.FrameworkElement.Loaded> event handler, copy and paste the following code.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersdatabindingwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf2.xaml.vb#customersordersdatabindingwpf)]

12. This code creates an instance of <xref:System.Data.Services.Client.DataServiceCollection%601> for the `Customers` type based on the execution of a LINQ query that returns an <xref:System.Collections.Generic.IEnumerable%601> of `Customers` along with related `Orders` objects from the Northwind data service and binds it to the `customersViewSource`.

## Use a project data source in a Windows form

1. In the **Data Sources** window, expand the **Customers** node in the **NorthwindEntities** project data source.

2. Click the **CustomerID** item, select **ComboBox** from the list, and drag the **CustomerID** item from the **Customers** node to the designer.

     This creates the following controls on the form:

    - An instance of <xref:System.Windows.Forms.BindingSource> named `customersBindingSource`.

    - An instance of <xref:System.Windows.Forms.BindingNavigator> named `customersBindingNavigator`. You can delete this control as it will not be needed.

    - A data-bound <xref:System.Windows.Forms.ComboBox> named `CustomerID`.

    - A <xref:System.Windows.Forms.Label>.

3. Drag the **Orders** navigation property to the form.

4. This creates the `ordersBindingSource` control with the <xref:System.Windows.Forms.BindingSource.DataSource%2A> property of the control set to the `customersBindingSource` and the <xref:System.Windows.Forms.BindingSource.DataMember%2A> property set to `Customers`. It also creates the `ordersDataGridView` data-bound control on the form, accompanied by an appropriately titled label control.

5. (Optional) Drag additional items from the **Customers** node to the designer.

6. Open the code page for the form and add the following `using` statements (`Imports` in Visual Basic):

     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersusing)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersusing)]

7. In the partial class that defines the form, add the following code that creates an <xref:System.Data.Objects.ObjectContext> instance and defines the `customerID` constant.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdefinition)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdefinition)]

8. In the form designer, double-click the form.

     This opens the code page for the form and creates the method that handles the `Load` event for the form.

9. In the `Load` event handler, copy and paste the following code.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdatabinding)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdatabinding)]

10. This code creates an instance of <xref:System.Data.Services.Client.DataServiceCollection%601> for the `Customers` type based on the execution of a <xref:System.Data.Services.Client.DataServiceQuery%601> that returns an <xref:System.Collections.Generic.IEnumerable%601> of `Customers` from the Northwind data service and binds it to the `customersBindingSource`.

## See also

- [WCF Data Services Client Library](wcf-data-services-client-library.md)
- [How to: Bind Data to Windows Presentation Foundation Elements](bind-data-to-wpf-elements-wcf-data-services.md)
