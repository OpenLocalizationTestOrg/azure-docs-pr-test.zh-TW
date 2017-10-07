---
title: "aaaIntegrate 金鑰保存庫在 Azure （資源管理員） 中的 Windows Vm 上的 SQL server |Microsoft 文件"
description: "了解如何 tooautomate hello 的 Azure 金鑰保存庫搭配使用的 SQL Server 加密組態。 本主題說明如何搭配 SQL Server 虛擬機器的 Azure 金鑰保存庫整合 toouse 建立與資源管理員。"
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
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="ab172-104">在 Azure 虛擬機器上設定 SQL Server 的 Azure Key Vault 整合 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="ab172-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab172-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="ab172-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="ab172-106">傳統</span><span class="sxs-lookup"><span data-stu-id="ab172-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ab172-107">概觀</span><span class="sxs-lookup"><span data-stu-id="ab172-107">Overview</span></span>
<span data-ttu-id="ab172-108">有多個 SQL Server 加密功能，例如[透明資料加密 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)、[資料行層級加密 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) 和[備份加密](https://msdn.microsoft.com/library/dn449489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ab172-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="ab172-109">這些形式的加密需要您 toomanage，而儲存 hello 用來加密的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="ab172-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="ab172-110">hello Azure 金鑰保存庫 (AKV) 服務是設計的 tooimprove hello 安全性和管理高可用性的位置中的這些索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ab172-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="ab172-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344)可讓 SQL Server toouse Azure 金鑰保存庫中的這些索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ab172-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="ab172-112">如果您在內部部署與執行 SQL Server 的電腦上，那里會[步驟，您可以從內部部署 SQL Server 電腦遵循 tooaccess Azure 金鑰保存庫](https://msdn.microsoft.com/library/dn198405.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ab172-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="ab172-113">在 Azure Vm 中的 SQL server，您可以使用 hello 來節省時間，但是*Azure 金鑰保存庫整合*功能。</span><span class="sxs-lookup"><span data-stu-id="ab172-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="ab172-114">啟用這項功能時，它會自動安裝 SQL Server Connector hello、 設定 hello EKM 提供者 tooaccess Azure 金鑰保存庫，並且建立 hello 認證 tooallow 您 tooaccess 您保存庫。</span><span class="sxs-lookup"><span data-stu-id="ab172-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="ab172-115">如果您在查看 hello 中的 hello 步驟先前所述內部文件，您可以看到這項功能會自動執行步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="ab172-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="ab172-116">您仍然必須 toodo 手動 hello 唯一的是 toocreate hello 金鑰保存庫和金鑰。</span><span class="sxs-lookup"><span data-stu-id="ab172-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="ab172-117">從該處，hello 整個安裝的 SQL VM 會自動執行。</span><span class="sxs-lookup"><span data-stu-id="ab172-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="ab172-118">此安裝程式完成後這項功能，您可以執行 T-SQL 陳述式 toobegin 加密您的資料庫或備份，像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="ab172-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="ab172-119">啟用及設定 AKV 整合</span><span class="sxs-lookup"><span data-stu-id="ab172-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="ab172-120">您可以在佈建期間啟用 AKV 整合，或針對現有的 VM 設定這項整合。</span><span class="sxs-lookup"><span data-stu-id="ab172-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="ab172-121">新的 VM</span><span class="sxs-lookup"><span data-stu-id="ab172-121">New VMs</span></span>
<span data-ttu-id="ab172-122">如果您佈建新的 SQL Server 虛擬機器與資源管理員，hello Azure 入口網站會提供步驟 tooenable Azure 金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="ab172-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="ab172-123">hello Azure 金鑰保存庫功能是僅供 hello Enterprise、 Developer 和 Evaluation 等版本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ab172-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="ab172-125">佈建的詳細逐步解說，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="ab172-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="ab172-126">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="ab172-126">Existing VMs</span></span>
<span data-ttu-id="ab172-127">如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ab172-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="ab172-128">然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ab172-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="ab172-130">在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 自動化的金鑰保存庫整合 > 一節中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab172-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![設定現有 VM 的 SQL AKV 整合](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="ab172-132">完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="ab172-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="ab172-133">您也可以使用範本來設定 AKV 整合。</span><span class="sxs-lookup"><span data-stu-id="ab172-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="ab172-134">如需詳細資訊，請參閱 [適用於 Azure 金鑰保存庫整合的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update)。</span><span class="sxs-lookup"><span data-stu-id="ab172-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

