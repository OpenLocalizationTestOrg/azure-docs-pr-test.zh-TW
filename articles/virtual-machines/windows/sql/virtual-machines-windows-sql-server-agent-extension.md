---
title: "SQL VM 上的自動化管理工作 (Resource Manager) | Microsoft 文件"
description: "本主題說明如何管理 SQL Server 代理程式擴充功能，此擴充功能可將特定 SQL Server 管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 這個主題會使用 Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7152d184bb6d1d4b81aeb47e2c7c9160ada36023
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="9c608-105">使用 SQL Server 代理程式延伸模組 (Resource Manager) 自動化 Azure 虛擬機器上的管理工作</span><span class="sxs-lookup"><span data-stu-id="9c608-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c608-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="9c608-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="9c608-107">傳統</span><span class="sxs-lookup"><span data-stu-id="9c608-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="9c608-108">SQL Server IaaS 代理程式擴充功能 (SQLIaaSExtension) 會在 Azure 虛擬機器上執行，以將管理工作自動化。</span><span class="sxs-lookup"><span data-stu-id="9c608-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="9c608-109">本主題概述擴充功能所支援的服務，以及與安裝、狀態及移除相關的指示。</span><span class="sxs-lookup"><span data-stu-id="9c608-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="9c608-110">如需檢視這篇文章的精簡版本，請參閱 [SQL Server IaaS 代理程式擴充功能 (傳統)](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="9c608-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="9c608-111">支援的服務</span><span class="sxs-lookup"><span data-stu-id="9c608-111">Supported services</span></span>
<span data-ttu-id="9c608-112">SQL Server IaaS 代理程式擴充功能支援下列管理工作︰</span><span class="sxs-lookup"><span data-stu-id="9c608-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="9c608-113">系統管理功能</span><span class="sxs-lookup"><span data-stu-id="9c608-113">Administration feature</span></span> | <span data-ttu-id="9c608-114">說明</span><span class="sxs-lookup"><span data-stu-id="9c608-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c608-115">**SQL 自動備份**</span><span class="sxs-lookup"><span data-stu-id="9c608-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="9c608-116">針對 VM 中 SQL Server 的預設執行個體，將所有資料庫的備份排程自動化。</span><span class="sxs-lookup"><span data-stu-id="9c608-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="9c608-117">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (Resource Manager)](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="9c608-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="9c608-118">**SQL 自動修補**</span><span class="sxs-lookup"><span data-stu-id="9c608-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="9c608-119">設定維護期間 (在此期間會進行 VM 的更新)，以避免在工作負載尖峰時段進行更新。</span><span class="sxs-lookup"><span data-stu-id="9c608-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="9c608-120">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (Resource Manager)](virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="9c608-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="9c608-121">**Azure 金鑰保存庫整合**</span><span class="sxs-lookup"><span data-stu-id="9c608-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="9c608-122">讓您在 SQL Server VM 上自動安裝和設定 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c608-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="9c608-123">如需詳細資訊，請參閱 [在 Azure VM (Resource Manager) 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="9c608-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="9c608-124">一旦安裝並執行 SQL Server IaaS 代理程式延伸模組之後，Azure 入口網站中虛擬機器的 SQL Server 面板即會提供這些管理功能，亦可透過 Azure PowerShell (若為 SQL Server Marketplace 映像) 以及 Azure PowerShell (若為手動安裝延伸模組) 使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="9c608-124">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9c608-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="9c608-125">Prerequisites</span></span>
<span data-ttu-id="9c608-126">在 VM 上使用 SQL Server IaaS 代理程式擴充功能的需求：</span><span class="sxs-lookup"><span data-stu-id="9c608-126">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="9c608-127">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="9c608-127">**Operating System**:</span></span>

* <span data-ttu-id="9c608-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="9c608-128">Windows Server 2012</span></span>
* <span data-ttu-id="9c608-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9c608-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="9c608-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9c608-130">Windows Server 2016</span></span>

<span data-ttu-id="9c608-131">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="9c608-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="9c608-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="9c608-132">SQL Server 2012</span></span>
* <span data-ttu-id="9c608-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="9c608-133">SQL Server 2014</span></span>
* <span data-ttu-id="9c608-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="9c608-134">SQL Server 2016</span></span>

<span data-ttu-id="9c608-135">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="9c608-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="9c608-136">下載及設定最新的 Azure PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="9c608-136">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="9c608-137">安裝</span><span class="sxs-lookup"><span data-stu-id="9c608-137">Installation</span></span>
<span data-ttu-id="9c608-138">當您佈建其中一個 SQL Server 虛擬機器資源庫映像時，系統會自動安裝 SQL Server IaaS 代理程式擴充功能。</span><span class="sxs-lookup"><span data-stu-id="9c608-138">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="9c608-139">如果您需要在其中一個 SQL Server 虛擬機器上手動重新安裝擴充功能，請使用下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="9c608-139">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="9c608-140">您也可以將「SQL Server IaaS 代理程式擴充功能」安裝在只有 OS 的 Windows Server 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="9c608-140">It is also possible to install the SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="9c608-141">只有當您也已在該機器上手動安裝 SQL Server 時，才支援此做法。</span><span class="sxs-lookup"><span data-stu-id="9c608-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="9c608-142">然後使用相同的 **Set-AzureVMSqlServerExtension** PowerShell Cmdlet 來手動安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="9c608-142">Then install the extension manually by using the same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="9c608-143">如果您手動在只有作業系統的 Windows Server 虛擬機器上安裝「SQL Server IaaS 代理程式擴充功能」，您便無法透過 Azure 入口網站管理 SQL Server 組態設定。</span><span class="sxs-lookup"><span data-stu-id="9c608-143">If you manually install the SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage the SQL Server configuration settings through the Azure portal.</span></span> <span data-ttu-id="9c608-144">在此情況下，您必須使用 PowerShell 來進行所有變更。</span><span class="sxs-lookup"><span data-stu-id="9c608-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="9c608-145">狀態</span><span class="sxs-lookup"><span data-stu-id="9c608-145">Status</span></span>
<span data-ttu-id="9c608-146">驗證已安裝擴充功能的其中一項方法，是在 Azure 入口網站中檢視代理程式狀態。</span><span class="sxs-lookup"><span data-stu-id="9c608-146">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="9c608-147">請選取虛擬機器刀鋒視窗中的 [所有設定]，然後按一下 [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="9c608-147">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="9c608-148">您應該會看到列出 **SQLIaaSExtension** 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="9c608-148">You should see the **SQLIaaSExtension** extension listed.</span></span>

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="9c608-150">您也可以使用 **Get-AzureVMSqlServerExtension** Azure Powershell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9c608-150">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="9c608-151">前一個命令會確認已安裝代理程式，並提供一般狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="9c608-151">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="9c608-152">您也可以使用下列命令取得有關自動備份和修補的特定狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="9c608-152">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="9c608-153">移除</span><span class="sxs-lookup"><span data-stu-id="9c608-153">Removal</span></span>
<span data-ttu-id="9c608-154">在「Azure 入口網站」中，您可以按一下虛擬機器屬性 [擴充功能]  刀鋒視窗上的省略符號，來將擴充功能解除安裝。</span><span class="sxs-lookup"><span data-stu-id="9c608-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="9c608-155">然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="9c608-155">Then click **Delete**.</span></span>

![將 Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能解除安裝](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="9c608-157">您也可以使用 **Remove-AzureRmVMSqlServerExtension** Powershell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9c608-157">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="9c608-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c608-158">Next Steps</span></span>
<span data-ttu-id="9c608-159">開始使用擴充功能所支援的其中一項服務。</span><span class="sxs-lookup"><span data-stu-id="9c608-159">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="9c608-160">如需詳細資訊，請參閱本文 [支援的服務](#supported-services) 一節中參考的主題。</span><span class="sxs-lookup"><span data-stu-id="9c608-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="9c608-161">如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9c608-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

