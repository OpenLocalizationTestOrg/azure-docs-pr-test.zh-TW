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
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>升級站台復原保存庫 tooan Azure 資源管理員為基礎的復原服務保存庫

本文說明如何 tooupgrade Azure Site Recovery 保存庫 tooAzure 資源管理員為基礎的復原服務保存庫，而不會影響進行中的複寫。 如需 Azure Resource Manager 功能和優點的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。

## <a name="introduction"></a>簡介
復原服務保存庫是 Azure 資源管理員資源管理原生 hello 雲端中的備份和災害復原。 Hello 新的 Azure 入口網站中是一致的保存庫，您可以使用它取代了 hello 傳統備份和站台復原保存庫。

復原服務保存庫提供了一系列的功能，包括：

* 支援 Azure Resource Manager：可以保護您的虛擬機器與實體機器，並將這些機器容錯移轉至 Azure Resource Manager 堆疊。

* 排除磁碟： 如果您的暫存檔案或高的變換資料，您不想 toouse 所有您的頻寬，您可以從複寫排除磁碟區。 這項功能目前已啟用*VMware tooAzure*和*HYPER-V tooAzure*延伸 tooother 情況。

* Premium 和本機備援儲存體的支援： 您現在可以來保護伺服器高階儲存體中，讓客戶 tooprotect 應用程式，以更高的帳戶輸入/輸出作業每秒 (IOPS)。 這項功能目前已啟用在*VMware tooAzure*。

* 簡化開始使用經驗： hello 增強開始使用經驗的設計是簡單的 toomake 災害復原安裝程式。

* 備份及 Site Recovery 管理從 hello 相同保存庫： 您現在可以保護的嚴重損壞修復伺服器或 hello 從執行備份相同的保存庫，可額外負荷會大幅減少您的管理。

如需有關升級的 hello 體驗和功能的詳細資訊，請參閱 hello[儲存體、 備份及復原的部落格](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/)。

## <a name="salient-features"></a>主要功能

* 不影響進行中的複寫：進行中的複寫在升級期間與升級後會繼續進行，完全不會中斷。

* 不必另外付費：不必另外付費即可獲得一整組更新後的功能。

* 無資料遺失： 因為此程序是升級而不會移轉，複寫現有的復原點和設定保留不變期間和之後 hello 升級。


## <a name="what-happens-during-hello-vault-upgrade"></a>Hello 保存庫升級期間會發生什麼情況？

Hello 在升級期間，您無法執行作業，例如註冊新的伺服器或啟用複寫虛擬機器 (VM)。 包含讀取資料來源，或寫入資料 toohello 保存庫，例如受保護項目 toohello 保存庫中，進行中的複寫作業持續不受干擾。

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>變更 tooautomation 和 hello 升級後的工具
當您升級 hello 保存庫類型從 hello 傳統部署模型 toohello Resource Manager 部署模型時，更新 hello 現有的自動化或工具 tooensure 仍 toowork hello 升級之後。

### <a name="prepare-your-environment-for-hello-upgrade"></a>準備環境以 hello 升級

