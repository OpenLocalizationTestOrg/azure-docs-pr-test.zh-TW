---
title: "將 Site Recovery 保存庫升級成 Azure 復原服務保存庫"
description: "了解如何將 Azure Site Recovery 保存庫升級成 Microsoft Azure 復原服務保存庫"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: fdb33ea0d08353b491f2934fcf885fcb6910b9a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-site-recovery-vault-to-an-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="01b75-103">將 Site Recovery 保存庫升級成以 Azure Resource Manager 為基礎的復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="01b75-103">Upgrade a Site Recovery vault to an Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="01b75-104">本文說明如何在不影響進行中複寫的情況下，將 Azure Site Recovery 保存庫升級成以 Azure Resource Manager 為基礎的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="01b75-104">This article describes how to upgrade Azure Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="01b75-105">如需 Azure Resource Manager 功能和優點的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="01b75-106">簡介</span><span class="sxs-lookup"><span data-stu-id="01b75-106">Introduction</span></span>
<span data-ttu-id="01b75-107">復原服務保存庫是一項 Azure Resource Manager 資源，可用來在雲端上以原生方式管理備份與災害復原。</span><span class="sxs-lookup"><span data-stu-id="01b75-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in the cloud.</span></span> <span data-ttu-id="01b75-108">此為整合保存庫，可供您在新的 Azure 入口網站內使用，並可取代傳統的備份與 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="01b75-108">It is a unified vault that you can use in the new Azure portal, and it replaces the classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="01b75-109">復原服務保存庫提供了一系列的功能，包括：</span><span class="sxs-lookup"><span data-stu-id="01b75-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="01b75-110">支援 Azure Resource Manager：可以保護您的虛擬機器與實體機器，並將這些機器容錯移轉至 Azure Resource Manager 堆疊。</span><span class="sxs-lookup"><span data-stu-id="01b75-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="01b75-111">排除磁碟：如果您有一些暫存檔案或高變換資料，但不想要讓它們用盡所有頻寬，則可以將磁碟區從複寫中排除。</span><span class="sxs-lookup"><span data-stu-id="01b75-111">Exclude disk: If you have temp files or high churn data that you don’t want to use all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="01b75-112">這項功能目前已在「VMware 到 Azure」與「Hyper-V 到 Azure」中啟用，而且也已經擴展到其他案例。</span><span class="sxs-lookup"><span data-stu-id="01b75-112">This capability has been enabled currently in *VMware to Azure* and *Hyper-V to Azure* and is extended to other scenarios as well.</span></span>

* <span data-ttu-id="01b75-113">支援進階與本地備援儲存體：現在可以讓伺服器進入進階儲存體帳戶加以保護，該帳戶允許客戶以更高的每秒輸入/輸出作業數 (IOPS) 保護應用程式。</span><span class="sxs-lookup"><span data-stu-id="01b75-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers to protect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="01b75-114">這項功能目前已在「VMware 到 Azure」中啟用。</span><span class="sxs-lookup"><span data-stu-id="01b75-114">This capability is currently enabled in *VMware to Azure*.</span></span>

* <span data-ttu-id="01b75-115">簡化使用者入門體驗：增強的使用者入門體驗是為了讓使用者能夠輕鬆地設定災害復原而設計。</span><span class="sxs-lookup"><span data-stu-id="01b75-115">Streamlined getting-started experience: The enhanced getting-started experience has been designed to make disaster-recovery setup easy.</span></span>

