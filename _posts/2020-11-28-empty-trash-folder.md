---
layout: post
title: "Empty a Trash Folder"
categories: SSJS
---

Unless you strictly manage data retention policy on each and every data extension, your collection of obsolete items grows over time. Users without rights to delete items from the user interface, can move such spare items to a *Trash* folder which then can be emptied by someone with delete permissions.

While unsuccessfully searching for a way to iterate over the items in a folder and delete them, a slightly different idea has eventually came to mind. Instead of deleting items from a trash folder in a series of iterations, perform two simple steps:

1. Delete a folder
2. (re)Create a folder

Then set up a monthly automation to clean the folder regularly.

## Use SSJS Core


```javascript
<script runat = "server" >

Platform.Load("Core", "1.1.1")

//DELETE OLD FOLDER - FULL of trash 
var myFolder = Folder.Retrieve({
    Property: "Name",
    SimpleOperator: "equals",
    Value: "TO_DELETE_DE"
    });

var delFolder = Folder.Init(myFolder[0].CustomerKey);
delFolder.Remove();

//CREATE NEW FOLDER - empty
var newFolder = {
    "Name": "TO_DELETE_DE",
    "CustomerKey": Platform.Function.GUID(),
    "Description": "Folder for obsolete items - trash",
    "ContentType": "dataextension",
    "IsActive": "true",
    "IsEditable": "false",
    "AllowChildren": "true",
    "ParentFolderID": myFolder[0].ParentFolder.ID
    };

Folder.Add(newFolder);

</script>
```


## Use SSJS WSProxy

### Static versions

```javascript
<script runat = "server" >

Platform.Load("core", "1.1.1");
var prox = new Script.Util.WSProxy();

cleanTrash("TO_DELETE_FILTERS", "filterdefinition");

function cleanTrash(folderName, contentType) {
    var cols = ["ObjectID", "ParentFolder.ID"]; //to delete a folder the ObjectID is needed; to create a folder an ID of the parent folder is needed
    var folderName = folderName;
    var contentType = contentType;
    var filter = {
        Property: "Name",
        SimpleOperator: "Equals",
        Value: folderName
    };
    var req = prox.retrieve("DataFolder", cols, filter);
    var folderObjID = req.Results[0].ObjectID;
    var parentFolderID = req.Results[0].ParentFolder.ID;
    var config = {
        "Name": folderName,
        "Description": "API created folder",
        "ParentFolder": {
            ID: parentFolderID,
            IDSpecified: true
        },
        "IsEditable": false,
        "AllowChildren": true,
        "ContentType": contentType
    };
    var delFolder = prox.deleteItem("DataFolder", {
        "ObjectID": folderObjID
    }); //delete the folder full of trash
    var createFolder = prox.createItem("DataFolder", config);
    return [delFolder, createFolder];
};

</script>
```

### Dynamic version

```javascript
<script runat = "server" >

Platform.Load("core", "1.1.1");
var prox = new Script.Util.WSProxy();

cleanTrash("TO_DELETE_FILTERS", "filterdefinition");

function cleanTrash(folderName, contentType) {
    var cols = ["ObjectID", "ParentFolder.ID"]; //to delete a folder the ObjectID is needed; to create a folder an ID of the parent folder is needed
    var folderName = folderName;
    var contentType = contentType;
    var filter = {
        Property: "Name",
        SimpleOperator: "Equals",
        Value: folderName
    };
    var req = prox.retrieve("DataFolder", cols, filter);
    var folderObjID = req.Results[0].ObjectID;
    var parentFolderID = req.Results[0].ParentFolder.ID;
    var config = {
        "Name": folderName,
        "Description": "API created folder",
        "ParentFolder": {
            ID: parentFolderID,
            IDSpecified: true
        },
        "IsEditable": false,
        "AllowChildren": true,
        "ContentType": contentType
    };
    var delFolder = prox.deleteItem("DataFolder", {
        "ObjectID": folderObjID
    }); //delete the folder full of trash
    var createFolder = prox.createItem("DataFolder", config);
    return [delFolder, createFolder];
};

</script>
```

Comment