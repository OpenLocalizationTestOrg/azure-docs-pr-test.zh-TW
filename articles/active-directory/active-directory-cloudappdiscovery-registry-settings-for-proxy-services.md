---
title: "Proxy 服務的雲端應用程式探索登錄設定 | Microsoft Docs"
description: "本主題的目標是為您提供在執行 Cloud App Discovery 代理程式的電腦上設定必要連接埠所需的步驟。"
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="7503d-103">Proxy 服務的 Cloud App Discovery 登錄設定</span><span class="sxs-lookup"><span data-stu-id="7503d-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="7503d-104">根據預設，Cloud App Discovery 代理程式設定為僅使用連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="7503d-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="7503d-105">如果您計劃要在具有使用自訂連接埠 (既不是 80 也不是 443) 的 Proxy 伺服器的環境中安裝 Cloud App Discovery，您必須設定代理程式使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="7503d-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="7503d-106">設定是以登錄機碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="7503d-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="7503d-107">本主題的目標是為您提供在執行 Cloud App Discovery 代理程式的電腦上設定必要連接埠所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="7503d-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="7503d-108">**若要修改執行 Cloud App Discovery 代理程式的電腦所使用的連接埠，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7503d-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="7503d-109">啟動 [登錄編輯器]。</span><span class="sxs-lookup"><span data-stu-id="7503d-109">Start the registry editor.</span></span> <br> ![執行](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="7503d-111">瀏覽至或建立下列登錄機碼：</span><span class="sxs-lookup"><span data-stu-id="7503d-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="7503d-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="7503d-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="7503d-113">建立新的**多字串**值，稱為**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="7503d-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="7503d-114">![新增](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="7503d-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="7503d-115">若要開啟 [編輯多字串]  對話方塊中，按兩下 [連接埠] 值。</span><span class="sxs-lookup"><span data-stu-id="7503d-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="7503d-116">在 [數值資料] 文字方塊中輸入以下的值，然後新增您組織所使用的所有自訂連接埠：</span><span class="sxs-lookup"><span data-stu-id="7503d-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="7503d-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="7503d-117">
   **80**</span></span> <br><span data-ttu-id="7503d-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="7503d-118">
   **8080**</span></span> <br><span data-ttu-id="7503d-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="7503d-119">
   **8118**</span></span> <br><span data-ttu-id="7503d-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="7503d-120">
   **8888**</span></span> <br><span data-ttu-id="7503d-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="7503d-121">
   **81**</span></span> <br><span data-ttu-id="7503d-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="7503d-122">
   **12080**</span></span> <br><span data-ttu-id="7503d-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="7503d-123">
**6999**</span></span> <br><span data-ttu-id="7503d-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="7503d-124">
**30606**</span></span> <br><span data-ttu-id="7503d-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="7503d-125">
**31595**</span></span> <br><span data-ttu-id="7503d-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="7503d-126">
**4080**</span></span> <br><span data-ttu-id="7503d-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="7503d-127">
**443**</span></span> <br><span data-ttu-id="7503d-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="7503d-128">
**1110**</span></span> <br><br><span data-ttu-id="7503d-129">
![編輯多字串](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="7503d-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="7503d-130">按一下 [確定]，關閉 [編輯多字串] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7503d-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="7503d-131">**其他資源**</span><span class="sxs-lookup"><span data-stu-id="7503d-131">**Additional Resources**</span></span>

* [<span data-ttu-id="7503d-132">如何探索組織內使用未經批准的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="7503d-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

