Introduction

 

In this article, we are going to discuss about Service Bus Queue Trigger
in Azure Functions. We are also going to create a simple Azure function
to send and read messages from Service bus queues. So we are going to
create a HTTP trigger function to send messages to the queue and a
Service bus queue trigger function to read messages from the queue.

What is Azure Service Bus?

 

Azure Service Bus is a message broker service that is hosted on the
Azure platform and it provides functionality to publish messages to
various applications and also decouple the applications. Azure service
bus has two different flavors; i.e. Queues and Topics. Azure Service Bus
Queues follows a First-In-First-Out (FIFO) pattern. Queues provide
one-way transport like the sender is going to send messages in the queue
and the receiver would collect messages from the queue. In queues, there
is a 1:1 relationship between the sender and receiver. Messages are
present in the queue until the receiver processes and complete the
messages.

 

Creating simple Azure Functions to send and read messages from the queue

Prerequisites 

-   [Azure ](https://portal.azure.com/)account(If you don\'t have an
    Azure subscription, [create a free trial
    account](https://azure.microsoft.com/free)).

-   Basic knowledge of Azure Functions

Overview of application

 

We are creating a simple Azure function application that consists of 3
parts,

1.  Create Azure Service Bus Queue using Azure Portal

2.  Create HTTP trigger Azure Function to send the message into Queue 

3.  Create a Service Bus Queue trigger Azure function to read a message
    from Queue

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image1.png){width="5.768055555555556in"
height="1.7458333333333333in"}

 

Create Azure Service Bus Queue using Azure Portal

 

Follow the below steps to creating a new Service Bus and Queue into
Azure.

-   Login to [Azure ](https://portal.azure.com/)and click on Create a
    resource button.

-   In the search box type service bus and select it. \
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image2.png){width="5.768055555555556in"
    height="3.2680555555555557in"}

-   Click on Create button. You will see the Create Namespace page.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image3.png){width="5.768055555555556in"
    height="4.300694444444445in"}\
    \
    Resource Group are nothing but a container to hold your resources in
    Azure. Service Bus is one of the resource so if you have already
    created Resource Group then select that or if haven\'t created it
    yet the click on Create button and give it a name. \
    \
    Namespace holds the multiple queues or topics resides under Service
    Bus. Specify a unique name for namespace.

-   Fill out all the required details and click on Review + Create
    button\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image4.png){width="5.768055555555556in"
    height="4.4430555555555555in"}

-   Review that everything is added properly and finally click on the
    Create button.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image5.png){width="5.768055555555556in"
    height="6.709027777777778in"}

-   Creating resources will take time so wait for some time to finish
    the deployment.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image6.png){width="5.768055555555556in"
    height="2.5340277777777778in"}

-   Once the deployment is completed you will see the Go to resource
    button.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image7.png){width="5.768055555555556in"
    height="2.2694444444444444in"}

-   Click on Go to resource button to see our Service Bus resource.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image8.png){width="5.768055555555556in"
    height="2.8333333333333335in"}

-   So we have successfully created a new Service Bus. Now next step is
    to create a Queue. Go to the Queues section in the left panel and
    click on Queue and give a unique name for queue and click on the
    Create button.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image9.png){width="5.768055555555556in"
    height="2.561111111111111in"}

-   That\'s it. We have created our first queue.\
    \
    ![How To Send And Read Messages From Azure Service Bus Queues Using
    Azure Functions](media/image10.png){width="5.768055555555556in"
    height="2.73125in"}

Create HTTP trigger Azure Function to send the message into Queue

 

**Prerequisites**

-   Visual Studio 19 with Azure Development workload installed 

So open Visual Studio and Go to File -\> New -\> Project. Search \"Azure
Functions\" in the search box and select the Azure function template and
click on Next.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image11.png){width="5.768055555555556in"
height="3.825in"}

 

Give a name to the function project and click on Create.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image12.png){width="5.768055555555556in"
height="3.8048611111111112in"}

 

Select the HTTP trigger template and set the Authorization level as
Anonymous and click on Create.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image13.png){width="5.768055555555556in"
height="3.872916666666667in"}

 

That\'s it. We have created our first Azure function. By default the
name of the function is Function1.cs so now change it to
\"SendMessage\".

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image14.png){width="5.768055555555556in"
height="2.8194444444444446in"}

 

Azure Functions has Triggers and Bindings. Triggers are the ones due to
which function code start executing forex. In the case of HTTP trigger
whenever you make HTTP request by hitting the function URL the specific
function will start its execution. The Azure function must have only one
trigger. Bindings are the direction of data coming in or going out from
the function. We have In, out, and both types of bindings.

 

So for our application, we are creating HTTP Trigger function which
takes data and sends it into the Queue. So to send data to the queue we
are using an Output binding. To connect with the queue we need a
connection string. So let\'s open the Service bus resource in portal -\>
Shared Access Policy -\> Copy the Primary Connection String under
RootManagedSharedAccessKey

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image15.png){width="5.768055555555556in"
height="2.609027777777778in"}

 

First, install the below NuGet package,

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image16.png){width="5.768055555555556in"
height="0.9125in"}

 

