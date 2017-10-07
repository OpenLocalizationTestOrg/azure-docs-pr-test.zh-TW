---
title: "Azure AD Connect 同步：排程器 | Microsoft Docs"
description: "本主題描述 Azure AD Connect 同步處理中的 hello 內建的排程器功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Azure AD Connect 同步處理：排程器
本主題描述 Azure AD Connect 同步處理中的 hello 內建排程器 （也稱為 同步處理引擎) 中內建的排程器。

此功能是隨組建 1.1.105.0 (於 2016 年 2 月發行) 一起導入。

## <a name="overview"></a>概觀
Azure AD Connect 同步處理會使用排程器來同步處理您內部部署目錄中發生的變更。 有兩個排程器程序，一個用於密碼同步處理，另一個用於物件/屬性同步處理以及維護工作。 本主題涵蓋 hello 後者。

Hello 排程器的物件和屬性的外部 toohello 同步處理引擎在較早的版本。 它使用 Windows 工作排程器或另一個 Windows 服務 tootrigger hello 同步處理程序。 hello 排程器是與 hello 1.1 版本內建 toohello 同步處理引擎，允許某項自訂作業。 hello 新預設同步處理頻率為 30 分鐘。

hello 排程器會負責這兩個工作項目：

* **同步處理循環**。 hello 程序 tooimport，同步處理及匯出變更。
* **維護工作**。 為密碼重設和「裝置註冊服務」(DRS) 更新金鑰和憑證。 清除 hello 作業記錄檔中的舊項目。

hello 排程器本身一直執行，但可以設定的 tooonly 執行一個或無這些工作。 例如，如果您需要 toohave 您自己的同步處理循環程序，您可以停用此 hello 排程器中的工作，但仍執行的 hello 維護工作。

## <a name="scheduler-configuration"></a>排程器組態
toosee 移 tooPowerShell 目前的組態設定，並執行`Get-ADSyncScheduler`。 它會向您顯示類似以下圖片︰

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

如果您看到**hello 同步命令或指令程式不提供**當您執行這個指令程式，然後 hello PowerShell 模組未載入。 如果您在網域控制站上，或具有較高的 PowerShell 限制層級比 hello 的預設設定的伺服器上執行 Azure AD Connect，可能會發生這個問題。 如果您看到此錯誤，然後執行`Import-Module ADSync`toomake hello cmdlet 可用。