* [安裝 PowerShell，或將它升級 tooversion 5 或更新版本](https://www.microsoft.com/download/details.aspx?id=50395)
* [安裝 Azure PowerShell MSI hello 最新版本](https://github.com/Azure/azure-powershell/releases)
* [下載 hello 復原服務保存庫升級指令碼](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>必要條件
tooupgrade 從 Site Recovery 保存庫 tooAzure 資源管理員為基礎的復原服務保存庫，您必須符合下列需求的 hello:

* 最小的代理程式版本： hello 的伺服器上安裝 Azure Site Recovery Provider 的版本必須是 5.1.1700.0 或更新版本。

* 支援的設定：您無法使用存放區域網路 (SAN) 或 SQL Server AlwaysOn 可用性群組來設定保存庫。 所有其他的設定則可支援。

    >[!NOTE]
    >Hello 升級之後，您可以管理儲存體對應，僅透過 PowerShell。

* 支援的部署案例： 您的保存庫不應該是 hello *VMware tooAzure*舊版部署模型。 在繼續之前，先移動 toohello 增強的部署模型。

* 沒有作用中使用者啟動的作業涉及管理平面作業： 因為升級期間，有限制存取 toohello 管理平面，完成所有管理平面動作之前觸發 hello 升級。 此程序不包含進行中的複寫。

## <a name="frequently-asked-questions"></a>常見問題集

**升級是否會影響進行中的複寫？**

否。 期間和之後 hello 升級正在進行的複寫會繼續不會中斷。

**發生什麼事 toonetwork 設定，例如站對站 VPN 和 IP 設定？**

hello 升級不會影響 hello 網路設定。 Azure 對內部部署的所有連線都會保持不變。

**如果我不打算在未來附近 hello tooupgrade 會怎樣 toomy 保存庫？**

將啟動 2017 年 9 月被取代的 hello 舊的 Azure 入口網站中的站台復原保存庫支援。 我們強烈建議您改用 hello 升級功能 toomove toohello 新入口網站。

**對於我現有的工具來說，此移轉計劃有何意義？**  

更新工具 toohello Resource Manager 部署模型是一種您必須負責在您升級計劃中的 hello 最重要變更。 hello Resource Manager 部署模型以 hello 復原服務保存庫。 

**時間長度沒有 hello 管理平面停機時間上一次嗎？**

hello 升級通常需要大約 15 too30 分鐘的時間，而且它最多可能需要 tooa 一小時的最大值。

**升級之後可以復原嗎？**

否。 已成功升級 hello 資源之後，不支援復原。

**可以我確認我的訂用帳戶或資源 toosee 是否可以升級？**

是。 Hello 平台支援升級選項，在 hello hello 升級第一個步驟是 toovalidate hello 資源都可以升級。 如果 hello 驗證失敗，您會收到適當的錯誤訊息或警告。

**如何回報 hello 升級的問題？**

如果在 hello 升級期間發生的任何錯誤，請注意 hello hello 錯誤中列出的作業識別碼。 Microsoft 支援會主動處理解決 hello 問題。 您也可以連絡與您的訂用帳戶 ID、 保存庫名稱，作業識別碼 hello 支援小組 支援將盡快運作 tooresolve hello 問題。 除非您另有明確指示 toodo，請勿重試 hello 作業是由 Microsoft。

## <a name="run-hello-script"></a>執行 hello 指令碼

在 PowerShell 中執行下列命令的 hello:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* 訂用帳戶 Id: hello 與您要升級的 hello 保存庫相關聯的訂用帳戶 ID。

* 您要升級的 hello 保存庫 VaultName: hello 名稱。

* 您要升級的 hello 保存庫的位置： hello 位置。

* ResourceType：Site Recovery 保存庫的 HyperVRecoveryManagerVault。

* TargetResourceGroupName: hello 資源群組要 hello 升級保存庫 toobe 放置。 TargetResourceGroupName 可為 Azure Resource Manager 中現有的資源群組，或是新的資源群組。 如果 hello TargetResourceGroupName 提供不存在，就會建立 hello 升級過程中 hello 相同 hello 保存庫的位置。 如需詳細資訊，請參閱 hello 「 資源群組 」 一節[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。

    >[!NOTE]
    >資源群組命名為主體 toocertain 條件約束。 tooprevent 保存庫升級失敗時，小心是確定 tooobserve hello 命名慣例。
    >
    >例如：
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

或者，您可以執行下列指令碼的 hello。 Hello 參數輸入值所需的 hello。

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. hello PowerShell 指令碼會提示您 tooenter 您的認證。 將其輸入兩次，一次 hello 傳統部署模型的帳戶，另一次 hello Azure 資源管理員帳戶。

2. 您輸入您的認證之後，hello 指令碼會執行檢查 toodetermine 是否您基礎結構安裝符合 hello 先前所述的需求。

3. Hello 必要條件已檢查並確認之後，您就會提示的 tooproceed hello 保存庫升級。 hello 升級程序會啟動升級您的保存庫。 hello 整個升級可能需要 15 too30 分鐘 toocomplete。

4. Hello 升級已順利完成之後，您可以存取 hello 新版 Azure 入口網站中的 hello 升級保存庫。

## <a name="post-upgrade-vault-management"></a>升級後保存庫的管理

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>使用 Azure Site Recovery 中復原服務保存庫的 hello 複寫

* 您現在可以從一個區域 tooanother 保護您的 Azure Vm。 如需詳細資訊，請參閱[使用 Azure Site Recovery 在區域之間椱寫 Azure VM](site-recovery-azure-to-azure.md)。

* 如需將 VMware Vm tooAzure 複寫的詳細資訊，請參閱[與 Site Recovery 的複寫 VMware Vm tooAzure](vmware-walkthrough-overview.md)。

* 如需複寫 （無 VMM) 的 HYPER-V Vm tooAzure 的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure](hyper-v-site-walkthrough-overview.md)。

* 如需複寫 （使用 VMM) 的 HYPER-V Vm tooAzure 的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器，在使用中的站台復原的 VMM 雲端 tooAzure hello Azure 入口網站](vmm-to-azure-walkthrough-overview.md)。

* 如需複寫 （使用 VMM) 的 Hyper-v Vm tooa 次要站台的詳細資訊，請參閱[複寫 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台使用 hello Azure 入口網站](site-recovery-vmm-to-vmm.md)。

* 如需將 VMware Vm tooa 次要站台複寫的詳細資訊，請參閱[複寫在內部部署 VMware 虛擬機器或實體伺服器 tooa 次要站台 hello 傳統 Azure 入口網站中的](site-recovery-vmware-to-vmware.md)。

### <a name="view-your-replicated-items"></a>檢視複寫的項目

hello 下列影像顯示 hello 復原服務保存庫儀表板頁面會顯示 hello 保存庫的實體索引鍵。 tooview hello 保存庫中的受保護實體的清單選取**Site Recovery** > **複寫項目**。


![複寫的項目](./media/upgrade-site-recovery-vaults/replicateditems.png)

hello 下列影像顯示 hello 工作流程，來檢視您的複寫的項目和 hello**容錯移轉**命令來起始容錯移轉。

![複寫的項目](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>檢視複寫設定

Hello Site Recovery 保存庫，在每個保護群組被設定的複製頻率、 復原點保留、 應用程式一致快照的頻率和其他複寫設定。 在 hello 復原服務保存庫，這些設定會設定為複寫原則。 hello hello 原則名稱是 hello hello 保護群組或名稱 hello *primarycloud_Policy*。

如需有關複寫原則的詳細資訊，請參閱[管理的 VMware tooAzure 的複寫原則](site-recovery-setup-replication-settings-vmware.md)。
