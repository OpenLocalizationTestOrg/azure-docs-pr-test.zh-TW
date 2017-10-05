---
title: "Operations Management Suite 安全性和稽核解決方案資料安全性 | Microsoft Docs"
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
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="f4e14-103">Operations Management Suite 安全性和稽核解決方案資料安全性</span><span class="sxs-lookup"><span data-stu-id="f4e14-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="f4e14-104">為了協助客戶預防、偵測及回應威脅，[Operations Management Suite (OMS) 安全性和稽核解決方案](operations-management-suite-overview.md)會收集和處理資源相關資料，其中包括︰</span><span class="sxs-lookup"><span data-stu-id="f4e14-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="f4e14-105">安全性事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="f4e14-105">Security event log</span></span>
* <span data-ttu-id="f4e14-106">Windows 事件追蹤 (ETW) 事件</span><span class="sxs-lookup"><span data-stu-id="f4e14-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="f4e14-107">AppLocker 稽核事件</span><span class="sxs-lookup"><span data-stu-id="f4e14-107">AppLocker auditing events</span></span>
* <span data-ttu-id="f4e14-108">Windows 防火牆記錄檔</span><span class="sxs-lookup"><span data-stu-id="f4e14-108">Windows Firewall log</span></span>
* <span data-ttu-id="f4e14-109">Advanced Threat Analytics 事件</span><span class="sxs-lookup"><span data-stu-id="f4e14-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="f4e14-110">基準評估結果</span><span class="sxs-lookup"><span data-stu-id="f4e14-110">Results of baseline assessment</span></span>
* <span data-ttu-id="f4e14-111">反惡意程式碼評估結果</span><span class="sxs-lookup"><span data-stu-id="f4e14-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="f4e14-112">更新/修補評估結果</span><span class="sxs-lookup"><span data-stu-id="f4e14-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="f4e14-113">在代理程式上明確啟用的 Syslog 串流</span><span class="sxs-lookup"><span data-stu-id="f4e14-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="f4e14-114">我們會強烈承諾，以保護此資料的隱私權和安全性。</span><span class="sxs-lookup"><span data-stu-id="f4e14-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="f4e14-115">Microsoft 從撰寫程式碼到運作服務均遵守嚴格的規範與安全性指導方針。</span><span class="sxs-lookup"><span data-stu-id="f4e14-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="f4e14-116">本文說明如何在 OMS 安全性和稽核解決方案中管理和保護資料。</span><span class="sxs-lookup"><span data-stu-id="f4e14-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="f4e14-117">資料來源</span><span class="sxs-lookup"><span data-stu-id="f4e14-117">Data sources</span></span>
<span data-ttu-id="f4e14-118">OMS 安全性和稽核解決方案會分析來自虛擬機器和 OM 代理程式安裝所在實體電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="f4e14-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="f4e14-119">OMS 安全性和稽核解決方案可以收集有關安全性事件的組態資訊，例如 Windows 事件、稽核記錄檔、IIS 記錄檔和 syslog 訊息。</span><span class="sxs-lookup"><span data-stu-id="f4e14-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="f4e14-120">這類資料的範例包括︰作業系統類型和版本、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f4e14-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="f4e14-121">資料保護</span><span class="sxs-lookup"><span data-stu-id="f4e14-121">Data protection</span></span>
<span data-ttu-id="f4e14-122">**資料隔離**：資料會以邏輯方式分開保存在服務的每個元件上。</span><span class="sxs-lookup"><span data-stu-id="f4e14-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="f4e14-123">每個組織加上標記的所有資料。</span><span class="sxs-lookup"><span data-stu-id="f4e14-123">All data is tagged per organization.</span></span> <span data-ttu-id="f4e14-124">這項標記作業在整個資料生命週期持續發生，它會強制執行服務的每個層級。</span><span class="sxs-lookup"><span data-stu-id="f4e14-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="f4e14-125">**資料存取**︰為了提供安全性建議及調查潛在的安全性威脅，Microsoft 人員可以存取服務所收集或分析的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4e14-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="f4e14-126">我們會遵守 [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) 和[隱私權聲明](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)，其中陳述 Microsoft 不會使用客戶資料或從中衍生資訊作為任何廣告或類似的商業用途。</span><span class="sxs-lookup"><span data-stu-id="f4e14-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="f4e14-127">為了提供安全性建議及調查潛在的安全性威脅，Microsoft 人員可以存取服務所收集或分析的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4e14-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="f4e14-128">我們會視需要只使用客戶資料為您提供 Azure 服務，包括與提供這些服務相容的用途。</span><span class="sxs-lookup"><span data-stu-id="f4e14-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="f4e14-129">您可保有自有資料的所有權限。</span><span class="sxs-lookup"><span data-stu-id="f4e14-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="f4e14-130">**資料使用**：Microsoft 使用可見於多個租用戶的模式和威脅智慧來加強我們的防護和偵測功能；我們會根據[隱私權聲明](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)中所述的隱私權承諾進行。</span><span class="sxs-lookup"><span data-stu-id="f4e14-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f4e14-131">資料位置是在工作區建立期間設定於 OMS 工作區層級，這是初始 OMS 安全性和稽核設定程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="f4e14-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="f4e14-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f4e14-132">See also</span></span>
<span data-ttu-id="f4e14-133">在本文件中，您已了解如何在 OMS 中管理和保護資料。</span><span class="sxs-lookup"><span data-stu-id="f4e14-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="f4e14-134">若要深入了解 OMS 安全性和稽核解決方案，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f4e14-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="f4e14-135">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="f4e14-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="f4e14-136">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="f4e14-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="f4e14-137">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="f4e14-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

