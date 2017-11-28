---
title: "在 Azure 資訊安全中心啟用儲存體帳戶的加密 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議：**啟用 Azure 儲存體帳戶的加密**。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="c7b58-103">在 Azure 資訊安全中心啟用 Azure 儲存體帳戶的加密</span><span class="sxs-lookup"><span data-stu-id="c7b58-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="c7b58-104">Azure 資訊安全中心可能建議您對待用資料啟用 Azure 儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="c7b58-105">儲存體服務加密 (SSE) 會在資料寫入 Azure 儲存體時加密資料，並於擷取資料之前解密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="c7b58-106">SSE 目前僅適用於 Azure Blob 服務，可用於區塊 Blob、分頁 Blob 和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="c7b58-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="c7b58-107">若要深入了解，請參閱[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="c7b58-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="c7b58-108">啟用加密之後，只有新的資料會加密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="c7b58-109">儲存體帳戶中任何現有的 blob 保持未加密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="c7b58-110">若要加密現有的 blob，請參閱[儲存體服務加密常見問題集](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。</span><span class="sxs-lookup"><span data-stu-id="c7b58-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="c7b58-111">只有 Resource Manager 儲存體帳戶才支援儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="c7b58-112">目前不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7b58-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="c7b58-113">若要了解傳統和 Resource Manager 部署模型，請參閱 [Azure 部署模型](../azure-classic-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="c7b58-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c7b58-114">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="c7b58-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c7b58-115">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="c7b58-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c7b58-116">實作建議</span><span class="sxs-lookup"><span data-stu-id="c7b58-116">Implement the recommendation</span></span>
1. <span data-ttu-id="c7b58-117">在 [建議] 刀鋒視窗中，選取 [啟用 Azure 儲存體帳戶的加密]。</span><span class="sxs-lookup"><span data-stu-id="c7b58-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="c7b58-118">![啟用儲存體帳戶的加密][1]</span><span class="sxs-lookup"><span data-stu-id="c7b58-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="c7b58-119">[啟用儲存體加密] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c7b58-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="c7b58-120">此刀鋒視窗會列出已停用儲存體加密的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7b58-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="c7b58-121">在此範例中，我們選取 [storageacct1]。</span><span class="sxs-lookup"><span data-stu-id="c7b58-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="c7b58-122">![啟用儲存體加密][2]</span><span class="sxs-lookup"><span data-stu-id="c7b58-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="c7b58-123">**storageacct1** 的 [加密] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c7b58-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="c7b58-124">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="c7b58-124">Select **Enabled**.</span></span>
   <span data-ttu-id="c7b58-125">![加密刀鋒視窗][3]</span><span class="sxs-lookup"><span data-stu-id="c7b58-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="c7b58-126">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="c7b58-126">Select **Save**.</span></span>

<span data-ttu-id="c7b58-127">您現在已啟用 **storageacct1** 的儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="c7b58-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="c7b58-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c7b58-128">See also</span></span>
<span data-ttu-id="c7b58-129">本文件說明如何實作資訊安全中心建議：「啟用 Azure 儲存體帳戶的加密」。</span><span class="sxs-lookup"><span data-stu-id="c7b58-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="c7b58-130">若要深入了解 Azure 儲存體服務加密，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="c7b58-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="c7b58-131">待用資料的 Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="c7b58-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="c7b58-132">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="c7b58-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c7b58-133">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) - 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="c7b58-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c7b58-134">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) - 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="c7b58-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c7b58-135">[在 Azure 資訊安全中心管理與回應安全性警示](security-center-managing-and-responding-alerts.md) - 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="c7b58-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c7b58-136">[在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="c7b58-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c7b58-137">[Azure 資訊安全中心常見問題集](security-center-faq.md) - 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="c7b58-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c7b58-138">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="c7b58-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
