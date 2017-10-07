---
title: "Azure AD Connect：從舊版升級 | Microsoft Docs"
description: "說明 hello 不同的方法 tooupgrade toohello 最新版的 Azure Active Directory Connect，包括就地升級和迴旋移轉。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>從先前版本 toohello 最新的 azure AD Connect： 升級
本主題描述 hello 不同，您可以使用 tooupgrade 您 Azure Active Directory (Azure AD) 連線安裝 toohello 最新版本的方法。 我們建議您保留自己目前與 Azure AD connect 的 hello 發行版本。 您也使用 hello hello 步驟[迴旋移轉](#swing-migration)區段進行大量的設定變更時。

如果您想從 DirSync tooupgrade，請參閱[從 Azure AD 同步作業工具 (DirSync) 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md)改為。

有幾個不同的策略，您可以使用 Azure AD Connect tooupgrade。

| 方法 | 說明 |
| --- | --- |
| [自動升級](active-directory-aadconnect-feature-automatic-upgrade.md) |這是 hello 的客戶進行快速安裝最簡單的方法。 |
| [就地升級](#in-place-upgrade) |如果您有一部伺服器，您可以在升級 hello 安裝就地 hello 相同的伺服器。 |
| [變換移轉](#swing-migration) |兩部伺服器，您可以準備 hello hello 新版本或組態中，伺服器的其中一個，並變更 hello 作用中的伺服器，當您準備好。 |

權限資訊，請參閱 hello[升級必要的權限](active-directory-aadconnect-accounts-permissions.md#upgrade)。

> [!NOTE]
> 啟用您新 Azure AD Connect 伺服器 toostart 同步處理變更 tooAzure AD 之後，您必須復原 toousing DirSync 或 Azure AD Sync。從 Azure AD Connect toolegacy 用戶端，包括 DirSync 和 Azure AD Sync，降級不受支援，而且可能會在 Azure AD 中的 tooissues，例如資料遺失。

## <a name="in-place-upgrade"></a>就地升級
就地升級適用於從 Azure AD Sync 或 Azure AD Connect 移轉， 但不適用於從 DirSync 移轉，也不適用於任何利用 Forefront Identity Manager (FIM) + Azure AD 連接器的解決方案。

您只有一台伺服器，且擁有的物件少於 100000 個時，這個方法是最適合您。 如果有任何變更 toohello 現成的同步處理規則，hello 升級之後會發生完整匯入和完整同步處理。 這個方法會確保 hello 新設定將套用的 tooall 現有物件處於 hello 系統。 此回合可能需要幾個小時，而是根據 hello 範圍中的 hello 同步處理引擎的物件數目。 暫止 hello 一般差異同步處理排程器 （可同步處理預設每隔 30 分鐘），但密碼同步處理繼續進行。 您可能會考慮在週末期間 hello 就地升級。 如果有任何變更 toohello 鶈蜪設定的 hello 新的 Azure AD Connect 版本，然後一般差異匯入/同步處理開始改為。  
![就地升級](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

如果您所做的變更 toohello 現成的同步處理規則，然後設定這些規則是回 toohello 預設組態升級時。 toomake 確定您的設定會保留之間升級時，請確定您進行變更，如所述[變更 hello 預設組態的最佳做法](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)。

就地升級時，有可能無法導入需要特定的同步處理活動 （包括完整匯入步驟和完整同步處理步驟） toobe 升級完成之後執行的變更。 toodefer 這類活動，請參閱 toosection [toodefer 完整升級後的同步處理的方式](#how-to-defer-full-synchronization-after-upgrade)。

## <a name="swing-migration"></a>變換移轉
如果您有複雜的部署或多個物件，它可能不太實用 toodo hello 即時系統的就地升級。 就某些客戶而言，此程序可能需花好幾天的時間，而在這段期間並不會處理任何差異變更。 您也可以使用這個方法，當您計劃 toomake 大量變更 tooyour 組態，而且您想 tootry 文之前它們正在推送 toohello 雲端。

建議使用的方法，這些案例的 hello 是 toouse 迴旋移轉。 您需要 (至少) 兩台伺服器，一台是作用中伺服器，而另一台是預備伺服器。 hello （hello 遵循圖片的藍色實線顯示） 的使用中伺服器負責 hello 作用中的生產負載。 hello 開發用伺服器 （虛線紫色顯示） 已準備好 hello 新版本或設定。 準備就緒時，這台伺服器的狀態會變成作用中。 hello 先前作用中伺服器，現在 hello 舊版本或安裝設定，會進行到開發用伺服器 hello 並會升級。

hello 兩部伺服器可以使用不同的版本。 例如，您計劃 toodecommission hello 作用中的伺服器可以使用 Azure AD Sync，和 hello 新臨時伺服器可以使用 Azure AD Connect。 如果您使用迴旋移轉 toodevelop 新的組態，它的建議 toohave hello 相同的版本上 hello 兩部伺服器。  
![預備伺服器](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> 某些客戶比較傾向 toohave 三或四個伺服器，在此案例。 開發用伺服器 hello 升級資料庫時，您不需要的備份伺服器[嚴重損壞修復](active-directory-aadconnectsync-operations.md#disaster-recovery)。 有三或四個伺服器，您就可以準備一組的 hello 新版本，確保永遠位於準備 tootake 臨時伺服器的主要/待命伺服器。

這些步驟也適用 toomove 從 Azure AD 同步或 FIM + Azure AD 連接器具有的解決方案。 這些步驟沒有作用的目錄同步，但卻是相同迴旋移轉方法 （也稱為平行部署） 的步驟進行目錄同步處理的 hello[升級 Azure Active Directory 同步作業 (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md)。

### <a name="use-a-swing-migration-tooupgrade"></a>使用迴旋移轉 tooupgrade
1. 當您使用 Azure AD Connect 的伺服器和計劃 tooonly 進行組態變更，請確定您的作用中的伺服器和臨時伺服器會同時使用 hello 相同版本。 可讓您更輕鬆 toocompare 差異更新版本。 如果您從 Azure AD 同步進行升級，這些伺服器會有不同的版本。 如果您要從較舊版本的 Azure AD Connect 升級，它是個不錯的主意 toostart hello 兩個伺服器與使用 hello 相同的版本，但它不需要。
2. 如果您所做的自訂組態，且您的臨時伺服器沒有它，請遵循下的 hello 步驟[移動自訂設定從臨時伺服器 hello active server toohello](#move-custom-configuration-from-active-to-staging-server)。
3. 如果您要從 Azure AD Connect 先前的版本升級，升級 hello 暫存伺服器 toohello 最新版本。 如果您要從 Azure AD 同步進行移動，請在預備伺服器上安裝 Azure AD Connect。
4. 可讓 hello 同步處理引擎執行完整匯入和完整同步處理您的臨時伺服器上。
5. 確認中的 hello 新設定未使用 [驗證] 下的 hello 步驟而造成未預期的任何變更[確認伺服器的 hello 設定](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server)。 如果項目未如預期，正確，執行 hello 匯入和同步處理，並確認 hello 資料，使其看起來不錯，依照 hello 步驟。
6. 切換 hello 暫存伺服器 toobe hello 作用中的伺服器。 這是最後一個步驟 「 交換器的作用中伺服器 」 hello[確認伺服器的 hello 設定](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server)。
7. 如果您要升級 Azure AD Connect，請在現在預備模式 toohello 最新版本的 hello 伺服器升級。 請遵循相同步驟之前 tooget hello 資料和設定升級的 hello。 如果您是從 Azure AD Sync 進行升級，現在可以關閉舊伺服器並解除任務。

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>移動自訂組態從 hello active server toohello 臨時伺服器
如果您所做的組態變更 toohello 作用中的伺服器，您需要 toomake 確定 hello 相同的變更會套用的 toohello 臨時伺服器。 與這個 toohelp 移動，您可以使用 hello [Azure AD Connect 設定文件產生器](https://github.com/Microsoft/AADConnectConfigDocumenter)。

您可以移動您使用 PowerShell 建立的 hello 自訂同步處理規則。 您必須先套用其他變更 hello 相同的方式上的系統，而且您無法移轉 hello 變更。 hello[組態文件產生器](https://github.com/Microsoft/AADConnectConfigDocumenter)可協助您比較兩個 hello 系統 toomake 確定它們是否完全相同。 hello 工具也可協助自動化 hello 本章節的步驟。

您需要 tooconfigure hello 下列項目 hello 相同兩部伺服器上的方式：

* 連接 toohello 相同的樹系
* 任何網域及 OU 篩選
* hello 相同的選用功能，例如密碼同步及密碼回寫

**移動自訂同步處理規則**  
toomove 自訂同步處理規則，hello 遵循：

1. 開啟作用中伺服器上的 [同步處理規則編輯器]  。
2. 選取自訂規則。 按一下 [匯出]。 此時會出現一個 [記事本] 視窗。 以 PS1 副檔名儲存 hello 暫存檔案。 這會讓該檔案變成 PowerShell 指令碼。 將複製 hello PS1 檔案 toohello 臨時伺服器。  
   ![同步處理規則匯出](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. hello 連接器 GUID 不同 hello 臨時伺服器上，且您必須變更它。 tooget hello GUID，啟動**同步處理規則編輯器**，選取其中一個 hello 鶈蜪規則相同連線系統中，然後按一下該代表 hello**匯出**。 從臨時伺服器 hello hello GUID 取代 hello PS1 檔案中的 GUID。
4. 在 PowerShell 命令提示字元中，執行 hello PS1 檔案。 這會建立暫存伺服器 hello hello 自訂同步處理規則。
5. 針對所有自訂規則重複此步驟。

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Toodefer 完整升級後的同步處理的方式
就地升級時，有可能無法導入需要特定的同步處理活動 （包括完整匯入步驟和完整同步處理步驟） toobe 執行的變更。 連接器結構描述變更的要求，例如**完整匯入**步驟和現成的同步處理規則變更需要**完整同步處理**步驟 toobe 受影響的連接器上執行。 在升級期間，Azure AD Connect 會決定需要何種同步處理活動，並將其記錄為「覆寫」。 在下列同步處理循環的 hello，hello 同步處理排程器會收取這些覆寫，並執行。 覆寫成功執行之後就會移除。

可能有一些情況，您不想這些覆寫 tootake 位置在升級之後立即。 例如，您有多個同步處理的物件，而您想讓這些同步處理步驟 toooccur 在上班時間之後。 這些覆寫 tooremove:

1. 在升級期間，**取消核取**hello 選項**組態完成時啟動 hello 同步處理程序**。 這會停用 hello 同步處理排程器，並防止同步處理循環進行自動移除 hello 覆寫之前。

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. 升級完成之後，執行下列 cmdlet 已加入哪些覆寫出的 toofind hello:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > hello 覆寫是連接器專屬的。 Hello 在下列範例中，完整匯入步驟和完整同步處理步驟已加入 tooboth hello 內部部署 AD 連接器與 Azure AD 連接器。

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. 記下現有的 hello 會覆寫已新增。
   
4. 完整匯入和完整同步處理任意的連接器，執行下列 cmdlet 的 hello 上覆寫 tooremove hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   tooremove hello 覆寫所有的連接器上執行下列 PowerShell 指令碼的 hello:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello 排程器，執行下列 cmdlet 的 hello:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > 請記住您的方便盡早 tooexecute hello 需要同步處理步驟。 您可以手動執行這些步驟使用 hello 同步處理服務管理員，或新增 hello 覆寫回使用 hello 組 ADSyncSchedulerConnectorOverride cmdlet。

完整匯入和完整同步處理任意的連接器，執行下列 cmdlet 的 hello 上覆寫 tooadd hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>後續步驟
深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。
