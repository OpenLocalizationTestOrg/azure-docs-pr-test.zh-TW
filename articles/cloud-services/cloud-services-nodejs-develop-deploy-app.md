---
title: "aaaNode.js 入門指南 |Microsoft 文件"
description: "了解如何 toocreate 簡單 Node.js web 應用程式，並將其部署 tooan Azure 雲端服務。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>建置和部署 Node.js 應用程式 tooan Azure 雲端服務

本教學課程示範如何 toocreate 簡單 Node.js 的 Azure 雲端服務中執行的應用程式。 雲端服務是可擴充的雲端應用程式在 Azure 中的 hello 建置組塊。 它們允許 hello 分開獨立管理和向外延展應用程式的前端和後端元件。  雲端服務提供穩定代管各個角色的強固專用虛擬機器。

如需有關雲端服務和如何比較 tooAzure 網站和虛擬機器的詳細資訊，請參閱[Azure 網站、 雲端服務和虛擬機器的比較]。

> [!TIP]
> 要尋找 toobuild 簡單網站嗎？ 如果您只需要簡單的網站前端，請考慮[使用輕量型 Web 應用程式]。 當您 web 應用程式成長並變更您的需求，您可以輕鬆地升級 tooa 雲端服務。

按照本教學課程進行，您將建立在 Web 角色內代管的簡單 Web 應用程式。 您將會在本機上，使用 hello 計算模擬器 tootest 您的應用程式，然後部署使用 PowerShell 命令列工具。

hello 應用程式是一個簡單的"hello world"應用程式：

