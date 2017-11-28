---
title: "在 Azure 資訊安全中心提供安全性連絡人詳細資料 | Microsoft Docs"
description: "本文件說明如何在 Azure 資訊安全中心提供安全性連絡人詳細資料。"
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
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="d5dc3-103">在 Azure 資訊安全中心提供安全性連絡人詳細資料</span><span class="sxs-lookup"><span data-stu-id="d5dc3-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="d5dc3-104">Azure 資訊安全中心會建議您針對您的 Azure 訂用帳戶提供安全性連絡人詳細資料 (如果您還沒有這麼做)。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="d5dc3-105">如果 Microsoft 安全性回應中心 (MSRC) 發現您的客戶資料遭到非法或未經授權的對象存取，Microsoft 會使用此資訊連絡您。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="d5dc3-106">MSRC 執行 Azure 網路和基礎結構的選取安全性監視，並接收來自協力廠商的威脅情報和濫用客訴。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="d5dc3-107">在每天第一個警示發生時且僅針對高嚴重性警示，才會傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="d5dc3-108">電子郵件喜好設定只能針對訂用帳戶原則設定。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="d5dc3-109">在訂用帳戶內的資源群組會繼承這些設定。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="d5dc3-110">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="d5dc3-111">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="d5dc3-112">實作建議</span><span class="sxs-lookup"><span data-stu-id="d5dc3-112">Implement the recommendation</span></span>
1. <span data-ttu-id="d5dc3-113">在 [建議] 刀鋒視窗中，選取 [提供安全性連絡人詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="d5dc3-114">![提供安全性連絡人][1]</span><span class="sxs-lookup"><span data-stu-id="d5dc3-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="d5dc3-115">[提供安全性連絡人詳細資料] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="d5dc3-116">選取要提供連絡人資訊的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="d5dc3-117">![][2]</span><span class="sxs-lookup"><span data-stu-id="d5dc3-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="d5dc3-118">第二個 [提供安全性連絡人詳細資料]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="d5dc3-119">輸入安全性連絡人的電子郵件地址，若有多個則以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="d5dc3-120">您可以輸入的電子郵件地址數沒有限制。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="d5dc3-121">輸入一個安全性連絡人國際電話號碼。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="d5dc3-122">若要接收有關高嚴重性警示的電子郵件，請開啟 [傳送給我有關警示的電子郵件] 選項。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="d5dc3-123">未來，您會有將電子郵件通知傳送給訂用帳戶擁有者的選項。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="d5dc3-124">此選項目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="d5dc3-125">選取 [確定]  將安全性連絡人資訊套用至您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="d5dc3-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5dc3-126">See also</span></span>
<span data-ttu-id="d5dc3-127">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="d5dc3-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d5dc3-128">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d5dc3-129">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d5dc3-130">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d5dc3-131">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d5dc3-132">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d5dc3-133">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d5dc3-134">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="d5dc3-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
