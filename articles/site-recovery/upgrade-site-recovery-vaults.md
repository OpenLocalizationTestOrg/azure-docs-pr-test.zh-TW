---
title: "aaaUpgrade Site Recovery 保存庫 tooan Azure 復原服務保存庫"
description: "了解如何 tooupgrade Azure Site Recovery 保存庫 tooa 復原服務保存庫"
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
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="92d51-103">升級站台復原保存庫 tooan Azure 資源管理員為基礎的復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="92d51-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="92d51-104">本文說明如何 tooupgrade Azure Site Recovery 保存庫 tooAzure 資源管理員為基礎的復原服務保存庫，而不會影響進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="92d51-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="92d51-105">如需 Azure Resource Manager 功能和優點的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="92d51-106">簡介</span><span class="sxs-lookup"><span data-stu-id="92d51-106">Introduction</span></span>
<span data-ttu-id="92d51-107">復原服務保存庫是 Azure 資源管理員資源管理原生 hello 雲端中的備份和災害復原。</span><span class="sxs-lookup"><span data-stu-id="92d51-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="92d51-108">Hello 新的 Azure 入口網站中是一致的保存庫，您可以使用它取代了 hello 傳統備份和站台復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="92d51-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="92d51-109">復原服務保存庫提供了一系列的功能，包括：</span><span class="sxs-lookup"><span data-stu-id="92d51-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="92d51-110">支援 Azure Resource Manager：可以保護您的虛擬機器與實體機器，並將這些機器容錯移轉至 Azure Resource Manager 堆疊。</span><span class="sxs-lookup"><span data-stu-id="92d51-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="92d51-111">排除磁碟： 如果您的暫存檔案或高的變換資料，您不想 toouse 所有您的頻寬，您可以從複寫排除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="92d51-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="92d51-112">這項功能目前已啟用*VMware tooAzure*和*HYPER-V tooAzure*延伸 tooother 情況。</span><span class="sxs-lookup"><span data-stu-id="92d51-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="92d51-113">Premium 和本機備援儲存體的支援： 您現在可以來保護伺服器高階儲存體中，讓客戶 tooprotect 應用程式，以更高的帳戶輸入/輸出作業每秒 (IOPS)。</span><span class="sxs-lookup"><span data-stu-id="92d51-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="92d51-114">這項功能目前已啟用在*VMware tooAzure*。</span><span class="sxs-lookup"><span data-stu-id="92d51-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="92d51-115">簡化開始使用經驗： hello 增強開始使用經驗的設計是簡單的 toomake 災害復原安裝程式。</span><span class="sxs-lookup"><span data-stu-id="92d51-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="92d51-116">備份及 Site Recovery 管理從 hello 相同保存庫： 您現在可以保護的嚴重損壞修復伺服器或 hello 從執行備份相同的保存庫，可額外負荷會大幅減少您的管理。</span><span class="sxs-lookup"><span data-stu-id="92d51-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="92d51-117">如需有關升級的 hello 體驗和功能的詳細資訊，請參閱 hello[儲存體、 備份及復原的部落格](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/)。</span><span class="sxs-lookup"><span data-stu-id="92d51-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="92d51-118">主要功能</span><span class="sxs-lookup"><span data-stu-id="92d51-118">Salient features</span></span>

