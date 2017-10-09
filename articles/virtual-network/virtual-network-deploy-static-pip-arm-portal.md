---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 具有靜態公用 IP 位址使用的 VM hello Azure 入口網站。"
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
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="3efe8-103">使用靜態公用 IP 位址使用 hello Azure 入口網站建立 VM</span><span class="sxs-lookup"><span data-stu-id="3efe8-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3efe8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3efe8-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="3efe8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3efe8-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="3efe8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3efe8-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="3efe8-107">範本</span><span class="sxs-lookup"><span data-stu-id="3efe8-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="3efe8-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="3efe8-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="3efe8-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3efe8-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3efe8-110">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="3efe8-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="3efe8-111">使用靜態公用 IP 建立 VM</span><span class="sxs-lookup"><span data-stu-id="3efe8-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="3efe8-112">toocreate 中 hello Azure 入口網站中，完成下列步驟的 hello VM 的靜態公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="3efe8-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="3efe8-113">從瀏覽器中，瀏覽 toohello [Azure 入口網站](https://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="3efe8-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3efe8-114">Hello hello 入口網站的最上層的左下角，按一下**新增**>>**計算**>**Windows Server 2012 R2 Datacenter**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="3efe8-115">在 hello**選取部署模型**清單中，選取**資源管理員**按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="3efe8-116">在 hello**基本概念**刀鋒視窗中，輸入 hello VM 資訊，如下所示，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure 入口網站 - 基本](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="3efe8-118">在 hello**大小選擇 「**刀鋒視窗中，按一下 **標準 A1**如下所示，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure 入口網站 - 選擇大小](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="3efe8-120">在 hello**設定**刀鋒視窗中，按一下 **公用 IP 位址**，然後在 hello**建立公用 IP 位址**刀鋒視窗底下**指派**，按一下**靜態**如下所示。</span><span class="sxs-lookup"><span data-stu-id="3efe8-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="3efe8-121">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3efe8-121">And then click **OK**.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="3efe8-123">在 hello**設定**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="3efe8-124">檢閱 hello**摘要**刀鋒視窗，如下所示，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="3efe8-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="3efe8-126">請注意您的儀表板中的 hello 新磚。</span><span class="sxs-lookup"><span data-stu-id="3efe8-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="3efe8-128">一旦建立 hello VM，hello**設定**刀鋒視窗會顯示，如下所示</span><span class="sxs-lookup"><span data-stu-id="3efe8-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure 入口網站 - 建立公用 IP 位址](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

