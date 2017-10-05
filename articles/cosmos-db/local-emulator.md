---
title: "使用 Azure Cosmos DB 模擬器在本機開發 | Microsoft Docs"
description: "您也可以免費使用 Azure Cosmos DB 模擬器在本機開發及測試應用程式，不需建立 Azure 訂用帳戶。"
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 模擬器"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="c670f-104">使用 Azure Cosmos DB 模擬器進行本機開發和測試</span><span class="sxs-lookup"><span data-stu-id="c670f-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="c670f-105"><strong>二進位檔</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="c670f-106">下載 MSI</span><span class="sxs-lookup"><span data-stu-id="c670f-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="c670f-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="c670f-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-109"><strong>Docker 來源</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="c670f-110">Github</span><span class="sxs-lookup"><span data-stu-id="c670f-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="c670f-111">Azure Cosmos DB 模擬器提供一個模擬 Azure Cosmos DB 服務的本機環境做為開發之用。</span><span class="sxs-lookup"><span data-stu-id="c670f-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="c670f-112">您可以使用 Azure Cosmos DB 模擬器在本機開發及測試應用程式，不需建立 Azure 訂用帳戶，也不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="c670f-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="c670f-113">如果您滿意應用程式在 Azure Cosmos DB 模擬器中的運作方式，就可以切換成使用雲端的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c670f-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="c670f-114">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="c670f-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c670f-115">安裝模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-115">Installing the Emulator</span></span>
> * <span data-ttu-id="c670f-116">在 Docker for Windows 上執行模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="c670f-117">驗證要求</span><span class="sxs-lookup"><span data-stu-id="c670f-117">Authenticating requests</span></span>
> * <span data-ttu-id="c670f-118">在模擬器中使用的資料總管</span><span class="sxs-lookup"><span data-stu-id="c670f-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="c670f-119">匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="c670f-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="c670f-120">從命令列呼叫模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="c670f-121">收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="c670f-121">Collecting trace files</span></span>

<span data-ttu-id="c670f-122">我們建議從觀看下列影片開始，其中 Kirill Gavrylyuk 示範如何開始使用 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="c670f-123">請注意，影片中將該模擬器稱為 DocumentDB 模擬器，但在錄製該影片之後，該工具本身已重新命名為 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="c670f-124">影片中的所有資訊對 Azure Cosmos DB 模擬器而言仍然正確。</span><span class="sxs-lookup"><span data-stu-id="c670f-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="c670f-125">模擬器的運作方式</span><span class="sxs-lookup"><span data-stu-id="c670f-125">How the Emulator works</span></span>
<span data-ttu-id="c670f-126">Azure Cosmos DB 模擬器提供 Azure Cosmos DB 服務的高逼真度模擬。</span><span class="sxs-lookup"><span data-stu-id="c670f-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="c670f-127">它支援與 Azure Cosmos DB 完全相同的功能，包括支援建立和查詢 JSON 文件、佈建和擴充集合，以及執行預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c670f-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="c670f-128">您可以使用 Azure Cosmos DB 模擬器來開發及測試應用程式，並且只需對 Azure Cosmos DB 的連接端點進行單一組態變更，就能將它們部署至全球規模的 Azure。</span><span class="sxs-lookup"><span data-stu-id="c670f-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="c670f-129">雖然我們已建立實際 Azure Cosmos DB 服務的高逼真度本機模擬，但是 Azure Cosmos DB 模擬器的實作是不同的服務。</span><span class="sxs-lookup"><span data-stu-id="c670f-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="c670f-130">例如，Azure Cosmos DB 模擬器會使用標準的作業系統元件，例如使用本機檔案系統以獲得持續性，以及使用 HTTPS 通訊協定堆疊進行連線。</span><span class="sxs-lookup"><span data-stu-id="c670f-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="c670f-131">這表示，依賴 Azure 基礎結構的某些功能，例如全域複寫、讀取/寫入的單一數字毫秒延遲，以及可調式的一致性層級等，都無法透過 Azure Cosmos DB 模擬器使用。</span><span class="sxs-lookup"><span data-stu-id="c670f-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="c670f-132">模擬器中的資料總管目前只支援建立 DocumentDB API 集合和 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="c670f-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="c670f-133">模擬器中的資料總管目前不支援建立資料表和圖表。</span><span class="sxs-lookup"><span data-stu-id="c670f-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="c670f-134">系統需求</span><span class="sxs-lookup"><span data-stu-id="c670f-134">System requirements</span></span>
<span data-ttu-id="c670f-135">Azure Cosmos DB 模擬器的硬體和軟體需求如下︰</span><span class="sxs-lookup"><span data-stu-id="c670f-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="c670f-136">軟體需求</span><span class="sxs-lookup"><span data-stu-id="c670f-136">Software requirements</span></span>
  * <span data-ttu-id="c670f-137">Windows Server 2012 R2、Windows Server 2016 或 Windows 10</span><span class="sxs-lookup"><span data-stu-id="c670f-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="c670f-138">最低硬體需求</span><span class="sxs-lookup"><span data-stu-id="c670f-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="c670f-139">2 GB RAM</span><span class="sxs-lookup"><span data-stu-id="c670f-139">2 GB RAM</span></span>
  * <span data-ttu-id="c670f-140">10 GB 可用硬碟空間</span><span class="sxs-lookup"><span data-stu-id="c670f-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="c670f-141">安裝</span><span class="sxs-lookup"><span data-stu-id="c670f-141">Installation</span></span>
