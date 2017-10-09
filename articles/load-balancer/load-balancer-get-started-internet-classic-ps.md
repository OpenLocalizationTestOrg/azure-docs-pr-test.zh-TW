---
title: "aaaCreate 網際網路對向負載平衡器-傳統的 Azure PowerShell |Microsoft 文件"
description: "了解如何的 toocreate 網際網路向負載平衡器中使用 PowerShell 的傳統模式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="fe366-103">開始在 PowerShell 中建立網際網路面向的負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="fe366-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe366-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="fe366-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="fe366-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe366-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="fe366-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fe366-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="fe366-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fe366-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="fe366-108">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="fe366-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fe366-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="fe366-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="fe366-110">您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。</span><span class="sxs-lookup"><span data-stu-id="fe366-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="fe366-111">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fe366-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="fe366-112">您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="fe366-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="fe366-113">使用 PowerShell 設定負載平衡器</span><span class="sxs-lookup"><span data-stu-id="fe366-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="fe366-114">tooset 設定負載平衡器使用 powershell，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="fe366-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="fe366-115">如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe366-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="fe366-116">建立虛擬機器之後，您可以使用 PowerShell cmdlet tooadd 負載平衡器 tooa 虛擬機器內 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fe366-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="fe366-117">在 hello 下列的範例，您將加入負載平衡器集稱為 「 web 伺服陣列 」 toocloud 服務 」 mytestcloud 」 （或 myctestcloud.cloudapp.net），加入 hello hello 端點負載平衡器 toovirtual 機器命名為"web1"和"web2"。</span><span class="sxs-lookup"><span data-stu-id="fe366-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="fe366-118">hello 負載平衡器會接收連接埠 80 上的網路流量並 hello hello 本機端點 （在本案例通訊埠 80） 所定義的虛擬機器之間進行負載平衡使用 TCP。</span><span class="sxs-lookup"><span data-stu-id="fe366-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="fe366-119">步驟 1</span><span class="sxs-lookup"><span data-stu-id="fe366-119">Step 1</span></span>

<span data-ttu-id="fe366-120">建立 hello 第一個 VM 「 web1 」 的負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="fe366-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="fe366-121">步驟 2</span><span class="sxs-lookup"><span data-stu-id="fe366-121">Step 2</span></span>

<span data-ttu-id="fe366-122">建立另一個端點 hello 第二個 VM 「 web2 」 使用 hello 相同負載平衡器集名稱</span><span class="sxs-lookup"><span data-stu-id="fe366-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="fe366-123">從負載平衡器移除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe366-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="fe366-124">您可以使用移除 AzureEndpoint tooremove 從 hello 負載平衡器虛擬機器端點</span><span class="sxs-lookup"><span data-stu-id="fe366-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="fe366-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe366-125">Next steps</span></span>

<span data-ttu-id="fe366-126">您也可以[開始建立內部負載平衡器](load-balancer-get-started-ilb-classic-ps.md)，以及為特定負載平衡器的網路流量行為設定何種[分配模式](load-balancer-distribution-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="fe366-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="fe366-127">如果您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，您可以瞭解多[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="fe366-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="fe366-128">當您使用 Azure 負載平衡器，它會協助 toolearn 有關閒置連線行為。</span><span class="sxs-lookup"><span data-stu-id="fe366-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
