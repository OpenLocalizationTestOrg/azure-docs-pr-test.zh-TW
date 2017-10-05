---
title: "使用 Azure Toolkit for Eclipse 啟用工作階段同質"
description: "了解如何使用 Azure Toolkit for Eclipse 來啟用工作階段同質。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="a8abf-103">啟用工作階段同質</span><span class="sxs-lookup"><span data-stu-id="a8abf-103">Enable Session Affinity</span></span>
<span data-ttu-id="a8abf-104">在 Azure Toolkit for Eclipse 中，您可以為角色啟用 HTTP 工作階段同質 (或「黏性工作階段」)。</span><span class="sxs-lookup"><span data-stu-id="a8abf-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="a8abf-105">下圖顯示用來啟用工作階段同質功能的 [負載平衡]  屬性對話方塊：</span><span class="sxs-lookup"><span data-stu-id="a8abf-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="a8abf-106">為角色啟用工作階段同質</span><span class="sxs-lookup"><span data-stu-id="a8abf-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="a8abf-107">在 Eclipse 的 [專案總管] 中以滑鼠右鍵按一下角色，然後依序按一下 [Azure] 和 [負載平衡]。</span><span class="sxs-lookup"><span data-stu-id="a8abf-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="a8abf-108">在 [WorkerRole1 的屬性] 的 [負載平衡]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="a8abf-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="a8abf-109">a.</span><span class="sxs-lookup"><span data-stu-id="a8abf-109">a.</span></span> <span data-ttu-id="a8abf-110">核取 [為這個角色啟用 HTTP 工作階段同質 (黏性工作階段)] </span><span class="sxs-lookup"><span data-stu-id="a8abf-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="a8abf-111">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8abf-111">b.</span></span> <span data-ttu-id="a8abf-112">針對 [要使用的輸入端點]，選取要使用的輸入端點，例如 **http (public:80, private:8080)**。</span><span class="sxs-lookup"><span data-stu-id="a8abf-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="a8abf-113">您的應用程式必須使用這個端點作為其 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="a8abf-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="a8abf-114">您可以為角色啟用多個端點，但只能選取其中一個端點來支援黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="a8abf-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="a8abf-115">c.</span><span class="sxs-lookup"><span data-stu-id="a8abf-115">c.</span></span> <span data-ttu-id="a8abf-116">重建您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a8abf-116">Rebuild your application.</span></span>

<span data-ttu-id="a8abf-117">啟用後，如果您有多個角色執行個體，來自特定用戶端的 HTTP 要求會繼續由相同的角色執行個體來處理。</span><span class="sxs-lookup"><span data-stu-id="a8abf-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="a8abf-118">Eclipse Toolkit 藉由將稱為應用程式要求路由 (ARR) 的特殊 IIS 模組安裝到每個角色執行個體，來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="a8abf-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="a8abf-119">ARR 會將 HTTP 要求重新路由傳送至適當的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="a8abf-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="a8abf-120">此工具組會自動重新設定選取的端點，因此傳入 HTTP 流量會先路由傳送至 ARR 軟體。</span><span class="sxs-lookup"><span data-stu-id="a8abf-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="a8abf-121">此工具組也會建立可設定您的 Java 伺服器接聽的新內部端點。</span><span class="sxs-lookup"><span data-stu-id="a8abf-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="a8abf-122">這是 ARR 將 HTTP 流量的端點重新路由傳送至適當角色執行個體時所用的端點。</span><span class="sxs-lookup"><span data-stu-id="a8abf-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="a8abf-123">如此一來，多個執行個體部署中的每個角色執行個體可作為其他所有執行個體的反向 Proxy，以啟用黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="a8abf-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="a8abf-124">工作階段同質的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="a8abf-124">Notes about session affinity</span></span>
* <span data-ttu-id="a8abf-125">工作階段同質不會在計算模擬器中執行。</span><span class="sxs-lookup"><span data-stu-id="a8abf-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="a8abf-126">您可以在不干擾建置流程或計算模擬器執行的情況下，將這些設定套用至計算模擬器，但功能本身不會在計算模擬器中執行。</span><span class="sxs-lookup"><span data-stu-id="a8abf-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="a8abf-127">啟用工作階段同質會導致 Azure 中的部署所佔用的磁碟空間量增加，因為當您在 Azure 雲端中啟動服務時，會下載額外的軟體並安裝到您的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="a8abf-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="a8abf-128">初始化每個角色的時間會比較長。</span><span class="sxs-lookup"><span data-stu-id="a8abf-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="a8abf-129">系統會加入一個內部端點，如上所述作為路由器來重新路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="a8abf-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="a8abf-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8abf-130">See Also</span></span>
<span data-ttu-id="a8abf-131">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8abf-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a8abf-132">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8abf-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a8abf-133">[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8abf-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a8abf-134">如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="a8abf-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
