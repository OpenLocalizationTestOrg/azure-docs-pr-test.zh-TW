---
title: "藉由限制租用戶-Azure aaaManage 存取 toocloud 應用程式 |Microsoft 文件"
description: "如何 toouse 租用戶限制 toomanage 哪些使用者可以存取應用程式會根據其 Azure AD 租用戶。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>使用租用戶限制 toomanage access tooSaaS 雲端應用程式

強調安全性的大型組織想 toomove toocloud 服務，例如 Office 365，但是使用者只可以存取的需求 tooknow 核准資源。 傳統上，公司網域名稱或 IP 位址時限制他們想要 toomanage 存取。 在 SaaS 應用程式裝載於公用雲端而在共用網域名稱 (例如 outlook.office.com 和 login.microsoftonline.com) 上執行的環境中，這個方法行不通。封鎖這些位址，會讓使用者無法存取 hello 網站上的 Outlook 完全，而不只限制它們 tooapproved 身分識別和資源。

Azure Active Directory 的方案 toothis 挑戰是名為租用戶限制的功能。 租用戶限制可讓組織 toocontrol 存取 tooSaaS 雲端應用程式，根據 hello Azure AD 租用戶 hello 進行單一登入的應用程式使用。 比方說，您可能想 tooallow 存取 tooyour 組織的 Office 365 應用程式，同時防止這些相同的應用程式存取 tooother 組織的執行個體。  

租用戶限制提供組織 hello 能力 toospecify hello 清單的使用者允許 tooaccess 租用戶。 然後 azure AD 只授與存取 toothese 允許租用戶。

本文著重 for Office 365 租用戶的限制，但 hello 功能應搭配使用新式驗證通訊協定與 Azure AD 進行單一登入任何 SaaS 雲端應用程式。 如果您使用的 SaaS 應用程式使用不同的 Azure AD 租用戶從 Office 365 所使用的 hello 租用戶，請確定所有必要的允許租用戶。 如需有關 SaaS 雲端應用程式的詳細資訊，請參閱 hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/)。

## <a name="how-it-works"></a>運作方式

hello 整體解決方案包含下列元件的 hello: 

1. **Azure AD** – 如果 hello `Restrict-Access-To-Tenants: <permitted tenant list>` hello 問題安全性語彙基元允許租用戶僅存在，Azure AD。 

2. **在內部部署 proxy 伺服器基礎結構**– proxy 裝置能夠 SSL 檢查，設定的 tooinsert hello 標頭，其中包含的 hello 清單允許排入流量的 Azure AD 的租用戶。 

3. **用戶端軟體**– toosupport 租用戶的限制，用戶端軟體必須要求權杖直接從 Azure AD，使流量可以攔截 hello proxy 基礎結構。 目前瀏覽器型 Office 365 應用程式和使用新式驗證 (例如 OAuth 2.0) 的 Office 用戶端都支援「租用戶限制」。 

4. **新式驗證**– 雲端服務必須使用新式驗證 toouse 租用戶限制，並封鎖存取 tooall 非允許租用戶。 Office 365 的雲端服務必須是預設設定的 toouse 新式驗證通訊協定。 Hello 最新的 Office 365 新式驗證支援的資訊，請參閱[更新 Office 365 新式驗證](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)。

hello 下列圖表說明 hello 高層級的流量。 SSL 檢查時，才需要在流量 tooAzure AD、 不 toohello Office 365 雲端服務。 這個差別是很重要的因為驗證 tooAzure AD hello 流量磁碟區通常遠比流量磁碟區 tooSaaS 應用程式，例如 Exchange Online 和 SharePoint Online。

