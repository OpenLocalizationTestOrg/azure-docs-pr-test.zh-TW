---
title: "Azure AD Connect︰從 DirSync 升級 | Microsoft Docs"
description: "深入了解如何從 DirSync tooAzure AD tooupgrade 連接。 此文章描述 hello 步驟從 DirSync tooAzure 升級 AD Connect。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect︰從 DirSync 升級
Azure AD Connect 是 hello 後續 tooDirSync。 您找出您可以升級從 DirSync，本主題中的 hello 方式。 這些步驟不適用於從另一個版本的 Azure AD Connect 或從 Azure AD Sync 升級。

您開始安裝 Azure AD Connect，請確定太[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)和中的步驟完成 hello 必要條件[Azure AD Connect： 硬體和必要條件](active-directory-aadconnect-prerequisites.md)。 特別的是，您想 tooread 有關 hello 下列項目，因為這些區域是從 DirSync 不同：

* hello 的.Net 和 PowerShell 的必要的版本。 較新版本時需要的 toobe hello 比 DirSync 所需的伺服器上。
* hello proxy 伺服器設定。 如果您使用 proxy 伺服器 tooreach hello 網際網路，則必須設定此設定，然後再升級。 DirSync，一律使用 hello proxy 伺服器設定為 hello 使用者安裝，但 Azure AD Connect 使用電腦的設定改為。
* hello Url 需要的 toobe 開啟 hello proxy 伺服器。 基本案例中，目錄同步，也支援這些案例 hello 需求是 hello 相同的。 如果您想要 toouse 任何 hello Azure AD Connect 所隨附的新功能，就必須開啟某些新的 Url。

> [!NOTE]
> 一旦您啟用了您新 Azure AD Connect 伺服器 toostart 同步處理變更 tooAzure AD，您必須復原 toousing DirSync 或 Azure AD Sync。從 Azure AD Connect toolegacy 用戶端，包括 DirSync 和 Azure AD Sync 降級不支援，而且可能會在 Azure AD 中的 tooissues，例如資料遺失。

