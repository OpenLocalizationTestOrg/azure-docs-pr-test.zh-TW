---
title: "在 Azure App Service 中建置和部署 Java API 應用程式"
description: "了解如何建立 Java 應用程式套件並將其部署至 Azure App Service。"
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="42753-103">在 Azure App Service 中建置和部署 Java API 應用程式</span><span class="sxs-lookup"><span data-stu-id="42753-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="42753-104">本教學課程說明如何建立 Java 應用程式，並使用 [Git]將其部署至 Azure App Service API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42753-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="42753-105">本教學課程中的指示可運用在任何足以執行 Java 應用程式的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="42753-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="42753-106">本教學課程中的程式碼，是使用 [Maven]建置的。</span><span class="sxs-lookup"><span data-stu-id="42753-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="42753-107">我們使用[Jax RS] 來建立 RESTful 服務，而這些 Jax RS 是根據 [Swagger] 中繼資料規格使用 [Swagger 編輯器]所產生的。</span><span class="sxs-lookup"><span data-stu-id="42753-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42753-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="42753-108">Prerequisites</span></span>
1. <span data-ttu-id="42753-109">[Java Developer Kit 8] \(或更新版本)</span><span class="sxs-lookup"><span data-stu-id="42753-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="42753-110">安裝在您開發電腦上的 [Maven]</span><span class="sxs-lookup"><span data-stu-id="42753-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="42753-111">安裝在您開發電腦上的 [Git]</span><span class="sxs-lookup"><span data-stu-id="42753-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="42753-112">付費或[免費試用]的 [Microsoft Azure] 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42753-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="42753-113">HTTP 測試應用程式，例如 [Postman]</span><span class="sxs-lookup"><span data-stu-id="42753-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="42753-114">使用 Swagger.IO 來建立 API 結構。</span><span class="sxs-lookup"><span data-stu-id="42753-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="42753-115">您可以使用 swagger.io 線上編輯器，來輸入代表您 API 結構的 Swagger JSON 或 YAML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="42753-116">當您完成設計 API 介面區時，就可以針對各種不同平台和架構來匯出程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="42753-117">在下一節中，我們將修改已建立結構的程式碼來包含模擬的功能。</span><span class="sxs-lookup"><span data-stu-id="42753-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="42753-118">這個示範將從會貼到 swagger.io 編輯器的 Swagger JSON 主體開始，然後我們要用該編輯器來產生會利用 JAX RS 來存取 REST API 端點的程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="42753-119">然後，您將編輯已建立結構的程式碼來傳回模擬資料，依照資料永續性機制來模擬 REST API 組建。</span><span class="sxs-lookup"><span data-stu-id="42753-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="42753-120">將下列 Swagger JSON 程式碼複製到剪貼簿中：</span><span class="sxs-lookup"><span data-stu-id="42753-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="42753-121">瀏覽至 [線上 Swagger 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="42753-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="42753-122">抵達之後，依序按一下 [檔案] -> [貼上 JSON] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="42753-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![貼上 JSON 功能表項目][paste-json]
3. <span data-ttu-id="42753-124">貼上您之前複製的連絡人清單 API Swagger JSON 程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![將 JSON 程式碼貼到 Swagger][pasted-swagger]
4. <span data-ttu-id="42753-126">檢視編輯器顯示的文件頁面和 API 摘要。</span><span class="sxs-lookup"><span data-stu-id="42753-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![檢視 Swagger 產生的文件][view-swagger-generated-docs]
5. <span data-ttu-id="42753-128">依序選取 [產生伺服器] -> **JAX RS** 功能表選項，來建立伺服器端的程式碼結構，讓您稍後能拿來新增模擬實作。</span><span class="sxs-lookup"><span data-stu-id="42753-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![產生程式碼功能表項目][generate-code-menu-item]
   
    <span data-ttu-id="42753-130">程式碼產生之後，編輯器會提供 ZIP 檔案來讓您下載。</span><span class="sxs-lookup"><span data-stu-id="42753-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="42753-131">這個檔案包含 Swagger 程式碼產生器所建構的程式碼，以及所有相關連的組建指令碼。</span><span class="sxs-lookup"><span data-stu-id="42753-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="42753-132">將整個程式庫解壓縮到您的開發工作站上的某個目錄。</span><span class="sxs-lookup"><span data-stu-id="42753-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="42753-133">編輯程式碼來新增 API 實作</span><span class="sxs-lookup"><span data-stu-id="42753-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="42753-134">在本節中，您將使用您自訂的程式碼，來取代 Swagger 所產生程式碼的伺服器端實作。</span><span class="sxs-lookup"><span data-stu-id="42753-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="42753-135">新的程式碼會把連絡人實體的 ArrayList 傳回給呼叫中的用戶端。</span><span class="sxs-lookup"><span data-stu-id="42753-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="42753-136">使用 [Visual Studio Code] 或您偏好的文字編輯器，來開啟 Contact.java 模型檔案 (位於 *src/gen/java/io/swagger/model* 資料夾)。</span><span class="sxs-lookup"><span data-stu-id="42753-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![開啟連絡人模型檔案][open-contact-model-file]
2. <span data-ttu-id="42753-138">將下列建構函式新增到 **Contact** 類別中。</span><span class="sxs-lookup"><span data-stu-id="42753-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="42753-139">使用 [Visual Studio Code] 或您偏好的文字編輯器來開啟 ContactsApiServiceImpl.java 服務實作檔案 (位於 src/main/java/io/swagger/api/impl 資料夾)。</span><span class="sxs-lookup"><span data-stu-id="42753-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![開啟連絡人服務程式碼][open-contact-service-code-file]
4. <span data-ttu-id="42753-141">用新的程式碼覆寫檔案中的程式碼，來將模擬實作新增至服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="42753-142">開啟命令提示字元，並將目錄變更至應用程式的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="42753-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="42753-143">執行下列 Maven 指令來建置程式碼，並在本機使用 Jetty 應用程式伺服器來執行。</span><span class="sxs-lookup"><span data-stu-id="42753-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="42753-144">您應該會在命令視窗看到 Jetty 已經在連接埠 8080 啟動您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="42753-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![開啟連絡人服務程式碼][run-jetty-war]
8. <span data-ttu-id="42753-146">使用 [Postman] 來對「取得所有連絡人」API 方法 (位於 http://localhost:8080/api/contacts) 提出要求。</span><span class="sxs-lookup"><span data-stu-id="42753-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![呼叫連絡人 API][calling-contacts-api]
9. <span data-ttu-id="42753-148">使用 [Postman] 來對「取得特定連絡人」API 方法 (位於 http://localhost:8080/api/contacts/2) 提出要求。</span><span class="sxs-lookup"><span data-stu-id="42753-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![呼叫連絡人 API][calling-specific-contact-api]
10. <span data-ttu-id="42753-150">最後，在您的主控台執行下列 Maven 命令來建立 Java WAR (網頁封存) 檔案。</span><span class="sxs-lookup"><span data-stu-id="42753-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="42753-151">當 WAR 檔案建立之後，將會放入 **target** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="42753-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="42753-152">瀏覽至 **target** 資料夾，然後將 WAR 檔案重新命名為 **ROOT.war**。</span><span class="sxs-lookup"><span data-stu-id="42753-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="42753-153">(請確定字母的大小寫符合這個格式)。</span><span class="sxs-lookup"><span data-stu-id="42753-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="42753-154">最後，從應用程式的根資料夾執行下列命令來建立 [deploy]  資料夾，以便用來將 WAR 檔案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="42753-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="42753-155">將輸出資料發佈至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="42753-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="42753-156">在本節中，您將了解如何使用 Azure 入口網站來建立新的 API 應用程式、準備該 API 應用程式來託管 Java 應用程式，以及將新建立的 WAR 檔案部署至 Azure App Service 來執行您的新 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42753-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="42753-157">在 [Azure 入口網站]中建立新的 API 應用程式，方法是依序按一下 [新增] -> [Web + 行動] -> [API 應用程式] 功能表項目、輸入應用程式詳細資料，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="42753-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![建立新的 API 應用程式][create-api-app]
2. <span data-ttu-id="42753-159">在建立了 API 應用程式之後，開啟應用程式的 [設定] 刀鋒視窗，然後按一下 [應用程式設定] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="42753-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="42753-160">在可用的選項中選取最新的 Java 版本，並在 [Web 容器] 功能表中選取最新的 Tomcat，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="42753-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![在 API 應用程式刀鋒視窗中設定 Java ][set-up-java]
3. <span data-ttu-id="42753-162">按一下 [部署認證]  設定功能表項目，並提供您要用來將檔案發佈至 API 應用程式的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="42753-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![設定部署認證][deployment-credentials]
4. <span data-ttu-id="42753-164">按一下 [部署來源]  設定功能表項目。</span><span class="sxs-lookup"><span data-stu-id="42753-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="42753-165">抵達之後，按一下 [選擇來源] 按鈕，選取 [本機 Git 存放庫] 選項，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="42753-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="42753-166">這會建立在 Azure 中執行的 Git 存放庫，而它與您的 API 應用程式有關聯。</span><span class="sxs-lookup"><span data-stu-id="42753-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="42753-167">每次您將程式碼交附給 Git 存放庫的「主要」  分支時，您的程式碼就會發佈到您執行中的 API 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="42753-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![設定新的本機 Git 存放庫][select-git-repo]
5. <span data-ttu-id="42753-169">將新的 Git 存放庫 URL 複製到剪貼簿中。</span><span class="sxs-lookup"><span data-stu-id="42753-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="42753-170">請務必保存這個網址，因為它在稍後會很重要。</span><span class="sxs-lookup"><span data-stu-id="42753-170">Save this as it will be important in a moment.</span></span> 
   
    ![為您的應用程式設定新的 Git 存放庫][copy-git-repo-url]
6. <span data-ttu-id="42753-172">Git 會把 WAR 檔案推送至線上存放庫。</span><span class="sxs-lookup"><span data-stu-id="42753-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="42753-173">方法是瀏覽至您先前建立的 [deploy]  資料，讓您能輕鬆地把程式碼交付給在您 App Service 中執行的存放庫。</span><span class="sxs-lookup"><span data-stu-id="42753-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="42753-174">當您抵達主控台視窗，並瀏覽至 [webapps] 資料夾所在的資料夾之後，請發出下列的 Git 命令來啟動處理程序並開始部署。</span><span class="sxs-lookup"><span data-stu-id="42753-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="42753-175">當您發出「推送」  要求之後，系統會詢問您之前為部署認證所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="42753-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="42753-176">在輸入認證之後，您應該就會看到入口網站顯示已部署更新。</span><span class="sxs-lookup"><span data-stu-id="42753-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="42753-177">如果您再次使用 Postman 來叫用您剛部署，且在 Azure App Service 中執行的新 API 應用程式，就會看到行為是一致的，且現在它會如預期般傳回連絡人資料，還會對以 Swagger.io 建構的 Java 程式碼進行簡單的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="42753-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![在 Azure 中即時使用您的 Java 連絡人 REST API][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="42753-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42753-179">Next steps</span></span>
<span data-ttu-id="42753-180">在這篇文章中，您從 Swagger JSON 檔案和一些利用 Swagger.io 編輯器建構的 Java 程式碼開始，</span><span class="sxs-lookup"><span data-stu-id="42753-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="42753-181">然後您做的簡單變更和 Git 部署程序，讓您得到以 Java 撰寫的實用 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42753-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="42753-182">下一個教學課程會示範如何[使用 CORS 從 JavaScript 用戶端取用 API 應用程式][App Service API CORS]。</span><span class="sxs-lookup"><span data-stu-id="42753-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="42753-183">本系列的教學課程稍後會顯示如何實作驗證與授權。</span><span class="sxs-lookup"><span data-stu-id="42753-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="42753-184">為了根據此範例進行建置，您可以深入了解 [Storage SDK for Java] 來保存 JSON blob。</span><span class="sxs-lookup"><span data-stu-id="42753-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="42753-185">或者，您可以使用 [Document DB Java SDK] 來將您的連絡人資料儲存到 Azure Document DB。</span><span class="sxs-lookup"><span data-stu-id="42753-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="42753-186">另請參閱</span><span class="sxs-lookup"><span data-stu-id="42753-186">See Also</span></span>
<span data-ttu-id="42753-187">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="42753-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure 入口網站]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[免費試用]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[線上 Swagger 編輯器]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK for Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger 編輯器]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
