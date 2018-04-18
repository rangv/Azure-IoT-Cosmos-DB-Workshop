## Azure IoT & Cosmos DB workshop 
Objective: Implement and end to end solution with real device connecting to Azure, sending, storing, analyzing and visualizing data in Azure. Stream data to time series insights Stream data to cosmos db using azure stream analytics Code for cosmos db change feeds and invoke azure functions
 
### Goals
 
- Stream data to time series insights
- Stream data to cosmos db using azure stream analytics
- Code for cosmos db change feeds and invoke azure functions

![alt text](https://wikiazure.com/wp-content/uploads/2018/04/06-Azure-IoT-Cosmos-DB-workshop.png)



# Agenda
 
Workshop overview
- Setup MXCHIMP
- Connect mxchip to iothub 
- Simulator: https://azure-samples.github.io/iot-devkit-web-simulator/

![alt text](https://wikiazure.com/wp-content/uploads/2018/04/01-Azure-IoT-Cosmos-DB-workshop.png)
 
1.	Connect to wifi: 
- Put the device into AP mode by doing the following:
- Press and hold the B button
- With the B button held down, press and release the Reset button
- Release the B button
- Verify that an SSID and an IP address appear on the device screen. The IP address is the one that you will use to connect to the device from your laptop.
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/02-Azure-IoT-Cosmos-DB-workshop.png)
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/03-Azure-IoT-Cosmos-DB-workshop.png)
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/04-Azure-IoT-Cosmos-DB-workshop.png)
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/05-Azure-IoT-Cosmos-DB-workshop.png)
  
 
 
### Create IoT Hub: 
 
1. Go to the Azure Portal, click Create New Resource and type Iot Hub, 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/07-Azure-IoT-Cosmos-DB-workshop-2.png)
 
 
 
2. Select IoT Hub and click create
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/08-Azure-IoT-Cosmos-DB-workshop-2.png)
 
 
3. Select Create IoT hub
 
![alt text](https://wikiazure.com/wp-content/uploads/2018/04/09-Azure-IoT-Cosmos-DB-workshop-2.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/010-Azure-IoT-Cosmos-DB-workshop-2.png)
 
 
### Set up Time Series Insight

 Now we will create a Time Series Insight service. 
  
1. Go to the Azure Portal, click on Create New Resource and type Time Series Insights as shown below:
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/011-Azure-IoT-Cosmos-DB-workshop.png)
 
2. Then select Time Series Insights: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/012-Azure-IoT-Cosmos-DB-workshop.png)
 
 
3. Click create: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/013-Azure-IoT-Cosmos-DB-workshop.png)
 
4.Now we will provide the environment parameters as follows: 
 
- Environment name: gab2018-cdmx
- Subscription - your Azure Pass / Subscription
- Resource group: gab2018-cdmx
- Location: west europe
- SKU: S1


 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/014-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
**Note: In case you are using an Azure Pass, please review the cost $150 per month!
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/015-Azure-IoT-Cosmos-DB-workshop.png)
 
 
Then Check the pin to dashboard and click create. 


 
6. It is important to have a consumer group for TSI (Time Series Insights), go to the IoT Hub, click Endpoints, select Events
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/016-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
7. Now create a New Consumer Group and then click save: 

![alt text](https://wikiazure.com/wp-content/uploads/2018/04/017-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
8. Now go back to Time Series Insights, click on Event Sources and Click on Add: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/018-Azure-IoT-Cosmos-DB-workshop.png)
 
 
9. Provide the following parameters to create the Event Source: 
- Event source name: gab2018cdmx
- source: IoT Hub
- Import Option: user IoT Hub from available subscription
- Subscription ID. VS Enterprise / Azure Pass
- Iot Hub name: gab2018-cdmx
- Iot Hub poicy name: iothubowner
- IoT consumer group: gabevents
- Serialization format: json
 
Click create


![alt text](https://wikiazure.com/wp-content/uploads/2018/04/019-Azure-IoT-Cosmos-DB-workshop.png)
![alt text](https://wikiazure.com/wp-content/uploads/2018/04/020-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
 
 
10. Now go to overview and click go to environment: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/021-Azure-IoT-Cosmos-DB-workshop.png)
 
**Note: We will add data access policies later. You will not be able to access the data in the environment with no data access policies defined.
 
You will see a screen like below: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/022-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
### Create a Stream analytics Job
1. Now go back to the Azure Portal,  we will create a Stream analytics Job. Go to Create New Resource, type Stream analytics: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/024-Azure-IoT-Cosmos-DB-workshop.png)
 
 
2. Select stream analytics job: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/025-Azure-IoT-Cosmos-DB-workshop.png)
 
 
3. Provide the following parameters: 
- Job Name: gab2018-cdmx
- Subscription: VS enterprise / Azure Pass
- Resource Group: gab2018-cdmx
-	Location: west Europe
-	Hosting environment: cloud
 
