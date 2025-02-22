# Intelligent Apps with Azure AI Services - L200/L300

Lab time: 10 minutes

## Contoso Traders

Contoso Traders are one of the leading E-Commerce platforms with a wide range of electronic products like Desktops and Laptops, Mobile Phones, Gaming console accessories, and Monitors. 
This includes a wide range of international brands like Microsoft Surface, XBOX, Samsung, ASUS, DELL, etc. Contoso Traders Organization is using Microsoft 365 for their collaboration works internally. 

Contoso Traders has different departments like Marketing, Sales, Accounts, HR, and IT. For internal communication, they are using Microsoft Teams and Outlook.
In Contoso Traders Organization, there are various functionalities with the Contoso Traders E-commerce platform like product approval, product price approval, Product price update approval, etc.

December 2022

## Abstract and learning objectives

In this lab, you will explore the Contoso traders application [https://contosotraders.com/](https://www.contosotraders.com/) and will go through the overview of an app with a focus on the need for AI/Visual Search, use the image search option in the application to find the device from the product catalog and finally you will learn on the **Azure AI service** used in the application and also the high-level idea of how the Cognitive services work.

For this, we use the service called **Computer Vision**, an Azure AI that analyzes content in images and video.

Azure's Computer Vision service gives you access to advanced algorithms that process images and return information based on the visual features you're interested in such as **Optical Character Recognition (OCR**), **Image Analysis**, **Face Service** and **Spatial Analysis**.

With the Analyze Image API, Computer Vision can analyze the content type of images, indicating whether an image is clip art or a line drawing.

## Requirements

- Microsoft Azure Subscription with required permissions. You can [create one for free](https://azure.microsoft.com/en-us/free/ai/)
- [A resource of Cognitive Services for Computer vision](https://portal.azure.com/#create/Microsoft.CognitiveServicesComputerVision)
- [Vision Studio website](https://portal.vision.cognitive.azure.com/)

## Solution Architecture

Contoso Traders is a 2-tier application and consists of the Client tier.

The presentation tier contains the React JS application that acts as a client, collects the information given by the user, and passes it to the Database tier. It consists of a collection of small, autonomous services. Each service is self-contained and should implement a single business capability within a bounded context. A bounded context is a natural division within a business and provides an explicit boundary within which a domain model exists.

The backend tier consists of 3 API components that are containerized.

1. Shopping Cart: An Azure containerized app 
2. Products &Inventory: Contains a Kubernetes cluster
3. Image Search: Containerized app service.

The workflow named Contoso-traders-infra-provisioning.yml will invoke the Bicep template that deploys the ACI app and AKS cluster.

### MICROSERVICES

Microservices are a popular architectural style for building applications that are resilient, highly scalable, independently deployable, and able to evolve quickly. 

![](https://raw.githubusercontent.com/microsoft/ContosoTraders/main/docs/architecture/contoso-traders-enhancements.drawio.png)


## Instructions

1. Open the browser, using a new tab navigate to `https://github.com/CloudLabs-AI/ContosoTraders` GitHub repository. This repository contains all the necessary files and documents which will guide you to host the Contoso traders application from the scratch.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct1.png)

1. Navigate to the **github/workflows** folder, which contains the workflow YAML files using which you can the deployment resources. Please see the individual workflows for more information.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct2.png)

1. **Contoso-traders-infra-deployment.yml** will deploy the infrastructure into Azure which includes resource groups, and resources, sets access policies to key vaults, and seeds the database from storage accounts into an Azure SQL database.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct3.png)

1. **contoso-traders-app-deployment.yml** deploys the application to the Azure cloud. The application is configured to use the pre-deployed resources.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct4.png)

1. **contoso-traders-load-testing.yml** configures the load testing for the application.
  
   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct5.png)

1. The **docs** folder contains the deployment instruction files, which guide you to deploy the infrastructure and application.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct6.png)

1. The **iac** folders contain the BICEP templates, which deploy the infrastructure needed for the application.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct7.png)

