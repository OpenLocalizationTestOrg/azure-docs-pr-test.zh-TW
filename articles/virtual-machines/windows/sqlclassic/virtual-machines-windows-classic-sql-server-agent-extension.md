---
title: "aaaAutomate SQL Vm （傳統） 上的管理工作 |Microsoft 文件"
description: "本主題描述如何 toomanage hello SQL Server 代理程式延伸特定的 SQL Server 系統管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 本主題使用 hello 傳統部署模式。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="add0f-105">自動化管理工作在 Azure 虛擬機器以 hello SQL Server 代理程式延伸模組 （傳統）</span><span class="sxs-lookup"><span data-stu-id="add0f-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="add0f-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="add0f-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="add0f-107">傳統</span><span class="sxs-lookup"><span data-stu-id="add0f-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="add0f-108">hello SQL Server IaaS 代理程式延伸模組 (SQLIaaSAgent) 會執行於 Azure 虛擬機器 tooautomate 系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="add0f-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="add0f-109">本主題提供支援 hello 延伸模組，以及安裝、 狀態及移除指示 hello 服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="add0f-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="add0f-110">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="add0f-111">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="add0f-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="add0f-112">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="add0f-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="add0f-113">請參閱這篇文章，tooview hello 資源管理員版本[SQL Server Agent 擴充功能的 SQL Server Vm 資源管理員](../sql/virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="add0f-114">支援的服務</span><span class="sxs-lookup"><span data-stu-id="add0f-114">Supported services</span></span>
<span data-ttu-id="add0f-115">hello SQL Server IaaS 代理程式延伸模組支援下列管理工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="add0f-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="add0f-116">系統管理功能</span><span class="sxs-lookup"><span data-stu-id="add0f-116">Administration feature</span></span> | <span data-ttu-id="add0f-117">說明</span><span class="sxs-lookup"><span data-stu-id="add0f-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="add0f-118">**SQL 自動備份**</span><span class="sxs-lookup"><span data-stu-id="add0f-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="add0f-119">會自動將 hello 預設執行個體的 SQL Server hello VM 中的所有資料庫的備份排程 hello。</span><span class="sxs-lookup"><span data-stu-id="add0f-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="add0f-120">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (傳統)](../classic/sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="add0f-121">**SQL 自動修補**</span><span class="sxs-lookup"><span data-stu-id="add0f-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="add0f-122">設定維護間隔期間哪些更新將放置的 tooyour VM 可以採取，如此您就不必在您的工作負載尖峰期間更新。</span><span class="sxs-lookup"><span data-stu-id="add0f-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="add0f-123">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (傳統)](../classic/sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="add0f-124">**Azure 金鑰保存庫整合**</span><span class="sxs-lookup"><span data-stu-id="add0f-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="add0f-125">可讓您 tooautomatically 上安裝及設定 Azure 金鑰保存庫 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="add0f-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="add0f-126">如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合 (傳統)](../classic/ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="add0f-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="add0f-127">Prerequisites</span></span>
<span data-ttu-id="add0f-128">SQL Server IaaS 代理程式延伸模組在您的 VM 上需求 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="add0f-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="add0f-129">作業系統：</span><span class="sxs-lookup"><span data-stu-id="add0f-129">Operating System:</span></span>
* <span data-ttu-id="add0f-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="add0f-130">Windows Server 2012</span></span>
* <span data-ttu-id="add0f-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="add0f-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="add0f-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="add0f-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="add0f-133">SQL Server 版本：</span><span class="sxs-lookup"><span data-stu-id="add0f-133">SQL Server versions:</span></span>
* <span data-ttu-id="add0f-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="add0f-134">SQL Server 2012</span></span>
* <span data-ttu-id="add0f-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="add0f-135">SQL Server 2014</span></span>
* <span data-ttu-id="add0f-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="add0f-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="add0f-137">Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="add0f-137">Azure PowerShell:</span></span>
<span data-ttu-id="add0f-138">[下載並設定最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="add0f-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="add0f-139">啟動 Windows PowerShell，並將它連接 tooyour Azure 訂用帳戶以 hello **Add-azureaccount**命令。</span><span class="sxs-lookup"><span data-stu-id="add0f-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="add0f-140">如果您有多個訂閱，使用**Select-azuresubscription** tooselect hello 訂用帳戶包含您的目標傳統 VM。</span><span class="sxs-lookup"><span data-stu-id="add0f-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="add0f-141">此時，您可以取得一份 hello 傳統虛擬機器和其相關聯的服務名稱與 hello **Get-azurevm**命令。</span><span class="sxs-lookup"><span data-stu-id="add0f-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="add0f-142">安裝</span><span class="sxs-lookup"><span data-stu-id="add0f-142">Installation</span></span>
<span data-ttu-id="add0f-143">對於傳統的 Vm，您必須使用 PowerShell tooinstall hello SQL Server IaaS 代理程式延伸模組，並設定相關聯的服務。</span><span class="sxs-lookup"><span data-stu-id="add0f-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="add0f-144">使用 hello**組 AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="add0f-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="add0f-145">例如，hello 下列命令會安裝在 Windows Server VM （傳統） 上的 hello 延伸模組並將它"SQLIaaSExtension"。</span><span class="sxs-lookup"><span data-stu-id="add0f-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="add0f-146">如果您更新 toohello hello SQL IaaS 代理程式延伸模組最新版本，您必須更新 hello 擴充功能之後，重新虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="add0f-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="add0f-147">傳統的虛擬機器沒有選項 tooinstall，並設定 hello SQL IaaS 代理程式延伸模組，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="add0f-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="add0f-148">狀態</span><span class="sxs-lookup"><span data-stu-id="add0f-148">Status</span></span>
<span data-ttu-id="add0f-149">其中一種方式 tooverify hello 延伸模組已安裝的是 tooview hello 代理程式狀態在 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="add0f-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="add0f-150">選取列在 hello 虛擬機器刀鋒視窗中，虛擬機器，然後按一下上**延伸**。</span><span class="sxs-lookup"><span data-stu-id="add0f-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="add0f-151">您應該會看見 hello **SQLIaaSAgent**列出的副檔名。</span><span class="sxs-lookup"><span data-stu-id="add0f-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="add0f-153">您也可以使用 hello **Get AzureVMSqlServerExtension** Azure Powershell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="add0f-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="add0f-154">移除</span><span class="sxs-lookup"><span data-stu-id="add0f-154">Removal</span></span>
<span data-ttu-id="add0f-155">在 hello Azure 入口網站，您可以解除安裝 hello 延伸 hello hello 上的省略符號，即可**延伸**刀鋒視窗中的虛擬機器內容。</span><span class="sxs-lookup"><span data-stu-id="add0f-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="add0f-156">然後按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="add0f-156">Then click **Uninstall**.</span></span>

![解除安裝 SQL Server IaaS 代理程式延伸模組在 Azure 入口網站中的 hello](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="add0f-158">您也可以使用 hello**移除 AzureVMSqlServerExtension** Powershell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="add0f-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="add0f-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="add0f-159">Next Steps</span></span>
<span data-ttu-id="add0f-160">開始使用其中一種 hello hello 延伸模組支援的服務。</span><span class="sxs-lookup"><span data-stu-id="add0f-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="add0f-161">如需詳細資訊，請參閱 hello 中參考的 hello 主題[支援服務](#supported-services)本文一節。</span><span class="sxs-lookup"><span data-stu-id="add0f-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="add0f-162">如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="add0f-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

