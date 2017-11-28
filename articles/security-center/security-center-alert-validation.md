---
title: "aaaAlerts 驗證 Azure 資訊安全中心 |Microsoft 文件"
description: "這份文件可協助您在 Azure 資訊安全中心 toovalidate hello 安全性警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="7cda9-103">Azure 資訊安全中心的警示驗證</span><span class="sxs-lookup"><span data-stu-id="7cda9-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="7cda9-104">這份文件可協助您瞭解如何 tooverify 系統已正確設定 Azure 資訊安全中心警示。</span><span class="sxs-lookup"><span data-stu-id="7cda9-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="7cda9-105">什麼是安全性警示：</span><span class="sxs-lookup"><span data-stu-id="7cda9-105">What are security alerts?</span></span>
<span data-ttu-id="7cda9-106">資訊安全中心會自動收集、 分析，並將記錄資料從 Azure 資源、 hello 網路和連線的協力廠商解決方案，例如防火牆和 endpoint protection 解決方案、 toodetect 和警示您 toothreats 相整合。</span><span class="sxs-lookup"><span data-stu-id="7cda9-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="7cda9-107">讀取[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)如需有關安全性警示] 及 [讀取[了解 Azure 資訊安全中心中的安全性警示](https://docs.microsoft.com/azure/security-center/security-center-alerts-type)toolearn 更多關於 hello 不同類型的警示。</span><span class="sxs-lookup"><span data-stu-id="7cda9-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="7cda9-108">警示驗證</span><span class="sxs-lookup"><span data-stu-id="7cda9-108">Alert validation</span></span>
<span data-ttu-id="7cda9-109">資訊安全中心代理程式安裝在電腦上之後，請依照 hello 執行下列步驟從 hello 電腦您要的 hello 警示 toobe 遭受攻擊的 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="7cda9-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="7cda9-110">複製可執行檔 （適用於範例 calc.exe) toohello 電腦的桌面或您的方便的其他目錄。</span><span class="sxs-lookup"><span data-stu-id="7cda9-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="7cda9-111">此檔案重新命名過**ASC_AlertTest_662jfi039N.exe**。</span><span class="sxs-lookup"><span data-stu-id="7cda9-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="7cda9-112">開啟 hello 命令提示字元並執行此檔案使用的引數 （只是假的引數名稱），例如： *ASC_AlertTest_662jfi039N.exe foo*</span><span class="sxs-lookup"><span data-stu-id="7cda9-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="7cda9-113">等待 5 too10 分鐘，然後開啟安全性中心警示。</span><span class="sxs-lookup"><span data-stu-id="7cda9-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="7cda9-114">您應該會那里發現警示類似 toofollowing 其中一個：</span><span class="sxs-lookup"><span data-stu-id="7cda9-114">There you should find an alert similar toofollowing one:</span></span>

    ![警示驗證](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="7cda9-116">當檢閱此警示，請確定啟用稽核引數的 hello 欄位會顯示為 true。</span><span class="sxs-lookup"><span data-stu-id="7cda9-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="7cda9-117">如果為 false，您需要稽核 tooenable 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="7cda9-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="7cda9-118">您可以啟用此選項，使用下列命令列的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cda9-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="7cda9-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="7cda9-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="7cda9-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7cda9-120">See also</span></span>
<span data-ttu-id="7cda9-121">這篇文章會引進 toohello 警示驗證程序。</span><span class="sxs-lookup"><span data-stu-id="7cda9-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="7cda9-122">既然您已熟悉這項驗證，請嘗試下列發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cda9-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="7cda9-123">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="7cda9-124">深入了解如何 toomanage 警示 」 和 「 資訊安全中心回應 toosecurity 事件。</span><span class="sxs-lookup"><span data-stu-id="7cda9-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="7cda9-125">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="7cda9-126">了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7cda9-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7cda9-127">[了解 Azure 資訊安全中心的安全性警示](https://docs.microsoft.com/azure/security-center/security-center-alerts-type)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="7cda9-128">深入了解 hello 不同類型的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="7cda9-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="7cda9-129">[Azure 資訊安全中心疑難排解指南](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="7cda9-130">了解如何 tootroubleshoot 常見問題資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="7cda9-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="7cda9-131">[Azure 資訊安全中心常見問題集](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="7cda9-132">尋找有關使用 hello 服務常見問題。</span><span class="sxs-lookup"><span data-stu-id="7cda9-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7cda9-133">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。</span><span class="sxs-lookup"><span data-stu-id="7cda9-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="7cda9-134">尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="7cda9-134">Find blog posts about Azure security and compliance.</span></span>