Note: if you already connected your device to Wifi you could try Cloud, otherwise try using Edge and connect your device to Wifi later on
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/026-Azure-IoT-Cosmos-DB-workshop.png)
 
 
### Create a cosmos db account. 
Now we will create a cosmos db account. 
 
1. Select create new resource, type cosmos db, select Azure Cosmos DB:
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/027-Azure-IoT-Cosmos-DB-workshop.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/028-Azure-IoT-Cosmos-DB-workshop.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/029-Azure-IoT-Cosmos-DB-workshop.png)
 
2. Click create: 
 
Provide the following parameters:
•	ID: gab2018cdmx
•	API: SQL
•	Subscription: VS Enterprise / Azure Pass
•	Resource group: gab2018cdmx
•	Location: West Europe
 
Click Create
 
* It is important to highlight that you should try to deploy all the resources in same location to avoid future issues within the service availability
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/030-Azure-IoT-Cosmos-DB-workshop.png)
 
 
### Create a Logic App. 
Now we will create a Logic App. 
 
1. Go to Create new Resource, type logic app
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/031-Azure-IoT-Cosmos-DB-workshop.png)
 
 
2. Select Logic App: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/032-Azure-IoT-Cosmos-DB-workshop.png)
 
 
3. Click on Logic App, Create: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/033-Azure-IoT-Cosmos-DB-workshop.png)
 
4. Now provide the following parameters: 
- Name. gab2018cdmx
- Subscription: VS Enterprise
- Resource Group. Gab2018 cdmx
- Location: West Europe
- Log Analytics: Off (for this case we are going to enable them later on)
 
Click Create
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/034-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
5. Now go back to the azure stream analytics job, from the blade select Input: 
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/035-Azure-IoT-Cosmos-DB-workshop.png)
 
 
6. The input for this will be the IoTHub you created in the resource group 
 
Select Add stream input, then select IoT Hub:
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/036-Azure-IoT-Cosmos-DB-workshop.png)

 
7. Provide the following parameters: 
- Input alias
- Select IoT Hub from your subscription
- Subscription
- IoT Hub (Azure will automatically provide you the available IoT Hub)
- Endpoint
- Shared access policy name
- Shared access policy key
- Consumer Group
- Event serialization format (you could select None, CSV, Json, etc.)
 Then click save
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/037-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
8. Now we will generate the Output.
 
This output will be the Cosmos DB you create in the resource group
 
8.1 Go to the Stream Job blade and select Output: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/038-Azure-IoT-Cosmos-DB-workshop.png)
 
8.2 Now click Add and select Cosmos DB. 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/039-Azure-IoT-Cosmos-DB-workshop.png)
 
Provide the following parameters:
- Output alias
- Select the Option: "Select Cosmos DB from your subscription"
- Select your subscription
- Account ID
- Account key
- Database
- Collection name pattern
- Document ID
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/040-Azure-IoT-Cosmos-DB-workshop.png)
 
Please Note: 
 
If the chosen resource and the stream analytics job are located in different regions, you will be billed to move data between regions.
 
 
 
8.3 Now we will define a Stream Job Function. 
 
Go to the stream job blade and click on Overview, then click on Edit query:
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/041-Azure-IoT-Cosmos-DB-workshop.png)
 
 
8.4 Copy and paste the following query:
 
SELECT [deviceId] AS [deviceId], avg(temperature) AS avgtemp INTO CosmosDB FROM mvp-iothub GROUP BY deviceId, TumblingWindow(second, 15); 
 
8.5 Now click save: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/042-Azure-IoT-Cosmos-DB-workshop.png)
 
 
### Create an Event Hub which will receive data from Azure Function. 
 
Now we will Create an Event Hub which will receive data from Azure Function. 
 
TIP: Take a note of keys and name.
 
1. Go to create Resources and type Event hub: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/043-Azure-IoT-Cosmos-DB-workshop.png)
 
2. Now select the event hubs and click create: 

![alt text](https://wikiazure.com/wp-content/uploads/2018/04/045-Azure-IoT-Cosmos-DB-workshop.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/046-Azure-IoT-Cosmos-DB-workshop.png)
 
3. Provide the following parameters and click create: 
- Name
- Pricing tier
- Subscription
- Resource Group
- Location
- Throughput units
- Enable auto-inflate
- Specify upper limit to 20
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/047-Azure-IoT-Cosmos-DB-workshop.png)
 

 
 
4. Once provisioned we will create a new event hub: 
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/048-Azure-IoT-Cosmos-DB-workshop.png)
 
 
5. Also, create a SAS policy for this event hub: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/049-Azure-IoT-Cosmos-DB-workshop.png)
 
### Create an Azure Function.
 
Now Create an Azure Function. 
 
