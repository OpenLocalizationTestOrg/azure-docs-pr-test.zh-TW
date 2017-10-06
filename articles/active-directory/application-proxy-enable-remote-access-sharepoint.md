---
title: "使用 Azure AD Application Proxy aaaEnable 遠端存取 tooSharePoint |Microsoft 文件"
description: "涵蓋如何 hello 基本概念 toointegrate Azure AD Application Proxy 的內部部署 SharePoint 伺服器。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint

本文將討論如何 toointegrate Azure Active Directory (Azure AD) 應用程式 Proxy 的內部部署 SharePoint 伺服器。

將遠端存取 tooSharePoint tooenable 與 Azure AD Application Proxy，請遵循本文逐步解說中的 hello 章節。

## <a name="prerequisites"></a>必要條件

本文假設您的環境中已經有 SharePoint 2013 或更新版本。 此外，請考慮下列必要條件 hello:

* SharePoint 包含 Kerberos 的原生支援。 因此，透過 Azure AD Application Proxy 從遠端存取內部網站的使用者可以假設的 toohave 單一登入 (SSO) 體驗。

* 您需要 toomake 一些組態變更 tooyour SharePoint 伺服器。 建議您使用預備環境。 如此一來，您可以做出更新 tooyour 首先，臨時伺服器，並再進行實際執行前先測試循環。

* 我們假設您有已設定 SSL for SharePoint，因為我們需要 SSL hello 上的發行 URL。 您需要啟用 SSL toohave tooensure 連結傳送/對應的正確內部網站。 如果您尚未設定 SSL，請參閱[設定 SharePoint 2013 的 SSL](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) 以取得相關指示。 此外，請確定該 hello 連接器電腦信任 hello 憑證所發出。 （hello 憑證不需要公開發出 toobe）。

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>步驟 1： 設定單一登入 tooSharePoint

我們的客戶想的 hello 最佳 SSO 的體驗的後端應用程式中，SharePoint 伺服器在此情況下。 在這個常見的 Azure AD 案例，hello 驗證使用者一次，因為它們不會進行一次驗證提示。

