---
title: "aaaCloud Proxy 服務的應用程式探索登錄設定 |Microsoft 文件"
description: "本主題的 hello 目標是您以 hello 會引導您 tooprovide 需要 tooperform tooset hello 需要連接埠 hello 執行 hello Cloud App Discovery 代理程式的電腦上。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="92359-103">Proxy 服務的 Cloud App Discovery 登錄設定</span><span class="sxs-lookup"><span data-stu-id="92359-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="92359-104">根據預設，hello Cloud App Discovery 代理程式是設定的 toouse 只有 hello 連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="92359-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="92359-105">如果您打算在與 proxy 伺服器使用自訂連接埠 （非 80 或 443） 的環境中安裝雲端應用程式探索，您需要 tooconfigure 代理程式 toouse 此連接埠。</span><span class="sxs-lookup"><span data-stu-id="92359-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="92359-106">hello 組態根據登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="92359-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="92359-107">本主題的 hello 目標是您以 hello 會引導您 tooprovide 需要 tooperform tooset hello 需要連接埠 hello 執行 hello Cloud App Discovery 代理程式的電腦上。</span><span class="sxs-lookup"><span data-stu-id="92359-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="92359-108">**toomodify hello 連接埠供 hello 電腦執行 hello Cloud App Discovery 代理程式，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="92359-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="92359-109">啟動 hello 登錄編輯程式。</span><span class="sxs-lookup"><span data-stu-id="92359-109">Start hello registry editor.</span></span> <br> ![執行](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="92359-111">瀏覽 tooor 建立下列登錄機碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="92359-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="92359-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="92359-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="92359-113">建立新的**多字串**值，稱為**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="92359-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="92359-114">![](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="92359-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="92359-115">tooopen hello**編輯多字串**] 對話方塊中，按兩下 hello 連接埠值。</span><span class="sxs-lookup"><span data-stu-id="92359-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="92359-116">在 hello 值資料] 文字方塊中，輸入下列值的 hello 並加入您的組織所使用的所有自訂連接埠：</span><span class="sxs-lookup"><span data-stu-id="92359-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="92359-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="92359-117">
   **80**</span></span> <br><span data-ttu-id="92359-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="92359-118">
   **8080**</span></span> <br><span data-ttu-id="92359-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="92359-119">
   **8118**</span></span> <br><span data-ttu-id="92359-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="92359-120">
   **8888**</span></span> <br><span data-ttu-id="92359-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="92359-121">
   **81**</span></span> <br><span data-ttu-id="92359-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="92359-122">
   **12080**</span></span> <br><span data-ttu-id="92359-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="92359-123">
**6999**</span></span> <br><span data-ttu-id="92359-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="92359-124">
**30606**</span></span> <br><span data-ttu-id="92359-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="92359-125">
**31595**</span></span> <br><span data-ttu-id="92359-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="92359-126">
**4080**</span></span> <br><span data-ttu-id="92359-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="92359-127">
**443**</span></span> <br><span data-ttu-id="92359-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="92359-128">
**1110**</span></span> <br><br><span data-ttu-id="92359-129">
![編輯多字串](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="92359-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="92359-130">按一下**確定**tooclose hello**編輯多字串**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="92359-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="92359-131">**其他資源**</span><span class="sxs-lookup"><span data-stu-id="92359-131">**Additional Resources**</span></span>

* [<span data-ttu-id="92359-132">如何探索組織內使用未經批准的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="92359-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

