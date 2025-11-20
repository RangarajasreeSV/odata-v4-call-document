# odata-v4-call-document
Document for odata v4 fiori 

From RAP or CAP odata v4 service , we will generally use the following methods or syntaxes for CRUD operations.

Pre-requisites :
 1) Add mainService in the manifest.json
 2) Make it as "" in the dataSource

Steps :
==============================================================================================================================================================
 ->  GET or READ call :
  // This will get the mainService Model
   var oModel = this.getOwnerComponent().getModel();
   // Pass the model name in the getModel() if its registered with specific name in manifest.json

   var oListBinding = oModel.bindList("/EntitySetName",undefined,undefined,undefined,{
                       $expand : "<Deep-Entity-Name",  or  $expand : "1stDeepEntity,2ndDeepEntity($expand=3rdDeepEntity)", (add when ever its required)
                       $filter : "FieldName eq'"+PropertyValue"'"  (add when ever its required)
   }
      // aFilters is the filters array that can be created with many filters using a get call
      // filters() is added when ever filter data is given , and fetching the data using the filters
      var aContexts = await oListBinding.filter(aFilters).requestContexts(0,99999);
\==================================================================================================================================================================
      -> POST or Create call 
      // This will get the mainService Model
        var oModel = this.getOwnerComponent().getModel(); 
        // Some times based on the more data , we need to pass the data in batch or group wise
        // onInit() , Intialize this.counter = 0;
        var GROUP = "GroupCreateName" + this.counter++;
        var oListBinding = oModel.bindList("/EntitySetName",undefined,undefined,undefined,{
          $$updateGroupId : GROUP
        });
        //  Add Create function
        oListBinding.create ( <payloadToPost> ,{

        bSkipRefresh : true 
        });

        // If any thing should be done post create we use  ".attachCreateCompleted()

        oListBinding.attachCreateCompleted((oEvent) => {
           // Add the required code here
        });
        =======================================================================================================================================================================      
       
   

