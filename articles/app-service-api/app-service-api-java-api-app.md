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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>在 Azure App Service 中建置和部署 Java API 應用程式
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

本教學課程示範如何 toocreate Java 應用程式並將其部署 tooAzure App Service API 應用程式使用[Git]。 在能夠執行 Java 任何作業系統上可依照本教學課程中的 hello 指示。 在此教學課程中的 hello 程式碼會建置使用[Maven]。 [Jax RS]使用的 toocreate hello rest 式服務，而且產生根據 hello [Swagger]中繼資料規格使用 hello [Swagger 編輯器]。

## <a name="prerequisites"></a>必要條件
1. [Java Developer Kit 8] \(或更新版本)
2. 安裝在您開發電腦上的 [Maven]
3. 安裝在您開發電腦上的 [Git]
4. 付費或[免費試用版]訂用帳戶太[Microsoft Azure]
5. HTTP 測試應用程式，例如 [郵差]

## <a name="scaffold-hello-api-using-swaggerio"></a>使用 Swagger.IO scaffold hello API
您可以使用 hello swagger.io 線上編輯器中，輸入 Swagger JSON 或 YAML 代表您的 API hello 結構的程式碼。 設計 hello API 介面區之後，您可以匯出為各種不同的平台和架構程式碼。 Hello 下一節，scaffold hello 程式碼將修改過的 tooinclude 模擬功能。 

本示範工作會將開始 Swagger JSON 本文，您將貼上 hello swagger.io 編輯器 中，這會接著使用的 toogenerate 程式碼提出 JAX RS tooaccess 使用 REST API 端點。 然後，您將編輯 hello scaffold tooreturn 模擬資料，並模擬在資料持續性機制之上建置 REST API。  

