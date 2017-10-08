---
title: "aaaGet 入門 hello Azure CDN SDK for Node.js |Microsoft 文件"
description: "深入了解如何 toowrite Node.js 應用程式 toomanage Azure CDN。"
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>開始使用 Azure CDN 開發
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

您可以使用 hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate 建立及管理的 CDN 設定檔和端點。  這個教學課程引導 hello 建立簡單的 Node.js 主控台應用程式，示範數個 hello 可用的作業。  本教學課程中處於不應的 toodescribe 所有層面 hello Azure CDN SDK for Node.js 詳細資料。

toocomplete 本教學課程中，您應該已經有[Node.js](http://www.nodejs.org) **為 4.x.x**或更新版本安裝和設定。  您可以使用任何文字編輯器，您希望 toocreate Node.js 應用程式。  toowrite 我使用這個教學課程中， [Visual Studio Code](https://code.visualstudio.com)。  

> [!TIP]
> hello[從本教學課程已完成的專案](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)MSDN 上的下載。
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>建立專案並新增 NPM 相依性
既然我們已為我們的 CDN 設定檔建立資源群組，並提供我們的 Azure AD 應用程式的權限 toomanage CDN 設定檔與該群組中的端點，我們可以開始建立應用程式。

建立資料夾 toostore 您的應用程式。  從您目前的路徑中的 hello Node.js 工具主控台，設定目前的位置 toothis 新資料夾，並藉由執行初始化您的專案：

    npm init

然後您會看到一系列的問題 tooinitialize 您的專案。  本教學課程使用 app.js 做為 *進入點*。  您可以看到 hello 下列範例中的其他選擇。

![NPM init 輸出](./media/cdn-app-dev-node/cdn-npm-init.png)

我們的專案現在會使用 packages.json  檔案加以初始化。  受測專案即將的 toouse NPM 封裝中包含的某些 Azure 程式庫。  我們將使用 hello Azure for Node.js (ms-rest-azure) 的用戶端執行階段和 hello (azure-arm-cd) Node.js 的 Azure CDN 用戶端程式庫。  讓我們加入這些 toohello 專案做為相依性。

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Hello 封裝完成之後安裝，hello *package.json*檔案應該看起來類似 toothis 範例 （版本號碼可能會有所不同）：

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

最後，使用文字編輯器，建立空白文字檔並將它儲存為我們專案資料夾的 hello 根*app.js*。  我們現在準備好 toobegin 撰寫程式碼。

## <a name="requires-constants-authentication-and-structure"></a>必要項目、常數、驗證和結構
與*app.js*我們編輯器中開啟，我們會收到 hello 基本結構，我們撰寫的程式。

1. 加入 hello 「 必須 」 在 hello 下列 hello 頂端我們 NPM 封裝：
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. 我們需要 toodefine 我們方法會使用某些常數。  加入下列 hello。  是確定 tooreplace hello 預留位置，包括 hello **&lt;角括號&gt;**，與您自己的值，視需要。
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. 接下來，我們會具現化 hello CDN 管理用戶端，並提供我們的認證。
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    如果您使用個別使用者驗證，這兩行看起來會稍有不同。
   
   > [!IMPORTANT]
   > 如果您選擇 toohave 個別使用者驗證，而不是服務主體，只能使用此程式碼範例。  是小心 tooguard 您個別使用者的認證，並將其保密。
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    中的 hello 項目是確定 tooreplace **&lt;角括號&gt;** hello 包含正確的資訊。  如`<redirect URI>`，使用 hello 重新導向 Azure AD 中註冊 hello 應用程式時所輸入的 URI。
4. 我們 Node.js 的主控台應用程式正在 tootake 一些命令列參數。  讓我們驗證看看是否已至少傳遞一個參數。
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. 接著我們的程式，其中我們分出分支 tooother 函式為基礎的參數傳遞 toohello 主要部分。
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. 在我們程式中的幾個地方，我們需要 toomake 確認傳遞的 hello 正確的參數數目，並顯示相關協助，如果它們看起來不正確。  讓我們來建立函式 toodo 的。
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. 最後，我們將使用 hello CDN 管理用戶端的 hello 函式是非同步作業，所以它們需要方法 toocall 它們完成時。  讓我們進行可以顯示 hello hello CDN 管理用戶端 （如果有的話） 的輸出，結束 hello 程式依正常程序。
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

寫入 hello 基本程式結構，我們應該建立 hello 函式呼叫根據我們的參數。

## <a name="list-cdn-profiles-and-endpoints"></a>列出 CDN 設定檔和端點
讓我們開始使用程式碼 toolist 我們現有的設定檔和端點。  我的程式碼註解提供預期的 hello 語法，以便讓我們知道每個參數的地方。

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>建立 CDN 設定檔和端點
接下來，我們會撰寫 hello 函式 toocreate 設定檔和端點。

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a>清除端點
假設已建立 hello 端點，一項通用工作，我們可能會想 tooperform 在我們程式中已清除我們端點中的內容。

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>刪除 CDN 設定檔和端點
hello，就會加入的最後一個函式會刪除端點和設定檔。

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a>執行 hello 程式
我們現在可以執行使用我們最喜愛的偵錯工具我們 Node.js 程式或在 hello 主控台。

> [!TIP]
> 如果您使用 Visual Studio 程式碼當作您偵錯工具，您必須 tooset 註冊您的環境 toopass hello 命令列參數中。  Visual Studio 程式碼會在 hello **lanuch.json**檔案。  尋找名為屬性**args**並加入您的參數的字串值的陣列，使它看起來類似 toothis: `"args": ["list", "profiles"]`。
> 
> 

讓我們從列出設定檔來著手。

![列出設定檔](./media/cdn-app-dev-node/cdn-list-profiles.png)

我們得到空白陣列。  我們的資源群組中並沒有任何設定檔，因此這很合理。  現在讓我們建立設定檔。

![建立設定檔](./media/cdn-app-dev-node/cdn-create-profile.png)

現在讓我們新增端點。

![建立端點](./media/cdn-app-dev-node/cdn-create-endpoint.png)

最後，讓我們刪除設定檔。

![刪除設定檔](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>後續步驟
這個逐步解說中，從 toosee hello 完成專案[下載 hello 範例](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)。

hello Azure CDN SDK for Node.js 檢視 hello toosee hello 參考[參考](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/)。

toofind 相關文件 hello Azure SDK for Node.js，檢視 hello[完整參考](http://azure.github.io/azure-sdk-for-node/)。

使用 [PowerShell](cdn-manage-powershell.md)管理 CDN 資源。

