---
title: "從 Azure 下載市集項目 | Microsoft Docs"
description: "我可以將市集項目從 Azure 下載到我的 Azure Stack 部署。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: erikje
ms.openlocfilehash: 4d7c335a3c68cc9bb8cb0c823883716a3dd6620a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="37d65-103">將市集項目從 Azure 下載到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="37d65-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="37d65-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="37d65-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="37d65-105">當您決定要將哪些內容包含在 Azure Stack 市集中時，應該考慮可從 Azure Marketplace 取得的內容。</span><span class="sxs-lookup"><span data-stu-id="37d65-105">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="37d65-106">您可以從已預先測試而能在 Azure Stack 上執行的 Azure Marketplace 項目策劃清單下載。</span><span class="sxs-lookup"><span data-stu-id="37d65-106">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="37d65-107">新項目會不斷新增到此清單中，因此請務必回來查看是否有新內容。</span><span class="sxs-lookup"><span data-stu-id="37d65-107">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="37d65-108">若要下載市集項目，您必須先[向 Azure 註冊 Azure Stack](azure-stack-register.md)。</span><span class="sxs-lookup"><span data-stu-id="37d65-108">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="37d65-109">下載</span><span class="sxs-lookup"><span data-stu-id="37d65-109">Download</span></span>
1. <span data-ttu-id="37d65-110">登入 Azure Stack 系統管理員入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="37d65-110">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="37d65-111">有些市集項目可能非常龐大。</span><span class="sxs-lookup"><span data-stu-id="37d65-111">Some marketplace items can be very large.</span></span>  <span data-ttu-id="37d65-112">按一下 [資源提供者] > [儲存體] 來檢查，以確定您的系統上有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="37d65-112">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="37d65-113">按一下 [更多服務] > [市集管理]。</span><span class="sxs-lookup"><span data-stu-id="37d65-113">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="37d65-114">按一下 [從 Azure 新增] 以查看可供下載的項目清單。</span><span class="sxs-lookup"><span data-stu-id="37d65-114">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="37d65-115">您可以按一下清單中的每個項目來檢視其描述與下載大小。</span><span class="sxs-lookup"><span data-stu-id="37d65-115">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="37d65-116">選取清單中您想要的項目，然後按一下下載。</span><span class="sxs-lookup"><span data-stu-id="37d65-116">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="37d65-117">這會開始下載您所選項目的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="37d65-117">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="37d65-118">下載時間會有所不同。</span><span class="sxs-lookup"><span data-stu-id="37d65-118">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="37d65-119">下載完成之後，您可以用 Azure Stack 操作員或使用者身分來部署新市集項目。</span><span class="sxs-lookup"><span data-stu-id="37d65-119">After the download completes, you can deploy your new marketplace item as either an Azure Stack operator or user.</span></span> <span data-ttu-id="37d65-120">按一下 [+新增]，在類別中搜尋新市集項目，然後選取該項目。</span><span class="sxs-lookup"><span data-stu-id="37d65-120">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="37d65-121">按一下 [建立] 以開啟新下載項目的建立體驗。</span><span class="sxs-lookup"><span data-stu-id="37d65-121">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="37d65-122">依照逐步指示來部署您的項目。</span><span class="sxs-lookup"><span data-stu-id="37d65-122">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37d65-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37d65-123">Next steps</span></span>

[<span data-ttu-id="37d65-124">建立及發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="37d65-124">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