1. The **src** folder contains all the source code files related to backend APIs, UI, and other parts of the application.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct8.png)  

1. The **tests** folder contains the files related to load testing.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct9.png)  

1. From the **code** tab, scroll down a little and you’ll find the **links (1)** to access the application. There are different links for the test, and production UI. You can also access the **deployment instructions (2)** files using the links provided in the documentation paragraph.

   ![](https://github.com/shivashant25/Demo-Docs/raw/main/media/ct10.png)  
   
1. Now open the browser and navigate to [https://contosotraders.com/](https://www.contosotraders.com/)

   ![image](https://user-images.githubusercontent.com/48020356/204910981-44806350-9b7d-4b88-95f4-0c3c08196430.png)

   On the webpage, you will be able to see the e-commerce store with a cluster of electronic products such as Laptops, Xbox controllers, Desktops, mobile phones, and monitors of different brands. 

1. Select the **Laptops** option from the list of Categories and observe the available laptops that can be purchased from the website on the product collection page and click on any product.

1. Then you be redirected to the specific product details page and here you can type the delivery Pincode for checking the delivery availability, then you can add the quantity, and also either you can add the product to the bag for checkout or the selected product can be pushed to wishlist.

1. Visit back to the **Homepage** for the special offers and recently added products, and also browse through the other product category for the newly launched and available products.

1.  In the search bar of the application type **Laptop** and this will return the list of Laptops available from the list of products available for purchase.

1. Select the **SerachImage (1)** icon in the right of the search bar and click on **Drag an image or upload a file (2)**.

   ![image](https://user-images.githubusercontent.com/48020356/204916409-3c559023-64e1-4c7a-95d5-558a5743dbde.png)
   
1. Either download an image from a browser and save it or select a locally existing image and click **Open**.
This will take you to the **Suggested Product list** page as per the image provided to search and you can select the product you wish to buy from the application from here.

   ![image](https://user-images.githubusercontent.com/48020356/204917533-db8beed3-29f5-4c34-9c4f-d35ffe8b906e.png)

   The **cloud-based Computer Vision API** provides developers with access to advanced algorithms for processing images and returning information. By uploading an image or specifying an image URL, Microsoft Computer Vision algorithms can analyze visual content in different ways based on inputs and user choices.

   The **Image Analysis service** extracts many visual features from images, such as objects, faces, adult content, and auto-generated text descriptions, it provides you with AI algorithms for processing images and returning information on their visual features. 

   We can use **Vision Studio** to understand the process of Image Analysis in cognitive service using Computer Vsion features
**Vision Studio** is a set of UI-based tools that lets you explore, build, and integrate features from Azure Computer Vision.
Vision Studio provides you with a platform to try several service features and sample their returned data in a quick, straightforward manner. Using Studio, you can start experimenting with the services and learning what they offer without needing to write any code. Then, use the available client libraries and REST APIs to get started embedding these services into your applications.

1. Sign in to Vision Studio from https://portal.vision.cognitive.azure.com/ with your Azure subscription and if it's your first time logging in, you'll see a popup window appear that prompts you to **Sign in to Azure** and then choose or create a Vision resource. You have the option to skip this step and do it later also.
   
   ![image](https://user-images.githubusercontent.com/48020356/204954594-90143c0a-65c1-4155-9136-bb93ee57985a.png)
  
1. Select the **Subscription** dropdown, and then select the available subscription and select an existing resource within your subscription under the **Azure Resources** option. If you'd like to create a new one, select Create a new resource. 
 
   ![image](https://user-images.githubusercontent.com/48020356/205177896-bcad5c19-ef01-47e5-96ed-099bf95e3f58.png)
   
1. If selected *Create a new resource* then enter information for your new resources, such as a name, subscription, resource group, Cognitive service resource type, location, and the pricing tier as below, and click **Create resource**.

   ![image](https://user-images.githubusercontent.com/83349577/205639512-bdbc8303-66fa-4341-96a2-d4e2ac920a84.png)

1. Once the resource is created, you'll be able to try Image Analysis offered by Vision Studio.

    ![image](https://user-images.githubusercontent.com/48020356/205178332-d2cab5a3-e553-4910-91fe-5058bceae12c.png)

1. Select the Analyze images tab, and select the panel titled** Extract common tags** from images.

    ![image](https://user-images.githubusercontent.com/48020356/205179384-90e35cd6-f5bd-4c71-9c08-d54e0a2055f3.png)    

1. Select an image from the available set, or upload your own.

1. After you select your image, you'll see the detected tags appear in the output window along with their confidence scores.

  ![image](https://user-images.githubusercontent.com/83349577/205631741-b8c58060-4ac2-4c1e-9354-5f0d15a6d27a.png)


1. You can also select the JSON tab to see the JSON output that the API call returns.

   ![image](https://user-images.githubusercontent.com/83349577/205631814-271fd174-d478-4bd6-9bd6-f0e5400f0d66.png)

   You can analyze images to provide insights into their visual features and characteristics.
   
   Image Analysis offers the ability to extract text from images. **OCR** traditionally started as a machine-learning-based technique for extracting text from in-the-wild and non-document images like product labels, user-generated images, screenshots, street signs, and posters. For several scenarios that include running OCR on single images that are not text-heavy, you need a fast, synchronous API or service. This allows OCR to be embedded in near real-time user experiences to enrich content understanding and follow-up user actions with fast turn-around times.
   
1. On **Vision Studio** page, navigate back to **Featured** tab and select **Extract Text from Image**.

    ![image](https://user-images.githubusercontent.com/83349577/205654069-13495462-c665-41cd-98e8-911842b4aa9a.png)

1. Drag and drop any image which contains text, and you'll see the detected text appear in the output window.

    ![image](https://user-images.githubusercontent.com/83349577/205656306-56226ce6-4ab1-453c-9655-4f44b6998612.png)

1. You can also select the JSON tab to see the JSON output that the API call returns.

    ![image](https://user-images.githubusercontent.com/83349577/205656524-8c1b8f43-4854-4692-b81e-cd66f9e8087c.png)

    There are a few key concepts to understand how Image Analysis works on Azure, for example, Image Analysis can return content tags for thousands of recognizable objects, living beings, scenery, and actions that appear in images. Tags are not organized as a taxonomy and do not have inheritance hierarchies. A collection of content tags forms the foundation for an image description displayed as human-readable language formatted in complete sentences. When tags are ambiguous or not common knowledge, the API response provides hints to clarify the meaning of the tag in the context of a known setting.

    After you upload an image or specify an image URL, the Analyze API can output tags based on the objects, living beings, and actions identified in the image. Tagging is not limited to the main subject, such as a person in the foreground, but also includes the setting (indoor or outdoor), furniture, tools, plants, animals, accessories, gadgets, and so on.

    The next one is that Computer Vision can analyze an image and generate a human-readable phrase that describes its contents. The algorithm returns several descriptions based on different visual features, and each description is given a confidence score. The final output is a list of descriptions ordered from highest to lowest confidence and this is called **Image description generation**.

    **Object detection** is similar to tagging, but the API returns the bounding box coordinates (in pixels) for each object found in the image. For example, if an image contains a dog, cat, and person, the Detect operation will list those objects with their coordinates in the image. You can use this functionality to process the relationships between the objects in an image. It also lets you determine whether there are multiple instances of the same object in an image.

    The object detection function applies tags based on the objects or living things identified in the image. There is currently no formal relationship between the tagging taxonomy and the object detection taxonomy. At a conceptual level, the object detection function only finds objects and living things, while the tag function can also include contextual terms like "indoor", which can't be localized with bounding boxes.

For more reference this link: ```https://learn.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-categorizing-images```   

## Summary

You have got an overview of the Contoso traders GitHub repository, Contoso traders web app usage, and Computer Vision services.

## Delete the resources
1. Within the Azure portal, select Resource Groups on the left navigation.

2. Delete the resource groups created by selecting them, followed by the Delete resource group button. You will need to confirm the name of the resource group to delete.
