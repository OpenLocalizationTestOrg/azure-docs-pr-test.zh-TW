---
title: "aaaManage 網路安全性群組-Azure 入口網站 |Microsoft 文件"
description: "了解如何使用將 toomanage 網路安全性群組 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="81117-103">管理使用 hello Azure 入口網站的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="81117-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="81117-104">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="81117-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="81117-105">您也可以[hello 傳統部署模型中建立 Nsg](virtual-networks-create-nsg-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="81117-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="81117-106">hello 範例 PowerShell 預期簡單的環境中已經建立下列命令會根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="81117-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="81117-107">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="81117-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="81117-108">使用以下步驟 hello **RG NSG** hello hello 資源群組 hello 範本名稱已部署至。</span><span class="sxs-lookup"><span data-stu-id="81117-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="81117-109">建立 hello NSG 前端 NSG</span><span class="sxs-lookup"><span data-stu-id="81117-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="81117-110">toocreate hello **NSG 前端**NSG 示 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="81117-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="81117-111">從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="81117-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="81117-112">按一下 [瀏覽] >  > [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="81117-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="81117-114">在 hello**網路安全性群組**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="81117-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="81117-116">在 hello**建立網路安全性群組**刀鋒視窗中，建立名為 NSG *NSG 前端*hello 中*RG NSG*資源群組，然後再按一下**建立**.</span><span class="sxs-lookup"><span data-stu-id="81117-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="81117-118">建立現有 NSG 中的規則</span><span class="sxs-lookup"><span data-stu-id="81117-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="81117-119">toocreate hello Azure 入口網站，從現有 NSG 中的規則，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="81117-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="81117-120">按一下 [瀏覽] >  > [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="81117-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="81117-121">在 hello Nsg 清單中按一下**NSG 前端** > **輸入安全性規則**</span><span class="sxs-lookup"><span data-stu-id="81117-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure 入口網站 - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="81117-123">中的 hello 清單**輸入安全性規則**，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="81117-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="81117-125">在 hello**新增連入的安全性規則**刀鋒視窗中，建立名為的規則*網頁規則*優先順序為*200*允許存取透過*TCP* tooport*80* tooany VM 從任何來源，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="81117-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="81117-126">請注意，這些設定大部分已是預設值。</span><span class="sxs-lookup"><span data-stu-id="81117-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure 入口網站 - 規則設定](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="81117-128">幾秒之後，您會看見 hello hello NSG 中的新規則。</span><span class="sxs-lookup"><span data-stu-id="81117-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="81117-130">重複步驟 too6 toocreate 名為的輸入的規則*rdp 規則*優先順序為*250*允許存取透過*TCP* tooport *3389*tooany 從任何來源的 VM。</span><span class="sxs-lookup"><span data-stu-id="81117-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="81117-131">Hello NSG toohello 前端子網路建立關聯</span><span class="sxs-lookup"><span data-stu-id="81117-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="81117-132">按一下 [瀏覽 >]  >  [資源群組]  >  [RG NSG]。</span><span class="sxs-lookup"><span data-stu-id="81117-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="81117-133">在 hello **RG NSG**刀鋒視窗中，按一下  **...**  >  **TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="81117-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure 入口網站 - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="81117-135">在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="81117-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="81117-137">在 hello**前端**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="81117-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="81117-139">建立 hello NSG 後端 NSG</span><span class="sxs-lookup"><span data-stu-id="81117-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="81117-140">toocreate hello **NSG 後端**NSG，並將它關聯 toohello**後端**子網路，後續 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="81117-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="81117-141">中的步驟重複 hello[建立 hello NSG 前端 NSG](#Create-the-NSG-FrontEnd-NSG) toocreate NSG 名為*NSG 後端*</span><span class="sxs-lookup"><span data-stu-id="81117-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="81117-142">中的步驟重複 hello[建立現有 NSG 中的規則](#Create-rules-in-an-existing-NSG)toocreate hello**輸入**hello 表中的規則。</span><span class="sxs-lookup"><span data-stu-id="81117-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="81117-143">輸入規則</span><span class="sxs-lookup"><span data-stu-id="81117-143">Inbound rule</span></span> | <span data-ttu-id="81117-144">輸出規則</span><span class="sxs-lookup"><span data-stu-id="81117-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure 入口網站 - 輸入規則](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure 入口網站 - 輸出規則](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="81117-147">中的步驟重複 hello [hello NSG toohello 前端子網路建立關聯](#Associate-the-NSG-to-the-FrontEnd-subnet)tooassociate hello **NSG 後端**NSG toohello**後端**子網路。</span><span class="sxs-lookup"><span data-stu-id="81117-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81117-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81117-148">Next Steps</span></span>
* <span data-ttu-id="81117-149">了解如何太[管理現有的 Nsg](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="81117-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="81117-150">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="81117-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

