---
title: "aaaPublish 應用程式與 Azure AD Application Proxy |Microsoft 文件"
description: "發行與 Azure AD Application Proxy 的內部部署應用程式 toohello 雲端中的 hello Azure 入口網站。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 發佈應用程式

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-proxy-publish-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-application-proxy-publish.md)

Azure Active Directory (AD) 應用程式 Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。 您可以發行這些應用程式透過 hello Azure 入口網站 tooprovide 安全遠端存取從網路外部。

這篇文章會引導您 hello 步驟 toopublish 在內部部署應用程式，但應用程式 Proxy。 完成本文之後，您的使用者將會是能 tooaccess 您的應用程式從遠端。 是您已準備就緒 tooconfigure hello 應用程式，例如額外的功能和單一登入、 個人化的資訊和安全性需求。

如果您是新 tooApplication Proxy，深入了解這項功能與 hello 文章[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。


## <a name="publish-an-on-premises-app-for-remote-access"></a>發佈可遠端存取的內部部署應用程式

請遵循這些步驟 toopublish 您的應用程式與應用程式 Proxy。 如果您沒有已下載，並為您的組織設定連接器，請移至太[應用程式 Proxy 快速入門及安裝 hello 連接器](active-directory-application-proxy-enable.md)第一次，然後發行您的應用程式。

> [!TIP]
> 如果您要測試應用程式 Proxy 出 hello 第一次，請選擇 設定密碼型驗證的應用程式。 應用程式 Proxy 支援其他類型的驗證，但密碼為基礎的應用程式總 hello 最簡單 tooget 快速及執行。 

1. Hello 中的系統管理員身分登入[Azure 入口網站](https://portal.azure.com/)。
2. 選取 [Azure Active Directory]  >  [企業應用程式]  >  [新增應用程式]。

  ![新增企業應用程式](./media/application-proxy-publish-azure-portal/add-app.png)

3. 依序選取 [所有]、[內部部署應用程式]。  

  ![新增您自己的應用程式](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. 提供下列應用程式的相關資訊的 hello:

   - **名稱**: hello 名稱會出現在 hello 存取面板和 hello Azure 入口網站中的 hello 應用程式。 

   - **內部 URL**: hello 您 tooaccess hello 從使用應用程式在私人網路內部的 URL。 未發行的 hello 伺服器 hello rest 時，您可以在 hello 後端伺服器 toopublish，提供特定路徑。 如此一來，您可以將不同站台發佈在 hello 與不同的應用程式相同的伺服器，並提供每一個其名稱和存取規則。

     > [!TIP]
     > 如果您發行路徑，請確定它包含所有的 hello 所需的映像、 指令碼和您的應用程式的樣式表。 例如，如果您的應用程式位於 https://yourapp/app，並且使用位於 https://yourapp/media 映像，然後您應該發佈 https://yourapp/ hello 路徑。 此內部 URL 沒有 toobe hello 登陸頁面，請參閱您的使用者。 如需詳細資訊，請參閱[針對發佈應用程式設定自訂的首頁](application-proxy-office365-app-launcher.md)。

   - **外部 URL**: hello 您的使用者將會移 tooin 順序 tooaccess hello 應用程式從外部網路的位址。 如果您不想 toouse hello 預設應用程式 Proxy 的網域，閱讀[Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。
   - **預先驗證**： 應用程式 Proxy 如何授與存取 tooyour 應用程式之前驗證使用者。 

     - Azure Active Directory： 應用程式 Proxy 會重新導向使用者 toosign 入 Azure AD，驗證其 hello 目錄和應用程式的權限。 我們建議您保持為 hello 預設值，這個選項，讓您可以利用 Azure AD 安全性功能，例如條件式存取以及多因素驗證。
     - 通過： 使用者不能 tooauthenticate 針對 Azure Active Directory tooaccess hello 應用程式。 您仍然可以設定 hello 後端上的驗證需求。
   - **連接器群組**： 連接器程序 hello 遠端存取 tooyour 應用程式，以及協助您組織連接器和應用程式區域、 網路或目的連接器群組。 如果您還沒有尚未建立任何連接器群組，您的應用程式會指派太**預設**。

   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/configure-app.png)
5. 如有必要，請設定其他設定。 對於大部分的應用程式，您應該在其預設狀態中保留這些設定。 
   - **後端應用程式逾時**： 將此值設定為太**長**只有在您的應用程式為緩慢 tooauthenticate 和連接。 
   - **轉譯標頭中的 Url**： 保留此值做為**是**除非您的應用程式所需的 hello 原始主機標頭在 hello 驗證要求。
   - **將轉譯 Url 中的應用程式主體**： 保留此值做為**否**除非您有硬式編碼的 HTML 連結 tooother 在內部部署應用程式，而未使用自訂網域。 如需詳細資訊，請參閱[使用應用程式 Proxy 連結轉譯](application-proxy-link-translation.md)。
   
   ![設定您的應用程式](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. 選取 [新增] 。


## <a name="add-a-test-user"></a>新增測試使用者 

tootest 發行應用程式已正確地加入測試使用者帳戶。 請確認此帳戶已經有權限 tooaccess hello 應用程式從 hello 公司網路內。

1. 在 hello 快速入門刀鋒視窗中，選取 **指派給使用者的測試**。

  ![指派測試使用者](./media/application-proxy-publish-azure-portal/assign-user.png)

2. 在 hello 使用者和群組 刀鋒視窗中，選取**新增**。

  ![新增使用者或群組](./media/application-proxy-publish-azure-portal/add-user.png)

3. 在 hello 新增指派刀鋒視窗中，選取 **使用者和群組**然後選擇您想要讓 tooadd 的 hello 帳戶。 
4. 選取 [指派]。

## <a name="test-your-published-app"></a>測試已發佈的應用程式

在瀏覽器中，瀏覽 toohello hello 在您已設定的外部 URL 發行步驟。 您應該會看到 hello [開始] 畫面，且無法 toosign 以 hello 測試帳戶您設定。

![測試已發佈的應用程式](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>後續步驟
- [下載連接器](active-directory-application-proxy-enable.md)和[建立連接器群組](active-directory-application-proxy-connectors-azure-portal.md)toopublish 應用程式在不同的網路和位置。

- 為您新發佈的應用程式[設定單一登入](application-proxy-sso-azure-portal.md)
