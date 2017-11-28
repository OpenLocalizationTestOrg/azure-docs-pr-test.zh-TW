---
title: "在本機以 hello Azure Cosmos DB 模擬器 aaaDevelop |Microsoft 文件"
description: "使用 hello Azure Cosmos DB 模擬器，您可以開發及測試您的應用程式在本機，而不需要建立 Azure 訂用帳戶。"
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
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="4a681-104">使用本機開發及測試 hello Azure Cosmos DB 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="4a681-105"><strong>二進位檔</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="4a681-106">下載 MSI</span><span class="sxs-lookup"><span data-stu-id="4a681-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="4a681-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="4a681-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-109"><strong>Docker 來源</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="4a681-110">Github</span><span class="sxs-lookup"><span data-stu-id="4a681-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="4a681-111">hello Azure Cosmos DB 模擬器提供模擬 hello Azure Cosmos 資料庫服務，供開發應用程式的本機環境。</span><span class="sxs-lookup"><span data-stu-id="4a681-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="4a681-112">使用 hello Azure Cosmos DB 模擬器，您可以開發及測試應用程式在本機，而不需要建立 Azure 訂用帳戶，或支付任何費用。</span><span class="sxs-lookup"><span data-stu-id="4a681-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="4a681-113">當您滿意 hello Azure Cosmos DB 模擬器中您的應用程式運作時，您可以切換 toousing hello 雲端中的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a681-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="4a681-114">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a681-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4a681-115">安裝模擬器 hello</span><span class="sxs-lookup"><span data-stu-id="4a681-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="4a681-116">Docker for Windows 上執行 hello 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="4a681-117">驗證要求</span><span class="sxs-lookup"><span data-stu-id="4a681-117">Authenticating requests</span></span>
> * <span data-ttu-id="4a681-118">使用 hello 模擬器中的 hello 資料總管</span><span class="sxs-lookup"><span data-stu-id="4a681-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="4a681-119">匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="4a681-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="4a681-120">從 hello 命令列呼叫 hello 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="4a681-121">收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="4a681-121">Collecting trace files</span></span>

<span data-ttu-id="4a681-122">我們建議您藉由監看下列影片 Kirill Gavrylyuk 顯示以 hello Azure Cosmos DB 模擬器 tooget 的啟動方式 hello 開始使用。</span><span class="sxs-lookup"><span data-stu-id="4a681-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="4a681-123">請注意，hello 視訊參照 toohello 模擬器做 hello DocumentDB 模擬器中，但 hello 工具本身已重新命名後點選 hello 視訊 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="4a681-124">Hello 視訊中的所有資訊都都仍正確 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="4a681-125">Hello 模擬器的運作方式</span><span class="sxs-lookup"><span data-stu-id="4a681-125">How hello Emulator works</span></span>
<span data-ttu-id="4a681-126">hello Azure Cosmos DB 模擬器提供高逼真度的模擬 hello Azure Cosmos 資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="4a681-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="4a681-127">它支援與 Azure Cosmos DB 完全相同的功能，包括支援建立和查詢 JSON 文件、佈建和擴充集合，以及執行預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="4a681-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="4a681-128">您可以開發和測試應用程式使用 hello Azure Cosmos DB 模擬器，及藉由只變更 Azure Cosmos DB toohello 連接端點的單一組態部署全域大規模 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4a681-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="4a681-129">當我們建立 hello 實際 Azure Cosmos DB 服務的高逼真度本機模擬時，hello Azure Cosmos DB 模擬器 hello 實作以不同於所 hello 服務時。</span><span class="sxs-lookup"><span data-stu-id="4a681-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="4a681-130">比方說，hello Azure Cosmos DB 模擬器會使用標準的作業系統元件，例如 hello 本機檔案系統的持續性和連線的 HTTPS 通訊協定堆疊。</span><span class="sxs-lookup"><span data-stu-id="4a681-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="4a681-131">這表示，某些功能依賴 Azure 基礎結構，例如全域複寫，讀取/寫入，以及可微調的一致性層級的單一位數毫秒延遲，無法透過 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="4a681-132">在此時間 hello 資料總管在 hello 模擬器只支援 hello 建立 DocumentDB API 集合和 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="4a681-133">hello 模擬器中的 hello 資料總管目前不支援 hello 建立資料表和圖形。</span><span class="sxs-lookup"><span data-stu-id="4a681-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="4a681-134">系統需求</span><span class="sxs-lookup"><span data-stu-id="4a681-134">System requirements</span></span>
<span data-ttu-id="4a681-135">hello Azure Cosmos DB 模擬器有下列硬體和軟體需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a681-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="4a681-136">軟體需求</span><span class="sxs-lookup"><span data-stu-id="4a681-136">Software requirements</span></span>
  * <span data-ttu-id="4a681-137">Windows Server 2012 R2、Windows Server 2016 或 Windows 10</span><span class="sxs-lookup"><span data-stu-id="4a681-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="4a681-138">最低硬體需求</span><span class="sxs-lookup"><span data-stu-id="4a681-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="4a681-139">2 GB RAM</span><span class="sxs-lookup"><span data-stu-id="4a681-139">2 GB RAM</span></span>
  * <span data-ttu-id="4a681-140">10 GB 可用硬碟空間</span><span class="sxs-lookup"><span data-stu-id="4a681-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="4a681-141">安裝</span><span class="sxs-lookup"><span data-stu-id="4a681-141">Installation</span></span>
