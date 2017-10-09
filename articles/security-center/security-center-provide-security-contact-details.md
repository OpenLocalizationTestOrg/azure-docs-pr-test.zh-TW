---
title: "aaaProvide 安全性連絡人詳細資料中 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件示範 tooprovide 安全性如何連絡 Azure 資訊安全中心中的詳細資料。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="e5d66-103">在 Azure 資訊安全中心提供安全性連絡人詳細資料</span><span class="sxs-lookup"><span data-stu-id="e5d66-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="e5d66-104">Azure 資訊安全中心會建議您針對您的 Azure 訂用帳戶提供安全性連絡人詳細資料 (如果您還沒有這麼做)。</span><span class="sxs-lookup"><span data-stu-id="e5d66-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="e5d66-105">這項資訊將供 Microsoft toocontact 您如果 hello Microsoft Security Response Center (MSRC) 探索非法或未經授權的合作對象已存取您的客戶資料。</span><span class="sxs-lookup"><span data-stu-id="e5d66-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="e5d66-106">MSRC 執行選取的安全性監視的 hello Azure 網路和基礎結構，並接收來自第三方 threat intelligence 和濫用抱怨。</span><span class="sxs-lookup"><span data-stu-id="e5d66-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="e5d66-107">在 hello 每日第一個警示的而且僅針對高嚴重性警示時傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="e5d66-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="e5d66-108">電子郵件喜好設定只能針對訂用帳戶原則設定。</span><span class="sxs-lookup"><span data-stu-id="e5d66-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="e5d66-109">在訂用帳戶內的資源群組會繼承這些設定。</span><span class="sxs-lookup"><span data-stu-id="e5d66-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="e5d66-110">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="e5d66-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="e5d66-111">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="e5d66-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="e5d66-112">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="e5d66-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="e5d66-113">在 hello**建議**刀鋒視窗中，選取**提供安全性連絡人詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="e5d66-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="e5d66-114">![提供安全性連絡人][1]</span><span class="sxs-lookup"><span data-stu-id="e5d66-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="e5d66-115">這會開啟刀鋒視窗中 hello**提供安全性連絡人詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="e5d66-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="e5d66-116">在 選取 hello Azure 訂用帳戶 tooprovide 連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d66-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="e5d66-117">![提供安全性連絡人詳細資料][2]</span><span class="sxs-lookup"><span data-stu-id="e5d66-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="e5d66-118">第二個 [提供安全性連絡人詳細資料]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e5d66-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="e5d66-119">輸入 hello 安全性連絡人的電子郵件地址或以逗號分隔地址。</span><span class="sxs-lookup"><span data-stu-id="e5d66-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="e5d66-120">沒有任何限制 toohello 數字，您可以輸入的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e5d66-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="e5d66-121">輸入一個安全性連絡人國際電話號碼。</span><span class="sxs-lookup"><span data-stu-id="e5d66-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="e5d66-122">tooreceive 有關高嚴重性警示的電子郵件開啟 hello 選項**傳送給我以電子郵件警示的相關**。</span><span class="sxs-lookup"><span data-stu-id="e5d66-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="e5d66-123">在 hello 未來，您可以 hello 選項 toosend 電子郵件通知 toosubscription 擁有者。</span><span class="sxs-lookup"><span data-stu-id="e5d66-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="e5d66-124">此選項目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="e5d66-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="e5d66-125">選取**確定**tooapply hello 安全性連絡資訊 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e5d66-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="e5d66-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e5d66-126">See also</span></span>
<span data-ttu-id="e5d66-127">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e5d66-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="e5d66-128">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="e5d66-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e5d66-129">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e5d66-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e5d66-130">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e5d66-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="e5d66-131">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="e5d66-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="e5d66-132">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="e5d66-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="e5d66-133">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="e5d66-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="e5d66-134">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d66-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
