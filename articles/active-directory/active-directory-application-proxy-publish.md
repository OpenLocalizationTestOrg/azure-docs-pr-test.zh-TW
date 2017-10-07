---
title: "aaaPublish 應用程式與 Azure AD Application Proxy |Microsoft 文件"
description: "將內部部署應用程式 toohello 雲端與 Azure AD Application Proxy 發行 hello 傳統入口網站中。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 發佈應用程式

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-proxy-publish-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-application-proxy-publish.md)

Azure AD Application Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。 此時，您應該已經有[hello Azure 傳統入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。 這篇文章會引導您完成 hello 步驟 toopublish 執行的應用程式在您的區域網路上，並提供安全的遠端存取從網路外部。 完成本文之後，您會準備 tooconfigure hello 應用程式與個人化的資訊或安全性需求。

> [!NOTE]
> 應用程式 Proxy 是升級 toohello Premium 或 Azure Active Directory Basic 版時，才可使用的功能。 如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。 如果您想 toouse 應用程式 Proxy，您可以[hello Azure 入口網站中發佈應用程式](application-proxy-publish-azure-portal.md)。

## <a name="publish-an-app-using-hello-wizard"></a>發行應用程式使用 hello 精靈
1. Hello 中的系統管理員身分登入[Azure 傳統入口網站](https://manage.windowsazure.com/)。
2. 請 tooActive 目錄並選取 hello 目錄啟用應用程式 Proxy 的位置。
   
    ![Active Directory - 圖示](./media/active-directory-application-proxy-publish/ad_icon.png)
3. 按一下 hello**應用程式**索引標籤，然後再按一下 hello**新增**在 hello 囉 」 畫面底部的按鈕
   
    ![新增應用程式](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. 選取 [發佈將可從您的網路外部存取的應用程式] 。
   
    ![發佈將可從您的網路外部存取的應用程式](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. 提供下列應用程式的相關資訊的 hello:
   
   * **名稱**: hello 應用程式的使用者易記名稱。 該名稱在您的目錄中必須是唯一的。
   * **內部 URL**: hello 應用程式 Proxy 連接器的 hello 位址使用 tooaccess hello 應用程式從您的私人網路內。 未發行的 hello 伺服器 hello rest 時，您可以在 hello 後端伺服器 toopublish，提供特定路徑。 如此一來，您可以將不同站台發佈在 hello 同一部伺服器，並提供每一個其名稱和存取規則。
     
     > [!TIP]
     > 如果您發行路徑，請確定它包含所有的 hello 所需的映像、 指令碼和您的應用程式的樣式表。 例如，如果您的應用程式位於 https://yourapp/app，並且使用位於 https://yourapp/media 映像，然後您應該發佈 https://yourapp/ hello 路徑。
     > 
     > 
   * **預先驗證方法**： 應用程式 Proxy 如何授與存取 tooyour 應用程式之前驗證使用者。 從 hello 下拉功能表中選擇其中一個 hello 選項。
     
     * Azure Active Directory： 應用程式 Proxy 會重新導向使用者 toosign 入 Azure AD，驗證其 hello 目錄和應用程式的權限。
     * 通過： 使用者不能 tooauthenticate tooaccess hello 應用程式。
     
     ![應用程式屬性](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. toofinish hello 精靈 中，按一下 hello 在 hello 囉 」 畫面底部的核取記號。 hello 應用程式現在是 Azure AD 中定義。

## <a name="assign-users-and-groups-toohello-application"></a>指派使用者和群組 toohello 應用程式
在順序為您的使用者 tooaccess 發佈的應用程式，您需要 tooassign 它們個別或群組。 (請記住 tooassign 自行存取，太。)您指派的每位使用者需要 Azure Basic 或更新版本的授權。 您可以將授權指派個別或 toogroups。 如需詳細資訊，請參閱[tooan 應用程式指派給使用者](active-directory-applications-guiding-developers-assigning-users.md)。 

針對需要預先驗證的應用程式，將使用者指派會授與權限 toouse hello 應用程式。 不需要的應用程式的預先驗證時，將使用者指派表示該 hello 使用者可以存取 hello 應用程式透過 hello 存取面板。

1. 分頁裝訂的 hello 新增應用程式精靈 之後，您會看到 hello 快速入門應用程式頁面。 toomanage 擁有存取 toohello 應用程式中，選取**使用者和群組**。
   
    ![應用程式 Proxy 快速啟動指派使用者 - 螢幕擷取畫面](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. 在您的目錄中搜尋特定群組，或顯示所有的使用者。 toodisplay hello 搜尋結果中，按一下 hello 核取記號。
   
      ![搜尋群組或使用者 - 螢幕擷取畫面](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. 選取每個使用者或群組，您想要 tooassign toothis 應用程式，然後按一下 **指派**。 您要求 tooconfirm 此動作。

> [!NOTE]
> 若是整合式 Windows 驗證應用程式，您可以僅指派從內部部署 Active Directory 同步的使用者及群組。 您無法為使用 Azure Active Directory 應用程式 Proxy 發佈的應用程式，指派使用 Microsoft 帳戶和來賓登入的使用者。 請確定您使用屬於 hello 的認證登入的使用者與您要發行的 hello 應用程式相同的網域。
> 
> 

## <a name="test-your-published-application"></a>測試已發佈的應用程式
一旦您已經發行您的應用程式，您可以藉由瀏覽您發行的 toohello URL 測試它。 確定您可以存取，且應用程式會正確地呈現，以及所有一切如預期般運作。 如果您有問題或出現錯誤訊息，再試一次 hello[疑難排解指南](active-directory-application-proxy-troubleshoot.md)。

## <a name="configure-your-application"></a>設定您的應用程式
您可以修改已發行的應用程式，或設定 hello 設定 頁面上的進階選項。 這個頁面上，您可以變更 hello 名稱或上傳標誌，以自訂您的應用程式。 您也可以管理存取規則一樣 hello 預先驗證方法或多重要素驗證。

![進階組態](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

發行應用程式之後使用 Azure Active Directory 應用程式 Proxy，它們會出現在 Azure AD 中在 hello 應用程式清單，並那里管理。

如果您停用應用程式 Proxy 服務已發行應用程式之後，，就不再可從私人網路外部存取 hello 應用程式。 您的使用者仍然可以存取 hello 應用程式內部像往常一樣。

tooview 應用程式，並確定它可以存取，按兩下 hello hello 應用程式名稱。 如果 hello 應用程式 Proxy 服務已停用 hello 應用程式不提供，在 hello 囉 」 畫面最上方會出現警告訊息。

toodelete 應用程式，hello 清單中選取的應用程式，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟
* [使用您自己的網域名稱發行應用程式](active-directory-application-proxy-custom-domains.md)
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [啟用條件式存取](active-directory-application-proxy-conditional-access.md)
* [使用宣告感知應用程式](active-directory-application-proxy-claims-aware-apps.md)

如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)

