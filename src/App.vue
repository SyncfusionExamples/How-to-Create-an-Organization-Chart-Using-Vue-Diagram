<template>
  <ejs-diagram :width="width" :height="height" :layout="layout"
    :dataSourceSettings="dataSourceSettings" :getNodeDefaults="getNodeDefaults"
    :getConnectorDefaults="getConnectorDefaults" :snapSettings="snapSettings" />
</template>

<script>
import {
  DiagramComponent,
  DataBinding,
  HierarchicalTree,
  SnapConstraints
} from '@syncfusion/ej2-vue-diagrams';
import { DataManager } from '@syncfusion/ej2-data';

const employeeData = [
  { Name: 'Elizabeth', Role: 'Director' },
  { Name: 'Christina', ReportingPerson: 'Elizabeth', Role: 'Manager' },
  { Name: 'Yoshi', ReportingPerson: 'Christina', Role: 'Lead' },
  { Name: 'Philip', ReportingPerson: 'Christina', Role: 'SalesExecutive' },
  { Name: 'John', ReportingPerson: 'Yoshi', Role: 'Engineer' },
  { Name: 'James', ReportingPerson: 'Yoshi', Role: 'Engineer' },
  { Name: 'Robert', ReportingPerson: 'Christina', Role: 'Lead' },
  { Name: 'David', ReportingPerson: 'Robert', Role: 'Engineer' },
  { Name: 'Yang', ReportingPerson: 'Elizabeth', Role: 'Manager' },
  { Name: 'Roland', ReportingPerson: 'Yang', Role: 'Lead' },
  { Name: 'Paul', ReportingPerson: 'Roland', Role: 'Engineer' },
  { Name: 'Yvonne', ReportingPerson: 'Yang', Role: 'Lead' },
  { Name: 'Jack', ReportingPerson: 'Yvonne', Role: 'Engineer' }
];

export default {
  name: 'App',
  components: {
    "ejs-diagram": DiagramComponent
  },
  data() {
    return {
      width: '1302px',
      height: '602px',
      snapSettings: { constraints: SnapConstraints.None },
      getNodeDefaults: function (node) {
        node.height = 60;
        node.width = 150;
      },
      getConnectorDefaults: function (connector) {
        connector.type = 'Orthogonal';
        connector.style = {
          strokeColor: '#6f409f',
          fill: '#6f409f',
          strokeWidth: 2
        };
        connector.targetDecorator = {
          style: {
            fill: '#6f409f',
            strokeColor: '#6f409f'
          }
        };
      },
      layout: {
        type: 'OrganizationalChart'
      },
      dataSourceSettings: {
        id: 'Name',
        parentId: 'ReportingPerson',
        dataSource: new DataManager(employeeData),
        /*  id: "Id",
         parentId: "ParentId",
         dataSource: new DataManager(
           {
             url: "https://services.syncfusion.com/vue/production/api/RemoteData",
             crossDomain: true
           }), */
        doBinding: (nodeModel, data) => {
          nodeModel.annotations = [
            {
              content: data.Name,
              //content: data["Label"],
              offset: { x: 0.5, y: 0.4 },
              style: { color: 'white' }
            },
            {
              content: "(" + data.Role + ")",
              offset: { x: 0.5, y: 0.7 },
              style: { color: "white" }
            }
          ];
          nodeModel.style = { fill: '#048785', strokeWidth: 0 };
        }
      }
    };
  },
  provide: { diagram: [DataBinding, HierarchicalTree] }
};
</script>

<style>
@import '../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css';
</style>
