---
title: "使用 Socket.io aaaNode.js 應用程式 |Microsoft 文件"
description: "了解 toouse socket.io node.js 應用程式中的裝載在 Azure 上的方式。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="59b5c-103">在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 交談應用程式</span><span class="sxs-lookup"><span data-stu-id="59b5c-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="59b5c-104">Socket.IO 提供 node.js 伺服器和用戶端之間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="59b5c-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="59b5c-105">本教學課程引導您將 socket.IO 型交談應用程式裝載於 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="59b5c-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="59b5c-106">如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。</span><span class="sxs-lookup"><span data-stu-id="59b5c-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="59b5c-107">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="59b5c-107">A screenshot of hello completed application is below:</span></span>

![瀏覽器視窗，以顯示裝載於 Azure 的 hello 服務][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="59b5c-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="59b5c-109">Prerequisites</span></span>
<span data-ttu-id="59b5c-110">確定該 hello 下列產品和版本會在本文中的已安裝的 toosuccessfully 完成 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="59b5c-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="59b5c-111">安裝 [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="59b5c-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="59b5c-112">安裝 [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="59b5c-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="59b5c-113">安裝 [Python 版本 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="59b5c-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="59b5c-114">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="59b5c-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="59b5c-115">hello 下列步驟建立 hello 雲端服務專案將裝載 hello Socket.IO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b5c-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="59b5c-116">從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="59b5c-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="59b5c-117">最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="59b5c-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon][powershell-menu]
2. <span data-ttu-id="59b5c-119">建立名為 **c:\\node** 的目錄。</span><span class="sxs-lookup"><span data-stu-id="59b5c-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="59b5c-120">變更目錄 toohello **c:\\節點**目錄</span><span class="sxs-lookup"><span data-stu-id="59b5c-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="59b5c-121">輸入下列命令 toocreate 名為新方案的 hello **chatapp**和名為的背景工作角色**WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="59b5c-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="59b5c-122">您會看到下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="59b5c-122">You will see hello following response:</span></span>
   
    ![hello 的輸出 hello 新 azureservice 和新增 azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="59b5c-124">下載 hello 聊天範例</span><span class="sxs-lookup"><span data-stu-id="59b5c-124">Download hello Chat Example</span></span>
<span data-ttu-id="59b5c-125">此專案中，我們將使用從 hello hello 聊天範例[Socket.IO GitHub 儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="59b5c-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="59b5c-126">執行下列步驟 toodownload hello 範例 hello，並將它加入您先前建立的 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="59b5c-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="59b5c-127">建立 hello 儲存機制的本機副本使用 hello**複製** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b5c-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="59b5c-128">您也可以使用 hello **ZIP**按鈕 toodownload hello 專案。</span><span class="sxs-lookup"><span data-stu-id="59b5c-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![反白顯示 hello ZIP 下載圖示以檢視 https://github.com/LearnBoost/socket.io/tree/master/examples/chat，在瀏覽器視窗][chat-example-view]
2. <span data-ttu-id="59b5c-130">瀏覽 hello hello 本機儲存機制的目錄結構，直到您到達 hello**範例\\聊天**目錄。</span><span class="sxs-lookup"><span data-stu-id="59b5c-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="59b5c-131">將這個目錄 toothe hello 內容複製**c:\\節點\\chatapp\\WorkerRole1**稍早建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="59b5c-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![總管 中，顯示 hello 範例 hello 內容\\從 hello 封存解壓縮的聊天目錄][chat-contents]
   
   <span data-ttu-id="59b5c-133">hello hello 上方螢幕擷取畫面中反白顯示的項目會從 hello 複製的 hello 檔案**範例\\聊天**目錄</span><span class="sxs-lookup"><span data-stu-id="59b5c-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="59b5c-134">在 hello **c:\\節點\\chatapp\\WorkerRole1**目錄中，刪除 hello**立即轉譯 server.js**檔案，然後再重新命名 hello **app.js**檔案太**立即轉譯 server.js**。</span><span class="sxs-lookup"><span data-stu-id="59b5c-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="59b5c-135">這會移除 hello 預設**立即轉譯 server.js**先前由 hello**新增 AzureNodeWorkerRole**指令程式，並從它與 hello 應用程式檔案的取代 hello 聊天範例。</span><span class="sxs-lookup"><span data-stu-id="59b5c-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="59b5c-136">修改 Server.js 和安裝模組</span><span class="sxs-lookup"><span data-stu-id="59b5c-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="59b5c-137">測試 hello 應用之前 hello Azure 模擬器中，我們必須進行一些次要的修改。</span><span class="sxs-lookup"><span data-stu-id="59b5c-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="59b5c-138">執行下列步驟 toothe 立即轉譯 server.js 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="59b5c-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="59b5c-139">開啟 hello**立即轉譯 server.js** Visual Studio 或任何文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="59b5c-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="59b5c-140">尋找 hello**模組相依性**區段開頭 hello 立即轉譯 server.js 和變更 hello 列包含**sio = require('..//..lib//socket.io')**太**sio = require('socket.io')**如下所示：</span><span class="sxs-lookup"><span data-stu-id="59b5c-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="59b5c-141">hello 正確的通訊埠上接聽的 tooensure hello 應用程式、 開啟立即轉譯 server.js [記事本] 或您偏好的編輯器，然後變更下列行取代**3000**與**process.env.port**所示如下：</span><span class="sxs-lookup"><span data-stu-id="59b5c-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="59b5c-142">儲存 hello 變更太之後**立即轉譯 server.js**使用 hello 下列步驟來安裝所需的模組，然後在 Azure 模擬器中測試 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="59b5c-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="59b5c-143">使用**Azure PowerShell**，變更目錄 toohello **c:\\節點\\chatapp\\WorkerRole1**目錄，並使用下列命令 tooinstall hello 的 hello此應用程式所需的模組：</span><span class="sxs-lookup"><span data-stu-id="59b5c-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="59b5c-144">這會安裝在 hello package.json 檔案中列出的 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="59b5c-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="59b5c-145">Hello 命令完成之後，您應該會看到類似 toothe 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="59b5c-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![hello 輸出的 hello npm 安裝命令][The-output-of-the-npm-install-command]
2. <span data-ttu-id="59b5c-147">由於本範例原本 hello Socket.IO GitHub 儲存機制的一部分，而且直接由相對路徑參考 hello Socket.IO 程式庫，Socket.IO 中都未參考 hello package.json 檔案，所以我們必須安裝它，藉由發出下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="59b5c-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="59b5c-148">測試和部署</span><span class="sxs-lookup"><span data-stu-id="59b5c-148">Test and Deploy</span></span>
1. <span data-ttu-id="59b5c-149">藉由發出下列命令的 hello 啟動 hello 模擬器：</span><span class="sxs-lookup"><span data-stu-id="59b5c-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="59b5c-150">如果您在啟動模擬器時遇到問題，例如：Start-AzureEmulator：發生未預期的失敗。</span><span class="sxs-lookup"><span data-stu-id="59b5c-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="59b5c-151">詳細資料： 發生未預期的錯誤 hello 通訊物件 System.ServiceModel.Channels.ServiceChannel 無法用於通訊，因為它處於 Faulted 狀態 hello。</span><span class="sxs-lookup"><span data-stu-id="59b5c-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="59b5c-152">重新安裝 AzureAuthoringTools v 2.7.1 和 AzureComputeEmulator v 2.7 - 請確定版本相符。</span><span class="sxs-lookup"><span data-stu-id="59b5c-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="59b5c-153">開啟瀏覽器並瀏覽過**http://127.0.0.1**。</span><span class="sxs-lookup"><span data-stu-id="59b5c-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="59b5c-154">當 hello 瀏覽器視窗開啟時，輸入別名，然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="59b5c-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="59b5c-155">這可讓您 toopost 訊息做為特定的暱稱。</span><span class="sxs-lookup"><span data-stu-id="59b5c-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="59b5c-156">tootest 多使用者功能，開啟其他瀏覽器視窗使用相同的 URL，並輸入不同的暱稱。</span><span class="sxs-lookup"><span data-stu-id="59b5c-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![兩個瀏覽器視窗顯示 User1 和 User2 的交談訊息](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="59b5c-158">測試的 hello 應用程式後停止模擬器 hello 發出下列命令：</span><span class="sxs-lookup"><span data-stu-id="59b5c-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="59b5c-159">toodeploy hello 應用程式 tooAzure，使用**發行 AzureServiceProject** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="59b5c-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="59b5c-160">例如：</span><span class="sxs-lookup"><span data-stu-id="59b5c-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="59b5c-161">要確定 toouse 唯一的名稱，否則 hello 發佈程序將會失敗。</span><span class="sxs-lookup"><span data-stu-id="59b5c-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="59b5c-162">Hello 部署完成後，hello 瀏覽器會開啟，並瀏覽 toohello 部署服務。</span><span class="sxs-lookup"><span data-stu-id="59b5c-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="59b5c-163">如果您收到錯誤，表示該 hello 提供訂用帳戶名稱不存在於 hello 匯入發行設定檔，您必須下載並匯入您的訂用帳戶，然後再部署 tooAzure hello 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="59b5c-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="59b5c-164">請參閱 hello**部署 hello 應用程式 tooAzure**區段[建置和部署 Node.js 應用程式 tooan Azure 雲端服務](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="59b5c-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![瀏覽器視窗，以顯示裝載於 Azure 的 hello 服務][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="59b5c-166">如果您收到錯誤，表示該 hello 提供訂用帳戶名稱不存在於 hello 匯入發行設定檔，您必須下載並匯入您的訂用帳戶，然後再部署 tooAzure hello 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="59b5c-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="59b5c-167">請參閱 hello**部署 hello 應用程式 tooAzure**區段[建置和部署 Node.js 應用程式 tooan Azure 雲端服務](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="59b5c-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="59b5c-168">應用程式現在已在 Azure 上執行，且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。</span><span class="sxs-lookup"><span data-stu-id="59b5c-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="59b5c-169">為了簡單起見，此範例是有限的使用者連接 toohello 之間 toochatting 相同的執行個體。</span><span class="sxs-lookup"><span data-stu-id="59b5c-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="59b5c-170">這表示，如果 hello 雲端服務會建立兩個背景工作角色執行個體，使用者將只能與其他人 toochat 連接 toohello 相同的背景工作角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="59b5c-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="59b5c-171">tooscale hello 與多個角色執行個體的應用程式 toowork，您可以使用一種技術類似 Service Bus tooshare hello Socket.IO 存放區狀態跨執行個體。</span><span class="sxs-lookup"><span data-stu-id="59b5c-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="59b5c-172">如需範例，請參閱 < 在 hello hello Service Bus 佇列和主題使用範例[Azure SDK for Node.js GitHub 儲存機制](https://github.com/WindowsAzure/azure-sdk-for-node)。</span><span class="sxs-lookup"><span data-stu-id="59b5c-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="59b5c-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59b5c-173">Next steps</span></span>
<span data-ttu-id="59b5c-174">在本教學課程中，您學會如何 toocreate 基本交談應用程式裝載於 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="59b5c-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="59b5c-175">toolearn 如何 toohost 此應用程式在 Azure 網站，請參閱[Node.js 聊天的建置應用程式 Socket.IO Azure 網站上][chatwebsite]。</span><span class="sxs-lookup"><span data-stu-id="59b5c-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="59b5c-176">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="59b5c-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub 儲存機制]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