Open the local.settings.json file in our function app and add a key
called \"AzureWebJobsServiceBus\" and paste the connection string of our
Service bus resource.

1.  {  

2.      \"IsEncrypted\": **false**,  

3.    \"Values\": {  

4.      \"AzureWebJobsStorage\": \"UseDevelopmentStorage=true\",  

5.      \"FUNCTIONS_WORKER_RUNTIME\": \"dotnet\",  

6.      \"AzureWebJobsServiceBus\": \"\<replace your
    > RootManageSharedAccessKey here>\"

7.    }  

8.  }  

Now add the below code to send a message to the queue using output
bindings.

1.  **using** System.IO;  

2.  **using** System.Text;  

3.  **using** System.Threading.Tasks;  

4.  **using** Microsoft.AspNetCore.Http;  

5.  **using** Microsoft.Azure.WebJobs;  

6.  **using** Microsoft.Azure.WebJobs.Extensions.Http;  

7.  **using** Microsoft.Azure.WebJobs.ServiceBus;  

8.  **using** Microsoft.Extensions.Logging;  

9.    

10. **namespace** AzServiceBusDemo  

11. {  

12.     **public** **static** **class** SendMessage  

13.     {  

14.         \[FunctionName(\"SendMessage\")\]  

15.         \[**return**: ServiceBus(\"az-queue\", EntityType.Queue)\]  

16.         **public** **static** async Task\<**string**\> Run(  

17.             \[HttpTrigger(AuthorizationLevel.Anonymous, \"post\", Route = **null**)\] HttpRequest req,  

18.             ILogger log)  

19.         {  

20.             log.LogInformation(\"SendMessage function requested\");  

21.             **string** body = **string**.Empty;  

22.             **using** (var reader = **new** StreamReader(req.Body, Encoding.UTF8))  

23.             {  

24.                 body = await reader.ReadToEndAsync();  

25.                 log.LogInformation(\$\"Message body : {body}\");  

26.             }  

27.             log.LogInformation(\$\"SendMessage processed.\");  

28.             **return** body;  

29.         }  

30.     }  

31. }  

-   From lines 21-28, we are just getting data from the request body &
    assigned it to a local variable. After that, we are just returning
    it from function. 

-   In line 15, since we are using C# for creating function, we can use
    ServiceBusAttribute to specify the output bindings. For the
    attribute constructor i.e. ServiceBus() we just need to pass queue
    name and type of entity to bind. 

Now run the SendMessage function.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image17.png){width="5.768055555555556in"
height="1.6166666666666667in"}

 

For testing the function open postman and hit the about function URL. 

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image18.png){width="5.768055555555556in"
height="1.7458333333333333in"}

 

Since we logged our request body, we can see the content.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image19.png){width="5.768055555555556in"
height="2.329861111111111in"}

 

Open queue \"az-queue\" and we can see the Active message count is now
showing as 1. 

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image20.png){width="5.768055555555556in"
height="2.472916666666667in"}

 

To check the message content in the queue you can click on Service Bus
Explorer(preview) in the left sidebar and then click on Peek and finally
click on the message to see the content.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image21.png){width="5.768055555555556in"
height="2.092361111111111in"}

 

Create a Service Bus Queue trigger Azure function to read a message from
Queue

 

Now the final step is to read a message from the queue i.e.
\"az-queue\". Right-click on the project and click on project -\> Click
on Add -\> Select New Azure Function. Select Azure function and give it
a name and click on Add button.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image22.png){width="5.768055555555556in"
height="3.546527777777778in"}

 

Now select Service Bus Queue Trigger and specify queue name and click on
Add button.

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image23.png){width="5.768055555555556in"
height="3.8048611111111112in"}

 

That\'s it \-- our Service Bus trigger function is created.

1.  **using** Microsoft.Azure.WebJobs;  

2.  **using** Microsoft.Extensions.Logging;  

3.    

4.  **namespace** AzServiceBusDemo  

5.  {  

6.      **public** **static** **class** ReadMessageFromQueue  

7.      {  

8.          \[FunctionName(\"ReadMessageFromQueue\")\]  

9.          **public** **static** **void** Run(\[ServiceBusTrigger(\"az-queue\")\]**string** myQueueItem, ILogger log)  

10.         {  

11.             log.LogInformation(\$\"C# ServiceBus queue trigger function processed message: {myQueueItem}\");  

12.         }  

13.     }  

14. }  

Now run our function app. Since we already have one active message in
our queue, as soon as the function starts it will read a message from
the queue as shown below,

 

![How To Send And Read Messages From Azure Service Bus Queues Using
Azure Functions](media/image24.png){width="5.768055555555556in"
height="2.479861111111111in"}

 

So in this way, we can use Azure functions to send and read messages
from Azure Service Bus Queues.

 

Conclusion

 

In this article, we have created a new Azure Service Bus instance and
added a new queue from the portal. Also, we have created the HTTP
trigger Azure function to send messages into the Queue and Service Bus
Queue trigger function to read messages from a queue. 

 Happy Coding!! 
