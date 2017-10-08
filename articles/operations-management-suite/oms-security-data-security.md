---
title: "管理套件的安全性和稽核解決方案資料安全性 aaaOperations |Microsoft 文件"
description: "本文件說明如何在 Operations Management Suite 安全性和稽核解決方案中管理和保護資料。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="d66df-103">Operations Management Suite 安全性和稽核解決方案資料安全性</span><span class="sxs-lookup"><span data-stu-id="d66df-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="d66df-104">toohelp 客戶防止、 偵測及回應 toothreats， [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)會收集並處理資源的相關資料，其中包括：</span><span class="sxs-lookup"><span data-stu-id="d66df-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="d66df-105">安全性事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="d66df-105">Security event log</span></span>
* <span data-ttu-id="d66df-106">Windows 事件追蹤 (ETW) 事件</span><span class="sxs-lookup"><span data-stu-id="d66df-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="d66df-107">AppLocker 稽核事件</span><span class="sxs-lookup"><span data-stu-id="d66df-107">AppLocker auditing events</span></span>
* <span data-ttu-id="d66df-108">Windows 防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="d66df-108">Windows Firewall log</span></span>
* <span data-ttu-id="d66df-109">Advanced Threat Analytics 事件</span><span class="sxs-lookup"><span data-stu-id="d66df-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="d66df-110">基準評估結果</span><span class="sxs-lookup"><span data-stu-id="d66df-110">Results of baseline assessment</span></span>
* <span data-ttu-id="d66df-111">反惡意程式碼評估結果</span><span class="sxs-lookup"><span data-stu-id="d66df-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="d66df-112">更新/修補評估結果</span><span class="sxs-lookup"><span data-stu-id="d66df-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="d66df-113">在 hello 代理程式上明確啟用 Syslog 資料流</span><span class="sxs-lookup"><span data-stu-id="d66df-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="d66df-114">我們不提供這項資料的強式承諾 tooprotect hello 隱私與安全性。</span><span class="sxs-lookup"><span data-stu-id="d66df-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="d66df-115">Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="d66df-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="d66df-116">本文說明如何在 OMS 安全性和稽核解決方案中管理和保護資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="d66df-117">資料來源</span><span class="sxs-lookup"><span data-stu-id="d66df-117">Data sources</span></span>
<span data-ttu-id="d66df-118">OMS 安全性和稽核解決方案分析 hello OMS 代理程式已安裝虛擬機器和實體電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="d66df-119">OMS 安全性和稽核解決方案可以收集有關安全性事件的組態資訊，例如 Windows 事件、稽核記錄檔、IIS 記錄檔和 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="d66df-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="d66df-120">這類資料的範例包括︰作業系統類型和版本、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="d66df-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="d66df-121">資料保護</span><span class="sxs-lookup"><span data-stu-id="d66df-121">Data protection</span></span>
<span data-ttu-id="d66df-122">**資料隔離**: hello 服務在每個元件上，資料以邏輯方式分開。</span><span class="sxs-lookup"><span data-stu-id="d66df-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="d66df-123">每個組織加上標記的所有資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-123">All data is tagged per organization.</span></span> <span data-ttu-id="d66df-124">這項標記作業在整個 hello 資料生命週期持續發生，它會強制執行各種層級的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d66df-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="d66df-125">**資料存取**: tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集或由服務分析的資訊。</span><span class="sxs-lookup"><span data-stu-id="d66df-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="d66df-126">我們將遵守 toohello [Microsoft Online Services 條款](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)和[隱私權聲明](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)，Microsoft 將不使用客戶資料，或衍生自它的資訊任何廣告或類似處理的狀態商業用途。</span><span class="sxs-lookup"><span data-stu-id="d66df-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="d66df-127">tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集或由服務分析的資訊。</span><span class="sxs-lookup"><span data-stu-id="d66df-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="d66df-128">我們只會為您的 Azure 服務，包括用途與提供這些服務相容的所需 tooprovide 使用客戶資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="d66df-129">您會保留所有權限 tooyour 自己的資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="d66df-130">**資料使用**： 使用模式，Microsoft 威脅情報看到跨多個租用戶 tooenhance 我們預防和偵測功能之後，我們這樣中所述的 hello 隱私權承諾根據我們[隱私權陳述式](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d66df-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d66df-131">Hello 工作區建立期間，也就是在 hello 初始 OMS 安全性和稽核設定程序在 hello OMS 工作區層級，設定資料的位置。</span><span class="sxs-lookup"><span data-stu-id="d66df-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="d66df-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d66df-132">See also</span></span>
<span data-ttu-id="d66df-133">在本文件中，您已了解如何在 OMS 中管理和保護資料。</span><span class="sxs-lookup"><span data-stu-id="d66df-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="d66df-134">toolearn 深入了解 OMS 安全性和稽核解決方案，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d66df-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="d66df-135">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="d66df-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="d66df-136">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="d66df-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="d66df-137">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="d66df-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

