---
title: "在 Azure 中的 aaaUse Windows 用戶端映像 |Microsoft 文件"
description: "如何 toouse Visual Studio 訂閱優點 toodeploy Windows 7、 Windows 8 或 Windows 10 在 Azure 中開發/測試案例"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a><span data-ttu-id="fb23b-103">在 Azure 中使用 Windows 用戶端進行開發/測試案例</span><span class="sxs-lookup"><span data-stu-id="fb23b-103">Use Windows client in Azure for dev/test scenarios</span></span>
<span data-ttu-id="fb23b-104">假設您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 進行開發/測試案例。</span><span class="sxs-lookup"><span data-stu-id="fb23b-104">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="fb23b-105">本文將概述在 Azure 中並使用 hello 的 Azure 資源庫映像執行 Windows 用戶端 hello 資格需求。</span><span class="sxs-lookup"><span data-stu-id="fb23b-105">This article outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="subscription-eligibility"></a><span data-ttu-id="fb23b-106">訂用帳戶資格</span><span class="sxs-lookup"><span data-stu-id="fb23b-106">Subscription eligibility</span></span>
<span data-ttu-id="fb23b-107">有效的 Visual Studio 訂閱者 (已取得 Visual Studio 訂用帳戶授權的人) 可以使用 Windows 用戶端進行開發和測試。</span><span class="sxs-lookup"><span data-stu-id="fb23b-107">Active Visual Studio subscribers (people who have acquired a Visual Studio subscription license) can use Windows client for development and testing purposes.</span></span> <span data-ttu-id="fb23b-108">Windows 用戶端可以用在您自己的硬體及以任何類型的 Azure 訂用帳戶執行的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fb23b-108">Windows client can be used on your own hardware and Azure virtual machines running in any type of Azure subscription.</span></span> <span data-ttu-id="fb23b-109">Windows 用戶端可能不是已部署的 tooor Azure 用於一般實際執行環境，或使用不是有效的 Visual Studio 訂閱者的人員。</span><span class="sxs-lookup"><span data-stu-id="fb23b-109">Windows client may not be deployed tooor used on Azure for normal production use, or used by people who are not active Visual Studio subscribers.</span></span>

