---
title: "開始使用適用於 Node.js 的 Azure CDN SDK | Microsoft Docs"
description: "了解如何撰寫 Node.js 應用程式來管理 Azure CDN。"
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
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="3c56a-103">開始使用 Azure CDN 開發</span><span class="sxs-lookup"><span data-stu-id="3c56a-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c56a-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c56a-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="3c56a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3c56a-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="3c56a-106">您可以使用 [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) ，自動建立和管理 CDN 設定檔與端點。</span><span class="sxs-lookup"><span data-stu-id="3c56a-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="3c56a-107">本教學課程會逐步建立簡單的 Node.js 主控台應用程式，示範數個可用的作業。</span><span class="sxs-lookup"><span data-stu-id="3c56a-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="3c56a-108">本教學課程的目的不是詳細說明 Azure CDN SDK for Node.js 的所有層面。</span><span class="sxs-lookup"><span data-stu-id="3c56a-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="3c56a-109">若要完成本教學課程，您應該已安裝和設定 [Node.js](http://www.nodejs.org) **4.x.x** 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3c56a-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="3c56a-110">您可以使用任何想要的文字編輯器，來建立 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="3c56a-111">為了撰寫本教學課程，我使用了 [Visual Studio 程式碼](https://code.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="3c56a-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="3c56a-112">您可以在 MSDN 上下載 [本教學課程中完成的專案](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) 。</span><span class="sxs-lookup"><span data-stu-id="3c56a-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="3c56a-113">建立專案並新增 NPM 相依性</span><span class="sxs-lookup"><span data-stu-id="3c56a-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="3c56a-114">現在，我們已為 CDN 設定檔建立資源群組，並為 Azure AD 應用程式授與權限來管理該群組內的 CDN 設定檔和端點，我們可以開始建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="3c56a-115">建立資料夾來儲存您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-115">Create a folder to store your application.</span></span>  <span data-ttu-id="3c56a-116">從主控台中使用您目前路徑中的 Node.js 工具，將您目前的位置設定為這個新資料夾，並執行下列命令來初始化您的專案︰</span><span class="sxs-lookup"><span data-stu-id="3c56a-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="3c56a-117">然後您會看到一系列用來初始化專案的問題。</span><span class="sxs-lookup"><span data-stu-id="3c56a-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="3c56a-118">本教學課程使用 app.js 做為 *進入點*。</span><span class="sxs-lookup"><span data-stu-id="3c56a-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="3c56a-119">您可以在下列範例中看到我的其他選擇。</span><span class="sxs-lookup"><span data-stu-id="3c56a-119">You can see my other choices in the following example.</span></span>

