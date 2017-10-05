---
title: "在 Azure (Resource Manager) 中的 Windows VM 上將 Key Vault 與 SQL Server 整合 | Microsoft Docs"
description: "了解如何自動化 SQL Server 加密的組態，以用於 Azure 金鑰保存庫。 本主題說明如何搭配「資源管理員」建立之 SQL Server 虛擬機器使用 Azure 金鑰保存庫整合。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 32b9564fa5c9ca6864ade343fda309b2c3edf123
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="7d6bf-104">在 Azure 虛擬機器上設定 SQL Server 的 Azure Key Vault 整合 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7d6bf-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d6bf-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="7d6bf-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="7d6bf-106">傳統</span><span class="sxs-lookup"><span data-stu-id="7d6bf-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7d6bf-107">概觀</span><span class="sxs-lookup"><span data-stu-id="7d6bf-107">Overview</span></span>
<span data-ttu-id="7d6bf-108">有多個 SQL Server 加密功能，例如[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)、[資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) 和[備份加密](https://msdn.microsoft.com/library/dn449489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="7d6bf-109">這些形式的加密需要您管理和儲存用來加密的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="7d6bf-110">Azure 金鑰保存庫 (AKV) 服務是設計來改善這些金鑰在安全且高度可用位置的安全性和管理。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="7d6bf-111">[SQL Server 連接器](http://www.microsoft.com/download/details.aspx?id=45344) 讓 SQL Server 可以從 Azure 金鑰保存庫使用這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="7d6bf-112">如果您使用內部部署電腦執行 SQL Server，有 [您可以遵循的步驟以從您的內部部署 SQL Server 電腦存取 Azure 金鑰保存庫](https://msdn.microsoft.com/library/dn198405.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="7d6bf-113">但是對於 Azure VM 中的 SQL server，您可以使用 *Azure 金鑰保存庫整合* 功能來節省時間。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="7d6bf-114">啟用這項功能時，它會自動安裝 SQL Server 連接器、設定 EKM 提供者來存取 Azure 金鑰保存庫，並建立認證讓您存取您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="7d6bf-115">如果您看到先前提及的內部部署文件中的步驟，您可以發現這項功能會自動執行步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="7d6bf-116">您唯一仍然需要手動進行的是建立金鑰保存庫和金鑰。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="7d6bf-117">從那裡開始，會自動化 SQL VM 的整個設定。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="7d6bf-118">這項功能完成此設定之後，您可以執行 T-SQL 陳述式以開始如往常一般加密您的資料庫或備份。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="7d6bf-119">啟用及設定 AKV 整合</span><span class="sxs-lookup"><span data-stu-id="7d6bf-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="7d6bf-120">您可以在佈建期間啟用 AKV 整合，或針對現有的 VM 設定這項整合。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="7d6bf-121">新的 VM</span><span class="sxs-lookup"><span data-stu-id="7d6bf-121">New VMs</span></span>
<span data-ttu-id="7d6bf-122">如果您是使用資源管理員佈建新的 SQL Server 虛擬機器，則 Azure 入口網站會提供一個步驟來啟用 Azure 金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="7d6bf-123">Azure 金鑰保存庫功能僅適用於 SQL Server 的 Enterprise、Developer 和 Evaluation 版本。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="7d6bf-125">如需佈建的詳細逐步解說，請參閱 [在 Azure 入口網站中佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="7d6bf-126">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="7d6bf-126">Existing VMs</span></span>
<span data-ttu-id="7d6bf-127">如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="7d6bf-128">然後選取 [設定] 刀鋒視窗的 [SQL Server 組態] 區段。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="7d6bf-130">在 [SQL Server 組態] 刀鋒視窗中，按一下 [自動金鑰保存庫整合] 區段中的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![設定現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="7d6bf-132">完成時，按一下 [SQL Server 組態] 刀鋒視窗底部的 [確定] 按鈕，以儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="7d6bf-133">您也可以使用範本來設定 AKV 整合。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="7d6bf-134">如需詳細資訊，請參閱 [適用於 Azure 金鑰保存庫整合的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)。</span><span class="sxs-lookup"><span data-stu-id="7d6bf-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