對於需要或不使用 Windows 驗證的內部部署應用程式，您可以使用 hello Kerberos 驗證通訊協定和名為 Kerberos 限制委派 (KCD) 的功能，以達到 SSO。 KCD 設定時，可以讓 hello 應用程式 Proxy 連接器 tooobtain windows 票證/權杖的使用者，即使 hello 使用者尚未直接登入 tooWindows。 toolearn 深入了解 KCD，請參閱[Kerberos 限制委派概觀](https://technet.microsoft.com/library/jj553400.aspx)。

for SharePoint 伺服器，使用 hello 程序，在下列各節循序 hello 向上 KCD tooset:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>確定 SharePoint 是在服務帳戶下執行

首先，確定 SharePoint 是在定義的服務帳戶下執行，而不是本機系統、本機服務或網路服務帳戶下。 如此您就可以附加服務主要名稱 (Spn) tooa 有效的帳戶，請執行這項操作。 Spn 是 hello Kerberos 通訊協定如何識別不同的服務。 您將需要 hello 帳戶和更新版本 tooconfigure hello KCD。

tooensure 定義的服務帳戶下執行您的站台執行下列步驟的 hello:

1. 開啟 hello **SharePoint 2013 管理中心內**站台。
2. 跳過**安全性**選取**設定服務帳戶**。
3. 選取 [Web 應用程式集區 - SharePoint - 80]。 hello 選項可能稍有不同根據 hello 名稱的 web 集區，或如果 hello web 集區預設會使用 SSL。

  ![設定服務帳戶的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. 如果**選取帳戶，此元件**是**本機服務**或**Network Service**，您需要 toocreate 帳戶。 如果沒有，您完成時，可以移 toohello 下一節。
5. 選取 [註冊新的受管理帳戶]。 建立您的帳戶之後，您必須設定**Web 應用程式集區**才能夠使用 hello 帳戶。

> [!NOTE]
您需要的先前 toohave 建立 hello 服務的 Azure AD 帳戶。 建議您允許密碼自動變更。 步驟和疑難排解問題的 hello 完整集的相關資訊，請參閱[SharePoint 2013 中設定自動密碼變更](https://technet.microsoft.com/library/ff724280.aspx)。

### <a name="configure-sharepoint-for-kerberos"></a>設定 SharePoint 的 Kerberos

使用 KCD tooperform 單一登入 toohello SharePoint 伺服器，這只適用於 Kerberos。

tooconfigure SharePoint 網站的 Kerberos 驗證：

1. 開啟 hello **SharePoint 2013 管理中心內**站台。
2. 跳過**應用程式管理**，選取**管理 web 應用程式**，然後選取您的 SharePoint 網站。 在此範例中為 **SharePoint - 80**。

  ![選取 hello SharePoint 網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. 按一下**驗證提供者**hello 工具列上。
4. 在 hello**驗證提供者**方塊中，按一下**預設區域**tooview hello 設定。
5. 在 hello**編輯驗證**對話方塊方塊中，向下捲動直到您看到**宣告驗證類型**，並確定兩者**啟用 Windows 驗證**和**整合式 Windows 驗證**已選取。
6. 在 [hello] 下拉式清單方塊中，確定**交涉 (Kerberos)**已選取。

  ![編輯 [驗證] 對話方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. 在 hello 底部 hello**編輯驗證**對話方塊中，按一下 **儲存**。

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>設定 hello SharePoint 服務帳戶的服務主體名稱

Hello KCD 設定之前，您需要以 hello 您已設定的服務帳戶執行 tooidentify hello SharePoint 服務。 您可以透過設定 SPN 來執行此動作。 如需詳細資訊，請參閱[服務主體名稱](https://technet.microsoft.com/library/cc961723.aspx)。

hello SPN 格式如下：

```
<service class>/<host>:<port>
```

Hello SPN 格式：

* _服務類別_是 hello 服務的唯一名稱。 針對 SharePoint，您會使用 **HTTP**。

* _主機_hello 完整的網域或 NetBIOS 名稱 hello 主控件以 hello 服務上執行。 對於 SharePoint 網站，此文字可能需要 toobe hello 網站的 URL hello，視您正在使用的 IIS hello 版本而定。

* port 是選擇性的。

如果是 hello hello SharePoint 伺服器的 FQDN:

```
sharepoint.demo.o365identity.us
```

然後是 hello SPN:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

您可能也需要 tooset Spn 特定網站的伺服器上。 如需詳細資訊，請參閱[設定 Kerberos 驗證](https://technet.microsoft.com/library/cc263449(v=office.12).aspx)。 特別注意 toohello 區段 」 建立服務主體使用 Kerberos 驗證的 Web 應用程式的名稱 」。

hello tooset Spn 的最簡單的方式是 toofollow hello 的 SPN 格式可能已經存在您的網站。 複製針對 hello 服務帳戶的 Spn tooregister。 toodo 這樣：

1. 瀏覽 toohello 站台，以從另一部電腦的 hello SPN。
 當您執行動作，hello 組相關的 Kerberos 票證會快取 hello 機器上。 這些票證包含 hello hello 您瀏覽至的目標網站的 SPN。

2. 您可以使用一個工具，稱為提取 hello SPN 該站台[Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html)。 在命令視窗中執行 hello hello 使用者身分存取的 hello 站台在 hello 瀏覽器中執行的相同內容 hello 下列命令：
```
Klist
```
Klist 則會傳回目標 Spn 的 hello 集合。 在此範例中，反白顯示 hello 值為 hello 所需的 SPN:

  ![範例 Klist 結果](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. 有 hello SPN 之後，您會需要 toomake 確認它已正確設定 hello 您稍早 hello web 應用程式設定的服務帳戶。 執行下列命令從 hello 命令提示字元，hello 網域的系統管理員身分的 hello:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 此命令集 hello SPN hello SharePoint 服務帳戶身分執行_demo\sp_svc_。

 取代_http/sharepoint.demo.o365identity.us_以 hello SPN 為您的伺服器和_demo\sp_svc_與您的環境中的 hello 服務帳戶。 hello Setspn hello 再增加其 SPN 的命令搜尋。 在此情況下，您可能會看到 **SPN 值重複**錯誤。 如果您看到此錯誤，請確定 hello 值為 hello 服務帳戶相關聯。

您可以確認該 hello 與 hello-l 選項執行 hello Setspn 命令加入 SPN。 toolearn 進一步了解此命令，請參閱[Setspn](https://technet.microsoft.com/library/cc731241.aspx)。

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>請確定該 hello 連接器設定為受信任的委派 tooSharePoint

設定 hello KCD 讓 hello Azure AD Application Proxy 服務可以委派使用者識別 toohello SharePoint 服務。 您可以啟用 hello 應用程式 Proxy 連接器 tooretrieve Kerberos 票證為您在 Azure AD 中已驗證的使用者。 然後該伺服器在此情況下傳遞 hello 內容 toohello 目標應用程式或 SharePoint。

tooconfigure 的 hello KCD，重複步驟，針對每個連接器機器的 hello:

1. 以網域系統管理員 tooa DC，登入，然後開啟**Active Directory 使用者和電腦**。
2. 尋找 hello hello 連接器的電腦上執行。 在此範例中，它具有 hello 相同 SharePoint 伺服器。
3. 按兩下 hello 電腦，然後按一下hello**委派** 索引標籤。
4. 確定 hello 委派設定已設定太**信任這台電腦所委派 toohello 指定僅限服務**，然後選取**使用任何驗證通訊協定**。

  ![委派設定](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. 按一下 hello**新增**按鈕，再按一下**使用者或電腦**，並找出 hello 服務帳戶。

  ![新增 hello SPN hello 服務帳戶](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. 在 hello Spn 的清單，選取您稍早建立 hello 服務帳戶的其中一個 hello。
7. 按一下 [確定] 。 按一下**確定**再次 toosave hello 變更。

## <a name="step-2-enable-remote-access-toosharepoint"></a>步驟 2： 啟用遠端存取 tooSharePoint

現在您已啟用 Kerberos 的 SharePoint，並設定 KCD，您已準備好設定單一登入 tooSharePoint tooset。 然後從 hello 連接器，您可以發佈 hello 經由 Azure AD Application Proxy 的遠端存取的 SharePoint 伺服器陣列。

tooperform hello 下列步驟，您需要 toobe 貴組織的 Azure Active Directory 帳戶中的 hello 全域管理員角色的成員。

1. 登入 toohello [Azure 入口網站](https://manage.windowsazure.com)並尋找您的 Azure AD 租用戶。
2. 按一下 應用程式，然後按一下新增。
3. 選取 [發佈將可從您的網路外部存取的應用程式] 。 如果您沒有看到此選項，請確定您有 Azure AD Basic 或 Premium hello 租用戶中設定。
4. 完成每個 hello 選項，如下所示：
 * **名稱**︰使用任何您想要的值，例如 SharePoint。
 * **內部 URL**： 這是 hello hello SharePoint 網站 URL 在內部，例如**https://SharePoint/**。 在此範例中，請確定 toouse **https**。
 * **預先驗證方法**︰選取 [Azure Active Directory]。

  ![用於新增應用程式的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Hello 應用程式發行之後，按一下 hello**設定** 索引標籤。
6. 捲動 toohello 選項**標頭中的 轉譯 URL**。 hello 預設值是**是**。 它也變更**否**。

 SharePoint 會使用 hello_主機標頭_值 toolook hello 站台。 它也會根據此值產生連結。 hello 淨效果為 toomake 確定 SharePoint 會產生任何連結已正確設定 toouse hello 外部 URL 的已發行的 URL。 將 hello 值設定為太**是**也可讓 hello 連接器 tooforward hello 要求 toohello 後端應用程式。 不過，設定太 hello 值**否**hello 連接器的方法不會傳送 hello 內部主機名稱。 相反地，hello 連接器會傳送 hello 主機標頭為 hello 發行 URL toohello 後端應用程式。

 此外，tooensure SharePoint 接受此 URL，您需要 toocomplete hello SharePoint 伺服器上其他的設定。 您要進行的 hello 下一節。

7. 變更**內部驗證方法**太**整合式 Windows 驗證**。 如果您的 Azure AD 租用戶會使用 UPN 不同 hello UPN 內部部署的 hello 雲端中，請記得 tooupdate**委派登入身分識別**以及。
8. 設定**內部應用程式 SPN** toohello 您先前設定的值。 例如，使用 **http/sharepoint.demo.o365identity.us**。
9. 指派 hello 應用程式 tooyour 目標使用者。

您的應用程式應該看起來類似下列範例的 toohello:

  ![完成的應用程式](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>步驟 3： 確定 SharePoint 知道 hello 外部 URL

SharePoint 可以找到 hello hello 外部 URL 為基礎的站台，讓它將會根據該外部 URL 的連結呈現您最後一個步驟 tooensure。 您藉由設定備用存取對應 hello SharePoint 網站。

1. 開啟 hello **SharePoint 2013 管理中心內**站台。
2. 在 [系統設定] 下，選取 [設定備用存取對應]。

 這會開啟 hello**備用存取對應**方塊。

  ![[備用存取對應] 方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. 在 [hello] 旁邊的下拉式清單中**備用存取對應集合**，選取**變更備用存取對應集合**。
4. 選取您的網站，例如 **SharePoint - 80**。

  ![選取網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. 您可以選擇 tooadd hello 發行 URL 做為內部的 URL 或公用 URL。 此範例使用 hello 外部網路的公用 URL。
6. 按一下**編輯公用 Url**在 hello**外部網路**路徑，然後輸入 hello hello 路徑發行應用程式中的，如同 hello 前一個步驟。 例如，輸入 **https://sharepoint-iddemo.msappproxy.net**。

  ![輸入 hello 路徑](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. 按一下 [儲存] 。

 您現在可以存取 hello SharePoint 網站，從外部透過 Azure AD Application Proxy。

## <a name="next-steps"></a>後續步驟

- [如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)
- [了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)
- [使用 Azure AD 應用程式 Proxy 發佈 SharePoint 2016 和 Office Online Server](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
