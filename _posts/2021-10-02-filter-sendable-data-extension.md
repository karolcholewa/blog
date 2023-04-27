---
layout: post
title: "Filter Sendable Data Extension Using SSJS"
categories: [SSJS]
---

To filter a sendable data extension using the **Filters** functionality is a way to go in any project. However, for repetitive, regular tasks to filter dozen of sendable data extensions into tens of filtered data extensions (e.g. by language or a country) a script is my preferred method.

## Clone Instead of Filtering
I could not find a method to filter a source DE or to refresh already filtered data extension. Renaming already created batches was cumbersome too. I am sure there is a way to do it but I found a different solution. I clone the main source DE using a simple filter for cloning criteria. By default the **retrieve** method calls up to 2500 records. The script is optimized to pull all the records that meet criteria.

```javascript
<script runat = "server">
Platform.Load("core", "1.1.1");

var countries = ['Austria', 'Germany', 'Switzerland'];

//execute the function, create lists in the loop for each country

for (var i = 0; i < countries.length; i++) {
    var resp = cloneDataExtension('SourceDEName', 'SourceDECustomerKey', '123456', countries[i], 'NewDEName');
    //Write(records);
    //Write(resp);
};


//function definition for cloning the DE and its records  

function cloneDataExtension(DEName, CustomerKey, FolderID, Country, newDEName) {
    var prox = new Script.Util.WSProxy();
    var DE = DataExtension.Init(CustomerKey); //initiate the cloned DE
    var fields = DE.Fields.Retrieve(); //get all the fields from DE

    var config = {
        name: DEName,
        cols: ['SubscriberKey','EmailAddress','Language','ID','Country', 'FirstName','LastName'],
        filter: {
            Property: 'Country',
            SimpleOperator: 'equals',
            Value: Country
        }
    };

    var records = retrieveRecords(config);

    for (var i = 0; i < fields.length; i++) {
        if (fields[i]['IsPrimaryKey'] == true)
            fields[i]['IsRequired'] = true;
    }
    var NewCustomerKey = Platform.Function.GUID();
    /*var randomNumber = Stringify(Math.floor(Math.random() * 1000));*/
    var recordCount = Stringify(records.length);

    var ClonedDE = {
        'CustomerKey': NewCustomerKey,
        'Name': COP + '-' + newDEName + '-' + recordCount,
        'CategoryID': FolderID,
        'Fields': fields,
        'IsSendable': true,
        'SendableSubscriberField': {
            'Name': 'Subscriber Key'
        },
        'SendableDataExtensionField': {
            'Name': 'SubscriberKey'
        }
    }

    if (records.length > 0) {
        var newDE = prox.createItem("DataExtension", ClonedDE);
    };

    newDE = DataExtension.Init(NewCustomerKey);
    newDE.Rows.Add(records);

}

function retrieveRecords(config) {

    var prox = new Script.Util.WSProxy();

    var records = [],
        moreData = true,
        reqID = data = null;

    while (moreData) {
        moreData = false;

        if (reqID == null) {
            data = prox.retrieve("DataExtensionObject[" + config.name + "]", config.cols, config.filter);
        } else {
            data = prox.getNextBatch("DataExtensionObject[" + config.name + "]", reqID);
        }

        if (data != null) {
            moreData = data.HasMoreRows;
            reqID = data.RequestID;
            for (var i = 0; i < data.Results.length; i++) {
                var result_list = data.Results[i].Properties;
                var obj = {};
                for (k in result_list) {
                    var key = result_list[k].Name;
                    var val = result_list[k].Value
                    if (key.indexOf("_") != 0) obj[key] = val;
                }
                records.push(obj);
            }
        }

    }

    return records;
}
</script>
```