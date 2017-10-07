---
title: "在 Azure AD 同步處理服務管理員 UI hello aaaConnectors |Microsoft 文件 '"
description: "了解 Azure AD Connect 同步處理服務管理員 hello 的 hello 連接器 索引標籤。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>使用連接器與 hello Azure AD Connect 同步處理服務管理員

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

hello 連接器 索引標籤是所有系統 hello 同步作業引擎已都連線到使用的 toomanage。

## <a name="connector-actions"></a>連接器動作
| 動作 | 註解 |
| --- | --- |
| 建立 |請勿使用。 連線 tooadditional AD 樹系，請使用 hello 安裝精靈。 |
| 屬性 |用於網域和 OU 篩選。 |
| [刪除](#delete) |使用的 tooeither 刪除 hello hello 連接器空間或 toodelete 連接 tooa 樹系中的資料。 |
| [更新執行設定檔](#configure-run-profiles) |除了網域篩選，執行任何動作 tooconfigure 這裡。 您可以使用此動作 toosee 已經設定執行設定檔。 |
| 執行 |使用的 toostart 單次執行的設定檔。 |
| 停止 |停止目前執行設定檔的連接器。 |
| 匯出連接器 |請勿使用。 |
| 匯入連接器 |請勿使用。 |
| 更新連接器 |請勿使用。 |
| 重新整理結構描述 |重新整理 hello 快取結構描述。 這是慣用的 toouse hello 選項 hello 安裝精靈 中之後，也更新同步處理規則。 |
| [搜尋連接器空間](#search-connector-space) |使用 toofind 物件和太[遵循物件和其資料透過 hello 系統](#follow-an-object-and-its-data-through-the-system)。 |

### <a name="delete"></a>刪除
hello delete 動作用於兩個不同的項目。  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

hello 選項**刪除連接器空間只**移除所有的資料，但保留 hello 組態。

hello 選項**刪除連接器與連接器空間**hello 資料與 hello 組態中移除。 當您不想 tooconnect tooa 樹系不再使用此選項。

這兩個選項會同步處理所有物件，與更新 hello metaverse 物件。 此動作是長時間執行的作業。

### <a name="configure-run-profiles"></a>更新執行設定檔
此選項可讓您執行設定檔設定連接器 toosee hello。

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>搜尋連接器空間
hello 搜尋連接器空間動作是很有用的 toofind 物件和疑難排解資料問題。

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

先選取一個 [範圍] 。 您可以搜尋依據的資料 （RDN，DN，錨點，子樹狀目錄），或 hello 物件 （所有其他選項） 的狀態。  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
例如，如果您進行樹狀子目錄的搜尋，將會取得某一個 OU 中的所有物件。  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
此方格中，您可以選取物件、 選取**屬性**，和[其後](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)從透過 hello metaverse，hello 來源連接器空間和 toohello 目標連接器空間。

### <a name="changing-hello-ad-ds-account-password"></a>變更 hello AD DS 帳戶的密碼
如果您變更 hello 帳戶密碼，hello 同步處理服務將不再能夠 tooimport/匯出變更 tooon 內部部署 AD。   您可能會看到下列 hello:

- hello hello AD 連接器匯入/匯出步驟失敗，發生 「 否-start-認證 」 錯誤。
- 在 Windows 事件檢視器，hello 應用程式事件記錄檔包含具有事件識別碼 6000 和訊息的錯誤"hello 管理代理程式"contoso.com"無法 toorun 因為 hello 認證無效。"

tooresolve hello 發出使用 hello 下列更新 hello AD DS 使用者帳戶：


1. 啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. 移 toohello**連接器** 索引標籤。
3. 選取 hello 設定的 toouse hello AD DS 帳戶 AD 連接器。
4. 選取 [動作] 下方的 [屬性]。
5. 在 hello 快顯對話方塊中，選取連接 tooActive Directory 樹系：
6. hello 樹系名稱表示 hello 對應由內部部署 AD。
7. hello 使用者名稱表示 hello AD DS 帳戶用於進行同步處理。
8. 在 hello 密碼 文字方塊中輸入 hello hello AD DS 帳戶新密碼![Azure AD 連線同步加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. 按一下 [確定] toosave hello 新密碼，然後重新啟動 hello 同步處理服務 tooremove hello 舊密碼從記憶體快取。



## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
