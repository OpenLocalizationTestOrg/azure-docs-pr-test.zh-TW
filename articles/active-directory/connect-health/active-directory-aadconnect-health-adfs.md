---
title: "使用 AD FS 的 Azure AD Connect Health aaaUsing |Microsoft 文件"
description: "這是如何 hello Azure AD Connect Health 頁面 toomonitor 您內部部署 AD FS 基礎結構。"
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>使用 Azure AD Connect Health 監視 AD FS
下列文件 hello 是特定 toomonitoring AD FS 基礎結構與 Azure AD Connect Health。 如需使用 Azure AD Connect Health 來監視 Azure AD Connect (同步處理) 的詳細資訊，請參閱 [使用適用於同步處理的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。此外，如需使用 Azure AD Connect Health 來監視 Active Directory 網域服務的詳細資訊，請參閱 [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。

## <a name="alerts-for-ad-fs"></a>AD FS 的警示
hello Azure AD Connect Health 警示 > 一節提供 hello 的作用中警示清單。 每個警示都包含相關資訊、 解決步驟和連結 toorelated 文件。

您可以按兩下作用中或已解決警示，tooopen 的其他資訊的新刀鋒視窗，您可以採取 tooresolve 步驟 hello 警示及連結 toorelevant 文件。 您也可以在 hello 過去已解決的警示檢視歷程記錄資料。

![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>AD FS 的使用情況分析
Azure AD Connect Health 流量分析會分析您同盟伺服器 hello 驗證流量。 您可以按兩下 hello 流量分析方塊，tooopen hello 流量分析分頁，它會顯示數個度量和群組。

> [!NOTE]
> toouse 流量分析與 AD FS，您必須確定已啟用 AD FS 稽核。 如需詳細資訊，請參閱 [啟用 AD FS 的稽核](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs)。
>
>

![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health/report1.png)

tooselect 其他度量，指定時間範圍或 toochange hello 群組、 hello 使用情況分析圖表上按一下滑鼠右鍵，然後選取 編輯圖表。 然後您可以指定 hello 的時間範圍，選取其他度量，並變更 hello 群組。 您可以檢視 hello hello 不同 「 度量 」 為基礎的驗證流量發佈，並使用相關 「 群組依據 」 參數 hello 之後 > 一節中所述的每個度量分組：

**計量：要求總數** - AD FS 服務所處理的要求總數。

|分組依據 | Hello 群組上的意義與為何有用？ |
| --- | --- |
| 全部 | 顯示所有的 AD FS 伺服器所處理的要求總數 hello 計數。|
| 應用程式 | 群組 hello hello 目標信賴憑證者的合作對象為基礎的要求總數。 此分組的有用 toounderstand 哪些應用程式收到 hello 總流量的多少百分比。 |
|  伺服器 |群組 hello 處理 hello 要求的 hello server 為基礎的要求總數。 此分組的有用 toounderstand hello 負載分配 hello 總流量。
| 加入工作場所 |群組 hello 總根據要求是否都來自工作地方聯結的裝置 （已知）。 此分組的有用 toounderstand，如果使用的是未知的 toohello 身分識別基礎結構的裝置存取您的資源。 |
|  驗證方法 | 群組 hello hello 用於驗證的驗證方法為基礎的要求總數。 此分組是有用的 toounderstand hello 一般驗證方法，取得用來驗證。 以下是 hello 可能的驗證方法 <ol> <li>Windows 整合式驗證 (Windows)</li> <li>表單型驗證 (表單)</li> <li>SSO (單一登入)</li> <li>X509 憑證驗證 (憑證)</li> <br>如果 hello 同盟伺服器收到包括 SSO Cookie hello 要求，會將該要求視為 SSO （單一登入）。 在這種情況下，如果 hello cookie 有效，hello 使用者未要求 tooprovide 認證，並取得無縫存取方式 toohello 應用程式。 這是一般，如果您有多個的信賴憑證者合作對象 hello 同盟伺服器所保護。 |
| 網路位置 | 群組 hello hello 使用者 hello 網路位置為基礎的要求總數。 它可以是內部網路或外部網路。 此分組的有用 tooknow hello 流量的百分比來自 hello 內部網路與外部網路。 |


**計量： 總失敗要求**-hello 總數失敗的 hello federation service 所處理的要求。 (此度量僅能在適用於 Windows Server 2012 R2 的 AD FS 上使用)

|分組依據 | Hello 群組上的意義與為何有用？ |
| --- | --- |
| 錯誤類型 | 顯示 hello 根據預先定義的錯誤類型的錯誤數目。 此分組的有用 toounderstand hello 常見的錯誤。 <ul><li>不正確的使用者名稱或密碼： 因為 tooincorrect 使用者名稱或密碼錯誤。</li> <li>「 外部網路鎖定 」: 因為 toohello 要求從鎖定的時間從外部網路使用者接收到的失敗 </li><li> 「 已過期的密碼 」: 因為 toousers 登入已過期的密碼才能執行失敗。</li><li>「 停用帳戶 」: 因為停用的帳戶與 toousers 記錄失敗。</li><li>[裝置驗證]: 因為 toousers 失敗 tooauthenticate 使用裝置驗證失敗。</li><li>[使用者憑證驗證]: 因為 toousers 失敗 tooauthenticate 因為無效的憑證失敗。</li><li>「 MFA": 因為 toouser 失敗 tooauthenticate 使用多重要素驗證失敗。</li><li>「 其他認證 」: 「 發行授權 」: 失敗，因為 tooauthorization 失敗。</li><li>「 發行委派 」: 因為 tooissuance 委派錯誤失敗。</li><li>「 權杖接受 「: 失敗，因為 tooADFS 拒絕 hello 從協力廠商身分識別提供者權杖。</li><li>「 通訊協定 」: 因為 tooprotocol 錯誤失敗。</li><li>「未知」：全部攔截。 不適合在 hello 的任何其他失敗定義的類別。</li> |
| 伺服器 | 群組 hello hello server 為基礎的錯誤。 此分組的有用 toounderstand hello 錯誤發佈到伺服器。 分佈不平均可能是伺服器處於錯誤狀態的指標。 |
| 網路位置 | 群組 hello hello 的 hello 要求 （內部網路與外部網路） 的網路位置為基礎的錯誤。 此分組的有用 toounderstand hello 失敗的要求類型。 |
|  應用程式 | 群組 hello hello 目標應用程式 （信賴憑證者的合作對象） 為基礎的失敗。 此分組的有用 toounderstand 哪一個目標的應用程式查看大多數的錯誤數目。 |

**度量︰使用者計數** - 使用 AD FS 主動驗證的唯一使用者平均數目

|分組依據 | Hello 群組上的意義與為何有用？ |
| --- | --- |
|全部 |這項標準提供使用 hello 選取的時間配量中的 hello 同盟服務之使用者的平均數目的計數。 hello 使用者並未分組。 <br>hello 平均取決於選取的 hello 時間配量。 |
| 應用程式 |應用程式 （信賴憑證者的合作對象） 為目標的 hello 為基礎的使用者群組 hello 平均數目。 此分組的有用 toounderstand 多少使用者正在使用哪一個應用程式。 |

## <a name="performance-monitoring-for-ad-fs"></a>AD FS 的效能監視
Azure AD Connect Health 效能監視會提供關於度量的監視資訊。 選取 hello [監視] 方塊中，開啟 hello 度量的詳細資訊的新刀鋒視窗。

![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health/perf1.png)

選取在 hello hello 刀鋒視窗頂端的 hello 篩選選項，您可以篩選由伺服器 toosee 個別伺服器的度量。 toochange 度量 hello 監視在監視刀鋒視窗中的 hello 圖表上按一下滑鼠右鍵，然後選取 [編輯圖表 （或選取 hello 編輯圖表] 按鈕）。 從 hello 新刀鋒視窗中開啟，您可以從 hello 下拉式清單選取其他度量，並指定檢視 hello 效能資料的時間範圍。

## <a name="reports-for-ad-fs"></a>AD FS 報告
Azure AD Connect Health 提供有關 AD FS 活動與效能的報告。 這些報告可協助系統管理員深入了解 AD FS 伺服器上的活動。

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>使用者名稱/密碼登入失敗的前 50 個使用者
Hello 的 AD FS 伺服器上失敗的驗證要求的常見原因之一是無效的認證，也就是錯誤的使用者名稱或密碼的要求。 通常是因為 toousers 到期 toocomplex 密碼、 忘記密碼或拼字錯誤。

但是還有其他可能會導致非預期的數目，例如處理由您的 AD FS 伺服器的要求的原因： 應用程式的快取使用者的認證和 hello 認證過期或惡意使用者嘗試 toosign 一系列的考量已知的密碼。 這兩個範例會在要求中可能會導致 tooa 超載的有效理由。

Azure AD Connect Health adfs 提供有關排行前 50 名使用者與登入嘗試失敗的 tooinvalid 使用者名稱或密碼到期的報表。 這份報表達成處理 hello hello 伺服陣列中的所有 hello AD FS 伺服器所產生的稽核事件

![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health-adfs/report1a.png)

此報表內，您可以輕鬆存取 toohello 下列資訊：

* 總計 # 個錯誤的使用者名稱/密碼在 hello 過去 30 天內失敗的要求
* 每天由於使用者名稱/密碼不正確而登入失敗的平均使用者人數。

按一下此組件會引導您 toohello 主報表刀鋒視窗，其中提供其他詳細資料。 此刀鋒視窗會包含與趨勢 toohelp 建立基準線使用錯誤的使用者名稱或密碼要求的相關資訊的圖形。 此外，它提供 hello 嘗試失敗次數 hello 排行前 50 名使用者清單。

hello 圖形提供下列資訊的 hello:

* hello 總計 # 個失敗的登入，因為 tooa 不正確的使用者名稱/密碼每日為基礎。
* hello 總計 # 個失敗的每日為基礎的登入的唯一使用者。
* 最後一個要求的用戶端 IP 位址

![Azure AD Connect Health 入口網站](./media/active-directory-aadconnect-health-adfs/report3a.png)

hello 報表會提供下列資訊的 hello:

| 報告項目 | 說明 |
| --- | --- |
| 使用者識別碼 |顯示 hello 所使用的使用者識別碼。 這個值是哪些 hello 使用者輸入，這在某些情況下是 hello 所使用的錯誤使用者識別碼。 |
| 嘗試失敗 |顯示 hello 總計 # 個失敗的嘗試為該特定使用者識別碼。 hello 資料表是以 hello 最數字的失敗嘗試，以遞減順序排序。 |
| 上次失敗 |Hello 上一次失敗發生時顯示 hello 時間戳記。 |
| 上次失敗 IP |顯示 hello 用戶端 IP 位址從 hello 最不正確的要求。 |

> [!NOTE]
> 此報表會自動更新之後每隔兩小時以 hello 該段時間內收集新的資訊。 如此一來，hello 最後兩小時內的登入嘗試可能不會包含在 hello 報表。
>
>

## <a name="related-links"></a>相關連結
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)