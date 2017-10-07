---
title: "aaaUse Azure 堆疊中的 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何在 Azure 堆疊 tooprovision 資源 toouse Azure Resource Manager 範本。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="4fa2e-103">在 Azure Stack 中使用 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="4fa2e-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="4fa2e-104">Azure 資源管理員範本部署和佈建您的應用程式在單一、 協調作業中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-104">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="4fa2e-105">您也可以重新部署範本 toomake 變更 toohello 資源 hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-105">You can also redeploy templates toomake changes toohello resources in hello resource group.</span></span>

<span data-ttu-id="4fa2e-106">這些範本可以部署與 hello Microsoft Azure 堆疊入口網站、 PowerShell、 hello 命令列，以及 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-106">These templates can be deployed with hello Microsoft Azure Stack portal, PowerShell, hello command line, and Visual Studio.</span></span>

<span data-ttu-id="4fa2e-107">hello 遵循快速入門範本位於[GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="4fa2e-107">hello following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="4fa2e-108">部署 SharePoint (非高可用性)</span><span class="sxs-lookup"><span data-stu-id="4fa2e-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="4fa2e-109">使用 hello PowerShell DSC 延伸模組 toocreate SharePoint 2013 伺服器陣列，其中包含 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="4fa2e-109">Use hello PowerShell DSC extension toocreate a SharePoint 2013 farm that includes hello following resources:</span></span>

* <span data-ttu-id="4fa2e-110">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4fa2e-110">A virtual network</span></span>
* <span data-ttu-id="4fa2e-111">三個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4fa2e-111">Three storage accounts</span></span>
* <span data-ttu-id="4fa2e-112">兩個外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-112">Two external load balancers</span></span>
* <span data-ttu-id="4fa2e-113">一部 VM，設定為具單一網域之新樹系的網域控制站</span><span class="sxs-lookup"><span data-stu-id="4fa2e-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="4fa2e-114">一部 VM，設定為 SQL Server 2014 獨立伺服器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="4fa2e-115">一部 VM，設定為一部電腦的 SharePoint 2013 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="4fa2e-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="4fa2e-116">部署 AD (非高可用性)</span><span class="sxs-lookup"><span data-stu-id="4fa2e-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="4fa2e-117">使用 hello PowerShell DSC 延伸模組 toocreate AD 網域控制站伺服器，其中包含 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="4fa2e-117">Use hello PowerShell DSC extension toocreate an AD domain controller server that includes hello following resources:</span></span>

* <span data-ttu-id="4fa2e-118">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4fa2e-118">A virtual network</span></span>
* <span data-ttu-id="4fa2e-119">一個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4fa2e-119">One storage account</span></span>
* <span data-ttu-id="4fa2e-120">一個外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-120">One external load balancer</span></span>
* <span data-ttu-id="4fa2e-121">一部 VM，設定為具單一網域之新樹系的網域控制站</span><span class="sxs-lookup"><span data-stu-id="4fa2e-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="4fa2e-122">部署 AD/SQL (非高可用性)</span><span class="sxs-lookup"><span data-stu-id="4fa2e-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="4fa2e-123">使用 hello PowerShell DSC 延伸模組 toocreate SQL Server 2014 獨立伺服器，其中包含 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="4fa2e-123">Use hello PowerShell DSC extension toocreate a SQL Server 2014 stand-alone server that includes hello following resources:</span></span>

* <span data-ttu-id="4fa2e-124">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4fa2e-124">A virtual network</span></span>
* <span data-ttu-id="4fa2e-125">兩個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4fa2e-125">Two storage accounts</span></span>
* <span data-ttu-id="4fa2e-126">一個外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-126">One external load balancer</span></span>
* <span data-ttu-id="4fa2e-127">一部 VM，設定為具單一網域之新樹系的網域控制站</span><span class="sxs-lookup"><span data-stu-id="4fa2e-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="4fa2e-128">一部 VM，設定為 SQL Server 2014 獨立伺服器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="4fa2e-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="4fa2e-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="4fa2e-130">使用 hello PowerShell DSC 延伸模組 tooconfigure 現有的虛擬機器本機設定管理員 (LCM)，然後登錄 tooan Azure 自動化帳戶 DSC 提取的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-130">Use hello PowerShell DSC extension tooconfigure an existing virtual machine Local Configuration Manager (LCM) and register it tooan Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="4fa2e-131">從使用者映像建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4fa2e-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="4fa2e-132">從自訂使用者映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="4fa2e-133">這個範本也會部署虛擬網路 (含 DNS)、公用 IP 位址及網路介面。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="4fa2e-134">簡單的 VM</span><span class="sxs-lookup"><span data-stu-id="4fa2e-134">Simple VM</span></span>
<span data-ttu-id="4fa2e-135">部署一部 Windows VM，其中包含虛擬網路 (含 DNS)、公用 IP 位址及網路介面。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="4fa2e-136">取消執行中的範本部署</span><span class="sxs-lookup"><span data-stu-id="4fa2e-136">Cancel a running template deployment</span></span>
<span data-ttu-id="4fa2e-137">toocancel 執行的範本部署，使用 hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4fa2e-137">toocancel a running template deployment, use hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fa2e-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fa2e-138">Next steps</span></span>
[<span data-ttu-id="4fa2e-139">部署範本與 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="4fa2e-139">Deploy templates with hello portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="4fa2e-140">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="4fa2e-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