![租用戶限制流量流程 - 圖表](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>設定租用戶限制

有兩個步驟 tooget 入門租用戶的限制。 hello 第一個步驟是確定您的用戶端可以連接 toohello 右位址 toomake。 hello 第二種是 tooconfigure proxy 基礎結構。

### <a name="urls-and-ip-addresses"></a>URL 和 IP 位址

toouse 租用戶的限制，您的用戶端必須能夠 tooconnect toohello 下列 Azure AD Url tooauthenticate: login.microsoftonline.com、 login.microsoft.com 和 login.windows.net。 此外，tooaccess Office 365，您的用戶端也必須能夠 tooconnect toohello Fqdn/Url 和 IP 位址中定義[Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。 

### <a name="proxy-configuration-and-requirements"></a>Proxy 組態和需求

下列組態的 hello 是透過 proxy 基礎結構的必要的 tooenable 租用戶的限制。 本指南是泛型，所以您應該參閱 tooyour proxy 廠商的文件的特定實作步驟。

#### <a name="prerequisites"></a>必要條件

- hello proxy 必須是能夠 tooperform SSL 攔截、 HTTP 標頭插入與篩選目的地使用 Fqdn/Url。 

- 用戶端必須信任 hello 出示 hello proxy 進行 SSL 通訊的憑證鏈結。 例如，如果使用來自內部的 PKI 憑證，hello 內部發行根憑證授權單位憑證必須受信任。

- 此功能隨附於 Office 365 訂閱，但如果您想 toouse 租用戶限制 toocontrol 存取 tooother SaaS 應用程式然後 Azure AD Premium 1 授權所需。

#### <a name="configuration"></a>組態

針對每個連入要求 toologin.microsoftonline.com、 login.microsoft.com，並且 login.windows.net 上插入兩個 HTTP 標頭：*限制的存取-到-租用戶*和*限制存取內容*。

hello 標頭應該包括下列項目 hello: 
- 如*限制的存取-到-租用戶*，值為\<允許租用戶清單\>，這是以逗號分隔的清單要 tooallow 使用者 tooaccess 的租用戶。 任何已向租用戶的網域可以是使用的 tooidentify hello 租用戶，這份清單中。 例如，toopermit 存取 tooboth Contoso 和 Fabrikam 租用戶，hello 名稱/值組看起來像是：`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- 如*限制存取內容*，單一目錄識別碼，宣告的租用戶已設定 hello 租用戶限制的值。 例如，toodeclare Contoso 做為設定 hello 租用戶限制原則的 hello 租用戶，hello 名稱/值組看起來像：`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> 您可以找到您目錄的識別碼在 hello [Azure 入口網站](https://portal.azure.com)。 請以系統管理員身分登入，選取 [Azure Active Directory]，然後選取 [屬性]。

tooprevent 使用者從自己的 HTTP 標頭插入與未經核准的租用戶，hello proxy 需要 tooreplace hello 限制的存取-到-租用戶標頭如果它已存在於 hello 連入要求中。 

用戶端必須強制的 toouse hello proxy 要求 toologin.microsoftonline.com、 login.microsoft.com，和 login.windows.net。 例如，如果 PAC 檔案使用的 toodirect 用戶端 toouse hello proxy，使用者應該不能 tooedit 或停用 hello PAC 檔案。

## <a name="hello-user-experience"></a>hello 使用者經驗

此區段會顯示 hello 經驗的使用者和系統管理員 」。

### <a name="end-user-experience"></a>使用者體驗

範例使用者在 hello contoso 公司網路，但正嘗試 tooaccess hello Fabrikam 共用 SaaS 應用程式執行個體類似 Outlook 線上。 如果該執行個體不允許租用戶 Contoso，hello 使用者會看到下列頁面的 hello:

![針對非允許之租用戶中使用者的拒絕存取頁面](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>管理員體驗

雖然 hello 公司 proxy 基礎結構上完成租用戶限制的設定，系統管理員可直接存取 hello Azure 入口網站中的 hello 租用戶限制報表。 tooview hello 報告，toohello Azure Active Directory 概觀 頁面上，然後查看 其他的功能 底下。

hello hello 租用戶系統管理員指定為 hello 受限存取內容的租用戶可以使用此報表 toosee，由於 hello 而封鎖所有的登入租用戶限制原則，包括使用 hello 身分識別，而且 hello 目標目錄識別碼。

![使用登入嘗試限制的 Azure 入口網站 tooview hello](./media/active-directory-tenant-restrictions/portal-report.png)

其他跟報表一樣 hello Azure 入口網站中，您可以使用報表的篩選器 toospecify hello 範圍。 您可以依據特定使用者、應用程式、用戶端或時間間隔進行篩選。

## <a name="office-365-support"></a>Office 365 支援

Office 365 應用程式必須符合兩個準則 toofully 支援租用戶的限制：

1. 使用 hello 用戶端支援新式驗證
2. 新式驗證會啟用為 hello 雲端服務的 hello 預設驗證通訊協定。

請參閱太[更新 Office 365 新式驗證](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)hello 最新的 office 用戶端目前支援新式驗證的資訊。 該頁面也包含連結 tooinstructions 啟用新式驗證等特定 Exchange Online Skype for Business Online 租用戶。 SharePoint Online 中已經預設啟用新式驗證。

Office 365 瀏覽器型應用程式目前支援租用戶限制 (hello Office 入口網站中，Yammer，SharePoint 網站、 Outlook hello Web 等。)。 針對豐富型用戶端 (Outlook、商務用 Skype、Word、Excel、PowerPoint 等)，只有在使用新式驗證的情況下，才能強制執行「租用戶限制」。  

Outlook 及 Skype 支援新式驗證的商務用戶端針對租用戶的仍能 toouse 傳統通訊協定不啟用新式驗證，有效地略過租用戶的限制。 在 Windows 上的 outlook，客戶可能選擇 tooimplement 限制防止使用者加入未經核准的郵件帳戶 tootheir 設定檔。 例如，請參閱 hello[防止新增非預設 Exchange 帳戶](http://gpsearch.azurewebsites.net/default.aspx?ref=1)群組原則設定。 對於非 Windows 平台上的 Outlook 與所有平台上的商務用 Skype，目前尚未完整支援租用戶限制。

## <a name="testing"></a>測試

如果您想出租用戶限制 tootry 供整個組織中實作之前，有兩個選項： 主控件為基礎的方法，使用 Fiddler 或 proxy 設定的分段首度發行工具。

### <a name="fiddler-for-a-host-based-approach"></a>適用於主機型方法的 Fiddler

Fiddler 是免費的 web 偵錯 proxy 可使用的 toocapture 和修改包括插入 HTTP 標頭的 HTTP/HTTPS 流量。 tooconfigure Fiddler tootest 租用戶的限制，執行下列步驟的 hello:

1.  [下載並安裝 Fiddler](http://www.telerik.com/fiddler)。
2.  Fiddler toodecrypt HTTPS 流量，設定每個[Fiddler 的說明 」 文件](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS)。
3.  設定 Fiddler tooinsert hello*限制的存取-到-租用戶*和*限制存取內容*標頭使用自訂規則：
  1. 在 hello Fiddler Web Debugger 工具中，選取 hello**規則**功能表，然後選取**自訂規則...** tooopen hello CustomRules 檔案。
  2. 新增下列在 hello hello 開頭的行 hello *OnBeforeRequest*函式。 使用與您租用戶一起註冊的網域來取代 \<tenant domain\>，例如 contoso.onmicrosoft.com。使用您租用戶的 Azure AD GUID 識別碼來取代 \<directory ID\>。

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  如果您需要 tooallow 多個租用戶，請使用逗號 tooseparate hello 租用戶名稱。 例如：

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. 儲存並關閉 hello CustomRules 檔案。

設定 Fiddler 之後，您可以擷取的流量將 toohello**檔案**功能表，然後選取**擷取流量**。

### <a name="staged-rollout-of-proxy-settings"></a>分段推出 Proxy 設定

根據 hello proxy 基礎結構的功能，您可能會無法 toostage hello 首度發行的設定 tooyour 使用者。 以下是一些可供考量的概略選項：

1.  使用 PAC 檔案 toopoint 測試使用者 tooa 測試 proxy 基礎結構，而一般使用者繼續 toouse hello 生產 proxy 基礎結構。
2.  有些 Proxy 伺服器可以使用群組來支援不同的組態。

如需特定詳細資料，請參閱 tooyour proxy 伺服器文件集。

## <a name="next-steps"></a>後續步驟

- 閱讀[更新的 Office 365 新式驗證 (英文)](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- 檢閱 hello [Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
