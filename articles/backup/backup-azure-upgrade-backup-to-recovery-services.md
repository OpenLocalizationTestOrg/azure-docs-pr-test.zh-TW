---
title: "aaaUpgrade 備份保存庫 tooa 復原服務保存庫 （預覽） |Microsoft 文件"
description: "指示和支援資訊 tooupgrade Azure 備份保存庫的 tooa 復原服務保存庫。"
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>升級備份保存庫 tooa 復原服務保存庫

本文說明如何備份保存庫 tooupgrade tooa 復原服務保存庫。 hello 升級程序不會影響任何執行中的備份作業，而且沒有備份的資料會遺失。 hello 主要原因 tooupgrade 備份保存庫 tooa 復原服務保存庫：
- 備份保存庫的所有功能都會保留在復原服務保存庫中。
- 復原服務保存庫較備份保存庫具有更多功能，包括更完善的安全性、整合式監控、更快速還原和項目等級還原。
- 從經過改良和簡化的入口網站管理備份項目。
- 新功能只適用於 tooRecovery 服務保存庫。

## <a name="impact-toooperations-during-upgrade"></a>在升級期間影響 toooperations

升級時的備份保存庫 tooa 復原服務保存庫，也不會影響 tooyour 資料平面作業。 所有備份作業都會照常繼續進行，且任何使用中的還原作業都會繼續而不受中斷。 Hello 在升級期間，管理作業帶來短的停機時間，而且您無法保護新的項目，或建立臨機操作備份工作。 IaaS Vm 的還原作業不會在 hello 升級期間執行。 hello 保存庫升級將會花費小時 toocomplete 底下。 一旦完成之後，復原服務保存庫會取代 hello 備份保存庫。

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>在升級之後變更 tooyour 自動化和工具

準備 hello 保存庫升級您的基礎結構，您必須更新您現有的自動化或 tooling tooensure 它繼續 toowork hello 升級之後。
請參閱 hello hello PowerShell cmdlet 參考[Service Manager 部署模型](backup-client-automation-classic.md)和 hello [Resource Manager 部署模型](backup-client-automation.md)。


## <a name="before-you-upgrade"></a>您在升級之前

檢查 hello 下列發出升級前備份保存庫 tooRecovery 服務保存庫。

- **最小的代理程式版本**: tooupgrade 保存庫，請確定 hello Microsoft Azure 復原服務 」 (MARS) 代理程式至少為版本 2.0.9070.0。 如果超過 2.0.9070.0 hello MARS 代理程式，請啟動 hello 升級程序之前更新 hello 代理程式。
- **執行個體為基礎的計費模型**： 復原服務保存庫只支援 hello 執行個體計費的模型。 如果您有備份保存庫使用 hello 舊版儲存體計費的模型，請升級期間轉換 hello 計費模型。
- **沒有任何進行中的備份設定作業**： 在升級期間，會限制存取 toohello 管理平面。 完成所有管理平面動作，然後再啟動 hello 升級。

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>使用 PowerShell 指令碼 tooupgrade 您保存庫

您可以使用 PowerShell 指令碼 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。 確認您擁有 hello 需要 PowerShell 元件 tootrigger hello 保存庫升級。 備份保存庫的 PowerShell 指令碼不適用於復原服務保存庫。 準備您的環境 tooupgrade hello 保存庫：

