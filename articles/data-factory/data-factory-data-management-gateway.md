---
title: "Data Factory 的資料管理閘道 | Microsoft Docs"
description: "設定資料閘道器以在內部部署與雲端之間移動資料。 使用 Azure Data Factory 中的資料管理閘道移動資料。"
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
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="0fdd9-104">資料管理閘道</span><span class="sxs-lookup"><span data-stu-id="0fdd9-104">Data Management Gateway</span></span>
<span data-ttu-id="0fdd9-105">資料管理閘道是一個用戶端代理程式，您必須在內部部署環境中部署此代理程式，才能在雲端與內部部署資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-105">The Data management gateway is a client agent that you must install in your on-premises environment to copy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="0fdd9-106">如需 Data Factory 所支援的內部部署資料存放區，請參閱 [支援的資料來源](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 一節。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-106">The on-premises data stores supported by Data Factory are listed in the [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="0fdd9-107">本文是用來補充 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文中的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-107">This article complements the walkthrough in the [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0fdd9-108">在該逐步解說中，您會建立一個使用閘道將資料從內部部署 SQL Server 資料庫移到 Azure Blob 的管線。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-108">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span> <span data-ttu-id="0fdd9-109">這篇文章提供有關資料管理閘道的詳細深入資訊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-109">This article provides detailed in-depth information about the data management gateway.</span></span> 

<span data-ttu-id="0fdd9-110">您可以將多個內部部署機器關聯到閘道以相應放大資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-110">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="0fdd9-111">您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="0fdd9-112">這項功能也適用於具有單一節點的邏輯閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="0fdd9-113">如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="0fdd9-114">目前在 Data Factory 中，閘道器只支援複製活動和預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-114">Currently, gateway supports only the copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="0fdd9-115">您不能使用自訂活動中的閘道器來存取內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-115">It is not possible to use the gateway from a custom activity to access on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="0fdd9-116">概觀</span><span class="sxs-lookup"><span data-stu-id="0fdd9-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="0fdd9-117">資料管理閘道功能</span><span class="sxs-lookup"><span data-stu-id="0fdd9-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="0fdd9-118">資料管理閘道提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-118">Data management gateway provides the following capabilities:</span></span>

* <span data-ttu-id="0fdd9-119">在相同 Data Factory 內建立內部部署資料來源和雲端資料來源的模型及移動資料。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-119">Model on-premises data sources and cloud data sources within the same data factory and move data.</span></span>
* <span data-ttu-id="0fdd9-120">具有用於監視和管理的單一窗格，可從 [Data Factory] 頁面看見閘道狀態。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-120">Have a single pane of glass for monitoring and management with visibility into gateway status from the Data Factory page.</span></span>
* <span data-ttu-id="0fdd9-121">安全地管理內部部署資料來源的存取權。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-121">Manage access to on-premises data sources securely.</span></span>
  * <span data-ttu-id="0fdd9-122">不需要變更公司防火牆。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-122">No changes required to corporate firewall.</span></span> <span data-ttu-id="0fdd9-123">閘道器只會使輸出 HTTP 連線開啟網際網路。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-123">Gateway only makes outbound HTTP-based connections to open internet.</span></span>
  * <span data-ttu-id="0fdd9-124">利用您的憑證加密內部部署資料存放區的認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="0fdd9-125">有效率地移動資料 – 資料會以平行方式傳輸，且系統會採用自動重試邏輯，修復間歇性網路問題。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-125">Move data efficiently – data is transferred in parallel, resilient to intermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="0fdd9-126">命令流程和資料流程</span><span class="sxs-lookup"><span data-stu-id="0fdd9-126">Command flow and data flow</span></span>
<span data-ttu-id="0fdd9-127">當您使用複製活動在內部部署與雲端之間複製資料時，該活動會使用閘道將資料從內部部署資料來源轉移到雲端，以及反向操作。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-127">When you use a copy activity to copy data between on-premises and cloud, the activity uses a gateway to transfer data from on-premises data source to cloud and vice versa.</span></span>

<span data-ttu-id="0fdd9-128">利用資料閘道來進行複製的高階資料流程和步驟摘要如下：![使用閘道的資料流程](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="0fdd9-128">Here is the high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="0fdd9-129">資料開發人員會使用 [Azure 入口網站](https://portal.azure.com)或 [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx)，為 Azure Data Factory 建立閘道器。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-129">Data developer creates a gateway for an Azure Data Factory using either the [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="0fdd9-130">資料開發人員會藉由指定閘道，建立內部部署資料存放區的連結服務。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-130">Data developer creates a linked service for an on-premises data store by specifying the gateway.</span></span> <span data-ttu-id="0fdd9-131">在設定連結服務資料的過程中，開發人員會使用 [設定認證] 應用程式來指定驗證類型和認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-131">As part of setting up the linked service, data developer uses the Setting Credentials application to specify authentication types and credentials.</span></span>  <span data-ttu-id="0fdd9-132">[設定認證] 應用程式對話方塊將會與資料存放區進行通訊，以測試要儲存認證的連線與閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-132">The Setting Credentials application dialog communicates with the data store to test connection and the gateway to save credentials.</span></span>
3. <span data-ttu-id="0fdd9-133">在雲端中儲存認證之前，閘道會利用與閘道 (由資料開發人員提供) 相關聯的憑證加密認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-133">Gateway encrypts the credentials with the certificate associated with the gateway (supplied by data developer), before saving the credentials in the cloud.</span></span>
4. <span data-ttu-id="0fdd9-134">Data Factory 服務會和閘道進行通訊，以透過使用共用 Azure 服務匯流排佇列的控制通道，進行工作的排程和管理。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-134">Data Factory service communicates with the gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="0fdd9-135">必須開始複製活動作業時，Data Factory 會將要求和認證資訊一起排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-135">When a copy activity job needs to be kicked off, Data Factory queues the request along with credential information.</span></span> <span data-ttu-id="0fdd9-136">輪詢佇列之後，閘道器隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-136">Gateway kicks off the job after polling the queue.</span></span>
5. <span data-ttu-id="0fdd9-137">閘道會利用相同的憑證解密認證，然後利用適當的驗證類型和認證連接到內部部署資料存放區。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-137">The gateway decrypts the credentials with the same certificate and then connects to the on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="0fdd9-138">閘道會根據「複製活動」在資料管線中的設定方式，將資料從內部部署存放區複製到雲端儲存體，或反向操作。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-138">The gateway copies data from an on-premises store to a cloud storage, or vice versa depending on how the Copy Activity is configured in the data pipeline.</span></span> <span data-ttu-id="0fdd9-139">針對這個步驟，閘道會透過安全的 (HTTPS) 通道，直接與雲端式儲存體服務 (例如 Azure Blob 儲存體) 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-139">For this step, the gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="0fdd9-140">使用閘道的考量</span><span class="sxs-lookup"><span data-stu-id="0fdd9-140">Considerations for using gateway</span></span>
* <span data-ttu-id="0fdd9-141">您可以將單一資料管理閘道執行個體用於多個內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="0fdd9-142">不過， **單一閘道執行個體只會繫結至一個 Azure Data Factory** ，不能與另一個 Data Factory 共用。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-142">However, **a single gateway instance is tied to only one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="0fdd9-143">單一電腦上**只能安裝一個資料管理閘道的執行個體**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="0fdd9-144">假設您有兩個需要存取內部部署資料來源的 Data Factory，您就需要在兩部內部部署電腦上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-144">Suppose, you have two data factories that need to access on-premises data sources, you need to install gateways on two on-premises computers.</span></span> <span data-ttu-id="0fdd9-145">換句話說，閘道會繫結至特定的 Data Factory</span><span class="sxs-lookup"><span data-stu-id="0fdd9-145">In other words, a gateway is tied to a specific data factory</span></span>
* <span data-ttu-id="0fdd9-146">**閘道不一定要在與資料來源相同的電腦上**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-146">The **gateway does not need to be on the same machine as the data source**.</span></span> <span data-ttu-id="0fdd9-147">不過，讓閘道較靠近資料來源可縮短閘道連線到資料來源的時間。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-147">However, having gateway closer to the data source reduces the time for the gateway to connect to the data source.</span></span> <span data-ttu-id="0fdd9-148">建議您將閘道安裝在與裝載內部部署資料來源的機器不同的機器上。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-148">We recommend that you install the gateway on a machine that is different from the one that hosts on-premises data source.</span></span> <span data-ttu-id="0fdd9-149">當閘道和資料來源位於不同的機器上時，閘道才不會與資料來源爭奪資源。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-149">When the gateway and data source are on different machines, the gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="0fdd9-150">您可以有「多個閘道器在不同電腦上，但連接至相同的內部部署資料來源」 。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-150">You can have **multiple gateways on different machines connecting to the same on-premises data source**.</span></span> <span data-ttu-id="0fdd9-151">例如，您可能有兩個閘道器用於服務兩個 Data Factory，但相同的內部部署資料來源都向這兩個 Data Factory 註冊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-151">For example, you may have two gateways serving two data factories but the same on-premises data source is registered with both the data factories.</span></span>
* <span data-ttu-id="0fdd9-152">若您已在電腦上安裝用於 **Power BI** 案例的閘道器，請於另一台電腦上安裝**另一個用於 Azure Data Factory 的閘道器**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="0fdd9-153">即使您使用 **ExpressRoute**，也必須使用閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="0fdd9-154">即使您使用 **ExpressRoute**，也應該將資料來源視為內部部署資料來源 (亦即在防火牆後面)。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="0fdd9-155">請使用閘道來建立服務與資料來源之間的連線。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-155">Use the gateway to establish connectivity between the service and the data source.</span></span>
* <span data-ttu-id="0fdd9-156">您必須**使用閘道**，即使資料存放區位於 **Azure IaaS VM** 上的雲端中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-156">You must **use the gateway** even if the data store is in the cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="0fdd9-157">安裝</span><span class="sxs-lookup"><span data-stu-id="0fdd9-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0fdd9-158">必要條件</span><span class="sxs-lookup"><span data-stu-id="0fdd9-158">Prerequisites</span></span>
* <span data-ttu-id="0fdd9-159">支援的 **作業系統** 版本包括 Windows 7、Windows 8/8.1、Windows 10、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-159">The supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="0fdd9-160">目前不支援在網域控制站上安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-160">Installation of the data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="0fdd9-161">必須有 .NET Framework 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="0fdd9-162">如果您要在 Windows 7 電腦上安裝閘道，請安裝 .NET Framework 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="0fdd9-163">如需詳細資訊，請參閱 [.NET Framework 系統需求](https://msdn.microsoft.com/library/8z6watww.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="0fdd9-164">建議的閘道機器「組態」  為至少 2 GHz、4 核心、8 GB RAM 和 80 GB 磁碟。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-164">The recommended **configuration** for the gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="0fdd9-165">如果主機電腦休眠，閘道器不會回應資料要求。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-165">If the host machine hibernates, the gateway does not respond to data requests.</span></span> <span data-ttu-id="0fdd9-166">因此，安裝閘道器之前，請先在電腦上設定適當的「電源計劃」  。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-166">Therefore, configure an appropriate **power plan** on the computer before installing the gateway.</span></span> <span data-ttu-id="0fdd9-167">如果電腦已設定為休眠，安裝閘道時會提示訊息。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-167">If the machine is configured to hibernate, the gateway installation prompts a message.</span></span>
* <span data-ttu-id="0fdd9-168">您必須是電腦上的系統管理員，才能成功安裝和設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-168">You must be an administrator on the machine to install and configure the data management gateway successfully.</span></span> <span data-ttu-id="0fdd9-169">您可以將其他使用者新增至**資料管理閘道使用者**本機 Windows 群組。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-169">You can add additional users to the **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="0fdd9-170">此群組的成員可以使用**資料管理閘道組態管理員**工具來設定閘道器。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-170">The members of this group are able to use the **Data Management Gateway Configuration Manager** tool to configure the gateway.</span></span>

<span data-ttu-id="0fdd9-171">因為複製活動執行會以特定的頻率發生，在電腦上的資源使用量 (CPU、記憶體) 也會遵循與尖峰和閒置時間相同的模式。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-171">As copy activity runs happen on a specific frequency, the resource usage (CPU, memory) on the machine also follows the same pattern with peak and idle times.</span></span> <span data-ttu-id="0fdd9-172">資源使用率也仰賴要移動的資料量。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-172">Resource utilization also depends heavily on the amount of data being moved.</span></span> <span data-ttu-id="0fdd9-173">如果有多個複製作業正在進行，您會看到資源使用量在尖峰時段增加。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="0fdd9-174">安裝選項</span><span class="sxs-lookup"><span data-stu-id="0fdd9-174">Installation options</span></span>
<span data-ttu-id="0fdd9-175">可以用下列方式安裝資料管理閘道：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-175">Data management gateway can be installed in the following ways:</span></span>

* <span data-ttu-id="0fdd9-176">從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=39717)下載 MSI 安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-176">By downloading an MSI setup package from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="0fdd9-177">MSI 也可用來將現有的資料管理閘道升級至最新的版本，並保留所有設定。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-177">The MSI can also be used to upgrade existing data management gateway to the latest version, with all settings preserved.</span></span>
* <span data-ttu-id="0fdd9-178">按一下 [手動設定] 底下的 [下載並安裝資料閘道] 連結，或 [快速安裝] 之下的 [直接安裝在此電腦上]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="0fdd9-179">如需使用快速安裝的逐步指示，請參閱 [在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="0fdd9-180">手動步驟會帶您前往下載中心。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-180">The manual step takes you to the download center.</span></span>  <span data-ttu-id="0fdd9-181">下一節會提供從下載中心下載並安裝閘道的指示。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-181">The instructions for downloading and installing the gateway from download center are in the next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="0fdd9-182">安裝最佳作法：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-182">Installation best practices:</span></span>
1. <span data-ttu-id="0fdd9-183">為閘道器設定主機電腦上的電源計劃，使電腦不休眠。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-183">Configure power plan on the host machine for the gateway so that the machine does not hibernate.</span></span> <span data-ttu-id="0fdd9-184">如果主機電腦休眠，閘道器不會回應資料要求。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-184">If the host machine hibernates, the gateway does not respond to data requests.</span></span>
2. <span data-ttu-id="0fdd9-185">請備份與閘道器相關聯的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-185">Back up the certificate associated with the gateway.</span></span>

### <a name="install-the-gateway-from-download-center"></a><span data-ttu-id="0fdd9-186">從下載中心安裝閘道</span><span class="sxs-lookup"><span data-stu-id="0fdd9-186">Install the gateway from download center</span></span>
1. <span data-ttu-id="0fdd9-187">瀏覽至 [Microsoft 資料管理閘道下載頁面](https://www.microsoft.com/download/details.aspx?id=39717)。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-187">Navigate to [Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="0fdd9-188">按一下 [下載]，選取適當的版本 (**32 位元**與**64 位元**)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-188">Click **Download**, select the appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="0fdd9-189">直接執行 **MSI** 或將它儲存至您的硬碟並執行。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-189">Run the **MSI** directly or save it to your hard disk and run.</span></span>
4. <span data-ttu-id="0fdd9-190">在 [歡迎] 頁面上，選取一個**語言**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-190">On the **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="0fdd9-191">**接受**使用者授權合約，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-191">**Accept** the End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="0fdd9-192">選取要安裝閘道的**資料夾**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-192">Select **folder** to install the gateway and click **Next**.</span></span>
7. <span data-ttu-id="0fdd9-193">在 [準備安裝] 頁面上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-193">On the **Ready to install** page, click **Install**.</span></span>
8. <span data-ttu-id="0fdd9-194">按一下 [完成]  來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-194">Click **Finish** to complete installation.</span></span>
9. <span data-ttu-id="0fdd9-195">從 Azure 入口網站取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-195">Get the key from the Azure portal.</span></span> <span data-ttu-id="0fdd9-196">如需逐步指示，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-196">See the next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="0fdd9-197">在您機器上執行的**資料管理閘道組態管理員**中的 [註冊閘道器] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-197">On the **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do the following steps:</span></span>
    1. <span data-ttu-id="0fdd9-198">將金鑰貼在文字中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-198">Paste the key in the text.</span></span>
    2. <span data-ttu-id="0fdd9-199">(選擇性) 按一下 [顯示閘道器金鑰]  以查看金鑰文字。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-199">Optionally, click **Show gateway key** to see the key text.</span></span>
    3. <span data-ttu-id="0fdd9-200">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="0fdd9-201">使用金鑰註冊閘道</span><span class="sxs-lookup"><span data-stu-id="0fdd9-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a><span data-ttu-id="0fdd9-202">如果您尚未在入口網站中建立邏輯閘道</span><span class="sxs-lookup"><span data-stu-id="0fdd9-202">If you haven't already created a logical gateway in the portal</span></span>
<span data-ttu-id="0fdd9-203">若要在入口網站中建立閘道並從 [設定] 頁面取得金鑰，請依照[在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)一文中的逐步解說步驟操作。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-203">To create a gateway in the portal and get the key from the **Configure** page, Follow steps from walkthrough in the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a><span data-ttu-id="0fdd9-204">如果您已經在入口網站中建立邏輯閘道</span><span class="sxs-lookup"><span data-stu-id="0fdd9-204">If you have already created the logical gateway in the portal</span></span>
1. <span data-ttu-id="0fdd9-205">在 Azure 入口網站中，瀏覽至 [Data Factory] 頁面，然後按一下 [連結服務] 圖格。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-205">In Azure portal, navigate to the **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Data Factory 頁面](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="0fdd9-207">在 [已連結的服務] 頁面中，選取您在入口網站中建立的邏輯**閘道**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-207">In the **Linked Services** page, select the logical **gateway** you created in the portal.</span></span>

    ![邏輯閘道](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="0fdd9-209">在 [資料閘道] 頁面中，按一下 [下載並安裝資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-209">In the **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![入口網站中的下載連結](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="0fdd9-211">在 [設定] 頁面中，按一下 [重新建立金鑰]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-211">In the **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="0fdd9-212">在仔細閱讀警告訊息後，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-212">Click Yes on the warning message after reading it carefully.</span></span>

    ![重新建立索引鍵](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="0fdd9-214">按一下金鑰旁的 [複製] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-214">Click Copy button next to the key.</span></span> <span data-ttu-id="0fdd9-215">金鑰會複製到剪貼簿中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-215">The key is copied to the clipboard.</span></span>

    ![複製金鑰](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="0fdd9-217">系統匣圖示/通知</span><span class="sxs-lookup"><span data-stu-id="0fdd9-217">System tray icons/ notifications</span></span>
<span data-ttu-id="0fdd9-218">下圖顯示您會看到的某些系統匣圖示。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-218">The following image shows some of the tray icons that you see.</span></span>

![系統匣圖示](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="0fdd9-220">如果您將游標放在系統匣圖示/通知訊息上，您會在快顯視窗中看到閘道/更新作業的狀態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-220">If you move cursor over the system tray icon/notification message, you see details about the state of the gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="0fdd9-221">連接埠和防火牆</span><span class="sxs-lookup"><span data-stu-id="0fdd9-221">Ports and firewall</span></span>
<span data-ttu-id="0fdd9-222">有兩個您需要考量的防火牆：在組織的中央路由器上執行的**公司防火牆**，以及在已安裝閘道的本機電腦上設定為精靈的 **Windows 防火牆**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-222">There are two firewalls you need to consider: **corporate firewall** running on the central router of the organization, and **Windows firewall** configured as a daemon on the local machine where the gateway is installed.</span></span>  

![防火牆](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="0fdd9-224">在公司防火牆層級，您需要設定下列網域和輸出連接埠：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-224">At corporate firewall level, you need configure the following domains and outbound ports:</span></span>

| <span data-ttu-id="0fdd9-225">網域名稱</span><span class="sxs-lookup"><span data-stu-id="0fdd9-225">Domain names</span></span> | <span data-ttu-id="0fdd9-226">連接埠</span><span class="sxs-lookup"><span data-stu-id="0fdd9-226">Ports</span></span> | <span data-ttu-id="0fdd9-227">說明</span><span class="sxs-lookup"><span data-stu-id="0fdd9-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0fdd9-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="0fdd9-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="0fdd9-229">443、80</span><span class="sxs-lookup"><span data-stu-id="0fdd9-229">443, 80</span></span> |<span data-ttu-id="0fdd9-230">用於與「資料移動服務」後端進行通訊</span><span class="sxs-lookup"><span data-stu-id="0fdd9-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="0fdd9-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="0fdd9-231">*.core.windows.net</span></span> |<span data-ttu-id="0fdd9-232">443</span><span class="sxs-lookup"><span data-stu-id="0fdd9-232">443</span></span> |<span data-ttu-id="0fdd9-233">用於使用 Azure Blob 的分段複製 (如果已設定)</span><span class="sxs-lookup"><span data-stu-id="0fdd9-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="0fdd9-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="0fdd9-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="0fdd9-235">443</span><span class="sxs-lookup"><span data-stu-id="0fdd9-235">443</span></span> |<span data-ttu-id="0fdd9-236">用於與「資料移動服務」後端進行通訊</span><span class="sxs-lookup"><span data-stu-id="0fdd9-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="0fdd9-237">Windows 防火牆層級通常會啟用這些輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="0fdd9-238">如果沒有，您可以在閘道電腦上相應地設定網域和連接埠。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-238">If not, you can configure the domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="0fdd9-239">視您的來源/接收器而定，您可能需要將額外的網域和輸出連接埠加到您公司/Windows 防火牆的白名單中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-239">Based on your source/ sinks, you may have to whitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="0fdd9-240">對於某些雲端資料庫 (例如：[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings)、[Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access) 等)，您可能需要將閘道電腦的 IP 位址加到其防火牆組態的白名單中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need to whitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a><span data-ttu-id="0fdd9-241">將資料從來源資料存放區複製到接收資料存放區</span><span class="sxs-lookup"><span data-stu-id="0fdd9-241">Copy data from a source data store to a sink data store</span></span>
<span data-ttu-id="0fdd9-242">請確定在公司防火牆、閘道機器上的 Windows 防火牆及資料存放區本身都已正確啟用防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-242">Ensure that the firewall rules are enabled properly on the corporate firewall, Windows firewall on the gateway machine, and the data store itself.</span></span> <span data-ttu-id="0fdd9-243">啟用這些規則可讓閘道成功連接到來源和接收器。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-243">Enabling these rules allows the gateway to connect to both source and sink successfully.</span></span> <span data-ttu-id="0fdd9-244">請為複製作業所涉及的每個資料存放區啟用規則。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-244">Enable rules for each data store that is involved in the copy operation.</span></span>

<span data-ttu-id="0fdd9-245">例如，若要 **從內部部署資料存放區複製到 Azure SQL Database 接收器或 Azure SQL 資料倉儲接收器**，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="0fdd9-245">For example, to copy from **an on-premises data store to an Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do the following steps:</span></span>

* <span data-ttu-id="0fdd9-246">在 Windows 防火牆和公司防火牆的通訊埠 **1433** 上都允許進行輸出 **TCP** 通訊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="0fdd9-247">設定 Azure SQL 伺服器的防火牆設定，將閘道機器的 IP 位址新增到允許的 IP 位址清單中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-247">Configure the firewall settings of Azure SQL server to add the IP address of the gateway machine to the list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="0fdd9-248">如果您的防火牆不允許使用輸出連接埠 1433，閘道將無法直接存取 Azure SQL。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="0fdd9-249">在此情況下，您可以使用[分段複製](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy)來移到 SQL Azure Database/SQL Azure DW。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) to SQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="0fdd9-250">在此案例中，您只需要 HTTPS (連接埠 443) 即可進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-250">In this scenario, you would only require HTTPS (port 443) for the data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="0fdd9-251">Proxy 伺服器考量</span><span class="sxs-lookup"><span data-stu-id="0fdd9-251">Proxy server considerations</span></span>
<span data-ttu-id="0fdd9-252">如果您的公司網路環境使用 Proxy 伺服器來存取網際網路，請將資料管理閘道設定為使用適當的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-252">If your corporate network environment uses a proxy server to access the internet, configure data management gateway to use appropriate proxy settings.</span></span> <span data-ttu-id="0fdd9-253">您可以在初始註冊階段期間設定 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-253">You can set the proxy during the initial registration phase.</span></span>

![在註冊期間設定 Proxy](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="0fdd9-255">閘道會使用 Proxy 伺服器來連線到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-255">Gateway uses the proxy server to connect to the cloud service.</span></span> <span data-ttu-id="0fdd9-256">進行初始設定時，按一下 [變更]  連結。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="0fdd9-257">您會看到 [Proxy 設定]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-257">You see the **proxy setting** dialog.</span></span>

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="0fdd9-259">有三個組態選項：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-259">There are three configuration options:</span></span>

* <span data-ttu-id="0fdd9-260">**不使用 Proxy**︰閘道不會明確地使用任何 Proxy 來連線到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-260">**Do not use proxy**: Gateway does not explicitly use any proxy to connect to cloud services.</span></span>
* <span data-ttu-id="0fdd9-261">**使用系統 Proxy**：閘道會使用 diahost.exe.config 和 diawp.exe.config 中設定的 Proxy 設定。如果 diahost.exe.config 和 diawp.exe.config 中未設定任何 Proxy，閘道就會直接連線到雲端服務而不經由 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-261">**Use system proxy**: Gateway uses the proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span>
* <span data-ttu-id="0fdd9-262">**使用自訂 Proxy**：設定要用於閘道的 HTTP Proxy 設定，而不使用 diahost.exe.config 和 diawp.exe.config 中的組態。必須指定「IP 位址」和「連接埠」。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-262">**Use custom proxy**: Configure the HTTP proxy setting to use for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="0fdd9-263">「使用者名稱」和「密碼」則為選擇性，需視您的 Proxy 驗證設定而定。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="0fdd9-264">所有設定都會由閘道的認證憑證予以加密，並儲存在閘道主機機器的本機。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-264">All settings are encrypted with the credential certificate of the gateway and stored locally on the gateway host machine.</span></span>

<span data-ttu-id="0fdd9-265">在您儲存已更新的 Proxy 設定之後，資料管理閘道主機服務會自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-265">The data management gateway Host Service restarts automatically after you save the updated proxy settings.</span></span>

<span data-ttu-id="0fdd9-266">在成功註冊閘道之後，如果您想要檢視或更新 Proxy 設定，請使用「資料管理閘道組態管理員」。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-266">After gateway has been successfully registered, if you want to view or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="0fdd9-267">啟動 **資料管理閘道器組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="0fdd9-268">切換到 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-268">Switch to the **Settings** tab.</span></span>
3. <span data-ttu-id="0fdd9-269">按一下 [HTTP Proxy] 區段中的 [變更] 連結，以啟動 [設定 HTTP Proxy] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-269">Click **Change** link in **HTTP Proxy** section to launch the **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="0fdd9-270">按 [下一步]  按鈕之後，您會看到一個警告對話方塊，此對話方塊會向您請求權限來儲存 Proxy 設定及重新啟動「閘道主機服務」。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-270">After you click the **Next** button, you see a warning dialog asking for your permission to save the proxy setting and restart the Gateway Host Service.</span></span>

<span data-ttu-id="0fdd9-271">您可以使用「組態管理員」工具來更新 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="0fdd9-273">如果您為 Proxy 伺服器設定了 NTLM 驗證，「閘道主機服務」就會以網域帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under the domain account.</span></span> <span data-ttu-id="0fdd9-274">如果您稍後變更網域帳戶的密碼，請記得更新服務的組態設定並相應地將它重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-274">If you change the password for the domain account later, remember to update configuration settings for the service and restart it accordingly.</span></span> <span data-ttu-id="0fdd9-275">基於這項需求，建議您使用不需要經常更新密碼的專用網域帳戶來存取 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-275">Due to this requirement, we suggest you use a dedicated domain account to access the proxy server that does not require you to update the password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="0fdd9-276">設定 Proxy 伺服器設定</span><span class="sxs-lookup"><span data-stu-id="0fdd9-276">Configure proxy server settings</span></span>
<span data-ttu-id="0fdd9-277">如果您為 HTTP Proxy 選取 [使用系統 Proxy] 設定，閘道就會使用 diahost.exe.config 和 diawp.exe.config 中的 Proxy 設定。如果 diahost.exe.config 和 diawp.exe.config 中未指定任何 Proxy，閘道就會直接連線到雲端服務而不經由 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-277">If you select **Use system proxy** setting for the HTTP proxy, gateway uses the proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span> <span data-ttu-id="0fdd9-278">下列程序說明如何更新 diahost.exe.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-278">The following procedure provides instructions for updating the diahost.exe.config file.</span></span>  

1. <span data-ttu-id="0fdd9-279">在「檔案總管」中，建立一份 C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config 的安全複本來備份原始檔案。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config to back up the original file.</span></span>
2. <span data-ttu-id="0fdd9-280">以系統管理員身分啟動 Notepad.exe，並開啟文字檔 C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config。您會在以下程式碼中看見 system.net 的預設標籤：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find the default tag for system.net as shown in the following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="0fdd9-281">接著，您可以新增 Proxy 伺服器詳細資料，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-281">You can then add proxy server details as shown in the following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="0fdd9-282">在 Proxy 標記內可以有其他屬性，用以指定必要的設定，例如 scriptLocation。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-282">Additional properties are allowed inside the proxy tag to specify the required settings like scriptLocation.</span></span> <span data-ttu-id="0fdd9-283">請參閱 [Proxy 項目 (網路設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) 以了解語法。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-283">Refer to [proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="0fdd9-284">將組態檔儲存到原始位置中，然後重新啟動「資料管理閘道主機服務」以套用變更。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-284">Save the configuration file into the original location, then restart the Data Management Gateway Host service, which picks up the changes.</span></span> <span data-ttu-id="0fdd9-285">重新啟動服務：使用 [控制台] 中的 [服務] 小程式，或是從 [資料管理閘道組態管理員] > 按一下 [停止服務] 按鈕，然後按一下 [啟動服務]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-285">To restart the service: use services applet from the control panel, or from the **Data Management Gateway Configuration Manager** > click the **Stop Service** button, then click the **Start Service**.</span></span> <span data-ttu-id="0fdd9-286">如果服務未啟動，可能因為在已編輯的應用程式組態檔中加入了不正確的 XML 標記語法。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-286">If the service does not start, it is likely that an incorrect XML tag syntax has been added into the application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fdd9-287">別忘了「同時」更新 diahost.exe.config 和 diawp.exe.config。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-287">Do not forget to update **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="0fdd9-288">除了這幾點以外，您也必須確定 Microsoft Azure 包含在公司的允許清單中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-288">In addition to these points, you also need to make sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="0fdd9-289">如需有效的 Microsoft Azure IP 位址清單，可從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=41653)下載。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-289">The list of valid Microsoft Azure IP addresses can be downloaded from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="0fdd9-290">防火牆和 Proxy 伺服器相關問題的可能徵兆</span><span class="sxs-lookup"><span data-stu-id="0fdd9-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="0fdd9-291">如果發生類似以下的錯誤，有可能是因為防火牆或 Proxy 伺服器的組態不正確，使得閘道無法連線到 Data Factory 來進行自我驗證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-291">If you encounter errors similar to the following ones, it is likely due to improper configuration of the firewall or proxy server, which blocks gateway from connecting to Data Factory to authenticate itself.</span></span> <span data-ttu-id="0fdd9-292">請參閱上一節，以確保您的防火牆和 Proxy 伺服器的設定皆正確。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-292">Refer to previous section to ensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="0fdd9-293">當您嘗試註冊閘道器時，您會收到下列錯誤：「無法註冊閘道器金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-293">When you try to register the gateway, you receive the following error: "Failed to register the gateway key.</span></span> <span data-ttu-id="0fdd9-294">再次嘗試註冊閘道器金鑰之前，請確認資料管理閘道已處於連線狀態，且已啟動資料管理閘道主機服務。」</span><span class="sxs-lookup"><span data-stu-id="0fdd9-294">Before trying to register the gateway key again, confirm that the data management gateway is in a connected state and the Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="0fdd9-295">當您開啟「組態管理員」時，您會看到「已中斷連線」或「正在連接」狀態。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="0fdd9-296">檢視 Windows 事件記錄檔時，在 [事件檢視器] > [應用程式和服務記錄檔] > [資料管理閘道] 下，您會看到如以下的錯誤訊息：`Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="0fdd9-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as the following error: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="0fdd9-297">開啟用於認證加密的連接埠 8050</span><span class="sxs-lookup"><span data-stu-id="0fdd9-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="0fdd9-298">當您在 Azure 入口網站中設定了內部部署連結服務時，**設定認證**應用程式會使用輸入連接埠 **8050** 將認證轉送到閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-298">The **Setting Credentials** application uses the inbound port **8050** to relay credentials to the gateway when you set up an on-premises linked service in the Azure portal.</span></span> <span data-ttu-id="0fdd9-299">閘道設定期間，閘道安裝預設會在閘道電腦上開啟此連接埠。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-299">During gateway setup, by default, the gateway installation opens it on the gateway machine.</span></span>

<span data-ttu-id="0fdd9-300">如果您使用協力廠商的防火牆，則可以手動開啟連接埠 8050。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-300">If you are using a third-party firewall, you can manually open the port 8050.</span></span> <span data-ttu-id="0fdd9-301">如果您在設定閘道時遇到防火牆問題，您可以嘗試使用下列命令來安裝閘道，而不設定防火牆。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-301">If you run into firewall issue during gateway setup, you can try using the following command to install the gateway without configuring the firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="0fdd9-302">如果您選擇不開啟閘道機器上的連接埠 8050，則請使用「設定認證」  應用程式以外的機制來設定資料存放區認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-302">If you choose not to open the port 8050 on the gateway machine, use mechanisms other than using the **Setting Credentials** application to configure data store credentials.</span></span> <span data-ttu-id="0fdd9-303">例如，您可以使用 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="0fdd9-304">如需了解如何設定資料存放區認證，請參閱 [設定認證和安全性](#set-credentials-and-securityy) 一節。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="0fdd9-305">更新</span><span class="sxs-lookup"><span data-stu-id="0fdd9-305">Update</span></span>
<span data-ttu-id="0fdd9-306">根據預設，資料管理閘道會在有更新版本的閘道時自動進行更新。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-306">By default, data management gateway is automatically updated when a newer version of the gateway is available.</span></span> <span data-ttu-id="0fdd9-307">在所有排定的工作完成前，閘道不會進行更新。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-307">The gateway is not updated until all the scheduled tasks are done.</span></span> <span data-ttu-id="0fdd9-308">更新作業完成後，閘道才會處理後續的工作。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-308">No further tasks are processed by the gateway until the update operation is completed.</span></span> <span data-ttu-id="0fdd9-309">如果更新失敗，閘道會回復為舊版本。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-309">If the update fails, gateway is rolled back to the old version.</span></span>

<span data-ttu-id="0fdd9-310">您會在下列位置看到已排定的更新時間︰</span><span class="sxs-lookup"><span data-stu-id="0fdd9-310">You see the scheduled update time in the following places:</span></span>

* <span data-ttu-id="0fdd9-311">Azure 入口網站中的 [閘道屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-311">The gateway properties page in the Azure portal.</span></span>
* <span data-ttu-id="0fdd9-312">「資料管理閘道組態管理員」的 [首頁]。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-312">Home page of the Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="0fdd9-313">系統匣通知訊息。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-313">System tray notification message.</span></span>

<span data-ttu-id="0fdd9-314">「資料管理閘道組態管理員」的 [首頁] 索引標籤會顯示更新排程，以及上次安裝/更新閘道的時間。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-314">The Home tab of the Data Management Gateway Configuration Manager displays the update schedule and the last time the gateway was installed/updated.</span></span>

![更新排程](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="0fdd9-316">您可以立即安裝更新，或等候閘道在排定時間自動更新。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-316">You can install the update right away or wait for the gateway to be automatically updated at the scheduled time.</span></span> <span data-ttu-id="0fdd9-317">例如，下圖顯示的是「閘道組態管理員」中所顯示的通知訊息以及 [更新] 按鈕，按一下此按鈕即可立即安裝更新。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-317">For example, the following image shows you the notification message shown in the Gateway Configuration Manager along with the Update button that you can click to install it immediately.</span></span>

![DMG 組態管理員中的更新](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="0fdd9-319">系統匣中的通知訊息看起來就像下圖：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-319">The notification message in the system tray would look as shown in the following image:</span></span>

![系統匣訊息](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="0fdd9-321">您會在系統匣中看到更新作業 (手動或自動) 的狀態。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-321">You see the status of update operation (manual or automatic) in the system tray.</span></span> <span data-ttu-id="0fdd9-322">下次啟動「閘道組態管理員」時，您會在通知列上看到指出閘道已更新的訊息，以及一個連到 [新功能主題](data-factory-gateway-release-notes.md)的連結。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-322">When you launch Gateway Configuration Manager next time, you see a message on the notification bar that the gateway has been updated along with a link to [what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="to-disableenable-auto-update-feature"></a><span data-ttu-id="0fdd9-323">停用/啟用自動更新功能</span><span class="sxs-lookup"><span data-stu-id="0fdd9-323">To disable/enable auto-update feature</span></span>
<span data-ttu-id="0fdd9-324">您可以執行下列步驟來停用/啟用自動更新功能：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-324">You can disable/enable the auto-update feature by doing the following steps:</span></span>

<span data-ttu-id="0fdd9-325">[適用於單一節點閘道]</span><span class="sxs-lookup"><span data-stu-id="0fdd9-325">[For single node gateway]</span></span>
1. <span data-ttu-id="0fdd9-326">在閘道電腦上啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-326">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="0fdd9-327">切換至 C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-327">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="0fdd9-328">執行下列命令，將自動更新功能關閉 (停用)。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-328">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="0fdd9-329">若要將它重新開啟：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-329">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="0fdd9-330">[[適用於多重節點高度可用且可擴充的閘道 (預覽)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="0fdd9-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="0fdd9-331">在閘道電腦上啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-331">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="0fdd9-332">切換至 C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-332">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="0fdd9-333">執行下列命令，將自動更新功能關閉 (停用)。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-333">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="0fdd9-334">對於具備高可用性功能的閘道 (預覽)，需要額外的 AuthKey 參數。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="0fdd9-335">若要將它重新開啟：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-335">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

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
<span data-ttu-id="0fdd9-336">如果您從閘道器電腦以外的另一台電腦存取入口網站，您必須確定「認證管理員」應用程式可以連接到閘道器電腦。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-336">If you access the portal from a machine that is different from the gateway machine, you must make sure that the Credentials Manager application can connect to the gateway machine.</span></span> <span data-ttu-id="0fdd9-337">如果應用程式無法連接閘道器電腦，它不會允許您設定資料來源的認證，以及測試資料來源的連接。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-337">If the application cannot reach the gateway machine, it does not allow you to set credentials for the data source and to test connection to the data source.</span></span>  

<span data-ttu-id="0fdd9-338">當您使用**設定認證**應用程式時，入口網站會使用在閘道機器上**閘道組態管理員**的 [憑證] 索引標籤中指定的憑證來加密認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-338">When you use the **Setting Credentials** application, the portal encrypts the credentials with the certificate specified in the **Certificate** tab of the **Gateway Configuration Manager** on the gateway machine.</span></span>

<span data-ttu-id="0fdd9-339">如果您要尋找以 API 為基礎的方法來加密認證，可以使用 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell Cmdlet 來加密認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-339">If you are looking for an API-based approach for encrypting the credentials, you can use the [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet to encrypt credentials.</span></span> <span data-ttu-id="0fdd9-340">此 cmdlet 會使用閘道器設定用來加密認證的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-340">The cmdlet uses the certificate that gateway is configured to use to encrypt the credentials.</span></span> <span data-ttu-id="0fdd9-341">您需將加密認證新增到 JSON 中 **connectionString** 的 **EncryptedCredential** 元素中。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-341">You add encrypted credentials to the **EncryptedCredential** element of the **connectionString** in the JSON.</span></span> <span data-ttu-id="0fdd9-342">您需搭配 [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) Cmdlet 或在「Data Factory 編輯器」中使用 JSON。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-342">You use the JSON with the [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in the Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="0fdd9-343">使用「Data Factory 編輯器」來設定認證還有另一個方法。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="0fdd9-344">如果您使用該編輯器來建立 SQL Server 連結服務，並以純文字輸入認證，系統就會使用 Data Factory 服務所擁有的憑證來加密該認證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-344">If you create a SQL Server linked service by using the editor and you enter credentials in plain text, the credentials are encrypted using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="0fdd9-345">它「不會」使用已設定讓閘道使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-345">It does NOT use the certificate that gateway is configured to use.</span></span> <span data-ttu-id="0fdd9-346">雖然這種方法在某些情況下可能快一點，但也比較不安全。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="0fdd9-347">因此，建議您只在開發/測試用途才採用此方法。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="0fdd9-348">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="0fdd9-348">PowerShell cmdlets</span></span>
<span data-ttu-id="0fdd9-349">本節說明如何使用 Azure PowerShell Cmdlet 建立和註冊閘道。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-349">This section describes how to create and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="0fdd9-350">在系統管理員模式下啟動 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="0fdd9-351">請執行下列命令並輸入您的 Azure 認證，登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-351">Log in to your Azure account by running the following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="0fdd9-352">使用 **New-AzureRmDataFactoryGateway** Cmdlet 來建立邏輯閘道器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-352">Use the **New-AzureRmDataFactoryGateway** cmdlet to create a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="0fdd9-353">**範例命令和輸出**：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-353">**Example command and output**:</span></span>

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

1. <span data-ttu-id="0fdd9-354">在 Azure PowerShell 中，切換至資料夾：**C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-354">In Azure PowerShell, switch to the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="0fdd9-355">執行與區域變數 **$Key** 相關聯的 **RegisterGateway.ps1**，如下列命令所示。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-355">Run **RegisterGateway.ps1** associated with the local variable **$Key** as shown in the following command.</span></span> <span data-ttu-id="0fdd9-356">此指令碼會向您稍早建立的邏輯閘道註冊您機器上安裝的用戶端代理程式。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-356">This script registers the client agent installed on your machine with the logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="0fdd9-357">您可以使用 IsRegisterOnRemoteMachine 參數在遠端電腦上註冊閘道器。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-357">You can register the gateway on a remote machine by using the IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="0fdd9-358">範例：</span><span class="sxs-lookup"><span data-stu-id="0fdd9-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="0fdd9-359">您可以使用 **Get-AzureRmDataFactoryGateway** Cmdlet 取得 Data Factory 中的閘道器器清單。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-359">You can use the **Get-AzureRmDataFactoryGateway** cmdlet to get the list of Gateways in your data factory.</span></span> <span data-ttu-id="0fdd9-360">當 [狀態] 顯示為 [線上] 時，表示您的閘道器已就緒可供使用。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-360">When the **Status** shows **online**, it means your gateway is ready to use.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="0fdd9-361">您可以使用 **Remove-AzureRmDataFactoryGateway** Cmdlet 移除閘道器，並使用 **Set-AzureRmDataFactoryGateway** Cmdlet 更新閘道器的說明。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-361">You can remove a gateway using the **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using the **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="0fdd9-362">如需這些 Cmdlet 的語法及其他詳細資訊，請參閱 Data Factory Cmdlet 參考文件。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="0fdd9-363">使用 PowerShell 列出閘道器</span><span class="sxs-lookup"><span data-stu-id="0fdd9-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="0fdd9-364">使用 PowerShell 移除閘道器</span><span class="sxs-lookup"><span data-stu-id="0fdd9-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="0fdd9-365">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fdd9-365">Next steps</span></span>
* <span data-ttu-id="0fdd9-366">請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0fdd9-367">在該逐步解說中，您會建立一個使用閘道將資料從內部部署 SQL Server 資料庫移到 Azure Blob 的管線。</span><span class="sxs-lookup"><span data-stu-id="0fdd9-367">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span>  
