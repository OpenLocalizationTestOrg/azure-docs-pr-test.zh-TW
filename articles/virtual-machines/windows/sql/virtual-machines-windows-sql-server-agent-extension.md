---
title: "aaaAutomate 管理工作上的 SQL Vm （資源管理員） |Microsoft 文件"
description: "本主題描述如何 toomanage hello SQL Server 代理程式延伸特定的 SQL Server 系統管理工作自動化。 其中包括自動備份、自動修補和 Azure 金鑰保存庫整合。 本主題使用 hello Resource Manager 部署模式。"
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
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="4a481-105">自動化管理工作在 Azure 虛擬機器以 hello SQL Server 代理程式延伸模組 （資源管理員）</span><span class="sxs-lookup"><span data-stu-id="4a481-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a481-106">資源管理員</span><span class="sxs-lookup"><span data-stu-id="4a481-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="4a481-107">傳統</span><span class="sxs-lookup"><span data-stu-id="4a481-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="4a481-108">hello SQL Server IaaS 代理程式延伸模組 (SQLIaaSExtension) 會執行於 Azure 虛擬機器 tooautomate 系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="4a481-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="4a481-109">本主題提供支援 hello 延伸模組，以及安裝、 狀態及移除指示 hello 服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="4a481-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="4a481-110">tooview hello 精簡版本的本文中，請參閱[SQL Server 代理程式延伸模組，如 SQL Server 傳統 Vm](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="4a481-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="4a481-111">支援的服務</span><span class="sxs-lookup"><span data-stu-id="4a481-111">Supported services</span></span>
<span data-ttu-id="4a481-112">hello SQL Server IaaS 代理程式延伸模組支援下列管理工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a481-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="4a481-113">系統管理功能</span><span class="sxs-lookup"><span data-stu-id="4a481-113">Administration feature</span></span> | <span data-ttu-id="4a481-114">說明</span><span class="sxs-lookup"><span data-stu-id="4a481-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a481-115">**SQL 自動備份**</span><span class="sxs-lookup"><span data-stu-id="4a481-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="4a481-116">會自動將 hello 預設執行個體的 SQL Server hello VM 中的所有資料庫的備份排程 hello。</span><span class="sxs-lookup"><span data-stu-id="4a481-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="4a481-117">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動備份 (Resource Manager)](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="4a481-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="4a481-118">**SQL 自動修補**</span><span class="sxs-lookup"><span data-stu-id="4a481-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="4a481-119">設定維護間隔期間哪些更新將放置的 tooyour VM 可以採取，如此您就不必在您的工作負載尖峰期間更新。</span><span class="sxs-lookup"><span data-stu-id="4a481-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="4a481-120">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補 (Resource Manager)](virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="4a481-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="4a481-121">**Azure 金鑰保存庫整合**</span><span class="sxs-lookup"><span data-stu-id="4a481-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="4a481-122">可讓您 tooautomatically 上安裝及設定 Azure 金鑰保存庫 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="4a481-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="4a481-123">如需詳細資訊，請參閱 [在 Azure VM (Resource Manager) 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="4a481-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="4a481-124">一旦安裝並執行，hello SQL Server IaaS 代理程式延伸模組提供這些管理功能 hello hello 虛擬機器在 hello Azure 入口網站，並透過 Azure PowerShell for SQL Server marketplace 映像，以及透過 SQL Server 面板上適用於 hello 延伸模組的手動安裝的 azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4a481-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4a481-125">必要條件</span><span class="sxs-lookup"><span data-stu-id="4a481-125">Prerequisites</span></span>
<span data-ttu-id="4a481-126">SQL Server IaaS 代理程式延伸模組在您的 VM 上需求 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="4a481-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="4a481-127">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="4a481-127">**Operating System**:</span></span>

* <span data-ttu-id="4a481-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4a481-128">Windows Server 2012</span></span>
* <span data-ttu-id="4a481-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4a481-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="4a481-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4a481-130">Windows Server 2016</span></span>

<span data-ttu-id="4a481-131">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="4a481-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="4a481-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="4a481-132">SQL Server 2012</span></span>
* <span data-ttu-id="4a481-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="4a481-133">SQL Server 2014</span></span>
* <span data-ttu-id="4a481-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="4a481-134">SQL Server 2016</span></span>

<span data-ttu-id="4a481-135">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="4a481-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="4a481-136">下載及設定 hello 最新的 Azure PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="4a481-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="4a481-137">安裝</span><span class="sxs-lookup"><span data-stu-id="4a481-137">Installation</span></span>
<span data-ttu-id="4a481-138">在佈建一個 hello SQL Server 虛擬機器圖庫映像時，會自動安裝 hello SQL Server IaaS 代理程式延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4a481-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="4a481-139">如果您需要以手動方式是在其中一個這些 SQL Server Vm 上的 tooreinstall hello 延伸模組，請使用下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a481-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="4a481-140">它也是可能 tooinstall hello SQL Server IaaS 代理程式延伸模組僅作業系統的 Windows Server 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="4a481-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="4a481-141">只有當您也已在該機器上手動安裝 SQL Server 時，才支援此做法。</span><span class="sxs-lookup"><span data-stu-id="4a481-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="4a481-142">然後透過手動安裝 hello 延伸 hello 相同**組 AzureVMSqlServerExtension** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4a481-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4a481-143">如果您手動安裝 SQL Server IaaS 代理程式延伸模組 hello 作業系統專用的 Windows Server VM 上，您不可以管理透過 hello Azure 入口網站的 hello SQL Server 組態設定。</span><span class="sxs-lookup"><span data-stu-id="4a481-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="4a481-144">在此情況下，您必須使用 PowerShell 來進行所有變更。</span><span class="sxs-lookup"><span data-stu-id="4a481-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="4a481-145">狀態</span><span class="sxs-lookup"><span data-stu-id="4a481-145">Status</span></span>
<span data-ttu-id="4a481-146">其中一種方式 tooverify hello 延伸模組已安裝的是 tooview hello 代理程式狀態在 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="4a481-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="4a481-147">選取**所有設定**在 hello 虛擬機器刀鋒視窗中，並按一下**延伸**。</span><span class="sxs-lookup"><span data-stu-id="4a481-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="4a481-148">您應該會看見 hello **SQLIaaSExtension**列出的副檔名。</span><span class="sxs-lookup"><span data-stu-id="4a481-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Azure 入口網站中的 SQL Server IaaS 代理程式擴充功能](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="4a481-150">您也可以使用 hello **Get AzureVMSqlServerExtension** Azure Powershell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4a481-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="4a481-151">hello 前一個命令會確認 hello 代理程式已安裝，並提供一般狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="4a481-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="4a481-152">您也可以使用下列命令的 hello 取得特定的狀態資訊自動備份和修補。</span><span class="sxs-lookup"><span data-stu-id="4a481-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="4a481-153">移除</span><span class="sxs-lookup"><span data-stu-id="4a481-153">Removal</span></span>
<span data-ttu-id="4a481-154">在 hello Azure 入口網站，您可以解除安裝 hello 延伸 hello hello 上的省略符號，即可**延伸**刀鋒視窗中的虛擬機器內容。</span><span class="sxs-lookup"><span data-stu-id="4a481-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="4a481-155">然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="4a481-155">Then click **Delete**.</span></span>

![解除安裝 SQL Server IaaS 代理程式延伸模組在 Azure 入口網站中的 hello](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="4a481-157">您也可以使用 hello**移除 AzureRmVMSqlServerExtension** Powershell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4a481-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="4a481-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a481-158">Next Steps</span></span>
<span data-ttu-id="4a481-159">開始使用其中一種 hello hello 延伸模組支援的服務。</span><span class="sxs-lookup"><span data-stu-id="4a481-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="4a481-160">如需詳細資訊，請參閱 hello 中參考的 hello 主題[支援服務](#supported-services)本文一節。</span><span class="sxs-lookup"><span data-stu-id="4a481-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="4a481-161">如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4a481-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

