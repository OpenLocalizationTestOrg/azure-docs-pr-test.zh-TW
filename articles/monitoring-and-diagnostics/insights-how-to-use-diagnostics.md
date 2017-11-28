---
title: "在 Microsoft Azure 中啟用監視和診斷 | Microsoft Docs"
description: "了解如何在 Azure 設定資源的診斷。"
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="f22c2-103">啟用監視和診斷</span><span class="sxs-lookup"><span data-stu-id="f22c2-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="f22c2-104">在 [Azure 入口網站](https://portal.azure.com)中，您可以為您的資源設定內容豐富且經常產生的監視與診斷資料。</span><span class="sxs-lookup"><span data-stu-id="f22c2-104">In the [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="f22c2-105">您也可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 設定，並以程式設計方式設定診斷。</span><span class="sxs-lookup"><span data-stu-id="f22c2-105">You can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to configure diagnostics programmatically.</span></span>

<span data-ttu-id="f22c2-106">在 Azure 中的診斷、監視和計量資料會被儲存到您所選擇的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f22c2-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="f22c2-107">這可讓您使用任何工具來讀取資料，從儲存體總管到 Power BI 再到協力廠商工具。</span><span class="sxs-lookup"><span data-stu-id="f22c2-107">This allows you to use whatever tooling you want to read the data, from a storage explorer, to Power BI to third-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="f22c2-108">建立資源的時機</span><span class="sxs-lookup"><span data-stu-id="f22c2-108">When you create a resource</span></span>
<span data-ttu-id="f22c2-109">當您在 [Azure 入口網站](https://portal.azure.com)中首次建立服務時，大部分的服務可讓您啟用診斷功能。</span><span class="sxs-lookup"><span data-stu-id="f22c2-109">Most services allow you to enable diagnostics when you first create them in the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f22c2-110">移至 [ **新增** ] 並選擇您感興趣的資源。</span><span class="sxs-lookup"><span data-stu-id="f22c2-110">Go to **New** and choose the resource you are interested in.</span></span>
2. <span data-ttu-id="f22c2-111">選取 [ **選用組態**]。</span><span class="sxs-lookup"><span data-stu-id="f22c2-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="f22c2-112">![診斷刀鋒視窗](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="f22c2-112">![Diagnostics blade](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="f22c2-113">選取 [診斷]，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f22c2-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="f22c2-114">您將必須選擇您要儲存診斷的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f22c2-114">You will need to choose the Storage account that you want diagnostics to be saved to.</span></span> <span data-ttu-id="f22c2-115">將診斷傳送至儲存體帳戶時，您將需要支付儲存和交易的一般數據傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="f22c2-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span></span>
4. <span data-ttu-id="f22c2-116">按一下 [ **確定** ]，並建立資源。</span><span class="sxs-lookup"><span data-stu-id="f22c2-116">Click **OK** and create the resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="f22c2-117">變更現有資源的設定</span><span class="sxs-lookup"><span data-stu-id="f22c2-117">Change settings for an existing resource</span></span>
<span data-ttu-id="f22c2-118">如果您已經建立資源，而且您想要變更診斷設定 (例如，變更資料收集的層級)，您可以直接在 Azure 入口網站中執行此作業。</span><span class="sxs-lookup"><span data-stu-id="f22c2-118">If you have already created a resource and you want to change the diagnostics settings (to change the level of data collection, for example), you can do that right in the Azure Portal.</span></span>

1. <span data-ttu-id="f22c2-119">移至資源，然後按一下 [ **設定** ] 命令。</span><span class="sxs-lookup"><span data-stu-id="f22c2-119">Go to the resource and click the **Settings** command.</span></span>
2. <span data-ttu-id="f22c2-120">選取 [ **診斷**]。</span><span class="sxs-lookup"><span data-stu-id="f22c2-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="f22c2-121">[ **診斷** ] 刀鋒視窗會有該資源的所有可能診斷和監視集合資料。</span><span class="sxs-lookup"><span data-stu-id="f22c2-121">The **Diagnostics** blade has all of the possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="f22c2-122">在某些資源中，您也可以為資料選擇 [ **保留** ] 原則，以便將它從儲存體帳戶中清除。</span><span class="sxs-lookup"><span data-stu-id="f22c2-122">For some resources you can also choose a **Retention** policy for the data, to clean it up from your storage account.</span></span>
    <span data-ttu-id="f22c2-123">![儲存體診斷](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="f22c2-123">![Storage diagnostics](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="f22c2-124">選擇設定之後，請按一下 [ **儲存** ] 命令。</span><span class="sxs-lookup"><span data-stu-id="f22c2-124">Once you've chosen your settings, click the **Save** command.</span></span> <span data-ttu-id="f22c2-125">如果您是第一次啟用此選項，則顯示監視資料可能需要一點時間。</span><span class="sxs-lookup"><span data-stu-id="f22c2-125">It may take a little while for monitoring data to show up if you are enabling it for the first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="f22c2-126">虛擬機器的資料收集類別</span><span class="sxs-lookup"><span data-stu-id="f22c2-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="f22c2-127">在虛擬機器中，所有的計量與記錄都將以一分鐘的間隔來記錄，以便您隨時保有最新的機器相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f22c2-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have the most up-to-date information about your machine.</span></span>

* <span data-ttu-id="f22c2-128">**基本計量** ：有關您的虛擬機器的健康情況計量，例如處理器與記憶體</span><span class="sxs-lookup"><span data-stu-id="f22c2-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="f22c2-129">**網路和 Web 計量** ：有關您的網路連線與 Web 服務的計量</span><span class="sxs-lookup"><span data-stu-id="f22c2-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="f22c2-130">**.NET 計量** ：有關在您的虛擬機器上執行的 .NET 與 ASP.NET 應用程式計量</span><span class="sxs-lookup"><span data-stu-id="f22c2-130">**.NET metrics** : Metrics about the .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="f22c2-131">**SQL 計量** ：如果您執行的是 Microsoft SQL 服務，這會是其效能計量</span><span class="sxs-lookup"><span data-stu-id="f22c2-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="f22c2-132">**Windows 事件應用程式記錄檔** ：傳送至應用程式通道的 Windows 事件</span><span class="sxs-lookup"><span data-stu-id="f22c2-132">**Windows event application logs** : Windows events that are sent to the application channel</span></span>
* <span data-ttu-id="f22c2-133">**Windows 事件系統記錄檔** ：傳送至系統通道的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="f22c2-133">**Windows event system logs** : Windows events that are sent to the system channel.</span></span> <span data-ttu-id="f22c2-134">此事件同時包含來自 [Microsoft 反惡意程式碼](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)(英文) 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="f22c2-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="f22c2-135">**Windows 事件安全性記錄檔** ：傳送至安全性通道的 Windows 事件</span><span class="sxs-lookup"><span data-stu-id="f22c2-135">**Windows event security logs** : Windows events that are sent to the security channel</span></span>
* <span data-ttu-id="f22c2-136">**診斷基礎結構記錄檔** ：記錄有關診斷收集基礎結構的資訊</span><span class="sxs-lookup"><span data-stu-id="f22c2-136">**Diagnostics infrastructure logs** : Logging about the diagnostics collection infrastructure</span></span>
* <span data-ttu-id="f22c2-137">**IIS 記錄檔** ：有關 IIS 伺服器的記錄</span><span class="sxs-lookup"><span data-stu-id="f22c2-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="f22c2-138">請注意，目前不支援特定的 Linux 散發套件，而且虛擬機器上必須安裝客體代理程式。</span><span class="sxs-lookup"><span data-stu-id="f22c2-138">Note that at this time certain distributions of Linux are not supported, and, the Guest Agent must be installed on the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f22c2-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f22c2-139">Next steps</span></span>
* <span data-ttu-id="f22c2-140">[接收警示通知](insights-receive-alert-notifications.md) 。</span><span class="sxs-lookup"><span data-stu-id="f22c2-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="f22c2-141">[監視服務計量](insights-how-to-customize-monitoring.md) 以確保您的服務可用且可回應。</span><span class="sxs-lookup"><span data-stu-id="f22c2-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="f22c2-142">[自動調整執行個體計數](insights-how-to-scale.md) 以確保您的服務可根據需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="f22c2-142">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service scale based on demand.</span></span>
* <span data-ttu-id="f22c2-143">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md) 。</span><span class="sxs-lookup"><span data-stu-id="f22c2-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="f22c2-144">[檢視事件和活動記錄檔](insights-debugging-with-events.md)以了解在您服務內發生的所有內容。</span><span class="sxs-lookup"><span data-stu-id="f22c2-144">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="f22c2-145">[追蹤服務健康狀況](insights-service-health.md) 可以找出 Azure 何時遭遇效能降低或服務中斷。</span><span class="sxs-lookup"><span data-stu-id="f22c2-145">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span></span>

