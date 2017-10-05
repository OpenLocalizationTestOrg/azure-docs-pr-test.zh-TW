---
title: "Azure Data Lake Store 常見問題集 | Microsoft Docs"
description: "針對 Azure Data Lake Store 的問題進行疑難排解或加以減緩的指導方針"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 44aaec9dc145b47b809a3ad4bc244eb9dfead24c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a><span data-ttu-id="5a1aa-103">Azure Data Lake Store 常見問題集</span><span class="sxs-lookup"><span data-stu-id="5a1aa-103">Frequently asked questions for Azure Data Lake Store</span></span>
<span data-ttu-id="5a1aa-104">在本文中，您將了解 Azure Data Lake Store 的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-104">In this article you will learn about FAQs related to Azure Data Lake Store.</span></span>

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a><span data-ttu-id="5a1aa-105">如何進一步保護我的資料以防止區域全面性災害或意外刪除？</span><span class="sxs-lookup"><span data-stu-id="5a1aa-105">How can I further protect my data from region-wide disasters or accidental deletions?</span></span>
<span data-ttu-id="5a1aa-106">透過自動化複本，Azure Data Lake Store 帳戶中的資料可彈性應對區域內發生的暫時性硬體故障。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-106">The data in your Azure Data Lake Store account is resilient to transient hardware failures within a region through automated replicas.</span></span> <span data-ttu-id="5a1aa-107">這可確保持久性和高可用性，符合 Azure Data Lake Store 的 SLA。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-107">This ensures durability and high availability, meeting the Azure Data Lake Store SLA.</span></span> <span data-ttu-id="5a1aa-108">以下提供了一些指引，說明如何進一步保護資料，使其不受罕見的全區停電或意外刪除事件影響。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-108">Here's some guidance on how to further protect your data from rare region-wide outages or accidental deletions.</span></span>

### <a name="disaster-recovery-guidance"></a><span data-ttu-id="5a1aa-109">災害復原指引</span><span class="sxs-lookup"><span data-stu-id="5a1aa-109">Disaster recovery guidance</span></span>
<span data-ttu-id="5a1aa-110">每位客戶備妥自己的災害復原計畫是相當重要的。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-110">It is critical for every customer to prepare their own disaster recovery plan.</span></span> <span data-ttu-id="5a1aa-111">請參閱下面的 Azure 文件，以建置災害復原計畫。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-111">Please refer to the Azure documentation below to build your disaster recovery plan.</span></span> <span data-ttu-id="5a1aa-112">這裡有一些資源可協助您建立自己的計畫。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-112">Here are some resources that can help you create your own plan.</span></span>

* [<span data-ttu-id="5a1aa-113">Azure 應用程式的災害復原和高可用性</span><span class="sxs-lookup"><span data-stu-id="5a1aa-113">Disaster recovery and high availability for Azure applications</span></span>](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [<span data-ttu-id="5a1aa-114">Azure 復原技術指導</span><span class="sxs-lookup"><span data-stu-id="5a1aa-114">Azure resiliency technical guidance</span></span>](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a><span data-ttu-id="5a1aa-115">最佳作法</span><span class="sxs-lookup"><span data-stu-id="5a1aa-115">Best practices</span></span>
<span data-ttu-id="5a1aa-116">我們建議您以符合災害復原計畫需求的頻率，將重要資料複製到位於其他區域的另一個 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-116">We recommend that you copy your critical data to another Data Lake Store account in another region with a frequency aligned to the needs of your disaster recovery plan.</span></span> <span data-ttu-id="5a1aa-117">您可以使用各種方法來複製資料，包括 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md)、[Azure PowerShell](data-lake-store-get-started-powershell.md) 或 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-117">There are a variety of methods to copy data including [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span> <span data-ttu-id="5a1aa-118">Azure Data Factory 這項服務很適合用來反覆建立和部署資料移動管線。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-118">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="5a1aa-119">發生區域性停電時，您可以立即從資料所複製到的區域存取資料。您可以監視 [Azure 服務健康狀況儀表板](https://azure.microsoft.com/status/)以判斷全球各地 Azure 服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-119">If a regional outage occurs, you can then access your data in the region where the data was copied.You can monitor the [Azure Service Health Dashboard](https://azure.microsoft.com/status/) to determine the Azure service status across the globe.</span></span>

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a><span data-ttu-id="5a1aa-120">資料損毀或意外刪除復原指引</span><span class="sxs-lookup"><span data-stu-id="5a1aa-120">Data corruption or accidental deletion recovery guidance</span></span>
<span data-ttu-id="5a1aa-121">雖然 Azure Data Lake Store 可透過自動化複本提供資料恢復，但這無法防止應用程式 (或開發人員/使用者) 的資料遭到損毀或意外刪除。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-121">While Azure Data Lake Store provides data resiliency through automated replicas, this does not prevent your application (or developers/users) from corrupting data or accidentally deleting it.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="5a1aa-122">最佳作法</span><span class="sxs-lookup"><span data-stu-id="5a1aa-122">Best practices</span></span>
<span data-ttu-id="5a1aa-123">若要防止意外刪除，建議您先為 Data Lake Store 帳戶設定正確的存取原則。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-123">To prevent accidental deletion, we recommend that you first set the correct access policies for your Data Lake Store account.</span></span>  <span data-ttu-id="5a1aa-124">這包括套用 [Azure 資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)來鎖定重要資源，以及套用採用可用 [Data Lake Store 安全性功能](data-lake-store-security-overview.md)的帳戶和檔案層級存取控制。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-124">This includes applying [Azure resource locks](../azure-resource-manager/resource-group-lock-resources.md) to lock down important resources as well as applying account and file level access control using the available [Data Lake Store security features](data-lake-store-security-overview.md).</span></span> <span data-ttu-id="5a1aa-125">另外，也建議您使用 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md)、[Azure PowerShell](data-lake-store-get-started-powershell.md) 或 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)，在另一個 Data Lake Store 帳戶、資料夾或 Azure 訂用帳戶定期建立重要資料的複本。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-125">We also recommend that you routinely create copies of your critical data using [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) in another Data Lake Store account, folder, or Azure subscription.</span></span>  <span data-ttu-id="5a1aa-126">這可用來從資料損毀或刪除事件中復原。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-126">This can be used to recover from a data corruption or deletion incident.</span></span> <span data-ttu-id="5a1aa-127">Azure Data Factory 這項服務很適合用來反覆建立和部署資料移動管線。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-127">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="5a1aa-128">組織也可以啟用 Azure Data Lake Store 帳戶的[診斷記錄](data-lake-store-diagnostic-logs.md)，收集資料存取稽核線索來提供刪除或更新檔案之可疑人員的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a1aa-128">Organizations can also enable [diagnostic logging](data-lake-store-diagnostic-logs.md) for their Azure Data Lake Store account to collect data access audit trails that provides information about who might have deleted or updated a file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a1aa-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a1aa-129">Next steps</span></span>
* [<span data-ttu-id="5a1aa-130">開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5a1aa-130">Get Started with Azure Data Lake Store</span></span>](data-lake-store-get-started-portal.md)
* [<span data-ttu-id="5a1aa-131">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="5a1aa-131">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

