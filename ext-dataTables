$(document).ready(function() {

  // Hook up an event handler for the load button click.
  // Wait to initialize until the button is clicked.
  $("#runParser").click(function() {

    // Disable the button after it's been clicked
    $("#runParser").prop('disabled', true);

    tableau.extensions.initializeAsync().then(function() {
      // Initialization succeeded! Get the dashboard
      var dashboard = tableau.extensions.dashboardContent.dashboard;
      //Get all worksheets
      const worksheets = tableau.extensions.dashboardContent.dashboard.worksheets;

      //if (window.console) console.log('Worksheets is of type ' + jQuery.type(worksheets));
      //console.dir(worksheets);
      //console.log(worksheets[0]['name']);
      worksheets.forEach(function (worksheet) {
        var data = worksheet.getSummaryDataAsync().then(function (sumdata){
          // console.log(worksheet);
          console.log('*** Beginning parsing of worksheet ***' + worksheet['name']);
          const worksheetData = sumdata;
          // console.log('Worksheet data is of type ' + jQuery.type(worksheetData))
          // console.log('Worksheet data has ' + Object.keys(worksheetData).length + ' items');
          // console.log(worksheetData);
          //get Total number of rows
          var rowCount = worksheetData['totalRowCount']
          var columns = worksheetData['columns']
          // console.log('Columns is of type ' + jQuery.type(columns));
          // console.log(worksheetData['columns']);
          var data = worksheetData['data']
          // console.log('Data is of type ' + jQuery.type(data));
          // console.log(data);
          // console.log(data[0]);
          
          //get Data
          var dataset = [];
          data.forEach(function (arrayOfData){
              var arrayDataValue = [];
            arrayOfData.forEach(function (dataValueArray){
              // console.log(dataValueArray);
              arrayDataValue.push(dataValueArray['formattedValue'])
          });
            // console.log(arrayDataValue);
            dataset.push(arrayDataValue);
        });
        console.log(dataset);
  
          //get column names
          var cmn = [];
          columns.forEach(function (clm){
            cmn.push({title:clm['fieldName']});
          })
          // console.log(cmn);
          $("#tableauTable").DataTable({
            dom: 'Bfrtip',
            buttons:[
              { 
                // action,
                extend: 'excelHtml5',
                text: 'Export to Excel',
                className: 'exportExcel',
                filename: 'excelEY'
               ,
              exportOptions:{
               modifier: {
                page: 'all'
              }}}
            ],
              columns: cmn,
              data: dataset


          });
          console.log('*** Finished Parsing ***' + worksheet['name']);
        })


      })
      //window.alert(11)
      // Display the name of dashboard in the UI
      // $("#enterDashName").html("I'm running in a dashboard named <strong>" + dashboard.name + "</strong>");
    }, function(err) {

      // something went wrong in initialization
  //    $("#resultBox").html("Error while Initializing: " + err.toString());
    });
  });
});
