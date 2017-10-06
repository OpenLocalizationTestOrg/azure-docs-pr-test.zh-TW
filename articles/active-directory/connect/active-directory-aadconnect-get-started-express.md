---
title: "Azure AD Connect：開始使用快速設定 | Microsoft Docs"
description: "了解如何 toodownload，安裝及執行 Azure AD Connect 的 hello 安裝精靈。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>使用快速設定開始使用 Azure AD Connect
當您有單一樹系拓撲和用於驗證的**密碼同步處理**時，便可使用 Azure AD Connect [快速設定](active-directory-aadconnectsync-implement-password-synchronization.md)。 **快速設定**是 hello 預設選項，而且是最常部署的 hello 案例。 您會在內部部署目錄 toohello 雲端只有幾個簡短按一下離開 tooextend。

您開始安裝 Azure AD Connect，請確定太[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)和中的步驟完成 hello 必要條件[Azure AD Connect： 硬體和必要條件](active-directory-aadconnect-prerequisites.md)。

如果快速設定不符合拓撲，請參閱 [相關文件](#related-documentation) 中的其他案例。

## <a name="express-installation-of-azure-ad-connect"></a>快速安裝 Azure AD Connect
您可以看到這些步驟在動作中 hello[視訊](#videos)> 一節。

1. 以您想 tooinstall Azure AD Connect 的本機系統管理員 toohello 伺服器登入。 您應該這樣 hello 在伺服器上您想 toobe hello 同步伺服器。
2. 瀏覽 tooand 按兩下**AzureADConnect.msi**。
3. 在 hello 歡迎畫面上，選取 hello 方塊即表示同意 toohello 授權條款，然後按一下**繼續**。  
4. 在 hello Express 設定畫面中，按一下 **使用 express 設定**。  
   ![歡迎使用 tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Hello 連接 tooAzure AD 在畫面上，輸入您的 Azure AD hello 使用者名稱和密碼的全域管理員。 按一下 [下一步] 。  
   ![連接 tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png)如果您收到錯誤，且有連線問題，然後查看[疑難排解連線問題](active-directory-aadconnect-troubleshoot-connectivity.md)。
6. Hello 連接 tooAD DS 在畫面上，輸入企業系統管理員帳戶 hello 使用者名稱和密碼。 您可以輸入 NetBios 或 FQDN 格式，也就是 FABRIKAM\administrator 或 fabrikam.com\administrator hello 網域 」 部分。 按一下 [下一步] 。  
   ![連接 tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. hello [ **Azure AD 登入組態**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration)頁面只會顯示是否您未完成[確認您的網域](../active-directory-add-domain.md)在 hello[必要條件](active-directory-aadconnect-prerequisites.md)。
   ![未驗證的網域](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   如果您看到此頁面，請檢閱每一個標示為**未新增**和**未驗證**的網域。 確定您所使用的網域皆已在 Azure AD 中完成驗證。 當您已確認您的網域，請按一下 hello 重新整理符號。
8. Hello 準備 tooconfigure 畫面上，按一下**安裝**。
   * （選擇性） 在 hello 準備 tooconfigure 頁面上，您可以取消選取 hello**啟動 hello 同步處理程序，設定完成之後儘速**核取方塊。 如果您想 toodo 額外的設定，例如，您應該取消選取此核取方塊[篩選](active-directory-aadconnectsync-configure-filtering.md)。 如果您取消選取此選項，hello 精靈設定同步處理，但會保留 hello 排程器已停用。 不會執行直到您手動藉由啟用[hello 安裝精靈重新執行](active-directory-aadconnectsync-installation-wizard.md)。
   * 如果您在您的內部部署 Active Directory、 Exchange，則您也可以選項 tooenable [ **Exchange 混合部署**](https://technet.microsoft.com/library/jj200581.aspx)。 啟用此選項，如果您計劃 toohave Exchange 信箱這兩個 hello 雲端和內部 hello 在相同的時間。
     ![準備好 tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Hello 安裝完成時，按一下**結束**。
10. Hello 安裝完成後，登出並再次登入之前您使用同步處理服務管理員或同步處理規則編輯器。

## <a name="videos"></a>影片
如需有關使用 hello 快速安裝的影片，請參閱：

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>後續步驟
既然您已安裝的 Azure AD Connect 可以[確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)。

深入了解這些功能，與 hello 安裝已啟用：[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)，[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)，和[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。

深入了解這些常見的主題：[排程器和 tootrigger 的同步處理](active-directory-aadconnectsync-feature-scheduler.md)。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

## <a name="related-documentation"></a>相關文件
| 主題 |
| --- | --- |
| Azure AD Connect 概觀 |
| 使用自訂設定進行安裝 |
| 從 DirSync 升級 |
| 用於安裝的帳戶 |

