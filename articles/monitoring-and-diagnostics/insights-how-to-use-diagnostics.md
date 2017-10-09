---
title: "aaaEnable 監視和 Microsoft Azure 中的診斷 |Microsoft 文件"
description: "深入了解如何針對您在 Azure 中的資源的診斷 tooset。"
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
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="5370c-103">啟用監視和診斷</span><span class="sxs-lookup"><span data-stu-id="5370c-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="5370c-104">在 hello [Azure 入口網站](https://portal.azure.com)，可以設定資源的相關豐富、 頻繁，監視和診斷資料。</span><span class="sxs-lookup"><span data-stu-id="5370c-104">In hello [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="5370c-105">您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure 診斷以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="5370c-105">You can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnostics programmatically.</span></span>

<span data-ttu-id="5370c-106">在 Azure 中的診斷、監視和計量資料會被儲存到您所選擇的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5370c-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="5370c-107">這可讓您 toouse 任何 tooling tooread hello 資料，存放裝置總管 」 tooPower BI toothird 合作對象的工具。</span><span class="sxs-lookup"><span data-stu-id="5370c-107">This allows you toouse whatever tooling you want tooread hello data, from a storage explorer, tooPower BI toothird-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="5370c-108">建立資源的時機</span><span class="sxs-lookup"><span data-stu-id="5370c-108">When you create a resource</span></span>
<span data-ttu-id="5370c-109">大部分服務可讓您 tooenable 診斷當您首次在 hello 建立[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5370c-109">Most services allow you tooenable diagnostics when you first create them in hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="5370c-110">跳過**新增**並選擇您感興趣的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5370c-110">Go too**New** and choose hello resource you are interested in.</span></span>
2. <span data-ttu-id="5370c-111">選取 [ **選用組態**]。</span><span class="sxs-lookup"><span data-stu-id="5370c-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="5370c-112">![診斷刀鋒視窗](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="5370c-112">![Diagnostics blade](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="5370c-113">選取 [診斷]，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="5370c-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="5370c-114">您將需要您想要儲存的診斷 toobe toochoose hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5370c-114">You will need toochoose hello Storage account that you want diagnostics toobe saved to.</span></span> <span data-ttu-id="5370c-115">您將支付儲存體和交易的一般資料費率當您傳送診斷 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5370c-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics tooa storage account.</span></span>
4. <span data-ttu-id="5370c-116">按一下**確定**和建立 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="5370c-116">Click **OK** and create hello resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="5370c-117">變更現有資源的設定</span><span class="sxs-lookup"><span data-stu-id="5370c-117">Change settings for an existing resource</span></span>
<span data-ttu-id="5370c-118">如果您已經建立的資源，而您想 toochange hello 診斷設定 （資料收集，例如 toochange hello 層級），您可以在 hello Azure 入口網站中的該權限。</span><span class="sxs-lookup"><span data-stu-id="5370c-118">If you have already created a resource and you want toochange hello diagnostics settings (toochange hello level of data collection, for example), you can do that right in hello Azure Portal.</span></span>

1. <span data-ttu-id="5370c-119">移 toohello 資源，然後按一下 hello**設定**命令。</span><span class="sxs-lookup"><span data-stu-id="5370c-119">Go toohello resource and click hello **Settings** command.</span></span>
2. <span data-ttu-id="5370c-120">選取 [ **診斷**]。</span><span class="sxs-lookup"><span data-stu-id="5370c-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="5370c-121">hello**診斷**刀鋒視窗都具有所有 hello 可能的診斷和監視該資源的集合資料。</span><span class="sxs-lookup"><span data-stu-id="5370c-121">hello **Diagnostics** blade has all of hello possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="5370c-122">某些資源您也可以選擇**保留**hello 資料，tooclean 的原則進行從儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5370c-122">For some resources you can also choose a **Retention** policy for hello data, tooclean it up from your storage account.</span></span>
    <span data-ttu-id="5370c-123">![儲存體診斷](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="5370c-123">![Storage diagnostics](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="5370c-124">一旦您已選擇您的設定，請按一下 hello**儲存**命令。</span><span class="sxs-lookup"><span data-stu-id="5370c-124">Once you've chosen your settings, click hello **Save** command.</span></span> <span data-ttu-id="5370c-125">它可能需要一點時資料 tooshow 監視設定，如果您要啟用它 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="5370c-125">It may take a little while for monitoring data tooshow up if you are enabling it for hello first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="5370c-126">虛擬機器的資料收集類別</span><span class="sxs-lookup"><span data-stu-id="5370c-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="5370c-127">虛擬機器的所有標準和記錄檔會都記錄在一分鐘的時間間隔，因此您可以一律 hello 大部分新的資訊關於您的電腦。</span><span class="sxs-lookup"><span data-stu-id="5370c-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have hello most up-to-date information about your machine.</span></span>

* <span data-ttu-id="5370c-128">**基本計量** ：有關您的虛擬機器的健康情況計量，例如處理器與記憶體</span><span class="sxs-lookup"><span data-stu-id="5370c-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="5370c-129">**網路和 Web 計量** ：有關您的網路連線與 Web 服務的計量</span><span class="sxs-lookup"><span data-stu-id="5370c-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="5370c-130">**.NET 度量**: hello.NET 和 ASP.NET 應用程式的相關虛擬機器上執行的度量</span><span class="sxs-lookup"><span data-stu-id="5370c-130">**.NET metrics** : Metrics about hello .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="5370c-131">**SQL 計量** ：如果您執行的是 Microsoft SQL 服務，這會是其效能計量</span><span class="sxs-lookup"><span data-stu-id="5370c-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="5370c-132">**Windows 事件應用程式記錄檔**： 傳送 toohello 應用程式通道的 Windows 事件</span><span class="sxs-lookup"><span data-stu-id="5370c-132">**Windows event application logs** : Windows events that are sent toohello application channel</span></span>
* <span data-ttu-id="5370c-133">**Windows 事件系統記錄檔**: toohello 系統通道傳送的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="5370c-133">**Windows event system logs** : Windows events that are sent toohello system channel.</span></span> <span data-ttu-id="5370c-134">此事件同時包含來自 [Microsoft 反惡意程式碼](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)(英文) 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="5370c-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="5370c-135">**Windows 事件安全性記錄檔**: toohello 安全性通道傳送的 Windows 事件</span><span class="sxs-lookup"><span data-stu-id="5370c-135">**Windows event security logs** : Windows events that are sent toohello security channel</span></span>
* <span data-ttu-id="5370c-136">**診斷基礎結構記錄檔**: hello 診斷收集基礎結構的相關記錄</span><span class="sxs-lookup"><span data-stu-id="5370c-136">**Diagnostics infrastructure logs** : Logging about hello diagnostics collection infrastructure</span></span>
* <span data-ttu-id="5370c-137">**IIS 記錄檔** ：有關 IIS 伺服器的記錄</span><span class="sxs-lookup"><span data-stu-id="5370c-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="5370c-138">請注意，此時不支援的 Linux 特定散發，而且，hello 客體代理程式必須安裝在 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5370c-138">Note that at this time certain distributions of Linux are not supported, and, hello Guest Agent must be installed on hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5370c-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5370c-139">Next steps</span></span>
* <span data-ttu-id="5370c-140">每當發生作業事件或計量超過臨界值時，[接收警示通知](insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="5370c-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="5370c-141">[監視服務計量](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="5370c-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="5370c-142">[自動調整執行個體計數](insights-how-to-scale.md)toomake 確定您的服務標尺依照需求。</span><span class="sxs-lookup"><span data-stu-id="5370c-142">[Scale instance count automatically](insights-how-to-scale.md) toomake sure your service scale based on demand.</span></span>
* <span data-ttu-id="5370c-143">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="5370c-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="5370c-144">[檢視事件和活動記錄檔](insights-debugging-with-events.md)toolearn 所有發生在您的服務中的項目。</span><span class="sxs-lookup"><span data-stu-id="5370c-144">[View events and activity log](insights-debugging-with-events.md) toolearn everything that has happened in your service.</span></span>
* <span data-ttu-id="5370c-145">[追蹤服務健全狀況](insights-service-health.md)toofind 出 Azure 時遇到效能降低或服務中斷。</span><span class="sxs-lookup"><span data-stu-id="5370c-145">[Track service health](insights-service-health.md) toofind out when Azure has experienced performance degradation or service interruptions.</span></span>

