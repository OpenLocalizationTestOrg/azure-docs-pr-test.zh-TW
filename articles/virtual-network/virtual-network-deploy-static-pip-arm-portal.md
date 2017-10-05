---
title: "建立具有靜態公用 IP 位址的 VM - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站建立具有靜態公用 IP 位址的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="8be83-103">使用 Azure 入口網站建立具有靜態公用 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="8be83-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8be83-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8be83-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="8be83-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8be83-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="8be83-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8be83-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="8be83-107">範本</span><span class="sxs-lookup"><span data-stu-id="8be83-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="8be83-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="8be83-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8be83-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8be83-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8be83-110">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="8be83-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="8be83-111">使用靜態公用 IP 建立 VM</span><span class="sxs-lookup"><span data-stu-id="8be83-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="8be83-112">若要在 Azure 入口網站中建立具有靜態公用 IP 位址的 VM，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8be83-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="8be83-113">透過瀏覽器瀏覽至 [Azure 入口網站](https://portal.azure.com) ，並視需要使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="8be83-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="8be83-114">在入口網站左上角，按一下 [新增]>>[計算]>[Windows Server 2012 R2 Datacenter]。</span><span class="sxs-lookup"><span data-stu-id="8be83-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="8be83-115">在 [選取部署模型] 清單中，選取 [Resource Manager]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="8be83-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="8be83-116">在 [基本] 刀鋒視窗中，輸入如下所示的 VM 資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8be83-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure 入口網站 - 基本](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="8be83-118">在 [選擇大小] 刀鋒視窗中，按一下如下所示的 [A1 標準]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="8be83-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure 入口網站 - 選擇大小](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="8be83-120">在 [設定] 刀鋒視窗中，按一下 [公用 IP 位址]，接著在 [建立公用 IP 位址] 刀鋒視窗的 [指派] 底下，按一下 [靜態]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8be83-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="8be83-121">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8be83-121">And then click **OK**.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="8be83-123">在 [設定] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8be83-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="8be83-124">檢視如下所示的 [摘要] 刀鋒視窗，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8be83-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="8be83-126">請注意您儀表板中新的磚。</span><span class="sxs-lookup"><span data-stu-id="8be83-126">Notice the new tile in your dashboard.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="8be83-128">VM 建立後，[設定]  刀鋒視窗隨即出現，如下所示</span><span class="sxs-lookup"><span data-stu-id="8be83-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

