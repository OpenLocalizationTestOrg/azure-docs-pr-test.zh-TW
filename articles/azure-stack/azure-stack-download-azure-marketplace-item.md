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
ms.openlocfilehash: 4baa1b675d2930cd111b5b8368ac081dc2b77841
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="62d5f-103">將市集項目從 Azure 下載到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="62d5f-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="62d5f-104">當您決定要將哪些內容包含在 Azure Stack 市集中時，應該考慮可從 Azure Marketplace 取得的內容。</span><span class="sxs-lookup"><span data-stu-id="62d5f-104">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="62d5f-105">您可以從已預先測試而能在 Azure Stack 上執行的 Azure Marketplace 項目策劃清單下載。</span><span class="sxs-lookup"><span data-stu-id="62d5f-105">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="62d5f-106">新項目會不斷新增到此清單中，因此請務必回來查看是否有新內容。</span><span class="sxs-lookup"><span data-stu-id="62d5f-106">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="62d5f-107">若要下載市集項目，您必須先[向 Azure 註冊 Azure Stack](azure-stack-register.md)。</span><span class="sxs-lookup"><span data-stu-id="62d5f-107">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="62d5f-108">下載</span><span class="sxs-lookup"><span data-stu-id="62d5f-108">Download</span></span>
1. <span data-ttu-id="62d5f-109">登入 Azure Stack 系統管理員入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="62d5f-109">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="62d5f-110">有些市集項目可能非常龐大。</span><span class="sxs-lookup"><span data-stu-id="62d5f-110">Some marketplace items can be very large.</span></span>  <span data-ttu-id="62d5f-111">按一下 [資源提供者] > [儲存體] 來檢查，以確定您的系統上有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="62d5f-111">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="62d5f-112">按一下 [更多服務] > [市集管理]。</span><span class="sxs-lookup"><span data-stu-id="62d5f-112">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="62d5f-113">按一下 [從 Azure 新增] 以查看可供下載的項目清單。</span><span class="sxs-lookup"><span data-stu-id="62d5f-113">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="62d5f-114">您可以按一下清單中的每個項目來檢視其描述與下載大小。</span><span class="sxs-lookup"><span data-stu-id="62d5f-114">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="62d5f-115">選取清單中您想要的項目，然後按一下 [下載]。</span><span class="sxs-lookup"><span data-stu-id="62d5f-115">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="62d5f-116">這會開始下載您所選項目的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="62d5f-116">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="62d5f-117">下載時間會有所不同。</span><span class="sxs-lookup"><span data-stu-id="62d5f-117">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="62d5f-118">下載完成之後，您可以用雲端操作員或租用戶使用者身分來部署新市集項目。</span><span class="sxs-lookup"><span data-stu-id="62d5f-118">After the download completes, you can deploy your new marketplace item as either a cloud operator or tenant user.</span></span> <span data-ttu-id="62d5f-119">按一下 [+新增]，在類別中搜尋新市集項目，然後選取該項目。</span><span class="sxs-lookup"><span data-stu-id="62d5f-119">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="62d5f-120">按一下 [建立] 以開啟新下載項目的建立體驗。</span><span class="sxs-lookup"><span data-stu-id="62d5f-120">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="62d5f-121">依照逐步指示來部署您的項目。</span><span class="sxs-lookup"><span data-stu-id="62d5f-121">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62d5f-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62d5f-122">Next steps</span></span>

[<span data-ttu-id="62d5f-123">建立及發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="62d5f-123">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
