---
title: "管理網路安全性群組 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站管理網路安全性群組。"
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
ms.openlocfilehash: ecb4fb4608628f5a1bd54fac6af19fecfa4508f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="934a5-103">使用 Azure 入口網站管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="934a5-103">Manage network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="934a5-104">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="934a5-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="934a5-105">您也可以 [在傳統部署模型中建立 NSG](virtual-networks-create-nsg-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="934a5-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="934a5-106">以下的範例 PowerShell 命令會預期已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="934a5-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="934a5-107">如果您想要以本文件顯示的方式執行命令，請先依照下列方式建置測試環境：部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 [部署至 Azure]，視情況取代預設參數值，然後遵循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="934a5-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="934a5-108">下列步驟使用 **RG-NSG** 作為部署範本之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="934a5-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="934a5-109">建立 NSG-FrontEnd NSG</span><span class="sxs-lookup"><span data-stu-id="934a5-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="934a5-110">若要根據上述案例建立 **NSG-FrontEnd** NSG，請遵循下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="934a5-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="934a5-111">透過瀏覽器瀏覽至 http://portal.azure.com，並視需要使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="934a5-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="934a5-112">按一下 [瀏覽] >  > [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="934a5-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="934a5-114">在 [網路安全性群組] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="934a5-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="934a5-116">在 [建立網路安全性群組] 刀鋒視窗的 *RG-NSG* 資源群組中建立名為 *NSG-FrontEnd* 的 NSG，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="934a5-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure 入口網站 - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="934a5-118">建立現有 NSG 中的規則</span><span class="sxs-lookup"><span data-stu-id="934a5-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="934a5-119">若要從 Azure 入口網站建立現有 NSG 中的規則，請遵循下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="934a5-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="934a5-120">按一下 [瀏覽] >  > [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="934a5-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="934a5-121">在 NSG 清單中按一下 [NSG-FrontEnd] **NSG-FrontEnd** > </span><span class="sxs-lookup"><span data-stu-id="934a5-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure 入口網站 - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="934a5-123">在 [輸入安全性規則] 清單中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="934a5-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="934a5-125">在 [新增輸入安全性規則] 刀鋒視窗中，建立一個名為 web-rule 的規則，優先順序設為 [200]，以允許從任何來源經由 [TCP] 與連接埠 [80] 存取任何 VM，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="934a5-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="934a5-126">請注意，這些設定大部分已是預設值。</span><span class="sxs-lookup"><span data-stu-id="934a5-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure 入口網站 - 規則設定](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="934a5-128">數秒後，您會看到 NSG 中的新規則。</span><span class="sxs-lookup"><span data-stu-id="934a5-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Azure 入口網站 - 新增規則](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="934a5-130">重複步驟 6，建立名為 rdp-rule 的輸入規則，設定優先順序為 [250]，並允許透過 [TCP] 連接埠 [3389] 從任何來源存取任何 VM。</span><span class="sxs-lookup"><span data-stu-id="934a5-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="934a5-131">建立 NSG 與 FrontEnd 子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="934a5-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="934a5-132">按一下 [瀏覽 >]  >  [資源群組]  >  [RG NSG]。</span><span class="sxs-lookup"><span data-stu-id="934a5-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="934a5-133">在 [RG-NSG] 刀鋒視窗中，按一下 [...]  >  [TestVNet]。</span><span class="sxs-lookup"><span data-stu-id="934a5-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure 入口網站 - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="934a5-135">在 [設定] 刀鋒視窗中，按一下 [子網路] > [FrontEnd] > [網路安全性群組] > [NSG-FrontEnd]。</span><span class="sxs-lookup"><span data-stu-id="934a5-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="934a5-137">在 [FrontEnd] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="934a5-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure 入口網站 - 子網路設定](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="934a5-139">建立 NSG-BackEnd NSG</span><span class="sxs-lookup"><span data-stu-id="934a5-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="934a5-140">若要建立 **NSG-BackEnd** NSG 並將它與 **BackEnd** 子網路建立關聯，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="934a5-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="934a5-141">重複 [建立 NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) 中的步驟，建立名為 *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="934a5-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="934a5-142">重複 [在現有的 NSG 中建立規則](#Create-rules-in-an-existing-NSG) 中的步驟，建立下表中的 **輸入** 規則。</span><span class="sxs-lookup"><span data-stu-id="934a5-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="934a5-143">輸入規則</span><span class="sxs-lookup"><span data-stu-id="934a5-143">Inbound rule</span></span> | <span data-ttu-id="934a5-144">輸出規則</span><span class="sxs-lookup"><span data-stu-id="934a5-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure 入口網站 - 輸入規則](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure 入口網站 - 輸出規則](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="934a5-147">重複[建立 NSG 與 FrontEnd 子網路的關聯](#Associate-the-NSG-to-the-FrontEnd-subnet)中的步驟，建立 **NSG-Backend** NSG 與 **BackEnd** 子網路的關聯。</span><span class="sxs-lookup"><span data-stu-id="934a5-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="934a5-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="934a5-148">Next Steps</span></span>
* <span data-ttu-id="934a5-149">了解如何 [管理現有的 NSG](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="934a5-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="934a5-150">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="934a5-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