1. 安裝或升級[Windows Management Framework (WMF) tooversion 5](https://www.microsoft.com/download/details.aspx?id=50395)或更新版本。
2. [安裝 Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi)。
3. 下載 hello [PowerShell 指令碼](https://aka.ms/vaultupgradescript2)tooupgrade 您保存庫。

### <a name="run-hello-powershell-script"></a>執行 hello PowerShell 指令碼

使用下列指令碼 tooupgrade hello 您保存庫。 下列範例指令碼的 hello 有 hello 參數的說明。

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**SubscriptionID** -hello 正在升級的 hello 保存庫的訂用帳戶識別碼。<br/>
**VaultName** -hello 正在升級的 hello 備份保存庫的名稱。<br/>
**位置**-正在升級的 hello 保存庫的位置。<br/>
**ResourceType** - 使用 BackupVault。<br/>
**TargetResourceGroupName** -因為您要升級 hello 保存庫 tooa 資源管理員為基礎的部署，請指定資源群組。 您可以使用現有的資源群組，或提供新的名稱來建立一個新的群組。 如果您拼錯 hello 資源群組名稱，您可以建立新的資源群組。 toolearn 進一步了解資源群組，請閱讀這[資源群組的相關概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。

>[!NOTE]
> 資源群組名稱具有條件約束。 要確定 toofollow hello 指引。因此，失敗 toodo 可能會造成保存庫升級 toofail。
>
>

hello 下列程式碼片段是一個範例的 PowerShell 命令應該看起來像：

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

您也可以執行不含任何參數的 hello 指令碼，系統會詢問 tooprovide 輸入所有必要的參數。

hello PowerShell 指令碼會提示您 tooenter 您的認證。 輸入您的認證兩次： 一次 hello Service Manager 帳戶和第二次 hello 資源管理員帳戶。

### <a name="pre-requisites-checking"></a>必要條件檢查
當您輸入您的 Azure 認證之後時，Azure 會檢查您的環境符合下列必要條件 hello:

- **最小的代理程式版本**-升級備份保存庫 tooRecovery 服務保存庫至少需要 hello MARS 代理程式 toobe 2.0.9070 版本。 如果您有項目向 tooa 備份保存庫的代理程式之前 2.0.9070，hello 先決條件檢查會失敗。 如果 hello 必要條件檢查失敗，更新 hello 代理程式並再試一次 tooupgrade hello 保存庫。 您可以下載 hello hello 代理程式，從最新版本[http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe)。
- **進行中的組態工作**： 如果有人備份保存庫設定 toobe 升級，或註冊項目設定作業，hello 必要條件檢查失敗。 完成 hello 項設定，或完成註冊 hello 項目，然後再啟動 hello 保存庫的升級程序。
- **儲存體計費的模型**： 復原服務保存庫支援 hello 執行個體計費的模型。 如果您 hello 保存庫上執行升級備份保存庫，使用 hello 儲存體計費的模型，會提示的 tooupgrade 保存庫以及 hello 計費模型。 否則，在第一次，更新您的計費模型，然後執行 hello 保存庫升級。
- 識別資源群組，如 hello 復原服務保存庫。 tootake 利用 hello 資源管理員部署功能，您必須將 復原服務保存庫的資源群組中。 如果您不知道哪一個資源群組 toouse，提供名稱和 hello 升級程序會為您建立 hello 資源群組。 hello 升級程序也會將 hello 保存庫與 hello 新資源群組。

一旦 hello 升級程序完成時檢查 hello 先決條件 hello 程序會提示您 toostart hello 保存庫升級。 確認之後，hello 升級程序通常會採用周圍 15 20 分鐘 toocomplete，視您的保存庫 hello 大小而定。 如果您有大型的保存庫，則升級可能佔用 too90 分鐘。

## <a name="managing-your-recovery-services-vaults"></a>管理復原服務保存庫

hello 下列畫面顯示新的復原服務保存庫，從備份保存庫，hello Azure 入口網站中升級。 hello 第一個畫面會顯示 hello 保存庫儀表板會顯示 hello 保存庫的實體索引鍵。

![從備份保存庫升級的復原服務保存庫範例](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

hello 第二個螢幕會顯示可用 toohelp 您開始使用 hello 復原服務保存庫的 hello 說明連結。

![hello 快速入門刀鋒視窗中的說明連結](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>升級後步驟
復原服務保存庫支援在備份原則中指定時區資訊。 保存庫已成功升級之後，從保存庫設定 功能表上，移至 tooBackup 原則，並更新 hello 時區資訊的每個設定 hello 保存庫中的 hello 原則。 此畫面已經顯示 hello 備份的排程時間指定為每個當地時區時，使用您建立原則。 

## <a name="enhanced-security"></a>強化的安全性

當備份保存庫會升級 tooa 復原服務保存庫時，自動開啟該保存庫的 hello 安全性設定。 當 hello 安全性設定是在特定作業，例如刪除備份，或變更複雜密碼需要[Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PIN。 如需有關 hello 增強式安全性的詳細資訊，請參閱 hello 文章[tooprotect 混合式備份的安全性功能](backup-azure-security-feature.md)。 

Hello 增強式安全性開啟時，資料會保留向上 too14 天後已從 hello 保存庫刪除 hello 復原點資訊。 客戶需支付此安全性資料的儲存體費用。 安全性資料保留套用 toorecovery 點所花費的 hello Azure 備份代理程式、 Azure 備份伺服器和 System Center Data Protection Manager。 

## <a name="gather-data-on-your-vault"></a>在保存庫上收集資料

一旦您升級 tooa 復原服務保存庫、 設定 Azure backup 的報告 （適用於 IaaS Vm 和 Microsoft Azure 復原服務 」 (MARS)），並使用 Power BI tooaccess hello 報表。 如需有關如何收集資料的詳細資訊，請參閱 hello 文章[設定 Azure 備份報告](backup-azure-configure-reports.md)。

## <a name="frequently-asked-questions"></a>常見問題集

**Hello 升級計畫是否會影響我進行中的備份？**</br>
否。 在升級期間和升級之後，進行中的備份持續不受干擾。

**如果我不打算立即升級，會發生什麼事 toomy 保存庫？**</br>
因為所有的新功能適用於僅 tooRecovery 服務保存庫，我們鼓勵您 tooupgrade 您保存庫。 最後，Microsoft 將會取代 hello 傳統入口網站。 從 9 月 1，2017，Microsoft 將會開始自動升級備份保存庫 tooRecovery 服務保存庫。 依年 11 月 1，2017，Microsoft 將會完成 hello 升級程序。 您的保存庫隨時會在 9 月或 10 月間自動升級。 Microsoft 建議您盡快升級您的保存庫。

**對於我現有的工具來說，此升級有何意義？**</br>
更新工具 toohello Resource Manager 部署模型。 復原服務保存庫已建立的使用中 hello Resource Manager 部署模型。 規劃 hello Resource Manager 部署模型，以及帳戶處理您的保存庫中的 hello 差異很重要。 

**Hello 在升級期間，是否有太多的停機時間？**</br>
Hello 正在升級的資源數目而定。 較小的部署 （數十受保護的執行個體），hello 整個升級花費時間不超過 20 分鐘。 對於較大型的部署，應該花費最多一小時的時間。

**升級之後可以復原嗎？**</br>
否。 已成功升級 hello 資源之後，不支援復原。

**如果它們支援的升級可以驗證我的訂用帳戶或資源 toosee 嗎？**</br>
是。 hello 升級第一個步驟中，會驗證 hello 資源可升級。 Hello 驗證的必要元件失敗時，您會收到所有 hello 原因，無法完成 hello 升級的訊息。

**應該有哪些權限 tootrigger 保存庫升級？**</br>
tooperform hello 保存庫升級時，您必須新增為 hello Azure 傳統入口網站中的 hello 訂用帳戶的共同管理員。 這是必要的即使您已列為 hello Azure 入口網站中擁有者。 如果您是 hello 訂用帳戶的共同管理員，嘗試 tooadd 的 Azure 傳統入口網站 toofind 出 hello 訂用帳戶的共同管理員。 如果您不能 tooadd 共同管理員，請連絡服務管理員或共同管理員 hello 訂用帳戶，使用者可以將您加入為共同管理員。

**可以升級以 CSP 為基礎的備份保存庫嗎？**</br>
否。 您目前無法升級以 CSP 為基礎的備份保存庫。 我們將新增對於升級 hello 下一個版本中的 CSP 為基礎的備份保存庫支援。

**在升級後可以檢視我的傳統保存庫嗎？**</br>
否。 您在升級後無法檢視或管理您的傳統保存庫。 您只能在能夠 toouse hello 新版 Azure 入口網站 hello 的保存庫上的所有管理動作。

**我升級失敗，但保留 hello 代理程式需要的 hello 機器更新已不存在。這種情況下我該怎麼做？**</br>
如果您需要 toouse hello 存放區，hello 供長期保存，這部電腦的備份，然後就可以 tooupgrade hello 保存庫。 在日後的版本中，我們會新增這類保存庫的升級支援。
如果您不需要此機器 toostore hello 備份失效，則請取消註冊此 hello 保存庫中的電腦，然後重試 hello 升級。

**為何我看不 hello 作業資訊的我的內部部署資源在升級後**</br>
監視內部部署備份 （MARS 代理程式，DPM 和 Azure 備份伺服器） 是的新功能，當您升級您備份保存庫 tooRecovery 服務保存庫中取得。 監視資訊的 hello 佔用 too12 小時 toosync 與 hello 服務。

**如何回報問題？**</br>
如果 hello 保存庫的任何部分升級會失敗，請注意 hello OperationId 列在 hello 錯誤。 Microsoft 支援服務運作主動 tooresolve hello 問題。 您可以連接 tooSupport 或以電子郵件給我們rsvaultupgrade@service.microsoft.com與您的訂用帳戶 ID、 保存庫名稱 OperationId。 我們會盡快嘗試 tooresolve hello 問題。 除非另有明確指示 toodo，請勿重試 hello 作業是由 Microsoft。


## <a name="next-steps"></a>後續步驟
使用下列文章來 hello:</br>
[備份 IaaS VM](backup-azure-arm-vms-prepare.md)</br>
[備份 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)</br>
[備份 Windows Server](backup-configure-vault.md)。
