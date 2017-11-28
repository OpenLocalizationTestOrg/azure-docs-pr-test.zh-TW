---
title: "aaaBuild 和部署 Azure App Service 中的 Java 應用程式開發介面應用程式"
description: "深入了解如何 toocreate Java 應用程式開發介面應用程式封裝，並將其部署 tooAzure 應用程式服務。"
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
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="e180b-103">在 Azure App Service 中建置和部署 Java API 應用程式</span><span class="sxs-lookup"><span data-stu-id="e180b-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="e180b-104">本教學課程示範如何 toocreate Java 應用程式並將其部署 tooAzure App Service API 應用程式使用[Git]。</span><span class="sxs-lookup"><span data-stu-id="e180b-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="e180b-105">在能夠執行 Java 任何作業系統上可依照本教學課程中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="e180b-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="e180b-106">在此教學課程中的 hello 程式碼會建置使用[Maven]。</span><span class="sxs-lookup"><span data-stu-id="e180b-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="e180b-107">[Jax RS]使用的 toocreate hello rest 式服務，而且產生根據 hello [Swagger]中繼資料規格使用 hello [Swagger 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="e180b-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e180b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="e180b-108">Prerequisites</span></span>
1. <span data-ttu-id="e180b-109">[Java Developer Kit 8] \(或更新版本)</span><span class="sxs-lookup"><span data-stu-id="e180b-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="e180b-110">安裝在您開發電腦上的 [Maven]</span><span class="sxs-lookup"><span data-stu-id="e180b-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="e180b-111">安裝在您開發電腦上的 [Git]</span><span class="sxs-lookup"><span data-stu-id="e180b-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="e180b-112">付費或[免費試用版]訂用帳戶太[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e180b-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="e180b-113">HTTP 測試應用程式，例如 [郵差]</span><span class="sxs-lookup"><span data-stu-id="e180b-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="e180b-114">使用 Swagger.IO scaffold hello API</span><span class="sxs-lookup"><span data-stu-id="e180b-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="e180b-115">您可以使用 hello swagger.io 線上編輯器中，輸入 Swagger JSON 或 YAML 代表您的 API hello 結構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="e180b-116">設計 hello API 介面區之後，您可以匯出為各種不同的平台和架構程式碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="e180b-117">Hello 下一節，scaffold hello 程式碼將修改過的 tooinclude 模擬功能。</span><span class="sxs-lookup"><span data-stu-id="e180b-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="e180b-118">本示範工作會將開始 Swagger JSON 本文，您將貼上 hello swagger.io 編輯器 中，這會接著使用的 toogenerate 程式碼提出 JAX RS tooaccess 使用 REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="e180b-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="e180b-119">然後，您將編輯 hello scaffold tooreturn 模擬資料，並模擬在資料持續性機制之上建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="e180b-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="e180b-120">複製下列 Swagger JSON 程式碼 tooyour 剪貼簿的 hello:</span><span class="sxs-lookup"><span data-stu-id="e180b-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="e180b-121">瀏覽 toohello[線上 Swagger 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="e180b-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="e180b-122">一次，按一下 hello**檔案]-> [貼上 JSON**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="e180b-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![貼上 JSON 功能表項目][paste-json]
3. <span data-ttu-id="e180b-124">在 hello 連絡人清單 API Swagger JSON 您之前複製中貼上。</span><span class="sxs-lookup"><span data-stu-id="e180b-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![將 JSON 程式碼貼到 Swagger][pasted-swagger]
4. <span data-ttu-id="e180b-126">Hello 的文件頁面和呈現 hello 編輯器中的 API 摘要檢視。</span><span class="sxs-lookup"><span data-stu-id="e180b-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![檢視 Swagger 產生的文件][view-swagger-generated-docs]
5. <span data-ttu-id="e180b-128">選取 hello**產生伺服器]-> [JAX RS**功能表選項 tooscaffold hello 伺服器端程式碼您將編輯稍後 tooadd 模擬實作。</span><span class="sxs-lookup"><span data-stu-id="e180b-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![產生程式碼功能表項目][generate-code-menu-item]
   
    <span data-ttu-id="e180b-130">一旦產生 hello 程式碼，您會提供 ZIP 檔案 toodownload。</span><span class="sxs-lookup"><span data-stu-id="e180b-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="e180b-131">這個檔案包含 hello scaffold hello Swagger 程式碼產生器的程式碼，而且所有相關聯建立指令碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="e180b-132">解壓縮您在開發工作站上的 hello 整個媒體櫃 tooa 目錄。</span><span class="sxs-lookup"><span data-stu-id="e180b-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="e180b-133">編輯 hello 程式碼 tooadd 應用程式開發介面實作</span><span class="sxs-lookup"><span data-stu-id="e180b-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="e180b-134">在本節中，您將使用自訂程式碼取代 hello Swagger 產生的程式碼的伺服器端實作。</span><span class="sxs-lookup"><span data-stu-id="e180b-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="e180b-135">hello 新程式碼將傳回的連絡人 ArrayList 實體 toohello 呼叫用戶端。</span><span class="sxs-lookup"><span data-stu-id="e180b-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="e180b-136">開啟 hello *Contact.java*模型檔案，位於 hello *src/gen/java/io/swagger/模型*資料夾中，使用[Visual Studio Code]或您慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="e180b-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![開啟連絡人模型檔案][open-contact-model-file]
2. <span data-ttu-id="e180b-138">新增下列建構函式內 hello hello**連絡人**類別。</span><span class="sxs-lookup"><span data-stu-id="e180b-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="e180b-139">開啟 hello *ContactsApiServiceImpl.java*服務實作檔案中，位於 hello *src/main/java/io/swagger/api/impl*資料夾中，使用[Visual Studio Code]或您慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="e180b-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![開啟連絡人服務程式碼][open-contact-service-code-file]
4. <span data-ttu-id="e180b-141">這個新的程式碼 tooadd 模擬實作 toohello 服務程式碼，覆寫 hello hello 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="e180b-142">開啟命令提示字元並變更您的應用程式目錄 toohello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="e180b-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="e180b-143">執行 hello 遵循 Maven 命令 toobuild hello 程式碼，並執行它在本機使用 hello Jetty 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="e180b-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="e180b-144">您應該會看到 hello 反映 Jetty 已在連接埠 8080 上啟動您的程式碼的命令視窗。</span><span class="sxs-lookup"><span data-stu-id="e180b-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![開啟連絡人服務程式碼][run-jetty-war]
8. <span data-ttu-id="e180b-146">使用[郵差]http://localhost:8080/< / api/連絡人 toomake 要求 toohello > 的 < 取得所有連絡人 API 方法。</span><span class="sxs-lookup"><span data-stu-id="e180b-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![呼叫 hello 連絡人應用程式開發介面][calling-contacts-api]
9. <span data-ttu-id="e180b-148">使用[郵差]toomake 要求 toohello 「 取得特定的連絡人 」 API 方法位於 http://localhost:8080/< / api/連絡人/2。</span><span class="sxs-lookup"><span data-stu-id="e180b-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![呼叫 hello 連絡人應用程式開發介面][calling-specific-contact-api]
10. <span data-ttu-id="e180b-150">最後，藉由執行下列 Maven 命令主控台中的 hello 建置 hello Java WAR （網頁封存） 檔案。</span><span class="sxs-lookup"><span data-stu-id="e180b-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="e180b-151">建置 hello WAR 檔案之後，它將會放置到 hello**目標**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e180b-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="e180b-152">瀏覽到 hello**目標**資料夾，然後重新命名 hello WAR 檔太**ROOT.war**。</span><span class="sxs-lookup"><span data-stu-id="e180b-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="e180b-153">（請確定 hello 大小寫符合以下格式）。</span><span class="sxs-lookup"><span data-stu-id="e180b-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="e180b-154">最後，執行您的應用程式 toocreate hello 根資料夾中的下列命令的 hello**部署**資料夾 toouse toodeploy hello WAR 檔案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e180b-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="e180b-155">發行 hello 輸出 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="e180b-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="e180b-156">本章節內容，您將學習如何 toocreate 新的應用程式開發介面應用程式使用 hello Azure 入口網站中，準備裝載 Java 應用程式，該應用程式開發介面應用程式和部署 hello 新建的 WAR 檔案 tooAzure App Service toorun 您新的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e180b-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="e180b-157">在 hello 中建立新的 API app [Azure 入口網站]，依序按一下 hello**新增]-> [Web + 行動裝置應用程式開發介面應用程式]-> [**功能表項目中，輸入您的應用程式詳細資料，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="e180b-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![建立新的 API 應用程式][create-api-app]
2. <span data-ttu-id="e180b-159">一旦建立您的應用程式開發介面應用程式之後，開啟您的應用程式**設定**刀鋒視窗中，然後按一下hello**應用程式設定**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="e180b-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="e180b-160">選取 hello hello 可用的選項，從最新的 Java 版本，然後選取 hello hello 從最新的 Tomcat**網頁容器**功能表，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="e180b-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![在 [hello API 應用程式] 刀鋒視窗中設定 Java][set-up-java]
3. <span data-ttu-id="e180b-162">按一下 hello**部署認證**設定功能表項目，並提供使用者名稱和密碼，您想 toouse 發行檔案 tooyour API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e180b-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![設定部署認證][deployment-credentials]
4. <span data-ttu-id="e180b-164">按一下 hello**部署來源**設定功能表項目。</span><span class="sxs-lookup"><span data-stu-id="e180b-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="e180b-165">一次，按一下 hello**選擇來源**按鈕、 選取 hello**本機 Git 儲存機制**選項，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e180b-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="e180b-166">這會建立在 Azure 中執行的 Git 存放庫，而它與您的 API 應用程式有關聯。</span><span class="sxs-lookup"><span data-stu-id="e180b-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="e180b-167">每次認可程式碼 toohello*主要*分支的 Git 儲存機制，將您的程式碼發行至即時執行應用程式開發介面應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="e180b-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![設定新的本機 Git 存放庫][select-git-repo]
5. <span data-ttu-id="e180b-169">將複製 hello 新 Git 儲存機制的 URL tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="e180b-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="e180b-170">請務必保存這個網址，因為它在稍後會很重要。</span><span class="sxs-lookup"><span data-stu-id="e180b-170">Save this as it will be important in a moment.</span></span> 
   
    ![為您的應用程式設定新的 Git 存放庫][copy-git-repo-url]
6. <span data-ttu-id="e180b-172">Git 推送 hello WAR 檔案 toohello 線上儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e180b-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="e180b-173">toodo，瀏覽到 hello**部署**您稍早建立，讓您可以輕鬆地認可 hello 向上 toohello 儲存機制的應用程式服務中執行的程式碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e180b-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="e180b-174">之後 hello 主控台視窗並巡覽至 hello hello webapps 資料夾所在的資料夾發出 hello Git 命令 toolaunch hello 程序和引發關閉部署。</span><span class="sxs-lookup"><span data-stu-id="e180b-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="e180b-175">一旦您發出 hello**發送**要求，系統會詢問您稍早建立的 hello 部署認證 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="e180b-176">輸入您的認證之後，您應該會看到您入口網站的顯示 hello 更新部署。</span><span class="sxs-lookup"><span data-stu-id="e180b-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="e180b-177">如果您再次使用的郵差 toohit hello 新部署的 Azure App Service 中執行的應用程式開發介面應用程式，您會看到 hello 行為處於一致，而且現在它會傳回連絡資料不如預期，並使用簡單的程式碼變更 toohello Swagger.io scaffold Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![在 Azure 中即時使用您的 Java 連絡人 REST API][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="e180b-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e180b-179">Next steps</span></span>
<span data-ttu-id="e180b-180">本文中，是無法 toostart Swagger JSON 檔案與 hello Swagger.io 編輯器從取得一些 scaffold 的 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e180b-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="e180b-181">然後您做的簡單變更和 Git 部署程序，讓您得到以 Java 撰寫的實用 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e180b-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="e180b-182">hello 下一個教學課程將示範如何太[取用 API 應用程式從 JavaScript 用戶端，使用 CORS][App Service API CORS]。</span><span class="sxs-lookup"><span data-stu-id="e180b-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="e180b-183">之後的教學課程中如何 hello 數列顯示 tooimplement 驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="e180b-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="e180b-184">在此範例 toobuild，您可以進一步了解 hello[儲存體 SDK for Java] toopersist hello JSON blob。</span><span class="sxs-lookup"><span data-stu-id="e180b-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="e180b-185">或者，您可以使用 hello[文件 DB Java SDK] toosave 您連絡人資料 tooAzure 文件 DB。</span><span class="sxs-lookup"><span data-stu-id="e180b-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="e180b-186">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e180b-186">See Also</span></span>
<span data-ttu-id="e180b-187">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="e180b-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure 入口網站]: https://portal.azure.com/
[文件 DB Java SDK]: ../documentdb/documentdb-java-application.md
[免費試用版]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[線上 Swagger 編輯器]: http://editor2.swagger.io/
[郵差]: https://www.getpostman.com/
[儲存體 SDK for Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
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
