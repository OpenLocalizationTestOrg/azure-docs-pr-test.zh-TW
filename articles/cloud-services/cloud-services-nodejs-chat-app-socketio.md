---
title: "使用 Socket.io 的 Node.js 應用程式 | Microsoft Docs"
description: "學習如何在裝載於 Azure 的 node.js 應用程式中使用 socket.io。"
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
ms.openlocfilehash: a85d4348a13b79b5b7542362de9956aa3398375a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="45b22-103">在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 交談應用程式</span><span class="sxs-lookup"><span data-stu-id="45b22-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="45b22-104">Socket.IO 提供 node.js 伺服器和用戶端之間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="45b22-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="45b22-105">本教學課程引導您將 socket.IO 型交談應用程式裝載於 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="45b22-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="45b22-106">如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。</span><span class="sxs-lookup"><span data-stu-id="45b22-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="45b22-107">完成之應用程式的螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="45b22-107">A screenshot of the completed application is below:</span></span>

![A browser window displaying the service hosted on Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="45b22-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="45b22-109">Prerequisites</span></span>
<span data-ttu-id="45b22-110">請確定已安裝下列產品及版本，以順利完成本文中的範例：</span><span class="sxs-lookup"><span data-stu-id="45b22-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="45b22-111">安裝 [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="45b22-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="45b22-112">安裝 [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="45b22-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="45b22-113">安裝 [Python 版本 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="45b22-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="45b22-114">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="45b22-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="45b22-115">下列步驟會建立雲端服務專案來裝載 Socket.IO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b22-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="45b22-116">從 [開始功能表] 或 [開始畫面] 搜尋 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="45b22-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="45b22-117">最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="45b22-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon][powershell-menu]
2. <span data-ttu-id="45b22-119">建立名為 **c:\\node** 的目錄。</span><span class="sxs-lookup"><span data-stu-id="45b22-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="45b22-120">切換至 **c:\\node** 目錄，</span><span class="sxs-lookup"><span data-stu-id="45b22-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="45b22-121">然後輸入下列命令來建立名為 **chatapp** 的新方案和名為 **WorkerRole1** 的背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="45b22-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="45b22-122">您將看見下列回應：</span><span class="sxs-lookup"><span data-stu-id="45b22-122">You will see the following response:</span></span>
   
    ![The output of the new-azureservice and add-azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="45b22-124">下載交談範例</span><span class="sxs-lookup"><span data-stu-id="45b22-124">Download the Chat Example</span></span>
<span data-ttu-id="45b22-125">在此專案中，我們使用 [Socket.IO GitHub 儲存機制]中的交談範例。</span><span class="sxs-lookup"><span data-stu-id="45b22-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="45b22-126">請執行下列步驟來下載範例，並將它加入至您先前建立的專案。</span><span class="sxs-lookup"><span data-stu-id="45b22-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="45b22-127">使用 [Clone]  按鈕來建立儲存機制的本機複本。</span><span class="sxs-lookup"><span data-stu-id="45b22-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="45b22-128">您也可以使用 [ZIP]  按鈕來下載專案。</span><span class="sxs-lookup"><span data-stu-id="45b22-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![A browser window viewing https://github.com/LearnBoost/socket.io/tree/master/examples/chat, with the ZIP download icon highlighted][chat-example-view]
2. <span data-ttu-id="45b22-130">瀏覽本機儲存機制的目錄結構，直到找到 **examples\\chat** 目錄為止。</span><span class="sxs-lookup"><span data-stu-id="45b22-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="45b22-131">將此目錄的內容複製到稍早建立的 **C:\\node\\chatapp\\WorkerRole1** 目錄。</span><span class="sxs-lookup"><span data-stu-id="45b22-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![總管，會顯示擷取自封存的 examples\\chat 目錄內容][chat-contents]
   
   <span data-ttu-id="45b22-133">上方螢幕擷取畫面中反白顯示的項目是從 **examples\\chat** 目錄複製的檔案</span><span class="sxs-lookup"><span data-stu-id="45b22-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="45b22-134">在 **C:\\node\\chatapp\\WorkerRole1** 目錄中，刪除 **server.js** 檔案，然後將 **app.js** 檔案重新命名為 **server.js**。</span><span class="sxs-lookup"><span data-stu-id="45b22-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="45b22-135">這樣會移除先前由 **Add-AzureNodeWorkerRole** Cmdlet 建立的預設 **server.js** 檔案，並取代為交談範例中的應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="45b22-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="45b22-136">修改 Server.js 和安裝模組</span><span class="sxs-lookup"><span data-stu-id="45b22-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="45b22-137">在 Azure 模擬器中測試應用程式之前，我們必須稍做一些修改。</span><span class="sxs-lookup"><span data-stu-id="45b22-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="45b22-138">請對 server.js 檔案執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="45b22-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="45b22-139">在 Visual Studio 或其他文字編輯器中開啟 **server.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="45b22-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="45b22-140">在 server.js 開頭找出 **Module dependencies** 區段，將含有 **sio = require('..//..//lib//socket.io')** 的那一行變更為 **sio = require('socket.io')**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b22-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="45b22-141">為了確保應用程式在正確的連接埠上接聽，請在 [記事本] 或您喜歡的編輯器中開啟 server.js，然後變更下列這一行，將 **3000** 改為 **process.env.port**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b22-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="45b22-142">儲存 **server.js**的變更之後，請使用下列步驟來安裝必要的模組，然後在 Azure 模擬器中測試應用程式：</span><span class="sxs-lookup"><span data-stu-id="45b22-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="45b22-143">使用 **Azure PowerShell**，切換至 **C:\\node\\chatapp\\WorkerRole1** 目錄，再使用下列命令來安裝此應用程式所需的模組：</span><span class="sxs-lookup"><span data-stu-id="45b22-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="45b22-144">這將會安裝 package.json 檔案中列出的模組。</span><span class="sxs-lookup"><span data-stu-id="45b22-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="45b22-145">命令完成之後，您應該會看到類似這樣的輸出：</span><span class="sxs-lookup"><span data-stu-id="45b22-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![The output of the npm install command][The-output-of-the-npm-install-command]
2. <span data-ttu-id="45b22-147">由於此範例原本為 Socket.IO GitHub 儲存機制的一部分，依相對路徑來直接參考 Socket.IO 程式庫，且 package.json 檔案中並沒有參考 Socket.IO，所以我們必須使用下列指令來安裝它：</span><span class="sxs-lookup"><span data-stu-id="45b22-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="45b22-148">測試和部署</span><span class="sxs-lookup"><span data-stu-id="45b22-148">Test and Deploy</span></span>
1. <span data-ttu-id="45b22-149">發出下列命令來啟動模擬器：</span><span class="sxs-lookup"><span data-stu-id="45b22-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="45b22-150">如果您在啟動模擬器時遇到問題，例如：Start-AzureEmulator：發生未預期的失敗。</span><span class="sxs-lookup"><span data-stu-id="45b22-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="45b22-151">詳細資料：發生未預期的錯誤。通訊物件 System.ServiceModel.Channels.ServiceChannel 無法用於通訊，因為它處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="45b22-151">Details: Encountered an unexpected error The communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in the Faulted state.</span></span>
   
      <span data-ttu-id="45b22-152">重新安裝 AzureAuthoringTools v 2.7.1 和 AzureComputeEmulator v 2.7 - 請確定版本相符。</span><span class="sxs-lookup"><span data-stu-id="45b22-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="45b22-153">開啟瀏覽器並瀏覽至 **http://127.0.0.1**。</span><span class="sxs-lookup"><span data-stu-id="45b22-153">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="45b22-154">當瀏覽器視窗開啟時，請輸入暱稱，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="45b22-154">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="45b22-155">這可讓您以特定的暱稱來張貼訊息。</span><span class="sxs-lookup"><span data-stu-id="45b22-155">This will allow you to post messages as a specific nickname.</span></span> <span data-ttu-id="45b22-156">若要測試多使用者功能，請使用相同 URL 開啟其他瀏覽器視窗，並輸入不同的暱稱。</span><span class="sxs-lookup"><span data-stu-id="45b22-156">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![兩個瀏覽器視窗顯示 User1 和 User2 的交談訊息](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="45b22-158">測試應用程式之後，發出下列命令來停止模擬器：</span><span class="sxs-lookup"><span data-stu-id="45b22-158">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="45b22-159">若要將應用程式部署至 Azure，請使用 **Publish-AzureServiceProject** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45b22-159">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="45b22-160">例如：</span><span class="sxs-lookup"><span data-stu-id="45b22-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="45b22-161">務必使用唯一的名稱，否則發行程序會失敗。</span><span class="sxs-lookup"><span data-stu-id="45b22-161">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="45b22-162">部署完成之後，瀏覽器會開啟並瀏覽至已部署的服務。</span><span class="sxs-lookup"><span data-stu-id="45b22-162">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="45b22-163">如果出現錯誤指出匯入的發行設定檔中沒有您所提供的訂用帳戶名稱，則在部署至 Azure 之前，您必須下載並匯入訂用帳戶的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="45b22-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="45b22-164">請參閱＜ **建立 Node.js 應用程式並部署至 Azure 雲端服務** ＞的＜ [將應用程式部署至 Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="45b22-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![A browser window displaying the service hosted on Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="45b22-166">如果出現錯誤指出匯入的發行設定檔中沒有您所提供的訂用帳戶名稱，則在部署至 Azure 之前，您必須下載並匯入訂用帳戶的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="45b22-166">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="45b22-167">請參閱＜ **建立 Node.js 應用程式並部署至 Azure 雲端服務** ＞的＜ [將應用程式部署至 Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="45b22-167">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="45b22-168">應用程式現在已在 Azure 上執行，且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。</span><span class="sxs-lookup"><span data-stu-id="45b22-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="45b22-169">為了簡化起見，此範例只能讓連線至相同執行個體的使用者聊天。</span><span class="sxs-lookup"><span data-stu-id="45b22-169">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="45b22-170">這表示如果雲端服務建立兩個背景工作角色執行個體，則使用者只能夠與連線至相同背景工作角色執行個體的其他使用者交談。</span><span class="sxs-lookup"><span data-stu-id="45b22-170">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="45b22-171">若要擴充應用程式來處理多個角色執行個體，您可以使用服務匯流排之類的技術，以便跨執行個體來共用 Socket.IO 儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="45b22-171">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="45b22-172">如需相關範例，請參閱＜ [Azure SDK for Node.js GitHub 儲存機制](https://github.com/WindowsAzure/azure-sdk-for-node)＞(英文) 中的服務匯流排佇列和主題使用範例。</span><span class="sxs-lookup"><span data-stu-id="45b22-172">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="45b22-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45b22-173">Next steps</span></span>
<span data-ttu-id="45b22-174">在本教學課程中，您學到如何建立裝載於 Azure 雲端服務的基本交談應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b22-174">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="45b22-175">若要了解如何在 Azure 網站中裝載此應用程式，請參閱[在 Azure 網站上使用 Socket.IO 建立 Node.js 交談應用程式][chatwebsite]。</span><span class="sxs-lookup"><span data-stu-id="45b22-175">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="45b22-176">如需詳細資訊，也請參閱 [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="45b22-176">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
<span data-ttu-id="45b22-177">[Socket.IO GitHub 儲存機制]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span><span class="sxs-lookup"><span data-stu-id="45b22-177">[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span></span>
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