* <span data-ttu-id="01b75-116">從相同保存庫管理備份與 Site Recovery：現在可以從同一個保存庫保護伺服器，以進行災害復原或進行備份，大幅減少您的管理負荷。</span><span class="sxs-lookup"><span data-stu-id="01b75-116">Backup and Site Recovery management from the same vault: You can now protect servers for disaster recovery or perform backup from the same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="01b75-117">如需升級後之體驗與功能的詳細資訊，請參閱[儲存、備份與復原部落格](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/)。</span><span class="sxs-lookup"><span data-stu-id="01b75-117">For more information about the upgraded experience and features, see the [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="01b75-118">主要功能</span><span class="sxs-lookup"><span data-stu-id="01b75-118">Salient features</span></span>

* <span data-ttu-id="01b75-119">不影響進行中的複寫：進行中的複寫在升級期間與升級後會繼續進行，完全不會中斷。</span><span class="sxs-lookup"><span data-stu-id="01b75-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="01b75-120">不必另外付費：不必另外付費即可獲得一整組更新後的功能。</span><span class="sxs-lookup"><span data-stu-id="01b75-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="01b75-121">不會遺失資料：由於此程序是升級而非移轉，現有複寫的復原點和設定在升級期間與升級後會維持不變。</span><span class="sxs-lookup"><span data-stu-id="01b75-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after the upgrade.</span></span>


## <a name="what-happens-during-the-vault-upgrade"></a><span data-ttu-id="01b75-122">保存庫升級期間會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="01b75-122">What happens during the vault upgrade?</span></span>

<span data-ttu-id="01b75-123">在升級期間，您將無法進行註冊新伺服器或為虛擬機器 (VM) 啟用複寫等作業。</span><span class="sxs-lookup"><span data-stu-id="01b75-123">During the upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="01b75-124">涉及在保存庫中讀取或寫入資料的作業 (例如正在將受保護項目複寫到保存庫) 仍會繼續進行而不中斷。</span><span class="sxs-lookup"><span data-stu-id="01b75-124">Operations that involve reading data from or writing data to the vault, such as ongoing replication of protected items to the vault, continue uninterrupted.</span></span>

### <a name="changes-to-automation-and-tooling-after-the-upgrade"></a><span data-ttu-id="01b75-125">升級之後對自動化和工具的變更</span><span class="sxs-lookup"><span data-stu-id="01b75-125">Changes to automation and tooling after the upgrade</span></span>
<span data-ttu-id="01b75-126">在將保存庫類型從傳統部署模型升級成 Resource Manager 部署模型時，請更新現有的自動化功能或工具，以確保它在移轉之後仍可繼續運作。</span><span class="sxs-lookup"><span data-stu-id="01b75-126">As you upgrade the vault type from the classic deployment model to the Resource Manager deployment model, update the existing automation or tooling to ensure that it continues to work after the upgrade.</span></span>

### <a name="prepare-your-environment-for-the-upgrade"></a><span data-ttu-id="01b75-127">讓環境進行升級準備</span><span class="sxs-lookup"><span data-stu-id="01b75-127">Prepare your environment for the upgrade</span></span>

* [<span data-ttu-id="01b75-128">安裝 PowerShell 或將它升級為第 5 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="01b75-128">Install PowerShell or upgrade it to version 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="01b75-129">安裝最新版的 Azure PowerShell MSI</span><span class="sxs-lookup"><span data-stu-id="01b75-129">Install the latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="01b75-130">下載復原服務保存庫升級指令碼</span><span class="sxs-lookup"><span data-stu-id="01b75-130">Download the Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="01b75-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="01b75-131">Prerequisites</span></span>
<span data-ttu-id="01b75-132">若要從 Site Recovery 保存庫升級成以 Azure Resource Manager 為基礎的復原服務保存庫，您必須符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="01b75-132">To upgrade from Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults, you must meet the following requirements:</span></span>

* <span data-ttu-id="01b75-133">最低代理程式版本：伺服器上安裝的 Azure Site Recovery Provider 版本必須為 5.1.1700.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="01b75-133">Minimum agent version: The version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="01b75-134">支援的設定：您無法使用存放區域網路 (SAN) 或 SQL Server AlwaysOn 可用性群組來設定保存庫。</span><span class="sxs-lookup"><span data-stu-id="01b75-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="01b75-135">所有其他的設定則可支援。</span><span class="sxs-lookup"><span data-stu-id="01b75-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="01b75-136">升級之後，您就只能透過 PowerShell 來管理儲存體對應。</span><span class="sxs-lookup"><span data-stu-id="01b75-136">After the upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="01b75-137">支援的部署案例：您的保存庫不應該是「VMware 到 Azure」舊有部署模型。</span><span class="sxs-lookup"><span data-stu-id="01b75-137">Supported deployment scenario: Your vault shouldn’t be the *VMware to Azure* legacy deployment model.</span></span> <span data-ttu-id="01b75-138">在繼續之前，請先改為增強部署模型。</span><span class="sxs-lookup"><span data-stu-id="01b75-138">Before you proceed, first move to the enhanced deployment model.</span></span>

* <span data-ttu-id="01b75-139">由使用者啟動的作用中作業皆未涉及管理平面作業：由於在升級期間會限制對管理平面的存取，因此請先完成所有的管理平面動作，再觸發升級。</span><span class="sxs-lookup"><span data-stu-id="01b75-139">No active user-initiated jobs that involve management plane operations: Because access to the management plane is restricted during upgrade, complete all your management plane actions before you trigger the upgrade.</span></span> <span data-ttu-id="01b75-140">此程序不包含進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="01b75-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="01b75-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="01b75-141">Frequently asked questions</span></span>

<span data-ttu-id="01b75-142">**升級是否會影響進行中的複寫？**</span><span class="sxs-lookup"><span data-stu-id="01b75-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="01b75-143">否。</span><span class="sxs-lookup"><span data-stu-id="01b75-143">No.</span></span> <span data-ttu-id="01b75-144">進行中的複寫在升級期間與升級後會繼續進行，不會中斷。</span><span class="sxs-lookup"><span data-stu-id="01b75-144">Your ongoing replication continues uninterrupted during and after the upgrade.</span></span>

<span data-ttu-id="01b75-145">**站對站 VPN 和 IP 設定等網路設定會發生什麼狀況？**</span><span class="sxs-lookup"><span data-stu-id="01b75-145">**What happens to network settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="01b75-146">升級不會影響網路設定。</span><span class="sxs-lookup"><span data-stu-id="01b75-146">The upgrade doesn't affect the network settings.</span></span> <span data-ttu-id="01b75-147">Azure 對內部部署的所有連線都會保持不變。</span><span class="sxs-lookup"><span data-stu-id="01b75-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="01b75-148">**如果近期內不打算升級，我的保存庫會怎麼樣？**</span><span class="sxs-lookup"><span data-stu-id="01b75-148">**What happens to my vaults if I don’t plan to upgrade in the near future?**</span></span>

<span data-ttu-id="01b75-149">自 2017 年 9 月起，舊 Azure 入口網站的 Site Recovery 保存庫支援將會淘汰。</span><span class="sxs-lookup"><span data-stu-id="01b75-149">Support for Site Recovery vault in the old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="01b75-150">我們強烈建議您使用升級功能來改用新的入口網站。</span><span class="sxs-lookup"><span data-stu-id="01b75-150">We strongly recommend that you use the upgrade feature to move to the new portal.</span></span>

<span data-ttu-id="01b75-151">**對於我現有的工具來說，此移轉計劃有何意義？**</span><span class="sxs-lookup"><span data-stu-id="01b75-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="01b75-152">將您的工具更新為 Resource Manager 部署模型，是您在升級計畫中必須說明的最重要變更之一。</span><span class="sxs-lookup"><span data-stu-id="01b75-152">Updating your tooling to the Resource Manager deployment model is one of the most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="01b75-153">復原服務保存庫是以 Resource Manager 部署模型作為基礎。</span><span class="sxs-lookup"><span data-stu-id="01b75-153">The Recovery Services vaults are based on the Resource Manager deployment model.</span></span> 

<span data-ttu-id="01b75-154">**管理平面的停機時間會持續多久？**</span><span class="sxs-lookup"><span data-stu-id="01b75-154">**How long does the management-plane downtime last?**</span></span>

<span data-ttu-id="01b75-155">升級通常需要約 15 到 30 分鐘，最多則可能需要一個小時。</span><span class="sxs-lookup"><span data-stu-id="01b75-155">The upgrade ordinarily takes about 15 to 30 minutes, and it could take up to a maximum of one hour.</span></span>

<span data-ttu-id="01b75-156">**升級之後可以復原嗎？**</span><span class="sxs-lookup"><span data-stu-id="01b75-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="01b75-157">否。</span><span class="sxs-lookup"><span data-stu-id="01b75-157">No.</span></span> <span data-ttu-id="01b75-158">將資源成功升級之後，即不支援復原。</span><span class="sxs-lookup"><span data-stu-id="01b75-158">Rollback is not supported after the resources have been successfully upgraded.</span></span>

<span data-ttu-id="01b75-159">**我是否可以驗證訂用帳戶或資源，以查看是否能夠將它們升級？**</span><span class="sxs-lookup"><span data-stu-id="01b75-159">**Can I validate my subscription or resources to see whether they can be upgraded?**</span></span>

<span data-ttu-id="01b75-160">是。</span><span class="sxs-lookup"><span data-stu-id="01b75-160">Yes.</span></span> <span data-ttu-id="01b75-161">在平台支援的升級選項中，升級的第一個步驟就是驗證資源是否能夠升級。</span><span class="sxs-lookup"><span data-stu-id="01b75-161">In the platform-supported upgrade option, the first step in the upgrade is to validate that the resources are capable of an upgrade.</span></span> <span data-ttu-id="01b75-162">如果驗證失敗，您會收到適當的錯誤訊息或警告。</span><span class="sxs-lookup"><span data-stu-id="01b75-162">If the validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="01b75-163">**如何回報升級問題？**</span><span class="sxs-lookup"><span data-stu-id="01b75-163">**How do I report an issue with the upgrade?**</span></span>

<span data-ttu-id="01b75-164">如果您在升級期間發生任何失敗，請記下錯誤所列出的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="01b75-164">If you experience any failures during the upgrade, note the operation ID that's listed in the error.</span></span> <span data-ttu-id="01b75-165">Microsoft 支援服務會主動解決問題。</span><span class="sxs-lookup"><span data-stu-id="01b75-165">Microsoft Support will proactively work on resolving the issue.</span></span> <span data-ttu-id="01b75-166">您也可以連絡支援小組，並提供您的訂用帳戶識別碼、保存庫名稱，以及作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="01b75-166">You can also contact the Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="01b75-167">支援人員會想辦法盡快解決問題。</span><span class="sxs-lookup"><span data-stu-id="01b75-167">Support will work to resolve the issue as quickly as possible.</span></span> <span data-ttu-id="01b75-168">除非 Microsoft 明確指示，否則請勿重試作業。</span><span class="sxs-lookup"><span data-stu-id="01b75-168">Do not retry the operation unless you are explicitly instructed to do so by Microsoft.</span></span>

## <a name="run-the-script"></a><span data-ttu-id="01b75-169">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="01b75-169">Run the script</span></span>

<span data-ttu-id="01b75-170">在 PowerShell 中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="01b75-170">In PowerShell, run the following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="01b75-171">SubscriptionID：與您要升級之保存庫相關聯的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="01b75-171">SubscriptionID: The subscription ID that's associated with the vault that you're upgrading.</span></span>

* <span data-ttu-id="01b75-172">VaultName：您要升級之保存庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="01b75-172">VaultName: The name of the vault that you're upgrading.</span></span>

* <span data-ttu-id="01b75-173">Location：您要升級之保存庫的所在位置。</span><span class="sxs-lookup"><span data-stu-id="01b75-173">Location: The location of the vault that you're upgrading.</span></span>

* <span data-ttu-id="01b75-174">ResourceType：Site Recovery 保存庫的 HyperVRecoveryManagerVault。</span><span class="sxs-lookup"><span data-stu-id="01b75-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="01b75-175">TargetResourceGroupName：要放置升級後保存庫的資源群組。</span><span class="sxs-lookup"><span data-stu-id="01b75-175">TargetResourceGroupName: The resource group into which you want the upgraded vault to be placed.</span></span> <span data-ttu-id="01b75-176">TargetResourceGroupName 可為 Azure Resource Manager 中現有的資源群組，或是新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="01b75-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="01b75-177">如果提供的 TargetResourceGroupName 不存在，則升級過程中會在與保存庫相同的位置建立一個。</span><span class="sxs-lookup"><span data-stu-id="01b75-177">If the TargetResourceGroupName that's supplied does not exist, it is created as part of the upgrade in the same location as the vault.</span></span> <span data-ttu-id="01b75-178">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)的＜資源群組＞一節。</span><span class="sxs-lookup"><span data-stu-id="01b75-178">For more information, see the "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="01b75-179">資源群組的命名受限於某些條件約束。</span><span class="sxs-lookup"><span data-stu-id="01b75-179">Resource group naming is subject to certain constraints.</span></span> <span data-ttu-id="01b75-180">若要防止保存庫升級失敗，請務必仔細遵守命名慣例。</span><span class="sxs-lookup"><span data-stu-id="01b75-180">To prevent vault upgrade failure, be sure to observe the naming convention carefully.</span></span>
    >
    ><span data-ttu-id="01b75-181">例如：</span><span class="sxs-lookup"><span data-stu-id="01b75-181">For example:</span></span>
    >
    ><span data-ttu-id="01b75-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="01b75-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="01b75-183">或者，您也可以執行下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="01b75-183">Alternatively, you can run the following script.</span></span> <span data-ttu-id="01b75-184">為必要參數輸入值。</span><span class="sxs-lookup"><span data-stu-id="01b75-184">Enter the values for the required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for the following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="01b75-185">PowerShell 指令碼會提示您輸入認證。</span><span class="sxs-lookup"><span data-stu-id="01b75-185">The PowerShell script prompts you to enter your credentials.</span></span> <span data-ttu-id="01b75-186">請輸入認證兩次，一次用於傳統部署模型帳戶，一次用於 Azure Resource Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="01b75-186">Enter them twice, once for the classic deployment model account and once for the Azure Resource Manager account.</span></span>

2. <span data-ttu-id="01b75-187">在輸入認證之後，指令碼會執行檢查，以判斷您的基礎結構設定是否符合先前所述的需求。</span><span class="sxs-lookup"><span data-stu-id="01b75-187">After you've entered your credentials, the script runs a check to determine whether your infrastructure setup meets the previously mentioned requirements.</span></span>

3. <span data-ttu-id="01b75-188">必要條件經過檢查並確認之後，系統會提示您繼續進行保存庫升級。</span><span class="sxs-lookup"><span data-stu-id="01b75-188">After the prerequisites have been checked and confirmed, you are prompted to proceed with the vault upgrade.</span></span> <span data-ttu-id="01b75-189">升級流程會開始升級您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="01b75-189">The upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="01b75-190">整個升級需要 15 到 30 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="01b75-190">The entire upgrade can take 15 to 30 minutes to complete.</span></span>

4. <span data-ttu-id="01b75-191">成功完成升級後，您便可以在新的 Azure 入口網站中存取升級後的保存庫。</span><span class="sxs-lookup"><span data-stu-id="01b75-191">After the upgrade has been completed successfully, you can access the upgraded vault in the new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="01b75-192">升級後保存庫的管理</span><span class="sxs-lookup"><span data-stu-id="01b75-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-the-recovery-services-vault"></a><span data-ttu-id="01b75-193">在復原服務保存庫中使用 Azure Site Recovery 來進行複寫</span><span class="sxs-lookup"><span data-stu-id="01b75-193">Replicate by using Azure Site Recovery in the Recovery Services vault</span></span>

* <span data-ttu-id="01b75-194">現在可在各個 Azure 區域之間保護您的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="01b75-194">You can now protect your Azure VMs from one region to another.</span></span> <span data-ttu-id="01b75-195">如需詳細資訊，請參閱[使用 Azure Site Recovery 在區域之間椱寫 Azure VM](site-recovery-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="01b75-196">如需將 VMware VM 複寫至 Azure 的詳細資訊，請參閱[使用 Site Recovery 將 VMWare VM 複寫至 Azure](vmware-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-196">For more information about replicating VMware VMs to Azure, see [Replicate VMware VMs to Azure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01b75-197">如需將 Hyper-V VM (不含 VMM) 複寫至 Azure 的詳細資訊，請參閱[將 Hyper-V 虛擬機器 (不含 VMM) 複寫至 Azure](hyper-v-site-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-197">For more information about replicating Hyper-V VMs (without VMM) to Azure, see [Replicate Hyper-V virtual machines (without VMM) to Azure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01b75-198">如需將 Hyper-V VM (含 VMM) 複寫至 Azure 的詳細資訊，請參閱[使用 Azure 入口網站中的 Site Recovery 將 Hyper-V 虛擬機器 (位於 VMM 雲端中) 複寫至 Azure](vmm-to-azure-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-198">For more information about replicating Hyper-V VMs (with VMM) to Azure, see [Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01b75-199">如需將 Hyper-V VM (含 VMM) 複寫至次要站台的詳細資訊，請參閱[使用 Azure 入口網站將位於 VMM 雲端中的 Hyper-V 虛擬機器複寫至次要 VMM 站台](site-recovery-vmm-to-vmm.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-199">For more information about replicating Hyper-VMs (with VMM) to a secondary site, see [Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using the Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="01b75-200">如需將 VMware VM 複寫至次要站台的詳細資訊，請參閱[在傳統 Azure 入口網站中，將內部部署 VMware 虛擬機器或實體伺服器複寫到次要站台](site-recovery-vmware-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-200">For more information about replicating VMware VMs to a secondary site, see [Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="01b75-201">檢視複寫的項目</span><span class="sxs-lookup"><span data-stu-id="01b75-201">View your replicated items</span></span>

<span data-ttu-id="01b75-202">下圖為復原服務保存庫儀表板頁面，其中顯示了保存庫的金鑰實體。</span><span class="sxs-lookup"><span data-stu-id="01b75-202">The following image shows the Recovery Services vault dashboard page that displays key entities for the vault.</span></span> <span data-ttu-id="01b75-203">若要檢視保存庫中受保護實體的清單，請選取 [Site Recovery] > [複寫的項目]。</span><span class="sxs-lookup"><span data-stu-id="01b75-203">To view a list of protected entities in the vault, select **Site Recovery** > **Replicated items**.</span></span>


![複寫的項目](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="01b75-205">下圖顯示用來檢視複寫項目的的工作流程和用來起始容錯移轉的**容錯移轉**命令。</span><span class="sxs-lookup"><span data-stu-id="01b75-205">The following image shows the workflow for viewing your replicated items and the **Failover** command for initiating a failover.</span></span>

![複寫的項目](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="01b75-207">檢視複寫設定</span><span class="sxs-lookup"><span data-stu-id="01b75-207">View your replication settings</span></span>

<span data-ttu-id="01b75-208">在 Site Recovery 保存庫中，每個保護群組皆有設定複製頻率、復原點保留期、應用程式一致的快照頻率，以及其他複寫設定。</span><span class="sxs-lookup"><span data-stu-id="01b75-208">In the Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="01b75-209">在復原服務保存庫中，這些設定會設成複寫原則。</span><span class="sxs-lookup"><span data-stu-id="01b75-209">In the Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="01b75-210">原則的名稱即為保護群組的名稱，也就是 primarycloud_Policy。</span><span class="sxs-lookup"><span data-stu-id="01b75-210">The name of the policy is the name of the protection group or the *primarycloud_Policy*.</span></span>

<span data-ttu-id="01b75-211">如需複寫原則的詳細資訊，請參閱[管理 VMware 至 Azure 的複寫原則](site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="01b75-211">For more information about replication policy, see [Manage replication policy for VMware to Azure](site-recovery-setup-replication-settings-vmware.md).</span></span>
