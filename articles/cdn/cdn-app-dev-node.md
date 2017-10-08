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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="ed088-103">開始使用 Azure CDN 開發</span><span class="sxs-lookup"><span data-stu-id="ed088-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed088-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="ed088-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="ed088-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ed088-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="ed088-106">您可以使用 hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate 建立及管理的 CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="ed088-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="ed088-107">這個教學課程引導 hello 建立簡單的 Node.js 主控台應用程式，示範數個 hello 可用的作業。</span><span class="sxs-lookup"><span data-stu-id="ed088-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="ed088-108">本教學課程中處於不應的 toodescribe 所有層面 hello Azure CDN SDK for Node.js 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ed088-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="ed088-109">toocomplete 本教學課程中，您應該已經有[Node.js](http://www.nodejs.org) **為 4.x.x**或更新版本安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="ed088-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="ed088-110">您可以使用任何文字編輯器，您希望 toocreate Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed088-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="ed088-111">toowrite 我使用這個教學課程中， [Visual Studio Code](https://code.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="ed088-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="ed088-112">hello[從本教學課程已完成的專案](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)MSDN 上的下載。</span><span class="sxs-lookup"><span data-stu-id="ed088-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="ed088-113">建立專案並新增 NPM 相依性</span><span class="sxs-lookup"><span data-stu-id="ed088-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="ed088-114">既然我們已為我們的 CDN 設定檔建立資源群組，並提供我們的 Azure AD 應用程式的權限 toomanage CDN 設定檔與該群組中的端點，我們可以開始建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed088-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="ed088-115">建立資料夾 toostore 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed088-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="ed088-116">從您目前的路徑中的 hello Node.js 工具主控台，設定目前的位置 toothis 新資料夾，並藉由執行初始化您的專案：</span><span class="sxs-lookup"><span data-stu-id="ed088-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="ed088-117">然後您會看到一系列的問題 tooinitialize 您的專案。</span><span class="sxs-lookup"><span data-stu-id="ed088-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="ed088-118">本教學課程使用 app.js 做為 *進入點*。</span><span class="sxs-lookup"><span data-stu-id="ed088-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="ed088-119">您可以看到 hello 下列範例中的其他選擇。</span><span class="sxs-lookup"><span data-stu-id="ed088-119">You can see my other choices in hello following example.</span></span>

![NPM init 輸出](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="ed088-121">我們的專案現在會使用 packages.json  檔案加以初始化。</span><span class="sxs-lookup"><span data-stu-id="ed088-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="ed088-122">受測專案即將的 toouse NPM 封裝中包含的某些 Azure 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ed088-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="ed088-123">我們將使用 hello Azure for Node.js (ms-rest-azure) 的用戶端執行階段和 hello (azure-arm-cd) Node.js 的 Azure CDN 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="ed088-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="ed088-124">讓我們加入這些 toohello 專案做為相依性。</span><span class="sxs-lookup"><span data-stu-id="ed088-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="ed088-125">Hello 封裝完成之後安裝，hello *package.json*檔案應該看起來類似 toothis 範例 （版本號碼可能會有所不同）：</span><span class="sxs-lookup"><span data-stu-id="ed088-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="ed088-126">最後，使用文字編輯器，建立空白文字檔並將它儲存為我們專案資料夾的 hello 根*app.js*。</span><span class="sxs-lookup"><span data-stu-id="ed088-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="ed088-127">我們現在準備好 toobegin 撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="ed088-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="ed088-128">必要項目、常數、驗證和結構</span><span class="sxs-lookup"><span data-stu-id="ed088-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="ed088-129">與*app.js*我們編輯器中開啟，我們會收到 hello 基本結構，我們撰寫的程式。</span><span class="sxs-lookup"><span data-stu-id="ed088-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="ed088-130">加入 hello 「 必須 」 在 hello 下列 hello 頂端我們 NPM 封裝：</span><span class="sxs-lookup"><span data-stu-id="ed088-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="ed088-131">我們需要 toodefine 我們方法會使用某些常數。</span><span class="sxs-lookup"><span data-stu-id="ed088-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="ed088-132">加入下列 hello。</span><span class="sxs-lookup"><span data-stu-id="ed088-132">Add hello following.</span></span>  <span data-ttu-id="ed088-133">是確定 tooreplace hello 預留位置，包括 hello **&lt;角括號&gt;**，與您自己的值，視需要。</span><span class="sxs-lookup"><span data-stu-id="ed088-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="ed088-134">接下來，我們會具現化 hello CDN 管理用戶端，並提供我們的認證。</span><span class="sxs-lookup"><span data-stu-id="ed088-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="ed088-135">如果您使用個別使用者驗證，這兩行看起來會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="ed088-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ed088-136">如果您選擇 toohave 個別使用者驗證，而不是服務主體，只能使用此程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ed088-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="ed088-137">是小心 tooguard 您個別使用者的認證，並將其保密。</span><span class="sxs-lookup"><span data-stu-id="ed088-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="ed088-138">中的 hello 項目是確定 tooreplace **&lt;角括號&gt;** hello 包含正確的資訊。</span><span class="sxs-lookup"><span data-stu-id="ed088-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="ed088-139">如`<redirect URI>`，使用 hello 重新導向 Azure AD 中註冊 hello 應用程式時所輸入的 URI。</span><span class="sxs-lookup"><span data-stu-id="ed088-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="ed088-140">我們 Node.js 的主控台應用程式正在 tootake 一些命令列參數。</span><span class="sxs-lookup"><span data-stu-id="ed088-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="ed088-141">讓我們驗證看看是否已至少傳遞一個參數。</span><span class="sxs-lookup"><span data-stu-id="ed088-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="ed088-142">接著我們的程式，其中我們分出分支 tooother 函式為基礎的參數傳遞 toohello 主要部分。</span><span class="sxs-lookup"><span data-stu-id="ed088-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="ed088-143">在我們程式中的幾個地方，我們需要 toomake 確認傳遞的 hello 正確的參數數目，並顯示相關協助，如果它們看起來不正確。</span><span class="sxs-lookup"><span data-stu-id="ed088-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="ed088-144">讓我們來建立函式 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="ed088-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="ed088-145">最後，我們將使用 hello CDN 管理用戶端的 hello 函式是非同步作業，所以它們需要方法 toocall 它們完成時。</span><span class="sxs-lookup"><span data-stu-id="ed088-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="ed088-146">讓我們進行可以顯示 hello hello CDN 管理用戶端 （如果有的話） 的輸出，結束 hello 程式依正常程序。</span><span class="sxs-lookup"><span data-stu-id="ed088-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="ed088-147">寫入 hello 基本程式結構，我們應該建立 hello 函式呼叫根據我們的參數。</span><span class="sxs-lookup"><span data-stu-id="ed088-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="ed088-148">列出 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="ed088-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="ed088-149">讓我們開始使用程式碼 toolist 我們現有的設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="ed088-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="ed088-150">我的程式碼註解提供預期的 hello 語法，以便讓我們知道每個參數的地方。</span><span class="sxs-lookup"><span data-stu-id="ed088-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="ed088-151">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="ed088-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="ed088-152">接下來，我們會撰寫 hello 函式 toocreate 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="ed088-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="ed088-153">清除端點</span><span class="sxs-lookup"><span data-stu-id="ed088-153">Purge an endpoint</span></span>
<span data-ttu-id="ed088-154">假設已建立 hello 端點，一項通用工作，我們可能會想 tooperform 在我們程式中已清除我們端點中的內容。</span><span class="sxs-lookup"><span data-stu-id="ed088-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="ed088-155">刪除 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="ed088-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="ed088-156">hello，就會加入的最後一個函式會刪除端點和設定檔。</span><span class="sxs-lookup"><span data-stu-id="ed088-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="ed088-157">執行 hello 程式</span><span class="sxs-lookup"><span data-stu-id="ed088-157">Running hello program</span></span>
<span data-ttu-id="ed088-158">我們現在可以執行使用我們最喜愛的偵錯工具我們 Node.js 程式或在 hello 主控台。</span><span class="sxs-lookup"><span data-stu-id="ed088-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="ed088-159">如果您使用 Visual Studio 程式碼當作您偵錯工具，您必須 tooset 註冊您的環境 toopass hello 命令列參數中。</span><span class="sxs-lookup"><span data-stu-id="ed088-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="ed088-160">Visual Studio 程式碼會在 hello **lanuch.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="ed088-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="ed088-161">尋找名為屬性**args**並加入您的參數的字串值的陣列，使它看起來類似 toothis: `"args": ["list", "profiles"]`。</span><span class="sxs-lookup"><span data-stu-id="ed088-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="ed088-162">讓我們從列出設定檔來著手。</span><span class="sxs-lookup"><span data-stu-id="ed088-162">Let's start by listing our profiles.</span></span>

![列出設定檔](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="ed088-164">我們得到空白陣列。</span><span class="sxs-lookup"><span data-stu-id="ed088-164">We got back an empty array.</span></span>  <span data-ttu-id="ed088-165">我們的資源群組中並沒有任何設定檔，因此這很合理。</span><span class="sxs-lookup"><span data-stu-id="ed088-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="ed088-166">現在讓我們建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="ed088-166">Let's create a profile now.</span></span>

![建立設定檔](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="ed088-168">現在讓我們新增端點。</span><span class="sxs-lookup"><span data-stu-id="ed088-168">Now, let's add an endpoint.</span></span>

![建立端點](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="ed088-170">最後，讓我們刪除設定檔。</span><span class="sxs-lookup"><span data-stu-id="ed088-170">Finally, let's delete our profile.</span></span>

![刪除設定檔](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="ed088-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed088-172">Next Steps</span></span>
<span data-ttu-id="ed088-173">這個逐步解說中，從 toosee hello 完成專案[下載 hello 範例](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)。</span><span class="sxs-lookup"><span data-stu-id="ed088-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="ed088-174">hello Azure CDN SDK for Node.js 檢視 hello toosee hello 參考[參考](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/)。</span><span class="sxs-lookup"><span data-stu-id="ed088-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="ed088-175">toofind 相關文件 hello Azure SDK for Node.js，檢視 hello[完整參考](http://azure.github.io/azure-sdk-for-node/)。</span><span class="sxs-lookup"><span data-stu-id="ed088-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="ed088-176">使用 [PowerShell](cdn-manage-powershell.md)管理 CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="ed088-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