* <span data-ttu-id="92d51-119">不影響進行中的複寫：進行中的複寫在升級期間與升級後會繼續進行，完全不會中斷。</span><span class="sxs-lookup"><span data-stu-id="92d51-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="92d51-120">不必另外付費：不必另外付費即可獲得一整組更新後的功能。</span><span class="sxs-lookup"><span data-stu-id="92d51-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="92d51-121">無資料遺失： 因為此程序是升級而不會移轉，複寫現有的復原點和設定保留不變期間和之後 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="92d51-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="92d51-122">Hello 保存庫升級期間會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="92d51-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="92d51-123">Hello 在升級期間，您無法執行作業，例如註冊新的伺服器或啟用複寫虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="92d51-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="92d51-124">包含讀取資料來源，或寫入資料 toohello 保存庫，例如受保護項目 toohello 保存庫中，進行中的複寫作業持續不受干擾。</span><span class="sxs-lookup"><span data-stu-id="92d51-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="92d51-125">變更 tooautomation 和 hello 升級後的工具</span><span class="sxs-lookup"><span data-stu-id="92d51-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="92d51-126">當您升級 hello 保存庫類型從 hello 傳統部署模型 toohello Resource Manager 部署模型時，更新 hello 現有的自動化或工具 tooensure 仍 toowork hello 升級之後。</span><span class="sxs-lookup"><span data-stu-id="92d51-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="92d51-127">準備環境以 hello 升級</span><span class="sxs-lookup"><span data-stu-id="92d51-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="92d51-128">安裝 PowerShell，或將它升級 tooversion 5 或更新版本</span><span class="sxs-lookup"><span data-stu-id="92d51-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="92d51-129">安裝 Azure PowerShell MSI hello 最新版本</span><span class="sxs-lookup"><span data-stu-id="92d51-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="92d51-130">下載 hello 復原服務保存庫升級指令碼</span><span class="sxs-lookup"><span data-stu-id="92d51-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="92d51-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="92d51-131">Prerequisites</span></span>
<span data-ttu-id="92d51-132">tooupgrade 從 Site Recovery 保存庫 tooAzure 資源管理員為基礎的復原服務保存庫，您必須符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="92d51-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="92d51-133">最小的代理程式版本： hello 的伺服器上安裝 Azure Site Recovery Provider 的版本必須是 5.1.1700.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92d51-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="92d51-134">支援的設定：您無法使用存放區域網路 (SAN) 或 SQL Server AlwaysOn 可用性群組來設定保存庫。</span><span class="sxs-lookup"><span data-stu-id="92d51-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="92d51-135">所有其他的設定則可支援。</span><span class="sxs-lookup"><span data-stu-id="92d51-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="92d51-136">Hello 升級之後，您可以管理儲存體對應，僅透過 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="92d51-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="92d51-137">支援的部署案例： 您的保存庫不應該是 hello *VMware tooAzure*舊版部署模型。</span><span class="sxs-lookup"><span data-stu-id="92d51-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="92d51-138">在繼續之前，先移動 toohello 增強的部署模型。</span><span class="sxs-lookup"><span data-stu-id="92d51-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="92d51-139">沒有作用中使用者啟動的作業涉及管理平面作業： 因為升級期間，有限制存取 toohello 管理平面，完成所有管理平面動作之前觸發 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="92d51-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="92d51-140">此程序不包含進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="92d51-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="92d51-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="92d51-141">Frequently asked questions</span></span>