<span data-ttu-id="4a681-142">您可以從下載並安裝 hello Azure Cosmos DB 模擬器 hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator)。</span><span class="sxs-lookup"><span data-stu-id="4a681-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="4a681-143">tooinstall，設定和執行 hello Azure Cosmos DB 模擬器，您必須擁有系統管理權限 hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="4a681-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="4a681-144">在 Docker for Windows 上執行</span><span class="sxs-lookup"><span data-stu-id="4a681-144">Running on Docker for Windows</span></span>

<span data-ttu-id="4a681-145">可以執行 Docker for Windows hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="4a681-146">hello 模擬器無法在上 Docker for Oracle Linux。</span><span class="sxs-lookup"><span data-stu-id="4a681-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="4a681-147">一旦[Docker for Windows](https://www.docker.com/docker-windows)安裝，您可以拉 hello 模擬器映像從 Docker Hub 藉由執行下列命令，從您喜愛的 shell hello (cmd.exe，PowerShell 等。)。</span><span class="sxs-lookup"><span data-stu-id="4a681-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="4a681-148">toostart hello 映像，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a681-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="4a681-149">hello 回應看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="4a681-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="4a681-150">Hello 模擬器已啟動一次關機 hello 模擬器的容器，請關閉 hello 互動式殼層。</span><span class="sxs-lookup"><span data-stu-id="4a681-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="4a681-151">在您的用戶端使用 hello 端點和從 hello 回應中的主要金鑰和 hello SSL 憑證匯入到您的主機。</span><span class="sxs-lookup"><span data-stu-id="4a681-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="4a681-152">請勿 hello tooimport hello SSL 憑證，系統管理員命令提示字元中的下列：</span><span class="sxs-lookup"><span data-stu-id="4a681-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="4a681-153">啟動模擬器 hello</span><span class="sxs-lookup"><span data-stu-id="4a681-153">Start hello Emulator</span></span>

