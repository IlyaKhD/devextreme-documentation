Use the following properties to create a shape template:

* The [customShapeTemplate](/api-reference/10%20UI%20Components/dxDiagram/1%20Configuration/customShapeTemplate.md '/Documentation/ApiReference/UI_Components/dxDiagram/Configuration/#customShapeTemplate') property defines a common template for all shapes in the UI component.
* The [template](/api-reference/10%20UI%20Components/dxDiagram/1%20Configuration/customShapes/template.md '/Documentation/ApiReference/UI_Components/dxDiagram/Configuration/customShapes/#template') property defines a template for an individual shape.

[note]

If the [textExpr](/api-reference/10%20UI%20Components/dxDiagram/1%20Configuration/nodes/textExpr.md '/Documentation/ApiReference/UI_Components/dxDiagram/Configuration/nodes/#textExpr') option is specified, template content may overlap with text from the data source. 

Since the [textExpr](/api-reference/10%20UI%20Components/dxDiagram/1%20Configuration/nodes/textExpr.md '/Documentation/ApiReference/UI_Components/dxDiagram/Configuration/nodes/#textExpr') option has the default value `'text'`, the widget will obtain node texts from the data source’s 'text' field. To prevent his behavior, set the option to an empty string: `nodes: { textExpr: "", ...`.

[/note]

#include btn-open-demo with {
    href: "https://js.devexpress.com/Demos/WidgetsGallery/Demo/Diagram/CustomShapesWithTemplates/jQuery/Light/"
}

---
##### jQuery

    <!-- tab: index.js -->
    $(function() {
        var diagram = $("#diagram").dxDiagram({
            customShapeTemplate: function(item, $container) {
                var employee = item.dataItem;
                var $content = $("<svg class='template'>" +
                    "<text class='template-name' x='50%' y='20%'>" + (employee ? employee.Full_Name : "Employee's Name") + "</text>" +
                    "<text class='template-title' x='50%' y='45%'>" + (employee ? employee.Title : "Employee's Title") + "</text>" +
                    "<text class='template-button' id='employee-edit' x='40%' y='85%'>Edit</text>" +
                    "<text class='template-button' id='employee-delete' x='62%' y='85%'>Delete</text>" +
                    "</svg >");
                $container.append($content);
                $content.find("#employee-edit").click(function() { editEmployee(employee); });
                $content.find("#employee-delete").click(function() { deleteEmployee(employee); });
            },
            ...

##### Angular

    <!-- tab: app.component.html -->
    <dx-diagram id="diagram" #diagram customShapeTemplate="customShapeTemplate">
        <svg *dxTemplate="let item of 'customShapeTemplate'" class="template">
            <text class="template-name" x="50%" y="20%">{{item.dataItem ? item.dataItem.Full_Name : "Employee's Name"}}</text>
            <text class="template-title" x="50%" y="45%">{{item.dataItem ? item.dataItem.Title : "Employee's Title"}}</text>
            <text class="template-button" x="40%" y="85%" (click)="editEmployee(item.dataItem)">Edit</text>
            <text class="template-button" x="62%" y="85%" (click)="deleteEmployee(item.dataItem)">Delete</text>
        </svg>
        ...

##### Vue

    <!-- tab: App.vue -->
    <DxDiagram
      id="diagram"
      ref="diagram"
      custom-shape-template="CustomShapeTemplate"
    >
      <template #CustomShapeTemplate="{ data }">
        <CustomShapeTemplate
          :employee="data.dataItem"
          :edit-employee="editEmployee"
          :delete-employee="deleteEmployee"
        />
      </template>
      ...

    <!-- tab: CustomShapeTemplate.vue -->
    <template>
    <svg class="template">
        <text
        class="template-name"
        x="50%"
        y="20%"
        >
        {{ employeeName }}
        </text>
        <text
        class="template-title"
        x="50%"
        y="45%"
        >
        {{ employeeTitle }}
        </text>
        <text
        class="template-button"
        x="40%"
        y="85%"
        @click="editEmployeeFunc"
        >
        Edit
        </text>
        <text
        class="template-button"
        x="62%"
        y="85%"
        @click="deleteEmployeeFunc"
        >
        Delete
        </text>
    </svg>
    </template>
    ...

##### React

    <!-- tab: App.js -->
    import Diagram, { CustomShape, ContextToolbox, PropertiesPanel, Group, Tab, Toolbox, Nodes, AutoLayout } from 'devextreme-react/diagram';
    import CustomShapeTemplate from './CustomShapeTemplate.js';

    class App extends React.Component {
    constructor(props) {
        this.diagramRef = React.createRef();
        this.customShapeTemplate = this.customShapeTemplate.bind(this);
        ...
    }

    render() {
        return (
        <div id="container">
            <Diagram id="diagram" ref={this.diagramRef} customShapeRender={this.customShapeTemplate}>
            ...

    <!-- tab: CustomShapeTemplate.js -->
    export default function CustomShapeTemplate(employee, editEmployee, deleteEmployee) {
        var employeeName = employee ? employee.Full_Name : 'Employee\'s Name';
        var employeeTitle = employee ? employee.Title : 'Employee\'s Title';
        return (
            <svg className="template">
            <text className="template-name" x="50%" y="20%">{employeeName}</text>
            <text className="template-title" x="50%" y="45%">{employeeTitle}</text>
            <text className="template-button" x="40%" y="85%" onClick={editEmployee}>Edit</text>
            <text className="template-button" x="62%" y="85%" onClick={deleteEmployee}>Delete</text>
            </svg>
        );
    }


##### ASP.NET Core Controls

    <!-- tab: CustomShapesWithTemplatesWithEditing.cshtml -->
    @(Html.DevExtreme().Diagram()
        .ID("diagram")
        .CustomShapeTemplate(@<text>
            <svg class="template">
                <text class="template-name" x="50%" y="20%"><%- dataItem ? dataItem.FullName : "Employee's Name" %></text>
                <text class="template-title" x="50%" y="45%"><%- dataItem ? dataItem.Title : "Employee's Title" %></text>
                <text class="template-button" x="40%" y="85%" onclick="editEmployee(<%- dataItem && JSON.stringify(dataItem) %>)">Edit</text>
                <text class="template-button" x="62%" y="85%" onclick="deleteEmployee(<%- dataItem && JSON.stringify(dataItem) %>)">Delete</text>
            </svg>
            </text>)
        ...

##### ASP.NET MVC Controls

    <!-- tab: CustomShapesWithTemplatesWithEditing.cshtml -->
    @(Html.DevExtreme().Diagram()
        .ID("diagram")
        .CustomShapeTemplate(@<text>
            <svg class="template">
                <text class="template-name" x="50%" y="20%"><%- dataItem ? dataItem.FullName : "Employee's Name" %></text>
                <text class="template-title" x="50%" y="45%"><%- dataItem ? dataItem.Title : "Employee's Title" %></text>
                <text class="template-button" x="40%" y="85%" onclick="editEmployee(<%- dataItem && JSON.stringify(dataItem) %>)">Edit</text>
                <text class="template-button" x="62%" y="85%" onclick="deleteEmployee(<%- dataItem && JSON.stringify(dataItem) %>)">Delete</text>
            </svg>
            </text>)
            ...

---

![Diagram - Shape Template](/images/diagram/shape-template.png) 