* **AllowedSyncCycleInterval**。 hello 最短時間間隔允許由 Azure AD 的同步處理循環之間。 同步處理頻率一旦超過此設定，即不受支援。
* **CurrentlyEffectiveSyncCycleInterval**。 hello 排程目前作用中。 它有相同的值做 CustomizedSyncInterval hello (如果設定) 如果不是比 AllowedSyncInterval 更頻繁。 如果您使用 1.1.281 之前的組件且變更 CustomizedSyncCycleInterval，將會在下一個同步處理循環後才生效。 從組建 1.1.281 hello 變更會立即生效。
* **CustomizedSyncCycleInterval**。 如果您想在任何其他頻率與 hello 預設 hello 排程器 toorun 30 分鐘內，您會設定此設定。 在上述的 hello 圖片，hello 排程器已設定 toorun 每小時改為。 如果您設定此設定 tooa 值低於 AllowedSyncInterval，則會使用第二個 hello。
* **NextSyncCyclePolicyType**。 Delta (差異) 或 Initial (初始)。 定義是否 hello 接下來執行應該只能處理差異變更，或如果 hello 下次執行應執行完整匯入和同步處理。hello 後者也會重新處理任何新的或變更的規則。
* **NextSyncCycleStartTimeInUTC**。 下一次 hello 排程器會開始 hello 下一個同步處理循環。
* **PurgeRunHistoryInterval**。 hello 應該保留記錄檔的階段作業。 可以在 hello 同步處理服務管理員中檢閱這些記錄檔。 hello 預設值是 7 天 tookeep 這些記錄檔。
* **SyncCycleEnabled**。 指出是否 hello 排程器執行 hello 匯入、 同步處理以及匯出處理程序做為其作業的一部分。
* **MaintenanceEnabled**。 顯示 hello 維護程序是否已啟用。 它會更新 hello 憑證/索引鍵，並清除 hello 作業記錄。
* **StagingModeEnabled**。 顯示是否已啟用 [預備模式](active-directory-aadconnectsync-operations.md#staging-mode) 。 如果已啟用此設定，然後它會隱藏 hello 匯出的執行，但仍執行 匯入和同步處理。
* **SchedulerSuspended**。 設定連線期間升級 tootemporarily 區塊 hello 排程器無法執行。

您可以使用 `Set-ADSyncScheduler`變更這些設定的其中一部分。 您可以修改 hello 下列參數：

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

在先前的 Azure AD Connect 組建中，**isStagingModeEnabled** 已在 Set-ADSyncScheduler 中公開。 它是**不支援**tooset 這個屬性。 hello 屬性**SchedulerSuspended**應該只能由連接進行修改。 它是**不支援**tooset 這 PowerShell 直接使用。

hello 排程器設定儲存在 Azure AD 中。 如果您有在臨時伺服器，則 hello 主要伺服器上的任何變更也會影響 hello 開發用伺服器 （除了 IsStagingModeEnabled)。

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
語法： `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - 天、HH - 小時、mm - 分鐘、ss - 秒

範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
變更 hello 排程器 toorun 每 3 個小時。

範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
變更每日變更 hello 排程器 toorun。

### <a name="disable-hello-scheduler"></a>停用 hello 排程器  
如果您需要 toomake 組態變更，您會想 toodisable hello 排程器。 例如，當您[設定篩選](active-directory-aadconnectsync-configure-filtering.md)或[變更 toosynchronization 規則](active-directory-aadconnectsync-change-the-configuration.md)。

toodisable hello 排程器執行`Set-ADSyncScheduler -SyncCycleEnabled $false`。

![停用 hello 排程器](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

當您完成變更之後，不要忘記再次 tooenable hello 排程器`Set-ADSyncScheduler -SyncCycleEnabled $true`。

## <a name="start-hello-scheduler"></a>啟動 hello 排程器
預設每隔 30 分鐘執行一次為 hello 排程器。 在某些情況下，您可能想的 toorun hello 之間的同步處理循環排程的循環，或者您需要 toorun 不同的型別。

**差異同步處理循環**  
差異同步處理循環包含下列步驟的 hello:

* 在所有的連接器上執行差異匯入
* 在所有的連接器上執行差異同步處理
* 在所有的連接器上執行匯出

這可能是您有緊急變更必須立即同步處理就是為什麼您需要 toomanually 執行循環。 如果您需要 toomanually 執行循環，然後從 PowerShell 執行`Start-ADSyncSyncCycle -PolicyType Delta`。

**完整同步處理循環**  
如果您做了其中一個 hello 下列組態變更，您 （也稱為需要完整同步處理週期 toorun Initial (初始))：

* 加入多個物件或屬性 toobe 匯入從來源目錄
* 變更 toohello 同步處理規則
* 變更 [篩選](active-directory-aadconnectsync-configure-filtering.md) 以納入不同數目的物件

如果您做了其中一個這些變更，您需要的 toorun 完整同步處理循環，所以 hello 同步處理引擎沒有 hello 機會 tooreconsolidate hello 連接器空間。 完整同步處理循環包含下列步驟的 hello:

* 在所有的連接器上執行完整匯入
* 在所有的連接器上執行完整同步處理
* 在所有的連接器上執行匯出

執行完整同步處理週期 tooinitiate`Start-ADSyncSyncCycle -PolicyType Initial`從 PowerShell 提示中。 此命令會啟動完整同步處理循環。

## <a name="stop-hello-scheduler"></a>停止 hello 排程器
如果 hello 排程器目前正在執行同步處理循環，您可能需要 toostop 它。 例如，如果您啟動 hello 安裝精靈，您會收到這個錯誤：

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

當同步處理循環正在執行時，您會無法進行組態變更。 您無法等到 hello 排程器已完成 hello 程序，但也可以停止它，因此您可以立即進行變更。 停止目前的循環 hello 不有害，暫止的變更會和處理接下來執行。

1. 藉由告訴 hello 排程器 toostop 其目前的開始與 hello PowerShell cmdlet 的循環`Stop-ADSyncSyncCycle`。
2. 如果您使用的組建之前 1.1.281，則停止 hello 排程器不會停止目前的 hello 連接器從其目前的工作。 tooforce hello 連接器 toostop，採取下列動作的 hello: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * 啟動**同步處理服務**從 hello [開始] 功能表。 跳過**連接器**，反白顯示 hello 連接器與 hello 狀態**執行**，然後選取**停止**從 hello 動作。

hello 排程器仍在作用中，並在下次有機會再次啟動。

## <a name="custom-scheduler"></a>自訂排程器
hello 本節中所述的 cmdlet 中才有建置[1.1.130.0](active-directory-aadconnect-version-history.md#111300)和更新版本。

如果 hello 內建的排程器無法滿足您的需求，您可以排程 hello 連接器使用 PowerShell。

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
您可使用下列方式，啟動連接器的設定檔：

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

如 hello 名稱 toouse[連接子名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md)和[執行設定檔名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles)位於 hello[同步處理服務管理員 UI](active-directory-aadconnectsync-service-manager-ui.md)。

![叫用執行設定檔](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

hello `Invoke-ADSyncRunProfile` cmdlet 是同步，亦即它不會傳回控制項 hello 連接器完成之前完成 hello 作業成功或錯誤。

當您排程的連接器時，hello 建議 tooschedule hello 順序中：

1. (完整/差異) 從內部部署目錄匯入，例如 Active Directory
2. (完整/差異) 從 Azure AD 匯入
3. (完整/差異) 從內部部署目錄同步處理，例如 Active Directory
4. (完整/差異) 從 Azure AD 同步處理
5. 匯出 tooAzure AD
6. 匯出 tooon 內部部署目錄，例如 Active Directory

這個順序是 hello 內建的排程器執行 hello 連接器的方式。

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
您也可以監視 hello 同步處理引擎 toosee，如果它是忙碌或閒置。 如果 hello 同步處理引擎會處於閒置狀態，但卻未執行連接器，此 cmdlet 會傳回空的結果。 如果執行連接器，它會傳回 hello hello 連接器名稱。

```
Get-ADSyncConnectorRunStatus
```

![連接器執行狀態](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
在上面的 hello 圖片，hello 第一行是從閒置 hello 同步處理引擎的狀態。 hello 從 hello Azure AD Connector 正在執行時的第二行。

## <a name="scheduler-and-installation-wizard"></a>排程器和安裝精靈
如果您啟動 hello 安裝精靈，然後 hello 排程器已暫時暫止。 這是因為它會假設您進行組態變更，但不可套用這些設定，如果 hello 同步處理引擎正在執行。 基於這個理由，不會讓 hello 安裝精靈開啟因為它會停止 hello 同步處理引擎從執行任何同步處理動作。

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