<span data-ttu-id="c670f-142">您可以從 [Microsoft 下載中心](https://aka.ms/cosmosdb-emulator)下載並安裝 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="c670f-143">若要安裝、設定和執行 Azure Cosmos DB 模擬器，您必須具備電腦的系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="c670f-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="c670f-144">在 Docker for Windows 上執行</span><span class="sxs-lookup"><span data-stu-id="c670f-144">Running on Docker for Windows</span></span>

<span data-ttu-id="c670f-145">Azure Cosmos DB 模擬器可以在 Docker for Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="c670f-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="c670f-146">模擬器無法在 Docker for Oracle Linux 上運作。</span><span class="sxs-lookup"><span data-stu-id="c670f-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="c670f-147">安裝 [Docker for Windows](https://www.docker.com/docker-windows) 之後，您可以從最喜愛的殼層 (cmd.exe、PowerShell 等) 執行下列命令，以便從 Docker Hub 提取模擬器映像。</span><span class="sxs-lookup"><span data-stu-id="c670f-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="c670f-148">若要啟動映像，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="c670f-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="c670f-149">回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c670f-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="c670f-150">模擬器啟動之後，關閉互動式殼層將會關閉模擬器的容器。</span><span class="sxs-lookup"><span data-stu-id="c670f-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="c670f-151">在您的用戶端使用回應中的端點和主要金鑰，並將 SSL 憑證匯入您的主機。</span><span class="sxs-lookup"><span data-stu-id="c670f-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="c670f-152">若要匯入 SSL 憑證，請從系統管理員命令提示字元中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="c670f-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="c670f-153">啟動模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-153">Start the Emulator</span></span>

<span data-ttu-id="c670f-154">若要啟動 Azure Cosmos DB 模擬器，請選取 [開始] 按鈕或按下 Windows 鍵。</span><span class="sxs-lookup"><span data-stu-id="c670f-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="c670f-155">先輸入 **Azure Cosmos DB 模擬器**，再從應用程式清單選取模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![選取 [開始] 按鈕或按下 Windows 鍵，先輸入 **Azure Cosmos DB 模擬器**，再從應用程式清單選取模擬器](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="c670f-157">如果模擬器正在執行，您就會在 Windows 工作列通知區域看到圖示。</span><span class="sxs-lookup"><span data-stu-id="c670f-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure Cosmos DB 本機模擬器的工作列通知](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="c670f-159">Azure Cosmos DB 模擬器預設會在接聽連接埠 8081 的本機電腦 ("localhost") 上執行。</span><span class="sxs-lookup"><span data-stu-id="c670f-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="c670f-160">Azure Cosmos DB 模擬器預設會安裝到 `C:\Program Files\Azure Cosmos DB Emulator` 目錄。</span><span class="sxs-lookup"><span data-stu-id="c670f-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="c670f-161">您也可以從命令列啟動和停止模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="c670f-162">如需詳細資訊，請參閱[命令列工具參考](#command-line)。</span><span class="sxs-lookup"><span data-stu-id="c670f-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="c670f-163">啟動資料總管</span><span class="sxs-lookup"><span data-stu-id="c670f-163">Start Data Explorer</span></span>

<span data-ttu-id="c670f-164">當 Azure Cosmos DB 模擬器啟動時，會自動在瀏覽器中開啟 Azure Cosmos DB 資料總管。</span><span class="sxs-lookup"><span data-stu-id="c670f-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="c670f-165">地址會顯示為 [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c670f-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="c670f-166">如果您關閉資料總管，想要稍後重新開啟，可以在瀏覽器中開啟 URL 或從 Windows 系統匣圖示中的 Azure Cosmos DB 模擬器啟動，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c670f-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB 本機模擬器的資料總管啟動程式](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="c670f-168">檢查更新</span><span class="sxs-lookup"><span data-stu-id="c670f-168">Checking for updates</span></span>
<span data-ttu-id="c670f-169">資料總管會表示是否有新的更新可供下載。</span><span class="sxs-lookup"><span data-stu-id="c670f-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="c670f-170">在某個 Azure Cosmos DB 模擬器版本中建立的資料不保證可以使用不同的版本存取。</span><span class="sxs-lookup"><span data-stu-id="c670f-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="c670f-171">如果您需要長期保存資料，建議您將資料儲存於 Azure Cosmos DB 帳戶中，而不是 Azure Cosmos DB 模擬器中。</span><span class="sxs-lookup"><span data-stu-id="c670f-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="c670f-172">驗證要求</span><span class="sxs-lookup"><span data-stu-id="c670f-172">Authenticating requests</span></span>
<span data-ttu-id="c670f-173">就像雲端的 Azure Cosmos DB 一樣，您對 Azure Cosmos DB 模擬器的每個要求都必須經過驗證。</span><span class="sxs-lookup"><span data-stu-id="c670f-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="c670f-174">Azure Cosmos DB 模擬器支援主要金鑰驗證的單一固定帳戶及已知驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="c670f-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="c670f-175">此帳戶和金鑰都是唯一允許搭配 Azure Cosmos DB 模擬器使用的認證，</span><span class="sxs-lookup"><span data-stu-id="c670f-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="c670f-176">如下：</span><span class="sxs-lookup"><span data-stu-id="c670f-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="c670f-177">Azure Cosmos DB 模擬器所支援的主要金鑰僅能與模擬器搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c670f-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="c670f-178">您無法將生產用的 Azure Cosmos DB 帳戶和金鑰與 Azure Cosmos DB 模擬器搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c670f-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="c670f-179">如果您使用 /Key 選項啟動模擬器，則請使用產生的金鑰，而不要使用 "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="c670f-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="c670f-180">此外，就像 Azure Cosmos DB 服務一樣，Azure Cosmos DB 模擬器僅支援透過 SSL 的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="c670f-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="c670f-181">在本機網路上執行模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-181">Running the emulator on a local network</span></span>

<span data-ttu-id="c670f-182">您可以在本機網路上執行模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="c670f-183">若要啟用網路存取，請在[命令列](#command-line-syntax)指定 /AllowNetworkAccess 選項，也需要您指定 /Key=key_string 或 /KeyFile=file_name。</span><span class="sxs-lookup"><span data-stu-id="c670f-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="c670f-184">您可以使用 /GenKeyFile=file_name 來產生具有預先隨機金鑰的檔案。</span><span class="sxs-lookup"><span data-stu-id="c670f-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="c670f-185">然後您可以將其傳遞至 /KeyFile=file_name 或 /Key=contents_of_file。</span><span class="sxs-lookup"><span data-stu-id="c670f-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="c670f-186">若是第一次啟用網路存取，使用者應該關閉模擬器，並且刪除模擬器的資料目錄 (C:\Users\user_name\AppData\Local\CosmosDBEmulator)。</span><span class="sxs-lookup"><span data-stu-id="c670f-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="c670f-187">使用模擬器進行開發</span><span class="sxs-lookup"><span data-stu-id="c670f-187">Developing with the Emulator</span></span>
<span data-ttu-id="c670f-188">在桌面上執行 Azure Cosmos DB 模擬器之後，就可以使用任何支援的 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 或 [Azure Cosmos DB REST API](/rest/api/documentdb/) 與模擬器互動。</span><span class="sxs-lookup"><span data-stu-id="c670f-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="c670f-189">Azure Cosmos DB 模擬器也包含內建的資料總管，可讓您建立 DocumentDB 和 MongoDB API 集合、檢視及編輯文件，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="c670f-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="c670f-190">如果您使用 [MongoDB 的 Azure Cosmos DB 通訊協定支援](mongodb-introduction.md)，請使用下列連接字串︰</span><span class="sxs-lookup"><span data-stu-id="c670f-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="c670f-191">您可以使用現有的工具，像是 [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) 連線到 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="c670f-192">您也可以使用 [Azure Cosmos DB 資料移轉工具](https://github.com/azure/azure-documentdb-datamigrationtool)在 Azure Cosmos DB 模擬器與 Azure Cosmos DB 服務之間移轉資料。</span><span class="sxs-lookup"><span data-stu-id="c670f-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="c670f-193">如果您使用 /Key 選項啟動模擬器，則請使用產生的金鑰，而不要使用 "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="c670f-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="c670f-194">使用 Azure Cosmos DB 模擬器，根據預設您可以建立最多 25 個單一分割區集合，或 1 個已分割集合。</span><span class="sxs-lookup"><span data-stu-id="c670f-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="c670f-195">如需變更此值的詳細資訊，請參閱[設定 PartitionCount 值](#set-partitioncount)。</span><span class="sxs-lookup"><span data-stu-id="c670f-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="c670f-196">匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="c670f-196">Export the SSL certificate</span></span>

<span data-ttu-id="c670f-197">.NET 語言和執行階段使用 Windows 憑證存放區來安全地連線到 Azure Cosmos DB 本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="c670f-198">其他語言則有自己管理和使用憑證的方法。</span><span class="sxs-lookup"><span data-stu-id="c670f-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="c670f-199">Java 使用自己的[憑證存放區](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)，而 Python 使用[通訊端包裝函式](https://docs.python.org/2/library/ssl.html)。</span><span class="sxs-lookup"><span data-stu-id="c670f-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="c670f-200">若要取得憑證來搭配未整合 Windows 憑證存放區的語言和執行階段使用，您必須使用 Windows 憑證管理員將它匯出。</span><span class="sxs-lookup"><span data-stu-id="c670f-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="c670f-201">您可以執行 certlm.msc 或依照[匯出 Azure Cosmos DB 模擬器憑證](./local-emulator-export-ssl-certificates.md)中的逐步指示開始。</span><span class="sxs-lookup"><span data-stu-id="c670f-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="c670f-202">憑證管理員執行之後時，開啟 [個人憑證] \(如下所示)，並將有 "DocumentDBEmulatorCertificate" 易記名稱的憑證匯出為 BASE-64 編碼的 X.509 (.cer) 檔案。</span><span class="sxs-lookup"><span data-stu-id="c670f-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB 本機模擬器的 SSL 憑證](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="c670f-204">遵循[新增憑證至 Java CA 憑證存放區](https://docs.microsoft.com/azure/java-add-certificate-ca-store)中的指示，X.509 憑證就可以匯入 Java 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="c670f-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="c670f-205">將憑證匯入憑證存放區之後，Java 和 MongoDB 應用程式就可以連線到 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="c670f-206">從 Python 和 Node.js SDK 連接到模擬器時，會停用 SSL 驗證。</span><span class="sxs-lookup"><span data-stu-id="c670f-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="c670f-207"><a id="command-line"></a>命令列工具參考</span><span class="sxs-lookup"><span data-stu-id="c670f-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="c670f-208">您可以從安裝位置使用命令列來啟動和停止模擬器、設定選項，以及執行其他作業。</span><span class="sxs-lookup"><span data-stu-id="c670f-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="c670f-209">命令列語法</span><span class="sxs-lookup"><span data-stu-id="c670f-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="c670f-210">若要檢視選項清單，請在命令提示字元輸入 `CosmosDB.Emulator.exe /?` 。</span><span class="sxs-lookup"><span data-stu-id="c670f-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="c670f-211"><strong>選項</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="c670f-212"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="c670f-213"><strong>命令</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="c670f-214"><strong>引數</strong></span><span class="sxs-lookup"><span data-stu-id="c670f-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-215">[無引數]</span><span class="sxs-lookup"><span data-stu-id="c670f-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="c670f-216">使用預設設定啟動 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="c670f-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="c670f-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-218">[說明]</span><span class="sxs-lookup"><span data-stu-id="c670f-218">[Help]</span></span></td>
  <td><span data-ttu-id="c670f-219">顯示支援的命令列引數清單。</span><span class="sxs-lookup"><span data-stu-id="c670f-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="c670f-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="c670f-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="c670f-221">Shutdown</span></span></td>
  <td><span data-ttu-id="c670f-222">關閉 Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="c670f-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="c670f-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="c670f-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-224">資料路徑</span><span class="sxs-lookup"><span data-stu-id="c670f-224">DataPath</span></span></td>
  <td><span data-ttu-id="c670f-225">指定用來儲存資料檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c670f-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="c670f-226">預設值為 %LocalAppdata%\CosmosDBEmulator。</span><span class="sxs-lookup"><span data-stu-id="c670f-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="c670f-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="c670f-228">&lt;datapath&gt;︰可存取的路徑</span><span class="sxs-lookup"><span data-stu-id="c670f-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-229">Port</span><span class="sxs-lookup"><span data-stu-id="c670f-229">Port</span></span></td>
  <td><span data-ttu-id="c670f-230">指定用於模擬器的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="c670f-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="c670f-231">預設值為 8081。</span><span class="sxs-lookup"><span data-stu-id="c670f-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="c670f-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="c670f-233">&lt;port&gt;︰單一連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="c670f-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="c670f-234">MongoPort</span></span></td>
  <td><span data-ttu-id="c670f-235">指定要用於 MongoDB 相容性 API 的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="c670f-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="c670f-236">預設值為 10255。</span><span class="sxs-lookup"><span data-stu-id="c670f-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="c670f-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="c670f-238">&lt;mongoport&gt;︰單一連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="c670f-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="c670f-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="c670f-240">指定要用於直接連線的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c670f-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="c670f-241">預設值為 10251、10252、10253、10254。</span><span class="sxs-lookup"><span data-stu-id="c670f-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="c670f-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="c670f-243">&lt;directports&gt;︰以逗號分隔的 4 個連接埠清單</span><span class="sxs-lookup"><span data-stu-id="c670f-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-244">Key</span><span class="sxs-lookup"><span data-stu-id="c670f-244">Key</span></span></td>
  <td><span data-ttu-id="c670f-245">模擬器的授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="c670f-245">Authorization key for the emulator.</span></span> <span data-ttu-id="c670f-246">金鑰必須是 64 位元組向量的 base-64 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="c670f-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="c670f-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="c670f-248">&lt;key&gt;：金鑰必須是 64 位元組向量的 base-64 編碼方式</span><span class="sxs-lookup"><span data-stu-id="c670f-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="c670f-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="c670f-250">指定要啟用要求率限制行為。</span><span class="sxs-lookup"><span data-stu-id="c670f-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="c670f-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="c670f-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="c670f-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="c670f-253">指定要停用要求率限制行為。</span><span class="sxs-lookup"><span data-stu-id="c670f-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="c670f-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="c670f-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="c670f-255">NoUI</span></span></td>
  <td><span data-ttu-id="c670f-256">不要顯示模擬器使用者介面。</span><span class="sxs-lookup"><span data-stu-id="c670f-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="c670f-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="c670f-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="c670f-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="c670f-259">啟動時不要顯示文件總管。</span><span class="sxs-lookup"><span data-stu-id="c670f-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="c670f-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="c670f-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="c670f-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="c670f-262">指定已分割集合的數目上限。</span><span class="sxs-lookup"><span data-stu-id="c670f-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="c670f-263">如需詳細資訊，請參閱[變更集合的數目](#set-partitioncount)。</span><span class="sxs-lookup"><span data-stu-id="c670f-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="c670f-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="c670f-265">&lt;partitioncount&gt;：允許的單一分割區集合數目上限。</span><span class="sxs-lookup"><span data-stu-id="c670f-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="c670f-266">預設值為 25。</span><span class="sxs-lookup"><span data-stu-id="c670f-266">Default is 25.</span></span> <span data-ttu-id="c670f-267">允許的上限為 250。</span><span class="sxs-lookup"><span data-stu-id="c670f-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="c670f-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="c670f-269">指定分割集合之分割數目的預設值。</span><span class="sxs-lookup"><span data-stu-id="c670f-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="c670f-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="c670f-271">&lt;defaultpartitioncount&gt; 預設值為 25。</span><span class="sxs-lookup"><span data-stu-id="c670f-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="c670f-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="c670f-273">讓模擬器可以透過網路存取。</span><span class="sxs-lookup"><span data-stu-id="c670f-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="c670f-274">您也必須傳遞 /Key=&lt;key_string&gt; 或 /KeyFile=&lt;file_name&gt; 以啟用網路存取。</span><span class="sxs-lookup"><span data-stu-id="c670f-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="c670f-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="c670f-276">或</span><span class="sxs-lookup"><span data-stu-id="c670f-276">or</span></span><br><br><span data-ttu-id="c670f-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="c670f-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="c670f-279">當 /AllowNetworkAccess 在使用中時請勿調整防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="c670f-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="c670f-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="c670f-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="c670f-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="c670f-282">產生新的授權金鑰並儲存到指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="c670f-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="c670f-283">產生的金鑰可以搭配 /Key 或 /KeyFile 選項使用。</span><span class="sxs-lookup"><span data-stu-id="c670f-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="c670f-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;金鑰檔案路徑&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-285">一致性</span><span class="sxs-lookup"><span data-stu-id="c670f-285">Consistency</span></span></td>
  <td><span data-ttu-id="c670f-286">設定帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="c670f-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="c670f-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="c670f-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="c670f-288">&lt;一致性&gt;：值必須是下列[一致性層級](consistency-levels.md)其中之一：Session、Strong、Eventual 或 BoundedStaleness。</span><span class="sxs-lookup"><span data-stu-id="c670f-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="c670f-289">預設值為 Session。</span><span class="sxs-lookup"><span data-stu-id="c670f-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c670f-290">?</span><span class="sxs-lookup"><span data-stu-id="c670f-290">?</span></span></td>
  <td><span data-ttu-id="c670f-291">顯示說明訊息。</span><span class="sxs-lookup"><span data-stu-id="c670f-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="c670f-292">Azure Cosmos DB 模擬器和 Azure Cosmos DB 之間的差異</span><span class="sxs-lookup"><span data-stu-id="c670f-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="c670f-293">因為 Azure Cosmos DB 模擬器是在本機開發人員工作站上提供一個執行的模擬環境，所以模擬器和雲端 Azure Cosmos DB 帳戶之間會有一些功能上的差異：</span><span class="sxs-lookup"><span data-stu-id="c670f-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="c670f-294">Azure Cosmos DB 模擬器僅支援單一固定帳戶及已知的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="c670f-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="c670f-295">在 Azure Cosmos DB 模擬器中無法重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="c670f-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="c670f-296">Azure Cosmos DB 模擬器服務無法擴充，也不支援大量集合。</span><span class="sxs-lookup"><span data-stu-id="c670f-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="c670f-297">Azure Cosmos DB 模擬器不會模擬不同的 [Azure Cosmos DB 一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="c670f-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="c670f-298">Azure Cosmos DB 模擬器不會模擬[多重區域複寫](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="c670f-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="c670f-299">Azure Cosmos DB 模擬器不支援 Azure Cosmos DB 服務中可用的服務配額覆寫 (例如文件大小限制、增加的分割集合儲存體)。</span><span class="sxs-lookup"><span data-stu-id="c670f-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="c670f-300">因為 Azure Cosmos DB 服務最近有變更，Azure Cosmos DB 模擬器複本可能不是最新狀態，請使用 [Azure Cosmos DB 容量規劃工具](https://www.documentdb.com/capacityplanner)，準確地評估應用程式的生產輸送量 (RU) 需求。</span><span class="sxs-lookup"><span data-stu-id="c670f-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="c670f-301"><a id="set-partitioncount"></a>變更集合的數目</span><span class="sxs-lookup"><span data-stu-id="c670f-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="c670f-302">根據預設，您可以使用 Azure Cosmos DB 模擬器建立最多 25 個單一分割區集合，或 1 個已分割集合。</span><span class="sxs-lookup"><span data-stu-id="c670f-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="c670f-303">藉由修改 **PartitionCount** 值，您可以建立最多 250 個單一分割區集合或是 10 個已分割的集合，或是這兩種的任何組合 (不超過 250 個單一分割區，其中 1 個已分割集合 = 25 個單一分割區集合)。</span><span class="sxs-lookup"><span data-stu-id="c670f-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="c670f-304">如果您在目前的分割計數超過限制後嘗試建立集合，模擬器會擲回 ServiceUnavailable 例外狀況，並隨附下列訊息。</span><span class="sxs-lookup"><span data-stu-id="c670f-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="c670f-305">若要變更 Azure Cosmos DB 模擬器可用的集合數目，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c670f-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="c670f-306">刪除所有的本機 Azure Cosmos DB 模擬器資料，方法是以滑鼠右鍵按一下系統匣上的 [Azure Cosmos DB 模擬器] 圖示，然後按一下 [重設資料...]。</span><span class="sxs-lookup"><span data-stu-id="c670f-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="c670f-307">刪除以下資料夾中所有的模擬器資料：C:\Users\user_name\AppData\Local\CosmosDBEmulator。</span><span class="sxs-lookup"><span data-stu-id="c670f-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="c670f-308">結束所有開啟的執行個體，方法是以滑鼠右鍵按一下系統匣上的 [Azure Cosmos DB 模擬器] 圖示，然後按一下 [結束]。</span><span class="sxs-lookup"><span data-stu-id="c670f-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="c670f-309">結束所有執行個體可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c670f-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="c670f-310">安裝最新版的 [Azure Cosmos DB Emulator 模擬器](https://aka.ms/cosmosdb-emulator)。</span><span class="sxs-lookup"><span data-stu-id="c670f-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="c670f-311">啟動具有 PartitionCount 旗標的模擬器，方法是設定值 <= 250。</span><span class="sxs-lookup"><span data-stu-id="c670f-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="c670f-312">例如， `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`。</span><span class="sxs-lookup"><span data-stu-id="c670f-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c670f-313">疑難排解</span><span class="sxs-lookup"><span data-stu-id="c670f-313">Troubleshooting</span></span>

<span data-ttu-id="c670f-314">使用下列秘訣可協助您對使用 Azure Cosmos DB 模擬器時遇到的問題進行疑難排解︰</span><span class="sxs-lookup"><span data-stu-id="c670f-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="c670f-315">如果您已安裝新版本的模擬器並發生錯誤，請確定重設您的資料。</span><span class="sxs-lookup"><span data-stu-id="c670f-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="c670f-316">您可以在系統匣上的 [Azure Cosmos DB 模擬器] 圖示上按一下滑鼠右鍵，然後按一下 [重設資料...]，以重設資料。</span><span class="sxs-lookup"><span data-stu-id="c670f-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="c670f-317">如果無法修正錯誤，您可以解除安裝，然後重新安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="c670f-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="c670f-318">如需相關指示，請參閱[解除安裝本機模擬器](#uninstall)。</span><span class="sxs-lookup"><span data-stu-id="c670f-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="c670f-319">如果 Azure Cosmos DB 模擬器當機，請從 c:\Users\user_name\AppData\Local\CrashDumps 資料夾中收集傾印檔案，壓縮檔案後，再附加到電子郵件寄至 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c670f-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="c670f-320">如果 CosmosDB.StartupEntryPoint.exe 發生損毀，請從系統管理員命令提示字元執行下列命令︰`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="c670f-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="c670f-321">如果您遇到連線問題，請[收集追蹤檔案](#trace-files)，壓縮檔案後，再附加到電子郵件寄至[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c670f-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="c670f-322">如果您收到**服務無法使用**訊息，模擬器可能無法初始化網路堆疊。</span><span class="sxs-lookup"><span data-stu-id="c670f-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="c670f-323">由於 Pulse 安全用戶端或 Juniper 網路用戶端的網路篩選驅動程式可能會造成問題，因此請檢查是否已安裝這些驅動程式。</span><span class="sxs-lookup"><span data-stu-id="c670f-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="c670f-324">解除安裝協力廠商網路篩選驅動程式通常便會修正問題。</span><span class="sxs-lookup"><span data-stu-id="c670f-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="c670f-325"><a id="trace-files"></a>收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="c670f-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="c670f-326">若要收集偵錯追蹤，請從系統管理命令提示字元執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="c670f-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="c670f-327">`CosmosDB.Emulator.exe /shutdown`。</span><span class="sxs-lookup"><span data-stu-id="c670f-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="c670f-328">監看系統匣，確認程式已經關閉，這可能需要一分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c670f-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="c670f-329">您也可以在 Azure Cosmos DB 模擬器使用者介面中，按一下 [結束]。</span><span class="sxs-lookup"><span data-stu-id="c670f-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="c670f-330">重現問題。</span><span class="sxs-lookup"><span data-stu-id="c670f-330">Reproduce the problem.</span></span> <span data-ttu-id="c670f-331">如果資料總管無法運作，您只需要等候數秒鐘的時間，等到瀏覽器開啟即可攔截錯誤。</span><span class="sxs-lookup"><span data-stu-id="c670f-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="c670f-332">瀏覽至 `%ProgramFiles%\Azure Cosmos DB Emulator` 並尋找 docdbemulator_000001.etl 檔案。</span><span class="sxs-lookup"><span data-stu-id="c670f-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="c670f-333">將 .etl 檔案以及重現步驟傳送至 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) 進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="c670f-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="c670f-334"><a id="uninstall"></a>解除安裝本機模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="c670f-335">結束本機模擬器之所有開啟的執行個體，方法是以滑鼠右鍵按一下系統匣上的 [Azure Cosmos DB 模擬器] 圖示，然後按一下 [結束]。</span><span class="sxs-lookup"><span data-stu-id="c670f-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="c670f-336">結束所有執行個體可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c670f-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="c670f-337">在 Windows 搜尋方塊中，輸入 **App 與功能**，然後按一下 [App 與功能 (系統設定)] 結果。</span><span class="sxs-lookup"><span data-stu-id="c670f-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="c670f-338">在應用程式清單中，捲動至 [Azure Cosmos DB 模擬器] 並將其選取，按一下 [解除安裝]，然後確認並再按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="c670f-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="c670f-339">解除安裝應用程式時，瀏覽至 C:\Users\<user>\AppData\Local\CosmosDBEmulator，然後刪除資料夾。</span><span class="sxs-lookup"><span data-stu-id="c670f-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c670f-340">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c670f-340">Next steps</span></span>

<span data-ttu-id="c670f-341">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="c670f-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c670f-342">已安裝本機模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="c670f-343">已在 Docker for Windows 上執行模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="c670f-344">已驗證要求</span><span class="sxs-lookup"><span data-stu-id="c670f-344">Authenticated requests</span></span>
> * <span data-ttu-id="c670f-345">已在模擬器中使用資料總管</span><span class="sxs-lookup"><span data-stu-id="c670f-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="c670f-346">已匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="c670f-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="c670f-347">已從命令列呼叫模擬器</span><span class="sxs-lookup"><span data-stu-id="c670f-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="c670f-348">已收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="c670f-348">Collected trace files</span></span>

<span data-ttu-id="c670f-349">在本教學課程中，您學習到如何使用免費的本機模擬器在本機開發。</span><span class="sxs-lookup"><span data-stu-id="c670f-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="c670f-350">現在您可以繼續進行下一個教學課程，了解如何匯出模擬器 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="c670f-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c670f-351">匯出 Azure Cosmos DB 模擬器憑證</span><span class="sxs-lookup"><span data-stu-id="c670f-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
