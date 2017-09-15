csu_admin
======
Describe your app.

Installation
-
Give instructions on how to get started with it.

Usage
-

##Navbar Menu Generation

The Top Navbar is generated dynamically via handelbars, a html template and a initial configuration JSON object that defines the NavBar structure.
The NavBar is rendered once when the admin interface is loaded. Any changes to the NavBar after initialization is managed via your custom code.


top_menu - array of objects 
  - items
    - dropdown (a dropdown can contain top level item, html snippet or other nested dropdowns)
       - @param dropdown {boolean} - is this a dropdown? (true in this case)
       - @param tm-title": {string} 
       - @param tm-class": {string} "dropdown forView" in this case forView is used to hide show menu items by context
       - @param tm-id": {string} 
       - @param tm-items": {[]}  - array of submenu items (can contain top level item, html snippet or other nested dropdowns)
         - submenu items
          - @param submenu {string} example: "Create New",
          - @param sm-class {string} example:glyphicon glyphicon-arrow-left
          - @param menu-item {[]}  - array of submenu items (can contain top level item, html snippet or other nested dropdowns)
          - menu-item
          										"title": "Vendor",
          										"mi-icon-class": "glyphicon glyphicon-star",
          										"mi-class": "btn-createReport",
          										"data-id": "vendor"
          
    - top level item
       - @param title {string} example: "Back to view",
       - @param dropdown  {boolean} - is this a dropdown? (false in this case)
       - @param mi-icon-class {string} example:glyphicon glyphicon-arrow-left
       - @param mi-class {string} example: "btn-back-to-view forForm"
       - @param mi-click {string}  - javascript function to be evaluated on click "toggleView(\"view_pane\");"
    - top level html snippet
       - @param dropdown {boolean} - is this a dropdown? (false in this case)
       - @param html {boolean} - is this a html snippet? (true in this case)
       - @param content {string}   - html snippet
    
