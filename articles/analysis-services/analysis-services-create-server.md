---
title: "在 Azure 中的 Analysis Services 伺服器 aaaCreate |Microsoft 文件"
description: "了解 toocreate Analysis Services 伺服器在 Azure 中的執行個體。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="0406b-103">在 Azure 入口網站中建立 Azure Analysis Services 伺服器</span><span class="sxs-lookup"><span data-stu-id="0406b-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="0406b-104">本文將逐步引導您在 Azure 訂用帳戶中建立 Analysis Services 伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="0406b-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0406b-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="0406b-105">Before you begin</span></span>
<span data-ttu-id="0406b-106">toocomplete 本快速入門中，您需要：</span><span class="sxs-lookup"><span data-stu-id="0406b-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="0406b-107">**Azure 訂用帳戶**： 瀏覽[Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0406b-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="0406b-108">**Azure Active Directory**：您的訂用帳戶必須與 Azure Active Directory 租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="0406b-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="0406b-109">此外，您必須使用 Azure Active Directory 中的帳戶登入 tooAzure toobe。</span><span class="sxs-lookup"><span data-stu-id="0406b-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="0406b-110">不支援 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0406b-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="0406b-111">詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。</span><span class="sxs-lookup"><span data-stu-id="0406b-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="0406b-112">**資源群組**：使用現有資源群組，或[建立新的群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0406b-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0406b-113">建立伺服器可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="0406b-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="0406b-114">詳細資訊，請參閱 toolearn [Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。</span><span class="sxs-lookup"><span data-stu-id="0406b-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="0406b-115">toocreate Azure 入口網站中的伺服器</span><span class="sxs-lookup"><span data-stu-id="0406b-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="0406b-116">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0406b-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="0406b-117">按一下 [+ 新增] > [資料 + 分析] > [Analysis Services]。</span><span class="sxs-lookup"><span data-stu-id="0406b-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="0406b-118">在 hello **Analysis Services**刀鋒視窗中，填寫必要的 hello 欄位，然後按**建立**。</span><span class="sxs-lookup"><span data-stu-id="0406b-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![建立伺服器](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="0406b-120">**伺服器名稱**： 輸入所使用的唯一名稱 tooreference hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0406b-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="0406b-121">**訂用帳戶**： 選取此伺服器帳單以 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0406b-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="0406b-122">**資源群組**： 這些容器會設計的 toohelp 管理 Azure 資源的集合。</span><span class="sxs-lookup"><span data-stu-id="0406b-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="0406b-123">詳細資訊，請參閱 toolearn[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0406b-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="0406b-124">**位置**： 此 Azure 資料中心位置主機 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0406b-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="0406b-125">請選擇最靠近最大使用者群體的位置。</span><span class="sxs-lookup"><span data-stu-id="0406b-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="0406b-126">**定價層**：選取定價層。</span><span class="sxs-lookup"><span data-stu-id="0406b-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="0406b-127">支援表格式模型向上 too400 GB。</span><span class="sxs-lookup"><span data-stu-id="0406b-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="0406b-128">詳細資訊，請參閱 toolearn [Azure Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。</span><span class="sxs-lookup"><span data-stu-id="0406b-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="0406b-129">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0406b-129">Click **Create**.</span></span>

<span data-ttu-id="0406b-130">建立程序通常不到一分鐘即可完成；往往在數秒內。</span><span class="sxs-lookup"><span data-stu-id="0406b-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="0406b-131">如果您選取**新增 tooPortal**，瀏覽 tooyour 入口 toosee 新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="0406b-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="0406b-132">或者，您也可以瀏覽過**更多服務** > **Analysis Services** toosee 是否準備您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="0406b-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![儀表板](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="0406b-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0406b-134">Next steps</span></span>
<span data-ttu-id="0406b-135">一旦您已建立您的伺服器，您可以[部署模型](analysis-services-deploy.md)tooit 使用 SSDT 或 SSMS。</span><span class="sxs-lookup"><span data-stu-id="0406b-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="0406b-136">如果您部署 tooyour 伺服器模型連接 tooon 內部部署資料來源，您需要 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)您網路中的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0406b-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

