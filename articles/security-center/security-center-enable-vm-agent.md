---
title: "aaaEnable VM 代理程式在 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用 VM 代理程式 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="c8ac1-103">在 Azure 資訊安全中心啟用 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="c8ac1-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="c8ac1-104">hello VM 代理程式必須安裝在順序中的虛擬機器 (Vm) 太[啟用資料收集](security-center-enable-data-collection.md)。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="c8ac1-105">Azure 資訊安全中心可讓您 toosee Vm 需要 hello VM 代理程式，以及將會建議您啟用 hello 在那些 Vm 上的 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="c8ac1-106">預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="c8ac1-107">hello 文章[VM 代理程式和延伸模組 – 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="c8ac1-108">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="c8ac1-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c8ac1-110">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="c8ac1-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="c8ac1-111">在 hello**建議刀鋒視窗**，選取**啟用 VM 代理程式**。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="c8ac1-112">![啟用 VM 代理程式][1]</span><span class="sxs-lookup"><span data-stu-id="c8ac1-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="c8ac1-113">這會開啟刀鋒視窗中 hello **VM 代理程式遺失或不回應**。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="c8ac1-114">此刀鋒視窗會列出 hello Vm 需要 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="c8ac1-115">遵循 hello 指示 hello 刀鋒視窗 tooinstall hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="c8ac1-116">![VM 代理程式已遺失][2]</span><span class="sxs-lookup"><span data-stu-id="c8ac1-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="c8ac1-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c8ac1-117">See also</span></span>
<span data-ttu-id="c8ac1-118">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c8ac1-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c8ac1-119">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c8ac1-120">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c8ac1-121">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c8ac1-122">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c8ac1-123">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c8ac1-124">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c8ac1-125">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="c8ac1-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