![NPM init 輸出](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="3c56a-121">我們的專案現在會使用 packages.json  檔案加以初始化。</span><span class="sxs-lookup"><span data-stu-id="3c56a-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="3c56a-122">我們的專案將使用 NPM 封裝內含的一些 Azure 程式庫。</span><span class="sxs-lookup"><span data-stu-id="3c56a-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="3c56a-123">我們將會針對 Node.js (ms-rest-azure) 使用 Azure 用戶端執行階段，針對 Node.js (azure-arm-cd) 使用 Azure CDN 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="3c56a-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="3c56a-124">讓我們將它們新增至專案做為相依性。</span><span class="sxs-lookup"><span data-stu-id="3c56a-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="3c56a-125">封裝完成安裝後，package.json  檔案看起來應該類似此範例 (版本號碼可能不同)：</span><span class="sxs-lookup"><span data-stu-id="3c56a-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

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

<span data-ttu-id="3c56a-126">最後，使用文字編輯器來建立空白文字檔，並將它儲存為專案資料夾根目錄中的 app.js 。</span><span class="sxs-lookup"><span data-stu-id="3c56a-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="3c56a-127">我們現在可以開始撰寫程式碼了。</span><span class="sxs-lookup"><span data-stu-id="3c56a-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="3c56a-128">必要項目、常數、驗證和結構</span><span class="sxs-lookup"><span data-stu-id="3c56a-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="3c56a-129">在編輯器中開啟 app.js  ，開始撰寫程式的基本結構。</span><span class="sxs-lookup"><span data-stu-id="3c56a-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="3c56a-130">使用下列內容在頂端為我們的 NPM 封裝新增「必要項目」︰</span><span class="sxs-lookup"><span data-stu-id="3c56a-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="3c56a-131">我們必須定義一些我們的方法將用到的常數。</span><span class="sxs-lookup"><span data-stu-id="3c56a-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="3c56a-132">新增下列內容。</span><span class="sxs-lookup"><span data-stu-id="3c56a-132">Add the following.</span></span>  <span data-ttu-id="3c56a-133">務必視需要使用您自己的值來取代預留位置，包括 **&lt;角括號&gt;**。</span><span class="sxs-lookup"><span data-stu-id="3c56a-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="3c56a-134">接下來，我們將會具現化 CDN 管理用戶端，並對它提供我們的認證。</span><span class="sxs-lookup"><span data-stu-id="3c56a-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="3c56a-135">如果您使用個別使用者驗證，這兩行看起來會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="3c56a-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3c56a-136">如果您選擇使用個別使用者驗證，而不是服務主體，只需使用這個程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="3c56a-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="3c56a-137">請謹慎地保護您的個別使用者認證，並且不要告訴他人。</span><span class="sxs-lookup"><span data-stu-id="3c56a-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="3c56a-138">務必使用正確資訊來取代 **&lt;角括號&gt;** 中的項目。</span><span class="sxs-lookup"><span data-stu-id="3c56a-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="3c56a-139">對於 `<redirect URI>`，請使用您在 Azure AD 中註冊應用程式時所輸入的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="3c56a-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="3c56a-140">我們的 Node.js 主控台應用程式將會採用一些命令列參數。</span><span class="sxs-lookup"><span data-stu-id="3c56a-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="3c56a-141">讓我們驗證看看是否已至少傳遞一個參數。</span><span class="sxs-lookup"><span data-stu-id="3c56a-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="3c56a-142">此動作會將我們帶到程式的主要部分，根據所傳遞的參數而定，這會讓我們轉往其他函式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="3c56a-143">在程式中有幾個地方，我們必須確定已傳遞正確數目的參數，並在參數不正確時顯示一些說明。</span><span class="sxs-lookup"><span data-stu-id="3c56a-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="3c56a-144">讓我們建立函式來執行此工作。</span><span class="sxs-lookup"><span data-stu-id="3c56a-144">Let's create functions to do that.</span></span>
   
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
7. <span data-ttu-id="3c56a-145">最後，我們將在 CDN 管理用戶端使用的函式為非同步的，因此需要有方法可在函式完成時回呼。</span><span class="sxs-lookup"><span data-stu-id="3c56a-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="3c56a-146">讓我們建立一個可顯示 CDN 管理用戶端輸出 (如果有的話)，並以正常程序結束程式的方法。</span><span class="sxs-lookup"><span data-stu-id="3c56a-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
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

<span data-ttu-id="3c56a-147">程式的基本結構已撰寫完成，接下來我們應該建立會根據我們的參數來呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="3c56a-148">列出 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="3c56a-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="3c56a-149">讓我們從列出現有設定檔和端點的程式碼來開始。</span><span class="sxs-lookup"><span data-stu-id="3c56a-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="3c56a-150">我的程式碼註解會提供預期的語法，因此我們會知道每個參數的去處。</span><span class="sxs-lookup"><span data-stu-id="3c56a-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="3c56a-151">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="3c56a-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="3c56a-152">接下來，我們將撰寫函式來建立設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="3c56a-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="3c56a-153">清除端點</span><span class="sxs-lookup"><span data-stu-id="3c56a-153">Purge an endpoint</span></span>
<span data-ttu-id="3c56a-154">假設端點已建立，我們可能想要在程式中執行的一個常見工作是清除此端點中的內容。</span><span class="sxs-lookup"><span data-stu-id="3c56a-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="3c56a-155">刪除 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="3c56a-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="3c56a-156">我們將會包含的最後一個函式會刪除端點和設定檔。</span><span class="sxs-lookup"><span data-stu-id="3c56a-156">The last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="3c56a-157">執行程式</span><span class="sxs-lookup"><span data-stu-id="3c56a-157">Running the program</span></span>
<span data-ttu-id="3c56a-158">現在我們可以使用慣用的偵錯工具或是在主控台執行我們的 Node.js 程式。</span><span class="sxs-lookup"><span data-stu-id="3c56a-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="3c56a-159">如果您要使用 Visual Studio 程式碼做為偵錯工具，您必須設定您的環境以傳入命令列參數。</span><span class="sxs-lookup"><span data-stu-id="3c56a-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="3c56a-160">Visual Studio 程式碼會在 **lanuch.json** 檔案中進行此動作。</span><span class="sxs-lookup"><span data-stu-id="3c56a-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="3c56a-161">尋找名為 **args** 的屬性，並為您的參數新增字串值陣列，使它看起來類似下列內容︰`"args": ["list", "profiles"]`。</span><span class="sxs-lookup"><span data-stu-id="3c56a-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="3c56a-162">讓我們從列出設定檔來著手。</span><span class="sxs-lookup"><span data-stu-id="3c56a-162">Let's start by listing our profiles.</span></span>

![列出設定檔](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="3c56a-164">我們得到空白陣列。</span><span class="sxs-lookup"><span data-stu-id="3c56a-164">We got back an empty array.</span></span>  <span data-ttu-id="3c56a-165">我們的資源群組中並沒有任何設定檔，因此這很合理。</span><span class="sxs-lookup"><span data-stu-id="3c56a-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="3c56a-166">現在讓我們建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="3c56a-166">Let's create a profile now.</span></span>

![建立設定檔](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="3c56a-168">現在讓我們新增端點。</span><span class="sxs-lookup"><span data-stu-id="3c56a-168">Now, let's add an endpoint.</span></span>

![建立端點](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="3c56a-170">最後，讓我們刪除設定檔。</span><span class="sxs-lookup"><span data-stu-id="3c56a-170">Finally, let's delete our profile.</span></span>

![刪除設定檔](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="3c56a-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c56a-172">Next Steps</span></span>
<span data-ttu-id="3c56a-173">若要查看此逐步解說中已完成的專案，請 [下載範例](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)。</span><span class="sxs-lookup"><span data-stu-id="3c56a-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="3c56a-174">若要查看 Azure CDN SDK for Node.js 的參考資料，請檢視 [參考資料](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/)。</span><span class="sxs-lookup"><span data-stu-id="3c56a-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="3c56a-175">若要尋找其他關於 Azure SDK for Node.js 的文件，請檢視 [完整參考資料](http://azure.github.io/azure-sdk-for-node/)。</span><span class="sxs-lookup"><span data-stu-id="3c56a-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="3c56a-176">使用 [PowerShell](cdn-manage-powershell.md)管理 CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="3c56a-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