<span data-ttu-id="4a681-154">toostart hello Azure Cosmos DB 模擬器中，選取 hello [開始] 按鈕或按 hello Windows 鍵。</span><span class="sxs-lookup"><span data-stu-id="4a681-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="4a681-155">開始輸入**Azure Cosmos DB 模擬器**，和選取 hello hello 清單中的應用程式的模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![選取 hello 開始按鈕或按 hello Windows 鍵，開始輸入 * * Azure Cosmos DB 模擬器 * *，和從 hello 的應用程式的清單選取 hello 模擬器](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="4a681-157">當 hello 模擬器正在執行時，您會看到 hello Windows 工作列通知區域中的圖示。</span><span class="sxs-lookup"><span data-stu-id="4a681-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Azure Cosmos DB 本機模擬器的工作列通知](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="4a681-159">hello Azure Cosmos DB 模擬器預設會 hello 本機電腦 ("localhost") 上接聽連接埠 8081 上執行。</span><span class="sxs-lookup"><span data-stu-id="4a681-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="4a681-160">hello Cosmos DB 安裝 Azure 模擬器的預設 toohello`C:\Program Files\Azure Cosmos DB Emulator`目錄。</span><span class="sxs-lookup"><span data-stu-id="4a681-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="4a681-161">您也可以啟動並停止從命令列 hello hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="4a681-162">如需詳細資訊，請參閱[命令列工具參考](#command-line)。</span><span class="sxs-lookup"><span data-stu-id="4a681-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="4a681-163">啟動資料總管</span><span class="sxs-lookup"><span data-stu-id="4a681-163">Start Data Explorer</span></span>

<span data-ttu-id="4a681-164">Hello Azure Cosmos DB 模擬器啟動時就會自動開啟 hello Azure Cosmos DB Data 總管，瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="4a681-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="4a681-165">hello 位址將會顯示為[https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)。</span><span class="sxs-lookup"><span data-stu-id="4a681-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="4a681-166">如果您關閉 hello 總管 中，而且想要 toore 開啟它之後，您可以在您的瀏覽器中開啟 hello URL 或啟動從 hello Azure Cosmos DB 模擬器在 hello Windows 系統匣圖示，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4a681-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB 本機模擬器的資料總管啟動程式](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="4a681-168">檢查更新</span><span class="sxs-lookup"><span data-stu-id="4a681-168">Checking for updates</span></span>
<span data-ttu-id="4a681-169">資料總管會表示是否有新的更新可供下載。</span><span class="sxs-lookup"><span data-stu-id="4a681-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a681-170">建立在 hello Azure Cosmos DB 模擬器的其中一個版本的資料不保證 toobe 存取時使用不同版本。</span><span class="sxs-lookup"><span data-stu-id="4a681-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="4a681-171">如果您需要 toopersist 資料供 hello 長期，建議您在 Azure Cosmos DB 帳戶，而非 hello Azure Cosmos DB 模擬器中儲存該資料。</span><span class="sxs-lookup"><span data-stu-id="4a681-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="4a681-172">驗證要求</span><span class="sxs-lookup"><span data-stu-id="4a681-172">Authenticating requests</span></span>
<span data-ttu-id="4a681-173">就像 Azure Cosmos DB hello 雲端中與您進行 hello Azure Cosmos DB 模擬器針對每個要求必須進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4a681-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="4a681-174">hello Azure Cosmos DB 模擬器主要金鑰驗證支援單一固定的帳戶及已知的驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a681-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="4a681-175">此帳戶與金鑰是 hello 僅允許以 hello Azure Cosmos DB 模擬器使用的認證。</span><span class="sxs-lookup"><span data-stu-id="4a681-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="4a681-176">如下：</span><span class="sxs-lookup"><span data-stu-id="4a681-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="4a681-177">hello 主要金鑰受到 hello Azure Cosmos DB 模擬器僅供 hello 模擬器只能搭配使用。</span><span class="sxs-lookup"><span data-stu-id="4a681-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="4a681-178">您無法使用您的生產 Azure Cosmos DB 帳戶及金鑰以 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4a681-179">如果您已經啟動 hello 模擬器以 hello /Key 選項，然後使用 hello 產生金鑰，而不是"C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="4a681-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="4a681-180">此外，就像 hello Azure Cosmos 資料庫服務，hello Azure Cosmos DB 模擬器僅支援安全通訊透過 SSL。</span><span class="sxs-lookup"><span data-stu-id="4a681-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="4a681-181">本機網路上執行 hello 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="4a681-182">您可以執行 hello 模擬器在本機網路上。</span><span class="sxs-lookup"><span data-stu-id="4a681-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="4a681-183">tooenable 網路存取，指定在 hello hello /AllowNetworkAccess 選項[命令列](#command-line-syntax)，這也會要求您指定 /Key = key_string 或 /KeyFile = file_name。</span><span class="sxs-lookup"><span data-stu-id="4a681-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="4a681-184">您可以使用 /GenKeyFile = file_name toogenerate 檔案使用預先隨機金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a681-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="4a681-185">然後您可以傳遞該太/KeyFile = file_name 或 /Key = contents_of_file。</span><span class="sxs-lookup"><span data-stu-id="4a681-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="4a681-186">第一個階段 hello 使用者 hello tooenable 的網路存取權應該關閉 hello 模擬器，然後刪除 hello 模擬器的資料目錄 (C:\Users\user_name\AppData\Local\CosmosDBEmulator)。</span><span class="sxs-lookup"><span data-stu-id="4a681-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="4a681-187">使用 hello 模擬器進行開發</span><span class="sxs-lookup"><span data-stu-id="4a681-187">Developing with hello Emulator</span></span>
<span data-ttu-id="4a681-188">一旦您擁有 hello 桌面上執行的 Azure Cosmos DB 模擬器，您可以使用任何支援[Azure Cosmos DB SDK](documentdb-sdk-dotnet.md)或 hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract 以 hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="4a681-189">hello Azure Cosmos DB 模擬器也包含內建的資料檔案總管，可讓您建立集合中的 hello DocumentDB 和 MongoDB Api，以及檢視和編輯文件，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a681-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="4a681-190">如果您使用[Azure Cosmos DB 通訊協定 support for MongoDB。](mongodb-introduction.md)，請使用下列連接字串 hello:</span><span class="sxs-lookup"><span data-stu-id="4a681-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="4a681-191">您可以使用現有的工具，像是[Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="4a681-192">您也可以移轉 hello Azure Cosmos DB 模擬器與使用 hello hello Azure Cosmos DB 服務之間的資料[Azure Cosmos DB 的資料移轉工具](https://github.com/azure/azure-documentdb-datamigrationtool)。</span><span class="sxs-lookup"><span data-stu-id="4a681-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="4a681-193">如果您已經啟動 hello 模擬器以 hello /Key 選項，然後使用 hello 產生金鑰，而不是"C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="4a681-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="4a681-194">依預設，使用 hello Azure Cosmos DB 模擬器中，您可以建立 too25 單一分割區集合或 1 的資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="4a681-195">如需有關如何變更此值的詳細資訊，請參閱[設定 hello PartitionCount 值](#set-partitioncount)。</span><span class="sxs-lookup"><span data-stu-id="4a681-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="4a681-196">匯出 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="4a681-196">Export hello SSL certificate</span></span>

<span data-ttu-id="4a681-197">.NET 語言和執行階段使用 hello Windows 憑證存放區 toosecurely toohello Azure Cosmos DB 本機模擬器的連接。</span><span class="sxs-lookup"><span data-stu-id="4a681-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="4a681-198">其他語言則有自己管理和使用憑證的方法。</span><span class="sxs-lookup"><span data-stu-id="4a681-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="4a681-199">Java 使用自己的[憑證存放區](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)，而 Python 使用[通訊端包裝函式](https://docs.python.org/2/library/ssl.html)。</span><span class="sxs-lookup"><span data-stu-id="4a681-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="4a681-200">在訂單 tooobtain 與語言和執行階段無法與整合 hello Windows 憑證存放區與您的憑證 toouse 需要 tooexport 使用 hello Windows 憑證管理員。</span><span class="sxs-lookup"><span data-stu-id="4a681-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="4a681-201">您可以開始執行 certlm.msc 或依照中的 hello 逐步解說指示[匯出 hello Azure Cosmos DB 模擬器憑證](./local-emulator-export-ssl-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="4a681-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="4a681-202">一旦 hello 憑證管理員正常執行，如下所示，則開啟 hello 個人憑證及匯出 hello hello 易記名稱 」 DocumentDBEmulatorCertificate"憑證為 base-64 編碼 X.509 (.cer) 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a681-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB 本機模擬器的 SSL 憑證](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="4a681-204">hello X.509 憑證可以匯入 hello Java 憑證存放區中的 hello 指示[加入 Java CA 憑證存放區的憑證 toohello](https://docs.microsoft.com/azure/java-add-certificate-ca-store)。</span><span class="sxs-lookup"><span data-stu-id="4a681-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="4a681-205">一旦 hello 憑證匯入 hello 憑證存放區，則 Java 和 MongoDB 應用程式將會無法 tooconnect toohello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="4a681-206">從 Python 和 Node.js Sdk 連接 toohello 模擬器，會停用 SSL 驗證。</span><span class="sxs-lookup"><span data-stu-id="4a681-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="4a681-207"><a id="command-line"></a>命令列工具參考</span><span class="sxs-lookup"><span data-stu-id="4a681-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="4a681-208">從 hello 安裝位置，您可以使用 hello 命令列 toostart 和停止 hello 模擬器、 設定選項，並執行其他作業。</span><span class="sxs-lookup"><span data-stu-id="4a681-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="4a681-209">命令列語法</span><span class="sxs-lookup"><span data-stu-id="4a681-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="4a681-210">tooview hello 選項清單，型別`CosmosDB.Emulator.exe /?`hello 的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="4a681-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="4a681-211"><strong>選項</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="4a681-212"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="4a681-213"><strong>命令</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="4a681-214"><strong>引數</strong></span><span class="sxs-lookup"><span data-stu-id="4a681-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-215">[無引數]</span><span class="sxs-lookup"><span data-stu-id="4a681-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="4a681-216">啟動 hello Azure Cosmos DB 模擬器使用預設設定。</span><span class="sxs-lookup"><span data-stu-id="4a681-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="4a681-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="4a681-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-218">[說明]</span><span class="sxs-lookup"><span data-stu-id="4a681-218">[Help]</span></span></td>
  <td><span data-ttu-id="4a681-219">顯示 hello 清單支援命令列引數。</span><span class="sxs-lookup"><span data-stu-id="4a681-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="4a681-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="4a681-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="4a681-221">Shutdown</span></span></td>
  <td><span data-ttu-id="4a681-222">關閉 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="4a681-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="4a681-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-224">資料路徑</span><span class="sxs-lookup"><span data-stu-id="4a681-224">DataPath</span></span></td>
  <td><span data-ttu-id="4a681-225">指定在哪個 toostore 資料檔案中的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="4a681-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="4a681-226">預設值為 %LocalAppdata%\CosmosDBEmulator。</span><span class="sxs-lookup"><span data-stu-id="4a681-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="4a681-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="4a681-228">&lt;datapath&gt;︰可存取的路徑</span><span class="sxs-lookup"><span data-stu-id="4a681-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-229">Port</span><span class="sxs-lookup"><span data-stu-id="4a681-229">Port</span></span></td>
  <td><span data-ttu-id="4a681-230">指定 hello 連接埠號碼 toouse hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="4a681-231">預設值為 8081。</span><span class="sxs-lookup"><span data-stu-id="4a681-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="4a681-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="4a681-233">&lt;port&gt;︰單一連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="4a681-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="4a681-234">MongoPort</span></span></td>
  <td><span data-ttu-id="4a681-235">指定 hello 連接埠號碼 toouse MongoDB 相容性應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4a681-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="4a681-236">預設值為 10255。</span><span class="sxs-lookup"><span data-stu-id="4a681-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="4a681-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="4a681-238">&lt;mongoport&gt;︰單一連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="4a681-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="4a681-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="4a681-240">指定直接連線的 hello 連接埠 toouse。</span><span class="sxs-lookup"><span data-stu-id="4a681-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="4a681-241">預設值為 10251、10252、10253、10254。</span><span class="sxs-lookup"><span data-stu-id="4a681-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="4a681-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="4a681-243">&lt;directports&gt;︰以逗號分隔的 4 個連接埠清單</span><span class="sxs-lookup"><span data-stu-id="4a681-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-244">Key</span><span class="sxs-lookup"><span data-stu-id="4a681-244">Key</span></span></td>
  <td><span data-ttu-id="4a681-245">Hello 模擬器的授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a681-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="4a681-246">索引鍵必須是 64 位元組向量的 hello base-64 編碼。</span><span class="sxs-lookup"><span data-stu-id="4a681-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="4a681-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="4a681-248">&lt;索引鍵&gt;： 索引鍵必須是 hello base 64 編碼的 64 位元組向量為單位</span><span class="sxs-lookup"><span data-stu-id="4a681-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="4a681-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="4a681-250">指定要啟用要求率限制行為。</span><span class="sxs-lookup"><span data-stu-id="4a681-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="4a681-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="4a681-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="4a681-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="4a681-253">指定要停用要求率限制行為。</span><span class="sxs-lookup"><span data-stu-id="4a681-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="4a681-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="4a681-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="4a681-255">NoUI</span></span></td>
  <td><span data-ttu-id="4a681-256">不要顯示 hello 模擬器使用者介面。</span><span class="sxs-lookup"><span data-stu-id="4a681-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="4a681-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="4a681-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="4a681-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="4a681-259">啟動時不要顯示文件總管。</span><span class="sxs-lookup"><span data-stu-id="4a681-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="4a681-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="4a681-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="4a681-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="4a681-262">指定 hello 最大的資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="4a681-263">請參閱[變更集合的 hello 數目](#set-partitioncount)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4a681-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="4a681-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="4a681-265">&lt;partitioncount&gt;：允許的單一分割區集合數目上限。</span><span class="sxs-lookup"><span data-stu-id="4a681-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="4a681-266">預設值為 25。</span><span class="sxs-lookup"><span data-stu-id="4a681-266">Default is 25.</span></span> <span data-ttu-id="4a681-267">允許的上限為 250。</span><span class="sxs-lookup"><span data-stu-id="4a681-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="4a681-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="4a681-269">指定 hello 預設資料分割數目的資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="4a681-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="4a681-271">&lt;defaultpartitioncount&gt; 預設值為 25。</span><span class="sxs-lookup"><span data-stu-id="4a681-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="4a681-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="4a681-273">啟用透過網路存取 toohello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="4a681-274">您還必須傳遞 /Key =&lt;key_string&gt;或 /KeyFile =&lt;file_name&gt; tooenable 網路存取。</span><span class="sxs-lookup"><span data-stu-id="4a681-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="4a681-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="4a681-276">或</span><span class="sxs-lookup"><span data-stu-id="4a681-276">or</span></span><br><br><span data-ttu-id="4a681-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="4a681-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="4a681-279">當 /AllowNetworkAccess 在使用中時請勿調整防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="4a681-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="4a681-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="4a681-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="4a681-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="4a681-282">產生新的授權金鑰並儲存 toohello 指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="4a681-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="4a681-283">hello 產生索引鍵可以搭配 hello /Key 或 /KeyFile 選項。</span><span class="sxs-lookup"><span data-stu-id="4a681-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="4a681-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;路徑 tookey 檔案&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-285">一致性</span><span class="sxs-lookup"><span data-stu-id="4a681-285">Consistency</span></span></td>
  <td><span data-ttu-id="4a681-286">設定 hello hello 帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="4a681-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="4a681-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="4a681-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="4a681-288">&lt;一致性&gt;： 值必須是 hello 下列其中一種[一致性層級](consistency-levels.md)： 工作階段、 強式、 Eventual 或 BoundedStaleness。</span><span class="sxs-lookup"><span data-stu-id="4a681-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="4a681-289">hello 預設值是工作階段。</span><span class="sxs-lookup"><span data-stu-id="4a681-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="4a681-290">?</span><span class="sxs-lookup"><span data-stu-id="4a681-290">?</span></span></td>
  <td><span data-ttu-id="4a681-291">顯示 hello 說明訊息。</span><span class="sxs-lookup"><span data-stu-id="4a681-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="4a681-292">Hello Azure Cosmos DB 模擬器和 Azure Cosmos DB 之間的差異</span><span class="sxs-lookup"><span data-stu-id="4a681-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="4a681-293">Hello Azure Cosmos DB 模擬器提供模擬的環境在本機開發人員工作站上執行，因此有一些差異功能 hello 模擬器和 Azure Cosmos DB 帳戶之間 hello 定域機組中：</span><span class="sxs-lookup"><span data-stu-id="4a681-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="4a681-294">hello Azure Cosmos DB 模擬器支援只有單一固定的帳戶及已知的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4a681-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="4a681-295">重新產生金鑰不能在 hello Azure Cosmos DB 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="4a681-296">hello Azure Cosmos DB 模擬器不是可擴充的服務，而且不支援大量的集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="4a681-297">hello Azure Cosmos DB 模擬器不會模擬不同[Azure Cosmos DB 一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="4a681-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="4a681-298">hello Azure Cosmos DB 模擬器不會模擬[多區域複寫](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="4a681-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="4a681-299">hello Azure Cosmos DB 模擬器不支援 hello 服務配額覆寫 hello Azure Cosmos DB 服務 （例如文件大小限制，增加的分割區的集合儲存體） 中可用。</span><span class="sxs-lookup"><span data-stu-id="4a681-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="4a681-300">因為 hello Azure Cosmos DB 模擬器副本可能不是向上 toodate hello 與 hello Azure Cosmos DB 服務的最新變更，請[Azure Cosmos DB 容量規劃](https://www.documentdb.com/capacityplanner)tooaccurately 估計生產輸送量 (RUs)應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="4a681-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="4a681-301"><a id="set-partitioncount"></a>變更集合的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="4a681-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="4a681-302">根據預設，您可以建立 too25 單一分割區的集合，或使用 hello Azure Cosmos DB 模擬器 1 的資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="4a681-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="4a681-303">藉由修改 hello **PartitionCount**值，您可以建立 too250 單一分割區集合或 10 個資料分割的集合，或任何組合的 hello 不能超過 250 單一的兩個資料分割 （位置 1 進行資料分割集合 = 25 的單一資料分割集合)。</span><span class="sxs-lookup"><span data-stu-id="4a681-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="4a681-304">如果超過 hello 目前資料分割計數後，您可以嘗試 toocreate 集合，hello 模擬器會擲回以 hello 下訊息 ServiceUnavailable 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a681-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="4a681-305">集合可用 toohello Azure Cosmos DB 模擬器，toochange hello 數目不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4a681-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="4a681-306">刪除所有的本機 Azure Cosmos DB 模擬器資料，以滑鼠右鍵按一下 hello **Azure Cosmos DB 模擬器**圖示 hello 系統匣中，然後按一下**重設資料...**.</span><span class="sxs-lookup"><span data-stu-id="4a681-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="4a681-307">刪除以下資料夾中所有的模擬器資料：C:\Users\user_name\AppData\Local\CosmosDBEmulator。</span><span class="sxs-lookup"><span data-stu-id="4a681-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="4a681-308">結束所有開啟的執行個體，以滑鼠右鍵按一下 hello **Azure Cosmos DB 模擬器**圖示 hello 系統匣中，然後按一下**結束**。</span><span class="sxs-lookup"><span data-stu-id="4a681-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="4a681-309">它可能會花一分鐘的所有執行個體 tooexit。</span><span class="sxs-lookup"><span data-stu-id="4a681-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="4a681-310">安裝 hello 最新版 hello [Azure Cosmos DB 模擬器](https://aka.ms/cosmosdb-emulator)。</span><span class="sxs-lookup"><span data-stu-id="4a681-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="4a681-311">藉由設定值，啟動模擬器 hello PartitionCount 旗標，hello < = 250。</span><span class="sxs-lookup"><span data-stu-id="4a681-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="4a681-312">例如： `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`。</span><span class="sxs-lookup"><span data-stu-id="4a681-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4a681-313">疑難排解</span><span class="sxs-lookup"><span data-stu-id="4a681-313">Troubleshooting</span></span>

<span data-ttu-id="4a681-314">使用下列秘訣 toohelp hello Azure Cosmos DB 模擬器與您遇到的問題進行疑難排解的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a681-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="4a681-315">如果您安裝新版本的 hello 模擬器，並發生錯誤，請確定您重設您的資料。</span><span class="sxs-lookup"><span data-stu-id="4a681-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="4a681-316">您可以 hello Azure Cosmos DB 模擬器圖示上 hello 系統匣中，按一下滑鼠右鍵，然後按一下重設資料重設您的資料...</span><span class="sxs-lookup"><span data-stu-id="4a681-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="4a681-317">如果無法解決 hello 錯誤，您可以解除安裝然後重新安裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a681-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="4a681-318">請參閱[解除安裝本機模擬器，hello](#uninstall)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="4a681-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="4a681-319">如果 hello Azure Cosmos DB 模擬器損毀，c:\Users\user_name\AppData\Local\CrashDumps 資料夾從收集傾印檔案，壓縮檔案，並且將它們附加 tooan 電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="4a681-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="4a681-320">如果您遇到當機 CosmosDB.StartupEntryPoint.exe，執行下列命令，從系統管理員命令提示字元的 hello:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="4a681-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="4a681-321">如果您遇到連接問題，[收集追蹤檔案](#trace-files)、 壓縮，並且將它們附加 tooan 電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="4a681-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="4a681-322">如果您收到**服務無法使用**訊息，hello 模擬器可能會失敗 tooinitialize hello 網路堆疊。</span><span class="sxs-lookup"><span data-stu-id="4a681-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="4a681-323">如果您擁有 hello Pulse 安全用戶端或 Juniper 網路用戶端安裝，因為其網路篩選器驅動程式可能會造成 hello 問題，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="4a681-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="4a681-324">解除安裝協力廠商網路篩選器驅動程式通常會修正 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="4a681-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="4a681-325"><a id="trace-files"></a>收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="4a681-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="4a681-326">toocollect 偵錯追蹤，執行 hello 系統管理命令提示字元中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="4a681-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="4a681-327">`CosmosDB.Emulator.exe /shutdown`。</span><span class="sxs-lookup"><span data-stu-id="4a681-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="4a681-328">監看式 hello 系統匣 toomake 確定 hello 程式已關閉時，可能需要一分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4a681-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="4a681-329">您也可以按一下**結束**hello Azure Cosmos DB 模擬器使用者介面中。</span><span class="sxs-lookup"><span data-stu-id="4a681-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="4a681-330">重新產生 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="4a681-330">Reproduce hello problem.</span></span> <span data-ttu-id="4a681-331">如果資料的總管尚未運作，您只需要 toowait 的 hello 瀏覽器 tooopen 幾秒 toocatch hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="4a681-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="4a681-332">瀏覽過`%ProgramFiles%\Azure Cosmos DB Emulator`尋找 hello docdbemulator_000001.etl 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a681-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="4a681-333">傳送嗨.etl 檔案以及重新產生步驟太[askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com)偵錯。</span><span class="sxs-lookup"><span data-stu-id="4a681-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="4a681-334"><a id="uninstall"></a>解除安裝 hello 本機模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="4a681-335">結束所有開啟的執行個體的 hello 本機模擬器，以滑鼠右鍵按一下 hello Azure Cosmos DB 模擬器圖示上 hello 系統匣中，然後按一下結束。</span><span class="sxs-lookup"><span data-stu-id="4a681-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="4a681-336">它可能會花一分鐘的所有執行個體 tooexit。</span><span class="sxs-lookup"><span data-stu-id="4a681-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="4a681-337">在 hello Windows 搜尋方塊中，輸入**應用程式和功能**，然後按一下 hello**應用程式和功能 （系統的設定）**結果。</span><span class="sxs-lookup"><span data-stu-id="4a681-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="4a681-338">在 hello 清單的應用程式中，捲動太**Azure Cosmos DB 模擬器**、 選取它、 按一下**解除安裝**、 確認，然後按一下 **解除安裝**一次。</span><span class="sxs-lookup"><span data-stu-id="4a681-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="4a681-339">解除安裝 hello 應用程式時，瀏覽 tooC:\Users\<使用者 > \AppData\Local\CosmosDBEmulator 和 delete hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4a681-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a681-340">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a681-340">Next steps</span></span>

<span data-ttu-id="4a681-341">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4a681-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a681-342">安裝 hello 本機模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="4a681-343">Rand hello Docker for Windows 上的模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="4a681-344">已驗證要求</span><span class="sxs-lookup"><span data-stu-id="4a681-344">Authenticated requests</span></span>
> * <span data-ttu-id="4a681-345">使用 hello 模擬器中的 hello 資料總管</span><span class="sxs-lookup"><span data-stu-id="4a681-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="4a681-346">已匯出 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="4a681-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="4a681-347">從 hello 命令列呼叫 hello 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a681-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="4a681-348">已收集追蹤檔案</span><span class="sxs-lookup"><span data-stu-id="4a681-348">Collected trace files</span></span>

<span data-ttu-id="4a681-349">在本教學課程中，您學到如何 toouse hello 可用的本機開發的本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a681-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="4a681-350">您現在可以繼續 toohello 下一個教學課程，並了解如何 tooexport 模擬器 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4a681-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a681-351">匯出 hello Azure Cosmos DB 模擬器憑證</span><span class="sxs-lookup"><span data-stu-id="4a681-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