![網頁瀏覽器顯示 hello Hello World 網頁][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>必要條件
> [!NOTE]
> 本教學課程使用 Azure PowerShell (需要 Windows)。

* 安裝並設定 [Azure PowerShell]。
* 下載並安裝 hello [Azure SDK for.NET 2.7]。 在 hello 安裝安裝程式中，選取：
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>建立 Azure 雲端服務專案
執行下列工作 toocreate 新的 Azure 雲端服務專案，以及基本 Node.js scaffolding hello:

1. 執行**Windows PowerShell**以系統管理員身分; 從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。
2. [連接 PowerShell] tooyour 訂用帳戶。
3. 輸入下列 PowerShell cmdlet toocreate toocreate hello 專案 hello:

        New-AzureServiceProject helloworld

    ![hello hello 新 AzureService helloworld 命令結果][hello result of hello New-AzureService helloworld command]

    hello**新增 AzureServiceProject** cmdlet 會產生用於發佈 Node.js 應用程式 tooa 雲端服務的基本結構。 它包含發行 tooAzure 所需的設定檔。 hello cmdlet 也會變更您的工作目錄 toohello 目錄 hello 服務。

    hello cmdlet 會建立下列檔案的 hello:

   * **ServiceConfiguration.Cloud.cscfg**、**ServiceConfiguration.Local.cscfg** 和 **ServiceDefinition.csdef**：是發佈應用程式時需使用的 Azure 特定檔案。 如需詳細資訊，請參閱 [雲端服務]。
   * **deploymentSettings.json**： 儲存 hello Azure PowerShell 部署 cmdlet 所使用的本機設定。
4. 輸入下列命令 tooadd 新的 web 角色的 hello:

       Add-AzureNodeWebRole

   ![hello 新增 AzureNodeWebRole 命令 hello 輸出][hello output of hello Add-AzureNodeWebRole command]

   hello**新增 AzureNodeWebRole** cmdlet 會建立基本的 Node.js 應用程式。 它也會修改 hello **.csfg**和**.csdef**檔案 tooadd hello 新角色的組態項目。

   > [!NOTE]
   > 如果您未指定角色名稱，系統會使用預設名稱。 您可以提供名稱做為第一個指令程式參數 hello:`Add-AzureNodeWebRole MyRole`

hello 檔案中定義 hello Node.js 應用程式**立即轉譯 server.js**hello web 角色的 hello 目錄中 (**WebRole1**依預設)。 Hello 程式碼如下：

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

此程式碼為基本上相同 hello"Hello World"範例 hello 的 hello [nodejs.org]網站，但它會使用指派的 hello 雲端環境的 hello 連接埠號碼。

## <a name="deploy-hello-application-tooazure"></a>部署 hello 應用程式 tooAzure

> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 您可以[啟用自己的 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)或是[註冊免費帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)。

### <a name="download-hello-azure-publishing-settings"></a>下載 hello Azure 發行設定
toodeploy 您的應用程式 tooAzure，您必須先下載 hello 發行您的 Azure 訂用帳戶的設定。

1. 執行下列 Azure PowerShell cmdlet 的 hello:

       Get-AzurePublishSettingsFile

   此選項會使用您的瀏覽器 toonavigate toohello 發佈設定 下載頁面。 您可以使用 Microsoft 帳戶的提示的 toolog。 如果是，使用與您 Azure 訂用帳戶相關聯的 hello 帳戶。

   儲存下載的 hello 設定檔 tooa 檔案位置可以輕易地存取。
2. 執行下列 cmdlet tooimport hello 發行您所下載的設定檔：

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > 匯入 hello 後發行設定，請考慮刪除 hello 下載.publishSettings 檔案，因為它包含資訊，可能會允許其他人 tooaccess 您的帳戶。

### <a name="publish-hello-application"></a>發行 hello 應用程式
toopublish，執行下列命令的 hello:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName**指定 hello 部署的 hello 名稱。 這必須是唯一的名稱，否則 hello 發佈程序將會失敗。 hello **Get-date**命令 tacks 應該讓 hello 名稱唯一日期/時間字串。
* **位置**指定將裝載 hello 應用程式中的 hello 資料中心。 一份可用的資料中心，使用 hello toosee **Get AzureLocation** cmdlet。
* **-啟動**開啟瀏覽器視窗，並完成部署之後，請瀏覽 toohello 裝載服務。

發行成功之後，您會看到類似 toohello 後的回應：

![hello Publish-azureservice 命令 hello 輸出][hello output of hello Publish-AzureService command]

> [!NOTE]
> 它可以使用 hello 應用程式 toodeploy 幾分鐘的時間，並變成可用時第一次發行。

Hello 部署完成後，請在瀏覽器視窗會開啟，並瀏覽 toohello 雲端服務。

![瀏覽器視窗，以顯示 hello hello world 網頁。hello URL 表示 hello 頁面裝載於 Azure。][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

您的應用程式現在成功在 Azure 上執行了！

hello**發行 AzureServiceProject** cmdlet 會執行下列步驟的 hello:

1. 建立封裝 toodeploy。 hello 套件包含所有應用程式資料夾中的 hello 檔案。
2. 建立新的 **儲存體帳戶** (如果不存在)。 hello Azure 儲存體帳戶是使用的 toostore hello 應用程式封裝，部署期間。 完成部署之後，您可以放心刪除 hello 儲存體帳戶。
3. 建立新的 **雲端服務** (如果不存在)。 A**雲端服務**是在其中裝載應用程式時，它已部署的 tooAzure hello 容器。 如需詳細資訊，請參閱 [雲端服務]。
4. 發行 hello 部署封裝 tooAzure。

## <a name="stopping-and-deleting-your-application"></a>停止並刪除您的應用程式
部署後您的應用程式，您可能會想 toodisable 它如此您就不必付出的額外成本。 Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。 使用伺服器時間為您的應用程式部署之後，即使 hello 執行個體未執行而且處於 hello 停止狀態。

1. 在 hello Windows PowerShell 視窗中，停止以 hello 下列 cmdlet 建立 hello 前一節中的 hello 服務部署：

       Stop-AzureService

   停止 hello 服務可能需要幾分鐘的時間。 Hello 服務停止時，您會收到訊息，指出 已停止。

   ![hello hello 停止 AzureService 命令狀態][hello status of hello Stop-AzureService command]
2. 下列指令程式呼叫 hello toodelete hello 服務：

       Remove-AzureService

   出現提示時，輸入**Y** toodelete hello 服務。

   刪除 hello 服務可能需要幾分鐘的時間。 刪除 hello 服務之後您會收到指出 hello 服務已刪除的訊息。

   ![hello hello 移除 AzureService 命令狀態][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > 正在刪除 hello 服務不會刪除 hello hello 服務最初發行時所建立的儲存體帳戶，您仍須繼續支付儲存體使用 toobe。 如果沒有其他使用 hello 儲存體，您可能想 toodelete 它。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [Node.js 開發人員中心]。

<!-- URL List -->

[Azure 網站、 雲端服務和虛擬機器的比較]: ../app-service-web/choose-web-site-cloud-service-vm.md
[使用輕量型 Web 應用程式]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK for.NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[連接 PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[雲端服務]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js 開發人員中心]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