1. 複製下列 Swagger JSON 程式碼 tooyour 剪貼簿的 hello:
   
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
2. 瀏覽 toohello[線上 Swagger 編輯器]。 一次，按一下 hello**檔案]-> [貼上 JSON**功能表項目。
   
    ![貼上 JSON 功能表項目][paste-json]
3. 在 hello 連絡人清單 API Swagger JSON 您之前複製中貼上。 
   
    ![將 JSON 程式碼貼到 Swagger][pasted-swagger]
4. Hello 的文件頁面和呈現 hello 編輯器中的 API 摘要檢視。 
   
    ![檢視 Swagger 產生的文件][view-swagger-generated-docs]
5. 選取 hello**產生伺服器]-> [JAX RS**功能表選項 tooscaffold hello 伺服器端程式碼您將編輯稍後 tooadd 模擬實作。 
   
    ![產生程式碼功能表項目][generate-code-menu-item]
   
    一旦產生 hello 程式碼，您會提供 ZIP 檔案 toodownload。 這個檔案包含 hello scaffold hello Swagger 程式碼產生器的程式碼，而且所有相關聯建立指令碼。 解壓縮您在開發工作站上的 hello 整個媒體櫃 tooa 目錄。 

## <a name="edit-hello-code-tooadd-api-implementation"></a>編輯 hello 程式碼 tooadd 應用程式開發介面實作
在本節中，您將使用自訂程式碼取代 hello Swagger 產生的程式碼的伺服器端實作。 hello 新程式碼將傳回的連絡人 ArrayList 實體 toohello 呼叫用戶端。 

1. 開啟 hello *Contact.java*模型檔案，位於 hello *src/gen/java/io/swagger/模型*資料夾中，使用[Visual Studio Code]或您慣用的文字編輯器。 
   
    ![開啟連絡人模型檔案][open-contact-model-file]
2. 新增下列建構函式內 hello hello**連絡人**類別。 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. 開啟 hello *ContactsApiServiceImpl.java*服務實作檔案中，位於 hello *src/main/java/io/swagger/api/impl*資料夾中，使用[Visual Studio Code]或您慣用的文字編輯器。
   
    ![開啟連絡人服務程式碼][open-contact-service-code-file]
4. 這個新的程式碼 tooadd 模擬實作 toohello 服務程式碼，覆寫 hello hello 檔案中的程式碼。 
   
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
5. 開啟命令提示字元並變更您的應用程式目錄 toohello 根資料夾。
6. 執行 hello 遵循 Maven 命令 toobuild hello 程式碼，並執行它在本機使用 hello Jetty 應用程式伺服器。 
   
        mvn package jetty:run
7. 您應該會看到 hello 反映 Jetty 已在連接埠 8080 上啟動您的程式碼的命令視窗。 
   
    ![開啟連絡人服務程式碼][run-jetty-war]
8. 使用[郵差]http://localhost:8080/< / api/連絡人 toomake 要求 toohello > 的 < 取得所有連絡人 API 方法。
   
    ![呼叫 hello 連絡人應用程式開發介面][calling-contacts-api]
9. 使用[郵差]toomake 要求 toohello 「 取得特定的連絡人 」 API 方法位於 http://localhost:8080/< / api/連絡人/2。
   
    ![呼叫 hello 連絡人應用程式開發介面][calling-specific-contact-api]
10. 最後，藉由執行下列 Maven 命令主控台中的 hello 建置 hello Java WAR （網頁封存） 檔案。 
    
         mvn package war:war
11. 建置 hello WAR 檔案之後，它將會放置到 hello**目標**資料夾。 瀏覽到 hello**目標**資料夾，然後重新命名 hello WAR 檔太**ROOT.war**。 （請確定 hello 大小寫符合以下格式）。
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. 最後，執行您的應用程式 toocreate hello 根資料夾中的下列命令的 hello**部署**資料夾 toouse toodeploy hello WAR 檔案 tooAzure。 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>發行 hello 輸出 tooAzure 應用程式服務
本章節內容，您將學習如何 toocreate 新的應用程式開發介面應用程式使用 hello Azure 入口網站中，準備裝載 Java 應用程式，該應用程式開發介面應用程式和部署 hello 新建的 WAR 檔案 tooAzure App Service toorun 您新的 API 應用程式。 

1. 在 hello 中建立新的 API app [Azure 入口網站]，依序按一下 hello**新增]-> [Web + 行動裝置應用程式開發介面應用程式]-> [**功能表項目中，輸入您的應用程式詳細資料，然後按一下**建立**。
   
    ![建立新的 API 應用程式][create-api-app]
2. 一旦建立您的應用程式開發介面應用程式之後，開啟您的應用程式**設定**刀鋒視窗中，然後按一下hello**應用程式設定**功能表項目。 選取 hello hello 可用的選項，從最新的 Java 版本，然後選取 hello hello 從最新的 Tomcat**網頁容器**功能表，然後再按一下**儲存**。
   
    ![在 [hello API 應用程式] 刀鋒視窗中設定 Java][set-up-java]
3. 按一下 hello**部署認證**設定功能表項目，並提供使用者名稱和密碼，您想 toouse 發行檔案 tooyour API 應用程式。 
   
    ![設定部署認證][deployment-credentials]
4. 按一下 hello**部署來源**設定功能表項目。 一次，按一下 hello**選擇來源**按鈕、 選取 hello**本機 Git 儲存機制**選項，然後再按一下**確定**。 這會建立在 Azure 中執行的 Git 存放庫，而它與您的 API 應用程式有關聯。 每次認可程式碼 toohello*主要*分支的 Git 儲存機制，將您的程式碼發行至即時執行應用程式開發介面應用程式執行個體。 
   
    ![設定新的本機 Git 存放庫][select-git-repo]
5. 將複製 hello 新 Git 儲存機制的 URL tooyour 剪貼簿。 請務必保存這個網址，因為它在稍後會很重要。 
   
    ![為您的應用程式設定新的 Git 存放庫][copy-git-repo-url]
6. Git 推送 hello WAR 檔案 toohello 線上儲存機制。 toodo，瀏覽到 hello**部署**您稍早建立，讓您可以輕鬆地認可 hello 向上 toohello 儲存機制的應用程式服務中執行的程式碼的資料夾。 之後 hello 主控台視窗並巡覽至 hello hello webapps 資料夾所在的資料夾發出 hello Git 命令 toolaunch hello 程序和引發關閉部署。 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    一旦您發出 hello**發送**要求，系統會詢問您稍早建立的 hello 部署認證 hello 密碼。 輸入您的認證之後，您應該會看到您入口網站的顯示 hello 更新部署。
7. 如果您再次使用的郵差 toohit hello 新部署的 Azure App Service 中執行的應用程式開發介面應用程式，您會看到 hello 行為處於一致，而且現在它會傳回連絡資料不如預期，並使用簡單的程式碼變更 toohello Swagger.io scaffold Java 程式碼。 
   
    ![在 Azure 中即時使用您的 Java 連絡人 REST API][postman-calling-azure-contacts]

## <a name="next-steps"></a>後續步驟
本文中，是無法 toostart Swagger JSON 檔案與 hello Swagger.io 編輯器從取得一些 scaffold 的 Java 程式碼。 然後您做的簡單變更和 Git 部署程序，讓您得到以 Java 撰寫的實用 API 應用程式。 hello 下一個教學課程將示範如何太[取用 API 應用程式從 JavaScript 用戶端，使用 CORS][App Service API CORS]。 之後的教學課程中如何 hello 數列顯示 tooimplement 驗證和授權。

在此範例 toobuild，您可以進一步了解 hello[儲存體 SDK for Java] toopersist hello JSON blob。 或者，您可以使用 hello[文件 DB Java SDK] toosave 您連絡人資料 tooAzure 文件 DB。 

<a name="see-also"></a>

## <a name="see-also"></a>另請參閱
如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。

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