<span data-ttu-id="92d51-142">**升級是否會影響進行中的複寫？**</span><span class="sxs-lookup"><span data-stu-id="92d51-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="92d51-143">否。</span><span class="sxs-lookup"><span data-stu-id="92d51-143">No.</span></span> <span data-ttu-id="92d51-144">期間和之後 hello 升級正在進行的複寫會繼續不會中斷。</span><span class="sxs-lookup"><span data-stu-id="92d51-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="92d51-145">**發生什麼事 toonetwork 設定，例如站對站 VPN 和 IP 設定？**</span><span class="sxs-lookup"><span data-stu-id="92d51-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="92d51-146">hello 升級不會影響 hello 網路設定。</span><span class="sxs-lookup"><span data-stu-id="92d51-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="92d51-147">Azure 對內部部署的所有連線都會保持不變。</span><span class="sxs-lookup"><span data-stu-id="92d51-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="92d51-148">**如果我不打算在未來附近 hello tooupgrade 會怎樣 toomy 保存庫？**</span><span class="sxs-lookup"><span data-stu-id="92d51-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="92d51-149">將啟動 2017 年 9 月被取代的 hello 舊的 Azure 入口網站中的站台復原保存庫支援。</span><span class="sxs-lookup"><span data-stu-id="92d51-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="92d51-150">我們強烈建議您改用 hello 升級功能 toomove toohello 新入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d51-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="92d51-151">**對於我現有的工具來說，此移轉計劃有何意義？**</span><span class="sxs-lookup"><span data-stu-id="92d51-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="92d51-152">更新工具 toohello Resource Manager 部署模型是一種您必須負責在您升級計劃中的 hello 最重要變更。</span><span class="sxs-lookup"><span data-stu-id="92d51-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="92d51-153">hello Resource Manager 部署模型以 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="92d51-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="92d51-154">**時間長度沒有 hello 管理平面停機時間上一次嗎？**</span><span class="sxs-lookup"><span data-stu-id="92d51-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="92d51-155">hello 升級通常需要大約 15 too30 分鐘的時間，而且它最多可能需要 tooa 一小時的最大值。</span><span class="sxs-lookup"><span data-stu-id="92d51-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="92d51-156">**升級之後可以復原嗎？**</span><span class="sxs-lookup"><span data-stu-id="92d51-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="92d51-157">否。</span><span class="sxs-lookup"><span data-stu-id="92d51-157">No.</span></span> <span data-ttu-id="92d51-158">已成功升級 hello 資源之後，不支援復原。</span><span class="sxs-lookup"><span data-stu-id="92d51-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="92d51-159">**可以我確認我的訂用帳戶或資源 toosee 是否可以升級？**</span><span class="sxs-lookup"><span data-stu-id="92d51-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="92d51-160">是。</span><span class="sxs-lookup"><span data-stu-id="92d51-160">Yes.</span></span> <span data-ttu-id="92d51-161">Hello 平台支援升級選項，在 hello hello 升級第一個步驟是 toovalidate hello 資源都可以升級。</span><span class="sxs-lookup"><span data-stu-id="92d51-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="92d51-162">如果 hello 驗證失敗，您會收到適當的錯誤訊息或警告。</span><span class="sxs-lookup"><span data-stu-id="92d51-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="92d51-163">**如何回報 hello 升級的問題？**</span><span class="sxs-lookup"><span data-stu-id="92d51-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="92d51-164">如果在 hello 升級期間發生的任何錯誤，請注意 hello hello 錯誤中列出的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="92d51-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="92d51-165">Microsoft 支援會主動處理解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="92d51-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="92d51-166">您也可以連絡與您的訂用帳戶 ID、 保存庫名稱，作業識別碼 hello 支援小組</span><span class="sxs-lookup"><span data-stu-id="92d51-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="92d51-167">支援將盡快運作 tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="92d51-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="92d51-168">除非您另有明確指示 toodo，請勿重試 hello 作業是由 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="92d51-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="92d51-169">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="92d51-169">Run hello script</span></span>