如果您不是要從 DirSync 升級，請參閱 [相關文件](#related-documentation) 中的其他案例。

## <a name="upgrade-from-dirsync"></a>從 DirSync 升級
根據您目前的目錄同步部署，有不同的 hello 升級選項。 如果 hello 預期升級時是不超過 3 個小時，然後 hello 建議 toodo 就地升級。 如果 hello 預期升級的時間會超過三個小時，然後 hello 建議 toodo 平行部署在另一部伺服器上。 預估，如果您有超過 50,000 個物件需要花費超過三個小時 toodo hello 升級。

| 案例 |
| --- | --- |
| [就地升級](#in-place-upgrade) |
| [平行部署](#parallel-deployment) |

> [!NOTE]
> 當您計劃 tooupgrade DirSync tooAzure AD 從連接中，不會解除安裝 DirSync 自行 hello 升級前。 Azure AD Connect 會讀取和從 DirSync 移轉 hello 組態，以及在檢查 hello 伺服器之後解除安裝。

**就地升級**  
hello 預期時間 toocomplete hello 升級由 hello 精靈顯示。 此預估值根據 hello 假設，需要花費三小時 toocomplete 具有 50,000 個物件 （使用者、 連絡人和群組） 的資料庫升級。 如果您的資料庫中物件的 hello 數目少於 50,000 個，Azure AD Connect 建議就地升級。 如果您決定 toocontinue，在升級期間，會自動套用您目前的設定，您的伺服器會自動繼續進行作用中的同步處理。

如果您想 toodo 設定移轉，且執行平行部署，然後您可以覆寫 hello 就地升級的建議。 您可能例如 hello 機會 toorefresh hello 硬體和作業系統。 如需詳細資訊，請參閱 hello[平行部署](#parallel-deployment)> 一節。

**平行部署**  
如果您有超過 5 萬個物件，則建議使用平行部署。 此部署可避免您的使用者經歷任何作業延遲。 hello Azure AD Connect 的安裝嘗試 hello 升級 tooestimate hello 停機時間，但如果您已在過去的 hello 升級目錄同步，您自己的經驗會可能 toobe hello 最佳指南。

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>支援的 DirSync 組態 toobe 升級
升級目錄同步支援 hello 下列組態變更：

* 網域和 OU 篩選
* 替代 ID (UPN)
* 密碼同步和 Exchange 混合式設定
* 您的樹系/網域與 Azure AD 設定
* 根據使用者屬性進行篩選

無法升級 hello 變更之後。 如果您有此設定，將會封鎖 hello 升級：

* 不支援的 DirSync 變更，例如移除屬性和使用自訂延伸模組 DLL

![已封鎖升級](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

在這些情況下，hello 建議 tooinstall 中新的 Azure AD Connect 伺服器[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)並確認 hello 舊 DirSync 和新的 Azure AD Connect 組態。 使用自訂組態重新套用任何變更，如 [Azure AD Connect 同步處理自訂組態](active-directory-aadconnectsync-whatis.md)中所述。

無法擷取 hello 以 DirSync 用於 hello 服務帳戶的密碼，並不會移轉。 Hello 升級期間重設這些密碼。

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>從 DirSync tooAzure 升級 AD Connect 的概要步驟
1. 歡迎使用 tooAzure AD Connect
2. 目前 DirSync 組態的分析
3. 收集 Azure AD 全域管理員密碼
4. （僅限用於 Azure AD connect 的 hello 安裝期間），請收集企業系統管理員帳戶的認證
5. Azure AD Connect 安裝
   * 解除安裝 DirSync (或暫時停用)
   * 安裝 Azure AD Connect。
   * 選擇性地開始同步處理

發生下列情況時，需要其他步驟：

* 您目前正在使用完整 SQL Server - 本機或遠端
* 您擁有超過 5 萬個物件的規模可進行同步處理

## <a name="in-place-upgrade"></a>就地升級
1. 啟動 hello Azure AD Connect installer (MSI)。
2. 請先詳閱並同意 toolicense 條款及隱私權注意事項。  
   ![歡迎使用 tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. 按一下 下一步 toobegin 分析您現有的 DirSync 安裝。  
   ![分析現有目錄同步作業安裝](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Hello 分析完成時，您會看到 hello 建議如何 tooproceed。  
   * 如果您使用 SQL Server Express，並具有少於 50,000 個物件，會顯示下列畫面的 hello:  
     ![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * 如果您使用完整的 SQL Server for DirSync 功能，您會看到這個頁面：  
     ![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     會顯示 hello hello 現有 SQL Server 資料庫伺服器正在使用目錄同步相關的資訊。 如果需要，請進行適當的調整。 按一下**下一步**toocontinue hello 安裝。
   * 如果您有超過 5 萬個物件，您會看到這個畫面：  
     ![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed 進行就地升級時，按一下 [hello] 核取方塊下一步 toothis 訊息：**繼續在此電腦上升級目錄同步。**
     toodo[平行部署](#parallel-deployment)請匯出 hello DirSync 組態設定，並且移動 hello 組態 toohello 新伺服器。
5. 提供您目前使用 tooconnect tooAzure AD hello 帳戶 hello 密碼。 這必須是目前使用的目錄同步的 hello 帳戶。  
   ![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   如果您收到錯誤訊息，而且有連線問題，請參閱 [針對連線問題進行疑難排解](active-directory-aadconnect-troubleshoot-connectivity.md)。
6. 提供 Active Directory 的企業系統管理員帳戶。  
   ![輸入您的 ADDS 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. 您現在準備好 tooconfigure。 當您按一下 [升級] 時，系統會解除安裝 DirSync，而 Azure AD Connect 會完成設定並開始同步處理。  
   ![準備好 tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Hello 安裝完成後，登出再登入一次 tooWindows 才能使用 [同步處理服務管理員，同步處理規則編輯器] 中，或嘗試 toomake 任何其他組態變更。

## <a name="parallel-deployment"></a>平行部署
### <a name="export-hello-dirsync-configuration"></a>匯出 hello DirSync 組態
**平行部署超過 5 萬個物件**

如果您有超過 50,000 個物件，則 hello Azure AD Connect 的安裝將會建議平行部署。

類似 toohello 後的螢幕會顯示：  
![分析完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

如果您想 tooproceed 平行部署，您需要下列步驟 tooperform hello:

* 按一下 hello**匯出設定** 按鈕。 當您安裝 Azure AD Connect 的伺服器上時，從目前目錄同步 tooyour 新 Azure AD Connect 的安裝移轉這些設定。

一旦成功匯出您的設定，您可以結束 hello hello DirSync 伺服器上的 Azure AD Connect 精靈。 太繼續進行下一個步驟的 hello[不同的伺服器上安裝 Azure AD Connect](#installation-of-azure-ad-connect-on-separate-server)

**平行部署少於 5 萬個物件**

如果您具有少於 50,000 個物件，但仍想 toodo 平行部署，然後 hello 遵循：

1. 執行 hello Azure AD Connect installer (MSI)。
2. 當您看到 hello ** 褖畫惎 tooAzure AD Connect**畫面上，按一下 hello 最上層視窗的右下角 hello hello"X"結束 hello 安裝精靈。
3. 開啟命令提示字元。
4. 從 hello 安裝 Azure AD Connect 的位置 (預設： C:\Program Files\Microsoft Azure Active Directory Connect) 執行下列命令的 hello: `AzureADConnect.exe /ForceExport`。
5. 按一下 hello**匯出設定** 按鈕。 當您安裝 Azure AD Connect 的伺服器上時，從目前目錄同步 tooyour 新 Azure AD Connect 的安裝移轉這些設定。

![分析完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

一旦成功匯出您的設定，您可以結束 hello hello DirSync 伺服器上的 Azure AD Connect 精靈。 太繼續進行下一個步驟的 hello[不同的伺服器上安裝 Azure AD Connect](#installation-of-azure-ad-connect-on-separate-server)。

### <a name="install-azure-ad-connect-on-separate-server"></a>在不同的伺服器上安裝 Azure AD Connect
當您在新伺服器上安裝 Azure AD Connect 時，hello 假設會是您想 tooperform Azure AD Connect 的全新安裝。 由於您希望 toouse hello DirSync 組態，有一些額外的步驟 tootake:

1. 執行 hello Azure AD Connect installer (MSI)。
2. 當您看到 hello ** 褖畫惎 tooAzure AD Connect**畫面上，按一下 hello 最上層視窗的右下角 hello hello"X"結束 hello 安裝精靈。
3. 開啟命令提示字元。
4. 從 hello 安裝 Azure AD Connect 的位置 (預設： C:\Program Files\Microsoft Azure Active Directory Connect) 執行下列命令的 hello: `AzureADConnect.exe /migrate`。
   hello Azure AD Connect 的安裝精靈會啟動，並會顯示下列畫面 hello:  
   ![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. 選取從您的 DirSync 安裝所匯出的 hello 設定檔。
6. 設定任何進階選項，包括：
   * Azure AD Connect 的自訂安裝位置。
   * 現有 SQL Server 執行個體 (預設值：Azure AD Connect 會安裝 SQL Server 2012 Express)。 請勿使用 hello 與 DirSync 伺服器相同的資料庫執行個體。
   * （如果您的 SQL Server 資料庫位於遠端，則此帳戶必須是網域的服務帳戶） tooconnect tooSQL 伺服器使用的服務帳戶。
     您可以在這個畫面上看到下列選項：  
     ![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. 按一下 [下一步] 。
8. 在 hello**準備 tooconfigure**頁面上，保留 hello **hello 組態完成之後儘速開始 hello 同步處理程序**檢查。 hello 伺服器現在為[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)讓變更不會匯出的 tooAzure AD。
9. 按一下 [Install] 。
10. Hello 安裝完成後，登出再登入一次 tooWindows 才能使用 [同步處理服務管理員，同步處理規則編輯器] 中，或嘗試 toomake 任何其他組態變更。

> [!NOTE]
> Windows Server Active Directory 與 Azure Active Directory 之間的同步處理開始，但不不匯出的 tooAzure AD 的任何變更。 一次只能有一個作用中的同步處理工具匯出變更。 此狀態稱為[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>驗證 Azure AD Connect 準備好 toobegin 同步處理
Azure AD Connect 是透過從目錄同步的準備 tootake 的 tooverify，您需要 tooopen**同步處理服務管理員**hello 群組中**Azure AD Connect**從 hello [開始] 功能表。

在 [hello 應用程式中，移 toohello**作業**] 索引標籤。此索引標籤上，確認已完成下列作業的 hello:

* 在 hello AD 連接器匯入
* 在 hello Azure AD 連接器匯入
* Hello AD 連接器上的完整同步處理
* 完整同步處理在 hello Azure AD Connector

![匯入和同步處理完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

檢閱 hello 從這些作業的結果，並確定沒有任何錯誤。

如果您想 toosee 並檢查所需 toobe 匯出 tooAzure AD hello 變更，然後讀取方式 tooverify hello 底下設定[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。 進行必要的組態變更，直到看不到非預期的任何項目。

您已準備好 tooswitch 從 DirSync tooAzure AD，當您完成這些步驟並滿意 hello 結果。

### <a name="uninstall-dirsync-old-server"></a>解除安裝 DirSync (舊伺服器)
* 在 [程式和功能] 中，尋找 [Windows Azure Active Directory 同步作業工具]
* 解除安裝 [Windows Azure Active Directory 同步作業工具] 
* hello 解除安裝可能會佔用 too15 分鐘 toocomplete。

如果您偏好 toouninstall 目錄同步之後，您就可以也會暫時關閉 hello 伺服器，或停用 hello 服務。 如果發生錯誤，這個方法可讓您 toore 啟用它。 不過，不應該該 hello 下一個步驟將會失敗，因此這應該不需要。

解除安裝或停用目錄同步，匯出 tooAzure AD 沒有作用中伺服器。 您在內部部署 Active Directory 中的任何變更將會繼續執行同步處理的 toobe tooAzure AD，則必須完成下一個步驟 tooenable hello Azure AD Connect。

### <a name="enable-azure-ad-connect-new-server"></a>啟用 Azure AD Connect (新伺服器)
安裝完成後，重新開啟 Azure AD 連接將會讓您 toomake 其他組態變更。 啟動**Azure AD Connect**從 hello [開始] 功能表或從 hello hello 桌面上的捷徑。 請確定您不會嘗試 toorun hello 安裝 MSI 一次。

您應該會看到下列 hello:  
![其他工作](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* 選取 [設定預備模式] 。
* 關閉正在取消 hello 臨時**啟用預備模式**核取方塊。

![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* 按一下 hello**下一步**按鈕
* 在 hello 確認頁面上，按一下 [hello**安裝**] 按鈕。

Azure AD Connect 現在是作用中的伺服器，您必須切換後 toousing 現有的 DirSync 伺服器。

## <a name="next-steps"></a>後續步驟
既然您已安裝的 Azure AD Connect 可以[確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)。

深入了解這些新功能，與 hello 安裝已啟用：[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)，[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)，和[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。

深入了解這些常見的主題：[排程器和 tootrigger 的同步處理](active-directory-aadconnectsync-feature-scheduler.md)。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
