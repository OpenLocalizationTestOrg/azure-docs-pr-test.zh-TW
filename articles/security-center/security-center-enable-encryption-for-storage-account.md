---
title: "在 Azure 資訊安全中心的儲存體帳戶的 aaaEnable 加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 啟用加密的 Azure 儲存體帳戶 * *。"
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="af9c5-103">在 Azure 資訊安全中心啟用 Azure 儲存體帳戶的加密</span><span class="sxs-lookup"><span data-stu-id="af9c5-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="af9c5-104">Azure 資訊安全中心可能建議您對待用資料啟用 Azure 儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="af9c5-105">儲存體服務加密 (SSE) 中的運作方式 hello 資料寫入 tooAzure 儲存時加密和解密 hello 之前擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="af9c5-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="af9c5-106">SSE 目前僅適用於 hello Azure Blob 服務可用於區塊 blob，分頁 blob，並附加 blob。</span><span class="sxs-lookup"><span data-stu-id="af9c5-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="af9c5-107">詳細資訊，請參閱 toolearn[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="af9c5-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="af9c5-108">啟用加密之後，只有新的資料會加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="af9c5-109">儲存體帳戶中任何現有的 blob 保持未加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="af9c5-110">tooencrypt 現有的 blob，請參閱 hello[儲存體服務加密常見問題集](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。</span><span class="sxs-lookup"><span data-stu-id="af9c5-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="af9c5-111">只有 Resource Manager 儲存體帳戶才支援儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="af9c5-112">目前不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="af9c5-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="af9c5-113">傳統的 toounderstand hello 和資源管理員部署模型，請參閱[Azure 部署模型](../azure-classic-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="af9c5-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="af9c5-114">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="af9c5-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="af9c5-115">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="af9c5-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="af9c5-116">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="af9c5-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="af9c5-117">在 hello**建議**刀鋒視窗中，選取**啟用 Azure 儲存體帳戶的加密**。</span><span class="sxs-lookup"><span data-stu-id="af9c5-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="af9c5-118">![啟用儲存體帳戶的加密][1]</span><span class="sxs-lookup"><span data-stu-id="af9c5-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="af9c5-119">hello**啟用儲存體加密**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="af9c5-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="af9c5-120">此刀鋒視窗會列出 hello Azure 儲存體帳戶已停用儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="af9c5-121">在此範例中，我們選取 [storageacct1]。</span><span class="sxs-lookup"><span data-stu-id="af9c5-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="af9c5-122">![啟用儲存體加密][2]</span><span class="sxs-lookup"><span data-stu-id="af9c5-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="af9c5-123">hello**加密**刀鋒伺服器**storageacct1**隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="af9c5-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="af9c5-124">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="af9c5-124">Select **Enabled**.</span></span>
   <span data-ttu-id="af9c5-125">![加密刀鋒視窗][3]</span><span class="sxs-lookup"><span data-stu-id="af9c5-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="af9c5-126">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="af9c5-126">Select **Save**.</span></span>

<span data-ttu-id="af9c5-127">您現在已啟用 **storageacct1** 的儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="af9c5-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="af9c5-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af9c5-128">See also</span></span>
<span data-ttu-id="af9c5-129">這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 啟用加密的 Azure 儲存體帳戶。 」</span><span class="sxs-lookup"><span data-stu-id="af9c5-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="af9c5-130">toolearn 進一步了解 Azure 儲存體服務加密，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="af9c5-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="af9c5-131">待用資料的 Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="af9c5-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="af9c5-132">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="af9c5-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="af9c5-133">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="af9c5-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="af9c5-134">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="af9c5-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="af9c5-135">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="af9c5-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="af9c5-136">[在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="af9c5-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="af9c5-137">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="af9c5-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="af9c5-138">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="af9c5-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
