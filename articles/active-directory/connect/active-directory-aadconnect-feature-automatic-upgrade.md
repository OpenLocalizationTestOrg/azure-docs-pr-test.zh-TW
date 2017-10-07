---
title: "Azure AD Connect：自動升級 | Microsoft Docs"
description: "本主題描述 hello 內建自動升級功能在 Azure AD Connect 同步處理。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect：自動升級
此功能是隨組建 1.1.105.0 (於 2016 年 2 月發行) 一起導入。

## <a name="overview"></a>概觀
確定您 Azure AD Connect 的安裝狀態永遠為 toodate 上從未如此輕鬆以 hello**自動升級**功能。 此功能預設為啟用，以供進行快速安裝及 DirSync 升級。 新版本發行時，您的安裝會自動升級。

Hello 下列預設會啟用自動升級：

* 快速設定安裝和 DirSync 升級。
* 使用 SQL Express LocalDB (這是「快速設定」一律使用的)。 使用 SQL Express 的 DirSync 也會使用 LocalDB。
* hello AD 帳戶是快速設定與 DirSync 所建立的 hello 預設 MSOL_ 帳戶。
* Hello metaverse 中有 100,000 個物件。

使用 「 hello PowerShell cmdlet，可以檢視 hello 的目前狀態的自動升級`Get-ADSyncAutoUpgrade`。 它有下列狀態的 hello:

| State | 註解 |
| --- | --- |
| 已啟用 |已啟用自動升級。 |
| 暫止 |只有 hello 系統設定。 hello 系統已不再符合資格 tooreceive 自動升級。 |
| 已停用 |已停用自動升級。 |

您可以使用 `Set-ADSyncAutoUpgrade` 在 [已啟用] 與 [已停用] 之間進行變更。 只有 hello 系統應該設定 hello 狀態**Suspended**。

自動升級為使用 Azure AD Connect Health hello 升級基礎結構。 自動升級 toowork，請確定您已開啟您的 proxy 伺服器的 hello Url **Azure AD Connect Health**如中所述[Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

如果 hello**同步處理服務管理員**hello 伺服器上執行 UI 然後 hello 升級會暫停，直到 hello UI 已關閉。

## <a name="troubleshooting"></a>疑難排解
如果您連接的安裝不會升級本身如預期般，請依照下列出功能可能是錯誤，這些步驟 toofind。

首先，您不應預期 hello 嘗試自動升級 toobe hello 發行新版本的第一天。 由於升級前有刻意設計的隨機性，因此不用擔心您的安裝沒有立即升級。

如果您認為有不正確，然後第一次執行`Get-ADSyncAutoUpgrade`tooensure 自動升級已啟用。

然後，請確定您在 proxy 或防火牆中開啟 hello 所需的 Url。 自動更新為使用 Azure AD Connect Health，如下所示 hello[概觀](#overview)。 如果您使用的 proxy，請確定健全狀況已設定的 toouse [proxy 伺服器](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)。 也測試 hello[健康情況連線](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)tooAzure AD。

Hello 連線 tooAzure AD 驗證，因此很時間 toolook 到 hello 事件記錄檔。 啟動 hello 事件檢視器，並查看 hello**應用程式**事件記錄檔。 新增事件記錄檔篩選器 hello 來源**連線升級 Azure AD**和 hello 事件識別碼範圍**300 399**。  
![自動升級的事件記錄篩選](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

您現在可以看到 hello 與自動升級的 hello 狀態相關聯的事件記錄檔。  
![自動升級的事件記錄篩選](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

hello 結果程式碼具有的前置詞 hello 狀態的概觀。

| 結果碼前置詞 | 說明 |
| --- | --- |
| 成功 |hello 安裝已順利升級。 |
| UpgradeAborted |暫時的狀況停止 hello 升級。 它將會重試一次，hello 預期是稍後成功。 |
| UpgradeNotSupported |hello 系統已封鎖 hello 系統會自動升級的組態。 它會重試的 toosee hello 狀態已變更，但 hello 預期是 hello 系統都必須以手動方式升級。 |

以下是一份 hello 您找到最常見的訊息。 不會列出所有項目，但 hello 結果訊息應該清除與 hello 問題。

| 結果訊息 | 說明 |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |無法寫入 toohello 登錄。 |
| UpgradeAbortedInsufficientDatabasePermissions |hello 內建的系統管理員群組沒有權限 toohello 資料庫。 手動升級 toohello 最新版本的 Azure AD Connect tooaddress 此問題。 |
| UpgradeAbortedInsufficientDiskSpace |沒有足夠的光碟空間 toosupport 升級。 |
| UpgradeAbortedSecurityGroupsNotPresent |無法尋找和解決 hello 同步處理引擎所使用的所有安全性群組。 |
| UpgradeAbortedServiceCanNotBeStarted |hello NT 服務**Microsoft Azure AD Sync**失敗 toostart。 |
| UpgradeAbortedServiceCanNotBeStopped |hello NT 服務**Microsoft Azure AD Sync**失敗 toostop。 |
| UpgradeAbortedServiceIsNotRunning |hello NT 服務**Microsoft Azure AD Sync**並未執行。 |
| UpgradeAbortedSyncCycleDisabled |hello SyncCycle 選項在 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)已停用。 |
| UpgradeAbortedSyncExeInUse |hello[同步處理服務管理員 UI](active-directory-aadconnectsync-service-manager-ui.md) hello 伺服器上開啟。 |
| UpgradeAbortedSyncOrConfigurationInProgress |hello 安裝精靈正在執行，或在同步處理已排程之外 hello 排程器。 |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |您已加入您自己的自訂規則 toohello 組態。 |
| UpgradeNotSupportedDeviceWritebackEnabled |您已啟用 hello[裝置回寫](active-directory-aadconnect-feature-device-writeback.md)功能。 |
| UpgradeNotSupportedGroupWritebackEnabled |您已啟用 hello[群組回寫](active-directory-aadconnect-feature-preview.md#group-writeback)功能。 |
| UpgradeNotSupportedInvalidPersistedState |hello 安裝不是 Express 設定或 DirSync 升級。 |
| UpgradeNotSupportedMetaverseSizeExceeeded |您 hello metaverse 中有 100,000 個以上的物件。 |
| UpgradeNotSupportedMultiForestSetup |您要連接 toomore 比一個樹系。 快速安裝只連接 tooone 樹系。 |
| UpgradeNotSupportedNonLocalDbInstall |您不是使用 SQL Server Express LocalDB 資料庫。 |
| UpgradeNotSupportedNonMsolAccount |hello [AD 連接器帳戶](active-directory-aadconnect-accounts-permissions.md#active-directory-account)已 hello 預設 MSOL_ 帳戶不再。 |
| UpgradeNotSupportedStagingModeEnabled |hello 伺服器中設定 toobe[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。 |
| UpgradeNotSupportedUserWritebackEnabled |您已啟用 hello[使用者回寫](active-directory-aadconnect-feature-preview.md#user-writeback)功能。 |

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
