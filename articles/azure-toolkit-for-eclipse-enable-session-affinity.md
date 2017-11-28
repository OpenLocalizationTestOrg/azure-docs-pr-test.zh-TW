---
title: "aaaEnable 工作階段親和性使用 hello Azure Toolkit for Eclipse"
description: "了解如何 tooenable 工作階段親和性使用 hello Azure Toolkit for Eclipse。"
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="3ef38-103">啟用工作階段同質</span><span class="sxs-lookup"><span data-stu-id="3ef38-103">Enable Session Affinity</span></span>
<span data-ttu-id="3ef38-104">在 hello Azure Toolkit for Eclipse，您可以啟用 HTTP 工作階段親和性或 「 自黏工作階段 」，您的角色。</span><span class="sxs-lookup"><span data-stu-id="3ef38-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="3ef38-105">hello 下列影像顯示 hello**負載平衡**屬性 對話方塊使用 tooenable hello 工作階段親和性功能：</span><span class="sxs-lookup"><span data-stu-id="3ef38-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="3ef38-106">tooenable 工作階段親和性，您的角色</span><span class="sxs-lookup"><span data-stu-id="3ef38-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="3ef38-107">以滑鼠右鍵按一下 Eclipse 的專案總管 中的 hello 角色中，按一下**Azure**，然後按一下**負載平衡**。</span><span class="sxs-lookup"><span data-stu-id="3ef38-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="3ef38-108">在 hello **WorkerRole1 負載平衡屬性**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="3ef38-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="3ef38-109">a.</span><span class="sxs-lookup"><span data-stu-id="3ef38-109">a.</span></span> <span data-ttu-id="3ef38-110">核取 [為這個角色啟用 HTTP 工作階段同質 (黏性工作階段)] </span><span class="sxs-lookup"><span data-stu-id="3ef38-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="3ef38-111">b.</span><span class="sxs-lookup"><span data-stu-id="3ef38-111">b.</span></span> <span data-ttu-id="3ef38-112">如**輸入端點 toouse**，例如，選取的輸入的端點 toouse， **http （public: 80，private: 8080）**。</span><span class="sxs-lookup"><span data-stu-id="3ef38-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="3ef38-113">您的應用程式必須使用這個端點作為其 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="3ef38-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="3ef38-114">您可以啟用多個端點，您的角色，但您可以選取其中一個 toosupport 黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="3ef38-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="3ef38-115">c.</span><span class="sxs-lookup"><span data-stu-id="3ef38-115">c.</span></span> <span data-ttu-id="3ef38-116">重建您的應用程式</span><span class="sxs-lookup"><span data-stu-id="3ef38-116">Rebuild your application.</span></span>

<span data-ttu-id="3ef38-117">啟用之後，如果您有多個角色執行個體，來自特定用戶端的 HTTP 要求會繼續處理 hello 相同角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ef38-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="3ef38-118">hello Eclipse 工具組支援此功能安裝到每個角色執行個體稱為 Application Request Routing (ARR) 的特殊 IIS 模組。</span><span class="sxs-lookup"><span data-stu-id="3ef38-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="3ef38-119">ARR 排列 HTTP 要求 toohello 適當的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3ef38-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="3ef38-120">hello 工具組會自動重新設定 hello 選取端點，以便 hello 傳入的 HTTP 流量會第一個路由的 toohello ARR 軟體。</span><span class="sxs-lookup"><span data-stu-id="3ef38-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="3ef38-121">hello 工具組也會建立您的 Java 伺服器是設定的 toolisten 至的新內部端點。</span><span class="sxs-lookup"><span data-stu-id="3ef38-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="3ef38-122">這是 hello ARR tooreroute hello HTTP 流量 toohello 適當的角色執行個體所使用的端點。</span><span class="sxs-lookup"><span data-stu-id="3ef38-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="3ef38-123">如此一來，多個執行個體部署中的每個角色執行個體是做為所有的反向 proxy hello 其他情況下，啟用自黏工作階段。</span><span class="sxs-lookup"><span data-stu-id="3ef38-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="3ef38-124">工作階段同質的相關注意事項</span><span class="sxs-lookup"><span data-stu-id="3ef38-124">Notes about session affinity</span></span>
* <span data-ttu-id="3ef38-125">工作階段親和性在 hello 計算模擬器中無法運作。</span><span class="sxs-lookup"><span data-stu-id="3ef38-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="3ef38-126">hello 設定可以套用 hello 計算模擬器中，而不會干擾您的建置程序或計算模擬器執行，但 hello 功能本身 hello 計算模擬器中無法運作。</span><span class="sxs-lookup"><span data-stu-id="3ef38-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="3ef38-127">啟用工作階段親和性會佔用您的部署在 Azure 中，因為其他軟體會下載並安裝到您的角色執行個體，以 hello Azure 雲端服務啟動時的磁碟空間的 hello 數量的增加。</span><span class="sxs-lookup"><span data-stu-id="3ef38-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="3ef38-128">hello 時間 tooinitialize 需要較久的每個角色。</span><span class="sxs-lookup"><span data-stu-id="3ef38-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="3ef38-129">內部端點，toofunction 流量重新路由傳送器，上面所述為將會加入。</span><span class="sxs-lookup"><span data-stu-id="3ef38-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="3ef38-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ef38-130">See Also</span></span>
<span data-ttu-id="3ef38-131">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ef38-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="3ef38-132">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ef38-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="3ef38-133">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ef38-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="3ef38-134">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="3ef38-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