1. Go to create New Resource, type functions: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/050-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
2. Select Functions App: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/051-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
3. Click create: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/052-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
4. Now Provide the following parameters: 
  - App name
  - Subscription
  - Resource Group
  - OS: windows
  - Hosting Plan: Consumption Plan
  - Location: west US
  - Storage: Create New
  - Application Insights: ON
  
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/053-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
### Use Azure Functions on the Azure Portal. 
 
1. GO to the azure portal, select your function and click on Add then select Azure Cosmos DB Trigger: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/054-Azure-IoT-Cosmos-DB-workshop.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/055-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
 
 
2. Now click on New and confirm this new account connection is related to your previously created Cosmos DB
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/056-Azure-IoT-Cosmos-DB-workshop.png)
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/057-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
3. Replace with the following code: 
```
#r "D:\home\site\wwwroot\CosmosTriggerCSharp1\bin\Microsoft.Azure.Documents.Client.dll"
#r "D:\home\site\wwwroot\CosmosTriggerCSharp1\bin\Microsoft.Azure.EventHubs.dll"
using System.Collections.Generic;
using System.Configuration;
using System.Text;
using Microsoft.Azure.Documents;
using Microsoft.Azure.EventHubs;
public static void Run(IReadOnlyList<Document> documents, TraceWriter log){
if (documents != null && documents.Count > 0) {
string connectionString = ConfigurationManager.ConnectionStrings["EventHubConnection"].ConnectionString;
log.Verbose(connectionString);
var connectionStringBuilder = new EventHubsConnectionStringBuilder(connectionString) {
EntityPath = "eventhub"
};
var client = Microsoft.Azure.EventHubs.EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
foreach (var doc in documents) {
string json = string.Format("{{\"iotid\":\"{0}\",\"temp\":{1}}}", doc.GetPropertyValue<string>("iotid"),
doc.GetPropertyValue<string>("temp"));
EventData data = new Microsoft.Azure.EventHubs.EventData(Encoding.UTF8.GetBytes(json));
client.SendAsync(data);
}
}
}
```
 
 
4. Now click on your function, then select platform features, then click on Kudu Console: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/058-Azure-IoT-Cosmos-DB-workshop.png)
 
 
5. You will be redirected to another tab in your browser to manage your Azure Function: 
 
https://gab2018-cdmx.scm.azurewebsites.net/


 
6. Click on debug console, cmd: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/059-Azure-IoT-Cosmos-DB-workshop.png)
 
7. Navigate to function directory by double clicking on wwwroot and then create a bin directory using the “+” sign.
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/060-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/061-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
 
 
 
 
 
8. Go to Bin directory by double clicking on it and then add the following DLL. Get these DLL from nuget

![alt text](https://wikiazure.com/wp-content/uploads/2018/04/063-Azure-IoT-Cosmos-DB-workshop.png)

 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/062-Azure-IoT-Cosmos-DB-workshop.png)
 
Repeat this for each of the following:
 
Microsoft.Azure.DocumentDB Version="1.21.0" https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/
Microsoft.Azure.EventHubs Version="1.1.0" https://www.nuget.org/packages/Microsoft.Azure.EventHubs/
https://www.nuget.org/packages/Microsoft.Azure.Amqp/
 
https://www.nuget.org/packages/Newtonsoft.Json
 
 
*Note: You can user 7zip and extract the nupkg to quickly get the DLLs. 
 
9. Once you downloaded this packages go back to AppSettings Click on AppSettings
 
 
10. On another tab open the Event Hub and get the Connection String: 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/064-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
11. Copy the connection-primary-key: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/065-Azure-IoT-Cosmos-DB-workshop.png)
 
 
12. Now go back to your Azure Function, select Application Settings and click on add connection string: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/066-Azure-IoT-Cosmos-DB-workshop.png)
 
 
13. Then provide a Connection Name, then paste the connection string and select Connection Type as Custom 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/067-Azure-IoT-Cosmos-DB-workshop.png)
 
14. Now go up and click Save: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/068-Azure-IoT-Cosmos-DB-workshop.png)
 
 
 
15. Now go back to your Logic App. Select "When events are available in EventHub"
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/069-Azure-IoT-Cosmos-DB-workshop.png)
 
 
16. Then provide a name and select the Event Hub. 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/070-Azure-IoT-Cosmos-DB-workshop.png)
 
 
17. Now click Create. 
![alt text](https://wikiazure.com/wp-content/uploads/2018/04/070-Azure-IoT-Cosmos-DB-workshop.png)
 
18. Now provide the interval and frequency to check for events coming in: 
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/071-Azure-IoT-Cosmos-DB-workshop.png)
 
 
19. Now Click new step then click add action
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/072-Azure-IoT-Cosmos-DB-workshop.png)
 
 
20. Look for "Send an email"
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/073-Azure-IoT-Cosmos-DB-workshop.png)
 
21. You will need to authorize your account,then setup the details for the email:
 
 ![alt text](https://wikiazure.com/wp-content/uploads/2018/04/074-Azure-IoT-Cosmos-DB-workshop.png)
 