<span data-ttu-id="92d51-170">在 PowerShell 中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="92d51-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="92d51-171">訂用帳戶 Id: hello 與您要升級的 hello 保存庫相關聯的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="92d51-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="92d51-172">您要升級的 hello 保存庫 VaultName: hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="92d51-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="92d51-173">您要升級的 hello 保存庫的位置： hello 位置。</span><span class="sxs-lookup"><span data-stu-id="92d51-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="92d51-174">ResourceType：Site Recovery 保存庫的 HyperVRecoveryManagerVault。</span><span class="sxs-lookup"><span data-stu-id="92d51-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="92d51-175">TargetResourceGroupName: hello 資源群組要 hello 升級保存庫 toobe 放置。</span><span class="sxs-lookup"><span data-stu-id="92d51-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="92d51-176">TargetResourceGroupName 可為 Azure Resource Manager 中現有的資源群組，或是新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92d51-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="92d51-177">如果 hello TargetResourceGroupName 提供不存在，就會建立 hello 升級過程中 hello 相同 hello 保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="92d51-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="92d51-178">如需詳細資訊，請參閱 hello 「 資源群組 」 一節[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="92d51-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="92d51-179">資源群組命名為主體 toocertain 條件約束。</span><span class="sxs-lookup"><span data-stu-id="92d51-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="92d51-180">tooprevent 保存庫升級失敗時，小心是確定 tooobserve hello 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="92d51-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="92d51-181">例如：</span><span class="sxs-lookup"><span data-stu-id="92d51-181">For example:</span></span>
    >
    ><span data-ttu-id="92d51-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="92d51-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="92d51-183">或者，您可以執行下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="92d51-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="92d51-184">Hello 參數輸入值所需的 hello。</span><span class="sxs-lookup"><span data-stu-id="92d51-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="92d51-185">hello PowerShell 指令碼會提示您 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="92d51-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="92d51-186">將其輸入兩次，一次 hello 傳統部署模型的帳戶，另一次 hello Azure 資源管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="92d51-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="92d51-187">您輸入您的認證之後，hello 指令碼會執行檢查 toodetermine 是否您基礎結構安裝符合 hello 先前所述的需求。</span><span class="sxs-lookup"><span data-stu-id="92d51-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="92d51-188">Hello 必要條件已檢查並確認之後，您就會提示的 tooproceed hello 保存庫升級。</span><span class="sxs-lookup"><span data-stu-id="92d51-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="92d51-189">hello 升級程序會啟動升級您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="92d51-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="92d51-190">hello 整個升級可能需要 15 too30 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="92d51-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="92d51-191">Hello 升級已順利完成之後，您可以存取 hello 新版 Azure 入口網站中的 hello 升級保存庫。</span><span class="sxs-lookup"><span data-stu-id="92d51-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="92d51-192">升級後保存庫的管理</span><span class="sxs-lookup"><span data-stu-id="92d51-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="92d51-193">使用 Azure Site Recovery 中復原服務保存庫的 hello 複寫</span><span class="sxs-lookup"><span data-stu-id="92d51-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="92d51-194">您現在可以從一個區域 tooanother 保護您的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="92d51-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="92d51-195">如需詳細資訊，請參閱[使用 Azure Site Recovery 在區域之間椱寫 Azure VM](site-recovery-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="92d51-196">如需將 VMware Vm tooAzure 複寫的詳細資訊，請參閱[與 Site Recovery 的複寫 VMware Vm tooAzure](vmware-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="92d51-197">如需複寫 （無 VMM) 的 HYPER-V Vm tooAzure 的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure](hyper-v-site-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="92d51-198">如需複寫 （使用 VMM) 的 HYPER-V Vm tooAzure 的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器，在使用中的站台復原的 VMM 雲端 tooAzure hello Azure 入口網站](vmm-to-azure-walkthrough-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="92d51-199">如需複寫 （使用 VMM) 的 Hyper-v Vm tooa 次要站台的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台使用 hello Azure 入口網站](site-recovery-vmm-to-vmm.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="92d51-200">如需將 VMware Vm tooa 次要站台複寫的詳細資訊，請參閱[複寫在內部部署 VMware 虛擬機器或實體伺服器 tooa 次要站台 hello 傳統 Azure 入口網站中的](site-recovery-vmware-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="92d51-201">檢視複寫的項目</span><span class="sxs-lookup"><span data-stu-id="92d51-201">View your replicated items</span></span>

<span data-ttu-id="92d51-202">hello 下列影像顯示 hello 復原服務保存庫儀表板頁面會顯示 hello 保存庫的實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="92d51-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="92d51-203">tooview hello 保存庫中的受保護實體的清單選取**Site Recovery** > **複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="92d51-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![複寫的項目](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="92d51-205">hello 下列影像顯示 hello 工作流程，來檢視您的複寫的項目和 hello**容錯移轉**命令來起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="92d51-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![複寫的項目](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="92d51-207">檢視複寫設定</span><span class="sxs-lookup"><span data-stu-id="92d51-207">View your replication settings</span></span>

<span data-ttu-id="92d51-208">Hello Site Recovery 保存庫，在每個保護群組被設定的複製頻率、 復原點保留、 應用程式一致快照的頻率和其他複寫設定。</span><span class="sxs-lookup"><span data-stu-id="92d51-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="92d51-209">在 hello 復原服務保存庫，這些設定會設定為複寫原則。</span><span class="sxs-lookup"><span data-stu-id="92d51-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="92d51-210">hello hello 原則名稱是 hello hello 保護群組或名稱 hello *primarycloud_Policy*。</span><span class="sxs-lookup"><span data-stu-id="92d51-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="92d51-211">如需有關複寫原則的詳細資訊，請參閱[管理的 VMware tooAzure 的複寫原則](site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="92d51-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
