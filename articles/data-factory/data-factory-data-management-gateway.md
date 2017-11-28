---
title: "aaaData Data Factory 的管理閘道器 |Microsoft 文件"
description: "設定內部部署與 hello 之間的資料閘道 toomove 資料雲端。 使用資料管理閘道器在 Azure Data Factory toomove 您的資料。"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="e7574-104">資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="e7574-104">Data Management Gateway</span></span>
<span data-ttu-id="e7574-105">hello 資料管理閘道器是用戶端代理程式，您必須安裝在內部部署環境 toocopy 資料之間雲端和內部部署資料存放區中。</span><span class="sxs-lookup"><span data-stu-id="e7574-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="e7574-106">hello 內部部署資料存放區支援的 Data Factory 會列在 hello[支援的資料來源](data-factory-data-movement-activities.md#supported-data-stores-and-formats)> 一節。</span><span class="sxs-lookup"><span data-stu-id="e7574-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="e7574-107">本文補充 hello 逐步解說中 hello[在內部部署與雲端之間移動資料的資料存放區](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="e7574-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="e7574-108">Hello 逐步解說中，您可以建立會使用內部部署 SQL Server 資料庫 tooan Azure blob 的 hello 閘道 toomove 資料管線。</span><span class="sxs-lookup"><span data-stu-id="e7574-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="e7574-109">本文章提供有關 hello 資料管理閘道器的詳細深入資訊。</span><span class="sxs-lookup"><span data-stu-id="e7574-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="e7574-110">您可以向外延展資料管理閘道將多部在內部部署電腦與 hello 閘道產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e7574-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="e7574-111">您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="e7574-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="e7574-112">這項功能也適用於具有單一節點的邏輯閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="e7574-113">如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e7574-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="e7574-114">目前，閘道器僅支援 hello 複製活動和預存程序活動 Data Factory 中。</span><span class="sxs-lookup"><span data-stu-id="e7574-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="e7574-115">它不是從自訂活動 tooaccess 在內部部署資料來源的可能 toouse hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="e7574-116">概觀</span><span class="sxs-lookup"><span data-stu-id="e7574-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="e7574-117">資料管理閘道功能</span><span class="sxs-lookup"><span data-stu-id="e7574-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="e7574-118">資料管理閘道器提供下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7574-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="e7574-119">模型在內部部署資料來源和雲端資料來源內 hello 相同的資料處理站，並將資料移動。</span><span class="sxs-lookup"><span data-stu-id="e7574-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="e7574-120">具有單一的監視和管理與閘道狀態從 hello Data Factory 頁面的可視性的半透明窗格。</span><span class="sxs-lookup"><span data-stu-id="e7574-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="e7574-121">安全地管理存取 tooon 內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="e7574-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="e7574-122">不需要 toocorporate 防火牆進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="e7574-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="e7574-123">閘道只會以 HTTP 為基礎的輸出連線 tooopen 網際網路。</span><span class="sxs-lookup"><span data-stu-id="e7574-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="e7574-124">利用您的憑證加密內部部署資料存放區的認證。</span><span class="sxs-lookup"><span data-stu-id="e7574-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="e7574-125">有效率地移動資料 – 平行、 復原 toointermittent 網路問題的自動重試邏輯以傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="e7574-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="e7574-126">命令流程和資料流程</span><span class="sxs-lookup"><span data-stu-id="e7574-126">Command flow and data flow</span></span>
<span data-ttu-id="e7574-127">當您使用內部部署與雲端之間的複製活動 toocopy 資料時，hello 活動會使用閘道 tootransfer 資料從內部部署資料來源 toocloud，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="e7574-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="e7574-128">以下是 hello 高層級的資料流程和複本資料閘道的步驟摘要：![使用閘道的資料流程](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="e7574-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="e7574-129">資料開發人員使用任一 hello Azure Data factory 建立閘道[Azure 入口網站](https://portal.azure.com)或[PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7574-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="e7574-130">資料開發人員藉由指定 hello 閘道建立內部部署資料存放區連結的服務。</span><span class="sxs-lookup"><span data-stu-id="e7574-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="e7574-131">資料開發人員在 hello 設定已連結的服務，使用 hello 設定認證的應用程式 toospecify 驗證類型和認證。</span><span class="sxs-lookup"><span data-stu-id="e7574-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="e7574-132">hello 設定認證與 hello 資料通訊的應用程式 對話方塊將 tootest 連接和 hello 閘道 toosave 認證儲存。</span><span class="sxs-lookup"><span data-stu-id="e7574-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="e7574-133">閘道會先將 hello 認證儲存在 hello 雲端進行 hello 認證加密與 hello 與 hello 閘道 （由資料開發人員提供），相關聯的憑證。</span><span class="sxs-lookup"><span data-stu-id="e7574-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="e7574-134">資料 Factory 服務會與 hello 閘道排程和管理工作會使用共用的 Azure 服務匯流排佇列的控制通道的通訊。</span><span class="sxs-lookup"><span data-stu-id="e7574-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="e7574-135">當複製活動作業需要 toobe 開始時，Data Factory 要求排入佇列 hello 以及認證資訊。</span><span class="sxs-lookup"><span data-stu-id="e7574-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="e7574-136">後輪詢 hello 佇列 hello 作業就會啟動閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="e7574-137">hello 閘道解密 hello 認證以 hello 相同憑證，然後使用適當的驗證類型和認證連接 toohello 在內部部署資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e7574-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="e7574-138">hello 閘道將資料從內部部署存放區 tooa 雲端儲存體，或反之亦然根據 hello 複製活動 hello 資料管線中的設定方式。</span><span class="sxs-lookup"><span data-stu-id="e7574-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="e7574-139">針對此步驟，直接與雲端儲存體服務，例如 Azure Blob 儲存體不要透過安全 (HTTPS) 通道通訊 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="e7574-140">使用閘道的考量</span><span class="sxs-lookup"><span data-stu-id="e7574-140">Considerations for using gateway</span></span>
* <span data-ttu-id="e7574-141">您可以將單一資料管理閘道執行個體用於多個內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="e7574-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="e7574-142">不過，**單一閘道執行個體是一個 Azure 資料處理站的繫結的 tooonly**並不能共用與另一個 data factory。</span><span class="sxs-lookup"><span data-stu-id="e7574-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="e7574-143">單一電腦上**只能安裝一個資料管理閘道的執行個體**。</span><span class="sxs-lookup"><span data-stu-id="e7574-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="e7574-144">假設您有兩個 data factory 需要 tooaccess 在內部部署資料來源，您需要在兩個內部部署電腦上的 tooinstall 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="e7574-145">換句話說，閘道已繫結的 tooa 特定的 data factory</span><span class="sxs-lookup"><span data-stu-id="e7574-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="e7574-146">hello**閘道不需要在相同電腦做 hello 資料來源的 hello toobe**。</span><span class="sxs-lookup"><span data-stu-id="e7574-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="e7574-147">不過，擁有閘道器更接近 toohello 資料來源可減少 hello hello 閘道 tooconnect toohello 資料來源的時間。</span><span class="sxs-lookup"><span data-stu-id="e7574-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="e7574-148">我們建議您在其中一個該主機在內部部署資料來源的 hello 與不同的電腦上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="e7574-149">不同的電腦上的 hello 閘道和資料來源時，hello 閘道不會爭奪與資料來源的資源。</span><span class="sxs-lookup"><span data-stu-id="e7574-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="e7574-150">您可以擁有**連接 toohello 不同的電腦上的多個閘道相同的內部部署資料來源**。</span><span class="sxs-lookup"><span data-stu-id="e7574-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="e7574-151">例如，您可能提供兩個 data factory，但是相同的內部部署資料來源已向這兩個 hello data factory 的 hello 的這兩個閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="e7574-152">若您已在電腦上安裝用於 **Power BI** 案例的閘道器，請於另一台電腦上安裝**另一個用於 Azure Data Factory 的閘道器**。</span><span class="sxs-lookup"><span data-stu-id="e7574-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="e7574-153">即使您使用 **ExpressRoute**，也必須使用閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="e7574-154">即使您使用 **ExpressRoute**，也應該將資料來源視為內部部署資料來源 (亦即在防火牆後面)。</span><span class="sxs-lookup"><span data-stu-id="e7574-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="e7574-155">使用 hello 服務與 hello 資料來源之間的 hello 閘道 tooestablish 連線。</span><span class="sxs-lookup"><span data-stu-id="e7574-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="e7574-156">您必須**使用 hello 閘道**即使 hello 資料存放區上處於 hello 雲端**Azure IaaS VM**。</span><span class="sxs-lookup"><span data-stu-id="e7574-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="e7574-157">安裝</span><span class="sxs-lookup"><span data-stu-id="e7574-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e7574-158">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7574-158">Prerequisites</span></span>
* <span data-ttu-id="e7574-159">支援的 hello**作業系統**版本是 Windows 7、 Windows 8/8.1、 Windows 10、 Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="e7574-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="e7574-160">目前不支援安裝在網域控制站上的 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="e7574-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="e7574-161">必須有 .NET Framework 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e7574-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="e7574-162">如果您要在 Windows 7 電腦上安裝閘道，請安裝 .NET Framework 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e7574-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="e7574-163">如需詳細資訊，請參閱 [.NET Framework 系統需求](https://msdn.microsoft.com/library/8z6watww.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e7574-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="e7574-164">建議的 hello**組態**hello 閘道機器是至少 2 GHz、 4 個核心，8 GB RAM 和 80 GB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e7574-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="e7574-165">如果 hello 主機電腦休眠，hello 閘道沒有回應 toodata 要求。</span><span class="sxs-lookup"><span data-stu-id="e7574-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="e7574-166">因此，設定適當**電源計劃**hello 之前安裝 hello 閘道的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e7574-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="e7574-167">如果已設定的 toohibernate hello 機器，hello 閘道安裝會提示訊息。</span><span class="sxs-lookup"><span data-stu-id="e7574-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="e7574-168">您必須是 hello 機器 tooinstall 的系統管理員，並已成功設定 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="e7574-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="e7574-169">您可以加入其他使用者 toohello**資料管理閘道使用者**本機 Windows 群組。</span><span class="sxs-lookup"><span data-stu-id="e7574-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="e7574-170">hello 這個群組的成員都能 toouse hello**資料管理閘道組態管理員**工具 tooconfigure hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="e7574-171">當發生複製活動執行特定的頻率，hello hello 電腦上 （CPU、 記憶體） 的資源使用量也會遵循的 hello 相同模式尖峰和閒置的時間。</span><span class="sxs-lookup"><span data-stu-id="e7574-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="e7574-172">資源使用量也仰賴 hello 移動的資料數量。</span><span class="sxs-lookup"><span data-stu-id="e7574-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="e7574-173">如果有多個複製作業正在進行，您會看到資源使用量在尖峰時段增加。</span><span class="sxs-lookup"><span data-stu-id="e7574-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="e7574-174">安裝選項</span><span class="sxs-lookup"><span data-stu-id="e7574-174">Installation options</span></span>
<span data-ttu-id="e7574-175">資料管理閘道可以安裝在 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="e7574-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="e7574-176">藉由從 hello 下載 MSI 安裝程式套件[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717)。</span><span class="sxs-lookup"><span data-stu-id="e7574-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="e7574-177">hello MSI 也可以使用的 tooupgrade 現有資料管理閘道 toohello 最新版本，以保留的所有設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="e7574-178">按一下 [手動設定] 底下的 [下載並安裝資料閘道] 連結，或 [快速安裝] 之下的 [直接安裝在此電腦上]。</span><span class="sxs-lookup"><span data-stu-id="e7574-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="e7574-179">如需使用快速安裝的逐步指示，請參閱 [在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="e7574-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="e7574-180">hello 手動步驟會帶您 toohello 下載中心取得。</span><span class="sxs-lookup"><span data-stu-id="e7574-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="e7574-181">hello 指示下載並從下載中心安裝 hello 閘道位於 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="e7574-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="e7574-182">安裝最佳作法：</span><span class="sxs-lookup"><span data-stu-id="e7574-182">Installation best practices:</span></span>
1. <span data-ttu-id="e7574-183">Hello hello 閘道的主機電腦上設定的電源計劃 hello 機器不休眠。</span><span class="sxs-lookup"><span data-stu-id="e7574-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="e7574-184">如果 hello 主機電腦休眠，hello 閘道沒有回應 toodata 要求。</span><span class="sxs-lookup"><span data-stu-id="e7574-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="e7574-185">備份 hello 與 hello 閘道相關聯的憑證。</span><span class="sxs-lookup"><span data-stu-id="e7574-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="e7574-186">從下載中心安裝 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="e7574-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="e7574-187">瀏覽過[Microsoft 資料管理閘道器下載頁面](https://www.microsoft.com/download/details.aspx?id=39717)。</span><span class="sxs-lookup"><span data-stu-id="e7574-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="e7574-188">按一下**下載**，選取 hello 適當版本 (**32 位元**vs。**64 位元**)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e7574-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="e7574-189">執行 hello **MSI**直接或將它儲存 tooyour 硬碟，並執行。</span><span class="sxs-lookup"><span data-stu-id="e7574-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="e7574-190">在 hello ** 褖畫惎**頁面上，選取**語言**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e7574-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="e7574-191">**接受**hello 使用者授權合約，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e7574-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="e7574-192">選取**資料夾**tooinstall hello 閘道，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e7574-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="e7574-193">在 hello**準備 tooinstall**頁面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="e7574-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="e7574-194">按一下**完成**toocomplete 安裝。</span><span class="sxs-lookup"><span data-stu-id="e7574-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="e7574-195">收到 hello Azure 入口網站中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e7574-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="e7574-196">請參閱 hello 下一節，如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="e7574-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="e7574-197">在 hello**註冊閘道**頁面**資料管理閘道組態管理員**您電腦上執行下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="e7574-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="e7574-198">貼上 hello 索引鍵中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="e7574-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="e7574-199">（選擇性） 按一下**顯示閘道器金鑰**toosee hello 文字。</span><span class="sxs-lookup"><span data-stu-id="e7574-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="e7574-200">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="e7574-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="e7574-201">使用金鑰註冊閘道</span><span class="sxs-lookup"><span data-stu-id="e7574-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="e7574-202">如果您尚未在 hello 入口網站中建立邏輯閘道</span><span class="sxs-lookup"><span data-stu-id="e7574-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="e7574-203">toocreate hello 入口網站及 get hello 機碼中的閘道，從 hello**設定**頁面上，遵循的步驟逐步解說中 hello[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="e7574-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="e7574-204">如果您已經在 hello 入口網站中建立 hello 邏輯閘道</span><span class="sxs-lookup"><span data-stu-id="e7574-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="e7574-205">在 Azure 入口網站，瀏覽 toohello **Data Factory**頁面，然後按一下**連結的服務**磚。</span><span class="sxs-lookup"><span data-stu-id="e7574-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Data Factory 頁面](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="e7574-207">在 hello**連結的服務**頁面上，選取 hello 邏輯**閘道**hello 入口網站中建立。</span><span class="sxs-lookup"><span data-stu-id="e7574-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![邏輯閘道](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="e7574-209">在 hello**資料閘道**頁面上，按一下**下載並安裝資料閘道**。</span><span class="sxs-lookup"><span data-stu-id="e7574-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![下載 hello 入口網站中的連結](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="e7574-211">在 hello**設定**頁面上，按一下**重新建立金鑰**。</span><span class="sxs-lookup"><span data-stu-id="e7574-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="e7574-212">按一下 [是] hello 警告訊息請仔細閱讀它之後。</span><span class="sxs-lookup"><span data-stu-id="e7574-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![重新建立索引鍵](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="e7574-214">按一下 [複製] 按鈕下一個 toohello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e7574-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="e7574-215">複製的 toohello 剪貼簿 hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7574-215">hello key is copied toohello clipboard.</span></span>

    ![複製金鑰](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="e7574-217">系統匣圖示/通知</span><span class="sxs-lookup"><span data-stu-id="e7574-217">System tray icons/ notifications</span></span>
<span data-ttu-id="e7574-218">hello 下圖顯示一些 hello 您看到的紙匣圖示。</span><span class="sxs-lookup"><span data-stu-id="e7574-218">hello following image shows some of hello tray icons that you see.</span></span>

![系統匣圖示](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="e7574-220">如果您將游標移 hello 系統匣圖示/通知訊息時，您會看到有關 hello 快顯視窗中的 hello 閘道/更新作業狀態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7574-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="e7574-221">連接埠和防火牆</span><span class="sxs-lookup"><span data-stu-id="e7574-221">Ports and firewall</span></span>
<span data-ttu-id="e7574-222">有兩個防火牆，您需要 tooconsider:**公司防火牆**hello 組織的 hello 中央路由器上執行和**Windows 防火牆**設定為 hello 本機電腦上的服務精靈，其中 hello安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="e7574-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![防火牆](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="e7574-224">在公司防火牆層級，您需要設定 hello 下列網域和輸出連接埠：</span><span class="sxs-lookup"><span data-stu-id="e7574-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="e7574-225">網域名稱</span><span class="sxs-lookup"><span data-stu-id="e7574-225">Domain names</span></span> | <span data-ttu-id="e7574-226">連接埠</span><span class="sxs-lookup"><span data-stu-id="e7574-226">Ports</span></span> | <span data-ttu-id="e7574-227">說明</span><span class="sxs-lookup"><span data-stu-id="e7574-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7574-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e7574-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="e7574-229">443、80</span><span class="sxs-lookup"><span data-stu-id="e7574-229">443, 80</span></span> |<span data-ttu-id="e7574-230">用於與「資料移動服務」後端進行通訊</span><span class="sxs-lookup"><span data-stu-id="e7574-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="e7574-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e7574-231">*.core.windows.net</span></span> |<span data-ttu-id="e7574-232">443</span><span class="sxs-lookup"><span data-stu-id="e7574-232">443</span></span> |<span data-ttu-id="e7574-233">用於使用 Azure Blob 的分段複製 (如果已設定)</span><span class="sxs-lookup"><span data-stu-id="e7574-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="e7574-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="e7574-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="e7574-235">443</span><span class="sxs-lookup"><span data-stu-id="e7574-235">443</span></span> |<span data-ttu-id="e7574-236">用於與「資料移動服務」後端進行通訊</span><span class="sxs-lookup"><span data-stu-id="e7574-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="e7574-237">Windows 防火牆層級通常會啟用這些輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="e7574-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="e7574-238">如果沒有，您可以設定 hello 網域和連接埠據此閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="e7574-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="e7574-239">根據您的來源 / 接收器，您可能必須 toowhitelist 其他網域與輸出連接埠，在您的公司/Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="e7574-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="e7574-240">針對某些雲端資料庫 (例如： [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings)， [Azure 資料湖](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)等等)，您可能需要閘道機器上的防火牆設定 toowhitelist IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e7574-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="e7574-241">複製資料來源建立資料存放區 tooa 接收資料存放區</span><span class="sxs-lookup"><span data-stu-id="e7574-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="e7574-242">請確認正確 hello 公司防火牆，hello 閘道電腦上的 Windows 防火牆上啟用 hello 防火牆規則，然後 hello 資料存放區本身。</span><span class="sxs-lookup"><span data-stu-id="e7574-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="e7574-243">啟用這些規則允許 hello 閘道 tooconnect tooboth 來源和接收器成功。</span><span class="sxs-lookup"><span data-stu-id="e7574-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="e7574-244">啟用每個資料存放區 hello 複製作業中所包含的規則。</span><span class="sxs-lookup"><span data-stu-id="e7574-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="e7574-245">例如，從 toocopy**在內部部署資料存放區 tooan Azure SQL Database 接收或 Azure SQL 資料倉儲接收**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="e7574-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="e7574-246">在 Windows 防火牆和公司防火牆的通訊埠 **1433** 上都允許進行輸出 **TCP** 通訊。</span><span class="sxs-lookup"><span data-stu-id="e7574-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="e7574-247">設定 Azure SQL server tooadd hello IP 位址的 hello 閘道機器 toohello 清單允許的 IP 位址的 hello 防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="e7574-248">如果您的防火牆不允許使用輸出連接埠 1433，閘道將無法直接存取 Azure SQL。</span><span class="sxs-lookup"><span data-stu-id="e7574-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="e7574-249">在此情況下，您可以使用[分段複製](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy)tooSQL Azure 資料庫 / SQL Azure DW。</span><span class="sxs-lookup"><span data-stu-id="e7574-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="e7574-250">在此案例中，您只需要 hello 資料移動的 HTTPS （連接埠 443）。</span><span class="sxs-lookup"><span data-stu-id="e7574-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="e7574-251">Proxy 伺服器考量</span><span class="sxs-lookup"><span data-stu-id="e7574-251">Proxy server considerations</span></span>
<span data-ttu-id="e7574-252">如果您的公司網路環境使用 proxy 伺服器 tooaccess hello 網際網路、 設定資料管理閘道 toouse 適當的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="e7574-253">您可以在 hello 初始註冊階段期間設定 hello proxy。</span><span class="sxs-lookup"><span data-stu-id="e7574-253">You can set hello proxy during hello initial registration phase.</span></span>

![在註冊期間設定 Proxy](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="e7574-255">閘道會使用 hello proxy 伺服器 tooconnect toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e7574-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="e7574-256">進行初始設定時，按一下 [變更]  連結。</span><span class="sxs-lookup"><span data-stu-id="e7574-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="e7574-257">您會看到 hello **proxy 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e7574-257">You see hello **proxy setting** dialog.</span></span>

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="e7574-259">有三個組態選項：</span><span class="sxs-lookup"><span data-stu-id="e7574-259">There are three configuration options:</span></span>

* <span data-ttu-id="e7574-260">**不使用 proxy**： 閘道器不會明確地使用任何 proxy tooconnect toocloud 服務。</span><span class="sxs-lookup"><span data-stu-id="e7574-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="e7574-261">**使用系統 proxy**： 閘道使用的設定也就設定在 diahost.exe.config 和 diawp.exe.config hello proxy。如果沒有任何 proxy 設定 diahost.exe.config，diawp.exe.config，閘道正在連接 toocloud 服務直接而不會經過 proxy。</span><span class="sxs-lookup"><span data-stu-id="e7574-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="e7574-262">**使用自訂 proxy**： 設定閘道，而不是使用組態在 diahost.exe.config 和 diawp.exe.config hello HTTP proxy 設定 toouse。必須指定「IP 位址」和「連接埠」。</span><span class="sxs-lookup"><span data-stu-id="e7574-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="e7574-263">「使用者名稱」和「密碼」則為選擇性，需視您的 Proxy 驗證設定而定。</span><span class="sxs-lookup"><span data-stu-id="e7574-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="e7574-264">所有設定都會經過加密與 hello 閘道 hello 認證憑證，並儲存在本機 hello 閘道主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="e7574-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="e7574-265">hello 資料管理閘道主機服務會自動重新啟動之後儲存 hello 更新 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="e7574-266">閘道已成功註冊之後，如果您想要 tooview 或更新 proxy 設定之後，使用資料管理閘道組態管理員。</span><span class="sxs-lookup"><span data-stu-id="e7574-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="e7574-267">啟動 **資料管理閘道器組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="e7574-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="e7574-268">切換 toohello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e7574-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="e7574-269">按一下**變更**中連結**HTTP Proxy**區段 toolaunch hello**設定 HTTP Proxy**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e7574-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="e7574-270">按一下 hello 之後**下一步** 按鈕，您會看到警告對話方塊，詢問您的權限 toosave hello proxy 設定並重新啟動 hello 閘道器主機服務的。</span><span class="sxs-lookup"><span data-stu-id="e7574-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="e7574-271">您可以使用「組態管理員」工具來更新 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="e7574-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="e7574-273">如果您設定使用 NTLM 驗證的 proxy 伺服器時，閘道器主機服務是 hello 網域帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="e7574-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="e7574-274">如果您變更 hello 稍後 hello 網域帳戶的密碼，請記住 tooupdate hello 服務的組態設定，並據此將它重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e7574-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="e7574-275">由於 toothis 需求，我們建議使用專用的網域帳戶 tooaccess hello proxy 伺服器，不需要您 tooupdate hello 密碼經常。</span><span class="sxs-lookup"><span data-stu-id="e7574-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="e7574-276">設定 Proxy 伺服器設定</span><span class="sxs-lookup"><span data-stu-id="e7574-276">Configure proxy server settings</span></span>
<span data-ttu-id="e7574-277">如果您選取**使用系統 proxy** hello HTTP proxy 設定，閘道會使用設定 diahost.exe.config 和 diawp.exe.config 中的 hello proxy。如果 proxy 不指定 diahost.exe.config 和 diawp.exe.config，閘道正在連接 toocloud 服務直接而不會經過 proxy。</span><span class="sxs-lookup"><span data-stu-id="e7574-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="e7574-278">hello 下列程序說明如何更新 hello diahost.exe.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="e7574-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="e7574-279">在 [檔案總管] 中，製作的安全 C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared\diahost.exe.config tooback hello 原始檔。</span><span class="sxs-lookup"><span data-stu-id="e7574-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="e7574-280">以系統管理員身分啟動 Notepad.exe，並開啟文字檔 C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config。尋找 hello 預設標記的 system.net hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="e7574-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="e7574-281">然後，您可以加入 proxy 伺服器的詳細資料中 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e7574-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="e7574-282">內部 hello proxy 標記 toospecify hello 需要設定，例如 scriptLocation 允許額外的屬性。</span><span class="sxs-lookup"><span data-stu-id="e7574-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="e7574-283">請參閱太[項目 （網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx)語法。</span><span class="sxs-lookup"><span data-stu-id="e7574-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="e7574-284">到 hello 原始位置中，儲存 hello 設定檔，然後重新啟動 hello 收取 hello 變更的資料管理閘道主機服務。</span><span class="sxs-lookup"><span data-stu-id="e7574-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="e7574-285">toorestart hello 服務： 使用 [服務] 小程式從 hello [控制台] 中，或從 hello**資料管理閘道組態管理員**> 按一下 hello**停止服務**按鈕，然後按一下 hello **啟動服務**。</span><span class="sxs-lookup"><span data-stu-id="e7574-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="e7574-286">如果 hello 服務未啟動，它可能是不正確的 XML 標記語法，已加入至已編輯過的 hello 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="e7574-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7574-287">不要忘記 tooupdate**兩者**diahost.exe.config 和 diawp.exe.config。</span><span class="sxs-lookup"><span data-stu-id="e7574-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="e7574-288">此外 toothese 點，您也需要 toomake 確定 Microsoft Azure 是在貴公司的白名單中。</span><span class="sxs-lookup"><span data-stu-id="e7574-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="e7574-289">有效的 Microsoft Azure IP 位址中的 hello 清單可以下載從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="e7574-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="e7574-290">防火牆和 Proxy 伺服器相關問題的可能徵兆</span><span class="sxs-lookup"><span data-stu-id="e7574-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="e7574-291">如果您遇到下列的錯誤類似 toohello，很可能是由於 tooimproper hello 防火牆或 proxy 伺服器，它會封鎖連接 tooData Factory tooauthenticate 本身的閘道設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="e7574-292">請參閱 tooprevious 區段 tooensure 防火牆和 proxy 伺服器已正確設定。</span><span class="sxs-lookup"><span data-stu-id="e7574-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="e7574-293">當您嘗試 tooregister hello 閘道時，您會收到 hello 下列錯誤: 「 無法 tooregister hello 閘道金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7574-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="e7574-294">後再重試 tooregister hello 閘道器金鑰，確認 「 資料管理閘道處於連線狀態的 hello 與 hello 資料管理閘道主機服務已啟動的。</span><span class="sxs-lookup"><span data-stu-id="e7574-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="e7574-295">當您開啟「組態管理員」時，您會看到「已中斷連線」或「正在連接」狀態。</span><span class="sxs-lookup"><span data-stu-id="e7574-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="e7574-296">檢視 Windows 事件記錄檔，在 「 事件檢視器 」 時 > 」 應用程式及服務記錄檔"> 「 資料管理閘道 」，您會看到錯誤訊息，例如 hello 下列錯誤：`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="e7574-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="e7574-297">開啟用於認證加密的連接埠 8050</span><span class="sxs-lookup"><span data-stu-id="e7574-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="e7574-298">hello**設定認證**應用程式會使用 hello 輸入連接埠**8050** toorelay 認證 toohello 閘道當您設定在內部連結 hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="e7574-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="e7574-299">閘道在安裝期間，根據預設，hello 閘道安裝開啟它 hello 閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="e7574-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="e7574-300">如果您使用協力廠商防火牆，您可以手動開啟 hello 連接埠 8050。</span><span class="sxs-lookup"><span data-stu-id="e7574-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="e7574-301">如果在閘道安裝期間遇到防火牆問題，您可以嘗試使用下列命令 tooinstall hello 閘道，但未設定 hello 防火牆 hello。</span><span class="sxs-lookup"><span data-stu-id="e7574-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="e7574-302">如果您選擇不 tooopen hello 連接埠 8050 hello 閘道機器上的，使用機制使用 hello 以外**設定認證**應用程式 tooconfigure 資料存放區認證。</span><span class="sxs-lookup"><span data-stu-id="e7574-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="e7574-303">例如，您可以使用 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7574-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="e7574-304">如需了解如何設定資料存放區認證，請參閱 [設定認證和安全性](#set-credentials-and-securityy) 一節。</span><span class="sxs-lookup"><span data-stu-id="e7574-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="e7574-305">更新</span><span class="sxs-lookup"><span data-stu-id="e7574-305">Update</span></span>
<span data-ttu-id="e7574-306">根據預設，資料管理閘道器會自動更新 hello 閘道較新版本可用時。</span><span class="sxs-lookup"><span data-stu-id="e7574-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="e7574-307">hello 閘道才可以更新所有 hello 排程工作都已都完成。</span><span class="sxs-lookup"><span data-stu-id="e7574-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="e7574-308">沒有進一步的工作會處理 hello 閘道，直到 hello 更新作業完成。</span><span class="sxs-lookup"><span data-stu-id="e7574-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="e7574-309">如果 hello 更新失敗，閘道會復原 toohello 舊版本。</span><span class="sxs-lookup"><span data-stu-id="e7574-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="e7574-310">您會看到 hello 排定更新時間，在下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7574-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="e7574-311">hello 閘道 hello Azure 入口網站中的屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="e7574-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="e7574-312">Hello 資料管理閘道組態管理員的首頁</span><span class="sxs-lookup"><span data-stu-id="e7574-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="e7574-313">系統匣通知訊息。</span><span class="sxs-lookup"><span data-stu-id="e7574-313">System tray notification message.</span></span>

<span data-ttu-id="e7574-314">hello hello 資料管理閘道組態管理員的 [常用] 索引標籤會顯示 hello 更新排程與 hello 最後一個時間 hello 閘道已安裝/更新。</span><span class="sxs-lookup"><span data-stu-id="e7574-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![更新排程](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="e7574-316">您可以立即安裝 hello 更新，或等候 hello 閘道 toobe 在 hello 排程時間自動更新。</span><span class="sxs-lookup"><span data-stu-id="e7574-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="e7574-317">例如，hello 下列影像顯示 hello 示 hello 閘道器組態管理員，您可以按一下 tooinstall hello 更新 按鈕以及它立即通知訊息。</span><span class="sxs-lookup"><span data-stu-id="e7574-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![DMG 組態管理員中的更新](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="e7574-319">hello 系統匣中的 hello 通知訊息看起來 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="e7574-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![系統匣訊息](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="e7574-321">您看到更新作業 （手動或自動） hello 系統匣中的 hello 的狀態。</span><span class="sxs-lookup"><span data-stu-id="e7574-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="e7574-322">當您下次啟動閘道器組態管理員時，您就會看到 hello 通知列該 hello 閘道上的訊息已更新以及連結太[什麼是新主題](data-factory-gateway-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="e7574-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="e7574-323">toodisable/啟用自動更新功能</span><span class="sxs-lookup"><span data-stu-id="e7574-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="e7574-324">您可以停用/啟用 hello 自動更新 」 功能執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7574-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="e7574-325">[適用於單一節點閘道]</span><span class="sxs-lookup"><span data-stu-id="e7574-325">[For single node gateway]</span></span>
1. <span data-ttu-id="e7574-326">Hello 閘道機器上啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e7574-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="e7574-327">切換 toohello C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7574-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="e7574-328">執行下列命令 tooturn hello 自動更新的 hello 功能關閉 （停用）。</span><span class="sxs-lookup"><span data-stu-id="e7574-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="e7574-329">重新 tooturn:</span><span class="sxs-lookup"><span data-stu-id="e7574-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="e7574-330">[[適用於多重節點高度可用且可擴充的閘道 (預覽)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="e7574-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="e7574-331">Hello 閘道機器上啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e7574-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="e7574-332">切換 toohello C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7574-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="e7574-333">執行下列命令 tooturn hello 自動更新的 hello 功能關閉 （停用）。</span><span class="sxs-lookup"><span data-stu-id="e7574-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="e7574-334">對於具備高可用性功能的閘道 (預覽)，需要額外的 AuthKey 參數。</span><span class="sxs-lookup"><span data-stu-id="e7574-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="e7574-335">重新 tooturn:</span><span class="sxs-lookup"><span data-stu-id="e7574-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="e7574-336">如果您從不同於 hello 閘道機器的電腦存取 hello 入口網站，您必須確定 hello 認證管理員應用程式可以連接 toohello 閘道機器。</span><span class="sxs-lookup"><span data-stu-id="e7574-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="e7574-337">如果 hello 應用程式無法到達 hello 閘道電腦，所以不允許您 tooset hello 資料來源和 tootest 連接 toohello 資料來源的認證。</span><span class="sxs-lookup"><span data-stu-id="e7574-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="e7574-338">當您使用 hello**設定認證**應用程式，hello 入口網站 hello 認證會以加密 hello 中所指定的 hello 憑證**憑證** 索引標籤的 hello**閘道Configuration Manager** hello 閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="e7574-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="e7574-339">如果您要尋找應用程式開發介面為基礎的方法來加密 hello 認證，您可以使用 hello[新增 AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt 認證。</span><span class="sxs-lookup"><span data-stu-id="e7574-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="e7574-340">hello cmdlet 會使用該閘道是設定的 toouse tooencrypt hello 認證 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="e7574-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="e7574-341">加入加密的認證 toohello **EncryptedCredential** hello 的項目**connectionString** hello JSON 中。</span><span class="sxs-lookup"><span data-stu-id="e7574-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="e7574-342">您可以使用 hello JSON 以 hello[新增 AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet 或 hello Data Factory 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="e7574-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="e7574-343">使用「Data Factory 編輯器」來設定認證還有另一個方法。</span><span class="sxs-lookup"><span data-stu-id="e7574-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="e7574-344">如果您建立連結的 SQL Server 服務，方法是使用 hello 編輯器和您輸入認證以純文字、 hello 認證會加密使用 hello Data Factory 服務所擁有的憑證。</span><span class="sxs-lookup"><span data-stu-id="e7574-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="e7574-345">它不會使用該閘道是設定的 toouse hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="e7574-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="e7574-346">雖然這種方法在某些情況下可能快一點，但也比較不安全。</span><span class="sxs-lookup"><span data-stu-id="e7574-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="e7574-347">因此，建議您只在開發/測試用途才採用此方法。</span><span class="sxs-lookup"><span data-stu-id="e7574-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="e7574-348">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e7574-348">PowerShell cmdlets</span></span>
<span data-ttu-id="e7574-349">本章節描述如何 toocreate 並登錄閘道使用 Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7574-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="e7574-350">在系統管理員模式下啟動 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="e7574-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="e7574-351">登入 tooyour Azure 帳戶執行下列命令，並輸入您的 Azure 認證的 hello。</span><span class="sxs-lookup"><span data-stu-id="e7574-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="e7574-352">使用 hello**新增 AzureRmDataFactoryGateway** cmdlet toocreate 邏輯閘道，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e7574-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="e7574-353">**範例命令和輸出**：</span><span class="sxs-lookup"><span data-stu-id="e7574-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="e7574-354">在 Azure PowerShell 中，切換 toohello 資料夾: **C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript\**。</span><span class="sxs-lookup"><span data-stu-id="e7574-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="e7574-355">執行**RegisterGateway.ps1** hello 本機變數與相關聯**$Key** hello 下列命令所示。</span><span class="sxs-lookup"><span data-stu-id="e7574-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="e7574-356">此指令碼會註冊 hello 與 hello 您稍早建立的邏輯閘道電腦上安裝的用戶端代理程式。</span><span class="sxs-lookup"><span data-stu-id="e7574-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="e7574-357">您可以註冊 hello 閘道在遠端電腦上的使用 hello IsRegisterOnRemoteMachine 參數。</span><span class="sxs-lookup"><span data-stu-id="e7574-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="e7574-358">範例：</span><span class="sxs-lookup"><span data-stu-id="e7574-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="e7574-359">您可以使用 hello **Get AzureRmDataFactoryGateway** data factory 中的閘道 cmdlet tooget hello 清單。</span><span class="sxs-lookup"><span data-stu-id="e7574-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="e7574-360">當 hello**狀態**顯示**線上**，這表示您的閘道已準備好 toouse。</span><span class="sxs-lookup"><span data-stu-id="e7574-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="e7574-361">您可以移除閘道使用 hello**移除 AzureRmDataFactoryGateway**閘道使用 hello 的 cmdlet，並更新描述**組 AzureRmDataFactoryGateway** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7574-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="e7574-362">如需這些 Cmdlet 的語法及其他詳細資訊，請參閱 Data Factory Cmdlet 參考文件。</span><span class="sxs-lookup"><span data-stu-id="e7574-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="e7574-363">使用 PowerShell 列出閘道器</span><span class="sxs-lookup"><span data-stu-id="e7574-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="e7574-364">使用 PowerShell 移除閘道器</span><span class="sxs-lookup"><span data-stu-id="e7574-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="e7574-365">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7574-365">Next steps</span></span>
* <span data-ttu-id="e7574-366">請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="e7574-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="e7574-367">Hello 逐步解說中，您可以建立會使用內部部署 SQL Server 資料庫 tooan Azure blob 的 hello 閘道 toomove 資料管線。</span><span class="sxs-lookup"><span data-stu-id="e7574-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