###Example JSON Definition 
```
"top_menu": [
  {
    "title": "Back to view",
    "dropdown": false,
    "mi-icon-class": "glyphicon glyphicon-arrow-left",
    "mi-class": "btn-back-to-view forForm",
    "mi-click": "toggleView(\"view_pane\");"
  },
  {
    "dropdown": true,
    "tm-title": "Actions",
    "tm-class": "dropdown forView",
    "tm-id": "view-action-menu",
    "tm-items": [
      {
        "submenu": "Create New",
        "sm-class": "glyphicon glyphicon-pencil",
        "menu-item": [
          {
            "title": "Vendor",
            "mi-icon-class": "glyphicon glyphicon-star",
            "mi-class": "btn-createReport",
            "data-id": "vendor"
          },
          {
            "title": "System User Status Profile",
            "mi-icon-class": "glyphicon glyphicon-glass",
            "mi-class": "btn-createReport",
            "data-id": "user_status"
          },
          {
            "title": "Business Unit Profile",
            "mi-icon-class": "glyphicon glyphicon-glass",
            "mi-class": "btn-createReport",
            "data-id": "bu"
          },
          {
            "title": "Reference Data",
            "mi-icon-class": "glyphicon glyphicon-glass",
            "mi-class": "btn-createReport",
            "data-id": "rd"
          },
          {
            "title": "Business Unit Invoicing Text",
            "mi-icon-class": "glyphicon glyphicon-glass",
            "mi-class": "btn-createReport",
            "data-id": "bu_it"
          }
        ]
      },
      {
        "title": "Delete Selected",
        "mi-icon-class": "",
        "mi-class": "btn-deleteSelected"
      }
    ]
  },
  {
    "dropdown": true,
    "tm-title": "Actions",
    "tm-class": "dropdown forForm",
    "tm-id": "export-menu",
    "tm-items": [
      {
        "mi-class": "",
        "title": " Save",
        "mi-icon-class": "glyphicon glyphicon-save",
        "mi-id": "menu-save",
        "mi-click": "$('#form_pane form:first').trigger('submit');"
      },
      {
        "mi-class": "",
        "title": " TEST",
        "mi-icon-class": "glyphicon glyphicon-save",
        "mi-id": "test123",
        "mi-click": "$.getJSON('https://dom01d.toronto.ca/inter/city/verify.nsf/rest.xsp/restapi/keys/921010SKYWALKER',function(data){console.log(data)});"
      }
    ]
  },
  {
    "dropdown": true,
    "tm-title": "View",
    "tm-class": "dropdown",
    "tm-id": "view-menu",
    "tm-items": [
      {
        "submenu": "System Admin",
        "sm-class": "glyphicon glyphicon-star",
        "menu-item": [
          {
            "title": "Vendor Profiles",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "vendor",
            "data-status": "",
            "data-filter": ""
          },
          {
            "title": "System User Status Profiles",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "user_status",
            "data-status": "",
            "data-filter": ""
          },
          {
            "title": "Business Unit Profile",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "bu",
            "data-status": "",
            "data-filter": ""
          },
          {
            "title": "Reference Data",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "rd",
            "data-status": "",
            "data-filter": ""
          },
          {
            "title": "Business Unit Invoicing Text",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "bu_it",
            "data-status": "",
            "data-filter": ""
          }
        ]
      },
      {
        "submenu": "Work Orders",
        "sm-class": "glyphicon glyphicon-glass",
        "menu-item": [
          {
            "title": "All Events",
            "mi-class": "tablink",
            "mi-icon-class": "",
            "data-id": "hot_eats",
            "data-status": "",
            "data-filter": ""
          },
          {
            "title": "Pending Events",
            "mi-class": "tablink",
            "data-id": "hot_eats",
            "data-status": "Pending",
            "data-filter": "{\"items\":[{\"field\":\"he_eventStatus\",\"value\":\"Pending\"}]}"
          },
          {
            "title": "Approved Events",
            "mi-class": "tablink",
            "data-id": "hot_eats",
            "data-status": "Approved",
            "data-filter": "{\"items\":[{\"field\":\"he_eventStatus\",\"value\":\"Approved\"}]}"
          }
        ]
      }
    ]
  },
  {
    "dropdown": true,
    "tm-title": "Export",
    "tm-class": "dropdown forView",
    "tm-id": "export-menu",
    "tm-items": [
      {
        "mi-class": "tabexport",
        "title": " PDF",
        "mi-icon-class": "fa fa-file-pdf-o",
        "mi-id": "tabExportPDF"
      },
      {
        "mi-class": "tabexport",
        "title": " CSV",
        "mi-icon-class": "fa fa-file-code-o",
        "mi-id": "tabExportCSV"
      },
      {
        "mi-class": "tabexport",
        "title": " EXCEL",
        "mi-icon-class": "fa fa-file-excel-o",
        "mi-id": "tabExportEXCEL"
      },
      {
        "mi-class": "tabexport",
        "title": " Copy",
        "mi-icon-class": "fa fa-clone",
        "mi-id": "tabExportCopy"
      }
    ]
  },
  {
    "dropdown": false,
    "html": true,
    "content": "<div class=\"forView\" id=\"custom-search-input\" style=\"width:200px !important;margin:3px;\"><div class=\"input-group\" ><div class=\"form-group has-feedback has-clear\" ><label for=\"admin_search\" class=\"sr-only\" >Site wide search input </label><input id=\"admin_search\" class=\"form-control\"  placeholder=\"keywordsearch\" name=\"admin_search\"><span class=\"form-control-clear glyphicon glyphicon-remove form-control-feedback hidden\"></span></div></div></div>"
  },
  {
    "dropdown": true,
    "tm-title": " UserName",
    "tm-class": "dropdown",
    "tm-icon-class": "glyphicon glyphicon-user",
    "tm-id": "user_auth",
    "tm-items": [
      {
        "title": "Logout",
        "mi-id": "lo_username",
        "mi-icon-class": "glyphicon glyphicon-log-out",
        "mi-click": "cot_login_app.logout();"
      }
    ]
  }
]
```
