---
title: "SQL VM 上的自動化管理工作 (傳統) | Microsoft 文件"
description: "本主題說明如何管理 SQL Server 代理程式擴充功能，此擴充功能可將特定 SQL Server 管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 本主題使用傳統部署模式。"
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
ms.openlocfilehash: 30fa9128cd51a7498449c991b58500ad9acdd3d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="6b54b-105">使用 SQL Server 代理程式延伸模組 (傳統) 自動化 Azure 虛擬機器上的管理工作</span><span class="sxs-lookup"><span data-stu-id="6b54b-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b54b-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="6b54b-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="6b54b-107">傳統</span><span class="sxs-lookup"><span data-stu-id="6b54b-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="6b54b-108">Azure 虛擬機器會執行 SQL Server IaaS Agent 擴充功能 (SQLIaaSAgent) 以自動化系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="6b54b-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="6b54b-109">本主題概述擴充功能所支援的服務，以及與安裝、狀態及移除相關的指示。</span><span class="sxs-lookup"><span data-stu-id="6b54b-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6b54b-110">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b54b-111">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6b54b-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6b54b-112">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="6b54b-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6b54b-113">若要檢視這篇文章的 Resource Manager 版本，請參閱 [適用於 SQL Server VM Resource Manager 的 SQL Server Agent 擴充功能](../sql/virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-113">To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="6b54b-114">支援的服務</span><span class="sxs-lookup"><span data-stu-id="6b54b-114">Supported services</span></span>
<span data-ttu-id="6b54b-115">SQL Server IaaS 代理程式擴充功能支援下列管理工作︰</span><span class="sxs-lookup"><span data-stu-id="6b54b-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="6b54b-116">系統管理功能</span><span class="sxs-lookup"><span data-stu-id="6b54b-116">Administration feature</span></span> | <span data-ttu-id="6b54b-117">說明</span><span class="sxs-lookup"><span data-stu-id="6b54b-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b54b-118">**SQL 自動備份**</span><span class="sxs-lookup"><span data-stu-id="6b54b-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="6b54b-119">針對 VM 中 SQL Server 的預設執行個體，將所有資料庫的備份排程自動化。</span><span class="sxs-lookup"><span data-stu-id="6b54b-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="6b54b-120">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (傳統)](../classic/sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="6b54b-121">**SQL 自動修補**</span><span class="sxs-lookup"><span data-stu-id="6b54b-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="6b54b-122">設定維護期間 (在此期間會進行 VM 的更新)，以避免在工作負載尖峰時段進行更新。</span><span class="sxs-lookup"><span data-stu-id="6b54b-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="6b54b-123">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (傳統)](../classic/sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="6b54b-124">**Azure 金鑰保存庫整合**</span><span class="sxs-lookup"><span data-stu-id="6b54b-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="6b54b-125">讓您在 SQL Server VM 上自動安裝和設定 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6b54b-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="6b54b-126">如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合 (傳統)](../classic/ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="6b54b-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="6b54b-127">Prerequisites</span></span>
<span data-ttu-id="6b54b-128">在 VM 上使用 SQL Server IaaS 代理程式擴充功能的需求：</span><span class="sxs-lookup"><span data-stu-id="6b54b-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="6b54b-129">作業系統：</span><span class="sxs-lookup"><span data-stu-id="6b54b-129">Operating System:</span></span>
* <span data-ttu-id="6b54b-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6b54b-130">Windows Server 2012</span></span>
* <span data-ttu-id="6b54b-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6b54b-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="6b54b-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6b54b-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="6b54b-133">SQL Server 版本：</span><span class="sxs-lookup"><span data-stu-id="6b54b-133">SQL Server versions:</span></span>
* <span data-ttu-id="6b54b-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="6b54b-134">SQL Server 2012</span></span>
* <span data-ttu-id="6b54b-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="6b54b-135">SQL Server 2014</span></span>
* <span data-ttu-id="6b54b-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="6b54b-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="6b54b-137">Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="6b54b-137">Azure PowerShell:</span></span>
<span data-ttu-id="6b54b-138">[下載及設定最新的 Azure PowerShell 命令](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-138">[Download and configure the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="6b54b-139">啟動 Windows PowerShell，然後使用 **Add-AzureAccount** 命令將它與您的 Azure 訂用帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="6b54b-139">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="6b54b-140">如果您有多個訂用帳戶，請使用 **Select-AzureSubscription** 以選取包含您目標傳統 VM 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b54b-140">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="6b54b-141">此時，您可以使用 **Get-AzureVM** 命令來取得傳統虛擬機器及其相關服務名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="6b54b-141">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="6b54b-142">安裝</span><span class="sxs-lookup"><span data-stu-id="6b54b-142">Installation</span></span>
<span data-ttu-id="6b54b-143">針對傳統 VM，您必須使用 PowerShell 來安裝「SQL Server IaaS 代理程式擴充功能」並設定其相關服務。</span><span class="sxs-lookup"><span data-stu-id="6b54b-143">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="6b54b-144">請使用 **Set-AzureVMSqlServerExtension** PowerShell Cmdlet 來安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6b54b-144">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="6b54b-145">例如，下列命令會在 Windows Server VM (傳統) 上安裝擴充功能，並將它命名為 "SQLIaaSExtension"。</span><span class="sxs-lookup"><span data-stu-id="6b54b-145">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="6b54b-146">如果更新到最新版的 SQL IaaS 代理程式擴充，您必須在更新擴充之後重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6b54b-146">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> <span data-ttu-id="6b54b-147">傳統虛擬機器沒有可透過入口網站安裝及設定「SQL IaaS 代理程式擴充功能」的選項。</span><span class="sxs-lookup"><span data-stu-id="6b54b-147">Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="6b54b-148">狀態</span><span class="sxs-lookup"><span data-stu-id="6b54b-148">Status</span></span>
<span data-ttu-id="6b54b-149">驗證已安裝擴充功能的其中一項方法，是在 Azure 入口網站中檢視代理程式狀態。</span><span class="sxs-lookup"><span data-stu-id="6b54b-149">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="6b54b-150">請選取虛擬機器刀鋒視窗中所列的一部虛擬機器，然後按一下 [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="6b54b-150">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="6b54b-151">您應該會看到其中列出 **SQLIaaSAgent** 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6b54b-151">You should see the **SQLIaaSAgent** extension listed.</span></span>

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="6b54b-153">您也可以使用 **Get-AzureVMSqlServerExtension** Azure Powershell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6b54b-153">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="6b54b-154">移除</span><span class="sxs-lookup"><span data-stu-id="6b54b-154">Removal</span></span>
<span data-ttu-id="6b54b-155">在「Azure 入口網站」中，您可以按一下虛擬機器屬性 [擴充功能]  刀鋒視窗上的省略符號，來將擴充功能解除安裝。</span><span class="sxs-lookup"><span data-stu-id="6b54b-155">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="6b54b-156">然後按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="6b54b-156">Then click **Uninstall**.</span></span>

![將 Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能解除安裝](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="6b54b-158">您也可以使用 **Remove-AzureVMSqlServerExtension** Powershell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6b54b-158">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="6b54b-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b54b-159">Next Steps</span></span>
<span data-ttu-id="6b54b-160">開始使用擴充功能所支援的其中一項服務。</span><span class="sxs-lookup"><span data-stu-id="6b54b-160">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="6b54b-161">如需詳細資訊，請參閱本文 [支援的服務](#supported-services) 一節中參考的主題。</span><span class="sxs-lookup"><span data-stu-id="6b54b-161">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="6b54b-162">如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6b54b-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