<span data-ttu-id="fb23b-110">為了方便起見，我們進行了特定的 Windows 10 映像可從 hello Azure 組件庫內[適合開發/測試提供](#eligible-offers)。</span><span class="sxs-lookup"><span data-stu-id="fb23b-110">For your convenience, we have made certain Windows 10 images available from hello Azure Gallery within [eligible dev/test offers](#eligible-offers).</span></span> <span data-ttu-id="fb23b-111">提供項目的任何型別中的 visual Studio 訂閱者也可以[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像，然後[上載 tooAzure](upload-generalized-managed.md)。</span><span class="sxs-lookup"><span data-stu-id="fb23b-111">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="fb23b-112">hello 使用仍有限的 toodev/測試的方法是使用 Visual Studio 的 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="fb23b-112">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

## <a name="eligible-offers"></a><span data-ttu-id="fb23b-113">符合資格者的優惠</span><span class="sxs-lookup"><span data-stu-id="fb23b-113">Eligible offers</span></span>
<span data-ttu-id="fb23b-114">下列資料表詳細資料 hello hello 供應項目會透過 hello Azure 組件庫的合格 toodeploy Windows 10 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="fb23b-114">hello following table details hello offer IDs that are eligible toodeploy Windows 10 through hello Azure Gallery.</span></span> <span data-ttu-id="fb23b-115">hello Windows 10 映像只會顯示 toohello 遵循優惠。</span><span class="sxs-lookup"><span data-stu-id="fb23b-115">hello Windows 10 images are only visible toohello following offers.</span></span> <span data-ttu-id="fb23b-116">Visual Studio 訂閱者需要 toorun 其他優惠類型中的 Windows 用戶端需要太[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像和[然後上傳 tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="fb23b-116">Visual Studio subscribers who need toorun Windows client in a different offer type require you too[adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and [then upload tooAzure](upload-generalized-managed.md).</span></span>

| <span data-ttu-id="fb23b-117">優惠名稱</span><span class="sxs-lookup"><span data-stu-id="fb23b-117">Offer Name</span></span> | <span data-ttu-id="fb23b-118">優惠號碼</span><span class="sxs-lookup"><span data-stu-id="fb23b-118">Offer Number</span></span> | <span data-ttu-id="fb23b-119">可用的用戶端映像</span><span class="sxs-lookup"><span data-stu-id="fb23b-119">Available client images</span></span> |
|:--- |:---:|:---:|
| [<span data-ttu-id="fb23b-120">隨用隨付開發/測試</span><span class="sxs-lookup"><span data-stu-id="fb23b-120">Pay-As-You-Go Dev/Test</span></span>](https://azure.microsoft.com/offers/ms-azr-0023p/) |<span data-ttu-id="fb23b-121">0023P</span><span class="sxs-lookup"><span data-stu-id="fb23b-121">0023P</span></span> |<span data-ttu-id="fb23b-122">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-122">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-123">Visual Studio Enterprise (MPN) 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fb23b-123">Visual Studio Enterprise (MPN) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0029p/) |<span data-ttu-id="fb23b-124">0029P</span><span class="sxs-lookup"><span data-stu-id="fb23b-124">0029P</span></span> |<span data-ttu-id="fb23b-125">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-125">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-126">Visual Studio Professional 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fb23b-126">Visual Studio Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0059p/) |<span data-ttu-id="fb23b-127">0059P</span><span class="sxs-lookup"><span data-stu-id="fb23b-127">0059P</span></span> |<span data-ttu-id="fb23b-128">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-128">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-129">Visual Studio Test Professional 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fb23b-129">Visual Studio Test Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0060p/) |<span data-ttu-id="fb23b-130">0060P</span><span class="sxs-lookup"><span data-stu-id="fb23b-130">0060P</span></span> |<span data-ttu-id="fb23b-131">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-131">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-132">Visual Studio Premium 含 MSDN (權益)</span><span class="sxs-lookup"><span data-stu-id="fb23b-132">Visual Studio Premium with MSDN (benefit)</span></span>](https://azure.microsoft.com/offers/ms-azr-0061p/) |<span data-ttu-id="fb23b-133">0061P</span><span class="sxs-lookup"><span data-stu-id="fb23b-133">0061P</span></span> |<span data-ttu-id="fb23b-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-134">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-135">Visual Studio Enterprise 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fb23b-135">Visual Studio Enterprise subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0063p/) |<span data-ttu-id="fb23b-136">0063P</span><span class="sxs-lookup"><span data-stu-id="fb23b-136">0063P</span></span> |<span data-ttu-id="fb23b-137">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-137">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-138">Visual Studio Enterprise (BizSpark) 訂閱者</span><span class="sxs-lookup"><span data-stu-id="fb23b-138">Visual Studio Enterprise (BizSpark) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0064p/) |<span data-ttu-id="fb23b-139">0064P</span><span class="sxs-lookup"><span data-stu-id="fb23b-139">0064P</span></span> |<span data-ttu-id="fb23b-140">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-140">Windows 10</span></span> |
| [<span data-ttu-id="fb23b-141">Enterprise 開發/測試</span><span class="sxs-lookup"><span data-stu-id="fb23b-141">Enterprise Dev/Test</span></span>](https://azure.microsoft.com/ofers/ms-azr-0148p/) |<span data-ttu-id="fb23b-142">0148P</span><span class="sxs-lookup"><span data-stu-id="fb23b-142">0148P</span></span> |<span data-ttu-id="fb23b-143">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fb23b-143">Windows 10</span></span> |

## <a name="check-your-azure-subscription"></a><span data-ttu-id="fb23b-144">檢查您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fb23b-144">Check your Azure subscription</span></span>
<span data-ttu-id="fb23b-145">如果您不知道您的優惠識別碼，您可以取得它透過 hello Azure 入口網站，這兩種方式之一：</span><span class="sxs-lookup"><span data-stu-id="fb23b-145">If you do not know your offer ID, you can obtain it through hello Azure portal in one of these two ways:</span></span>  

- <span data-ttu-id="fb23b-146">Hello 'Subscriptions' 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="fb23b-146">On hello 'Subscriptions' blade:</span></span>

  ![從 hello Azure 入口網站的優惠識別碼詳細資料](./media/client-images/offer-id-azure-portal.png) 

- <span data-ttu-id="fb23b-148">或者，按一下 [計費]，然後按一下訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="fb23b-148">Or, click **Billing** and then click your subscription ID.</span></span> <span data-ttu-id="fb23b-149">hello 供應項目識別碼會出現在 hello 帳單 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb23b-149">hello offer ID appears in hello Billing blade.</span></span>

<span data-ttu-id="fb23b-150">您也可以檢視從 hello hello 供應項目識別碼['Subscriptions' 索引標籤](http://account.windowsazure.com/Subscriptions)hello Azure 帳戶入口網站的：</span><span class="sxs-lookup"><span data-stu-id="fb23b-150">You can also view hello offer ID from hello ['Subscriptions' tab](http://account.windowsazure.com/Subscriptions) of hello Azure Account portal:</span></span>

![從 hello Azure 帳戶入口網站中提供識別碼詳細資料](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a><span data-ttu-id="fb23b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb23b-152">Next steps</span></span>
<span data-ttu-id="fb23b-153">您現在可以使用 [PowerShell](quick-create-powershell.md)、[Resource Manager templates](ps-template.md) 或 [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 來部署您的 VM。</span><span class="sxs-lookup"><span data-stu-id="fb23b-153">You can now deploy your VMs using [PowerShell](quick-create-powershell.md), [Resource Manager templates](ps-template.md), or [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

