---
title: "aaaApplications 和瀏覽器的 Azure Active Directory 中使用條件式存取規則 |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查特定條件時，它會驗證 hello 使用者及 tooallow 應用程式存取。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器

Azure Active Directory (Azure AD) 連線應用程式、預先整合的同盟軟體即服務 (SaaS) 應用程式、使用密碼單一登入 (SSO) 的應用程式、商務營運應用程式以及使用 Azure AD 應用程式 Proxy 的應用程式，都支援條件式存取規則。 如需可使用條件式存取的應用程式詳細清單，請參閱[已啟用條件式存取功能的服務](active-directory-conditional-access-technical-reference.md)。 條件式存取可以與運用新式驗證的行動和傳統型應用程式搭配使用。 在本文中，我們將討論條件式存取功能在行動和桌面應用程式中的運作方式。

您可以在使用新式驗證的應用程式中使用 Azure AD 登入頁面。 在登入頁面中，系統會提示您進行 Multi-Factor Authentication。 會顯示訊息，是否將會封鎖 hello 使用者的存取權。 以裝置型條件式存取原則評估需要使用 Azure AD，hello 裝置 tooauthenticate 新式驗證。

它是重要 tooknow 哪些應用程式可以使用條件式存取規則，並在 hello 步驟，您可能需要 tootake toosecure 其他應用程式進入點。

## <a name="applications-that-use-modern-authentication"></a>使用新式驗證的應用程式
> [!NOTE]
> 如果 Azure AD 中的條件式存取原則等同於 Office 365 中的條件式存取原則，請設定這兩個條件式存取原則。 這會套用，比方說，tooconditional Exchange Online 或 SharePoint Online 的存取原則。
>
>

hello 下列應用程式支援條件式存取 Office 365 和其他 Azure AD 連線的服務應用程式：


| 目標服務| 平台| 應用程式 |
| --- | --- | --- |
| 任何 My Apps 應用程式服務| Android 和 iOS| 應用程式的 MFA 和位置原則。 不支援裝置型原則。|
| Azure 遠端應用程式服務| Windows 10、Windows 8.1、Windows 7、iOS、Android 和 Mac OS X| Azure 遠端應用程式|
| Dynamics CRM| Windows 10、Windows 8.1、Windows 7、iOS 和 Android| Dynamics CRM 應用程式|
| Microsoft Teams| Windows 10、Windows 8.1、Windows 7、iOS/Android 和 MAC OSX| Microsoft Teams Services - 這會控制支援 Microsoft Teams 及其所有用戶端應用程式的所有服務 - Windows 桌面、MAC OS X、iOS、Android、WP 和 Web 用戶端|
| Office 365 Exchange Online| Windows 10| 郵件/行事曆/連絡人應用程式、Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)|
| Office 365 Exchange Online| Windows 8.1、Windows 7| Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)|
| Office 365 Exchange Online| iOS| Outlook 行動應用程式|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (macOS 版 Office)|
| Office 365 SharePoint Online| Windows 10| Office 2016 應用程式、 通用 Office 應用程式 （使用新式驗證） 時，Office 2013 OneDrive 同步用戶端 (請參閱[備忘稿](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))，規劃未來的 hello Office 群組支援 SharePoint 應用程式的支援計劃未來 hello|
| Office 365 SharePoint Online| Windows 8.1、Windows 7| Office 2016 應用程式、Office 2013 (具備新式驗證)、OneDrive 同步處理用戶端 (請參閱[附註](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS、Android| Office 行動應用程式|
| Office 365 SharePoint Online| Mac OS X| macOS 版 Office 2016 (僅限 Word、Excel、PowerPoint、OneNote)。 支援商務用 OneDrive 規劃未來的 hello|
| Office 365 Yammer| Windows 10、iOS、Android| Office Yammer 應用程式|
| PowerBI service| Windows 10、Windows 8.1、Windows 7 及 iOS| PowerBI 應用程式。 hello 適用於 Android 的 Power BI 應用程式目前不支援裝置型條件式存取。|
| Visual Studio Team Services| Windows 10、Windows 8.1、Windows 7、iOS 和 Android| Visual Studio Team Services 應用程式|








## <a name="applications-that-do-not-use-modern-authentication"></a>未使用新式驗證的應用程式
目前，您必須使用其他方法 tooblock 存取 tooapps 不使用新式驗證。 條件式存取不會強制執行未使用新式驗證之應用程式的存取規則。 這主要是 Exchange 和 SharePoint 存取的考量。 大部分舊版應用程式使用較舊的存取控制通訊協定。

### <a name="control-access-in-office-365-sharepoint-online"></a>Office 365 SharePoint Online 中的控制存取
您可以使用 hello 組 SPOTenant cmdlet 來停用 SharePoint 的存取權的舊版通訊協定。 使用這個指令程式 tooprevent Office 用戶端的存取 SharePoint Online 資源的非新式驗證通訊協定。

**範例命令**：`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Office 365 Exchange Online 中的控制存取
Exchange 提供兩個主要的通訊協定類別。 檢閱 hello 下列選項，然後選取最適合貴組織的 hello 原則。

* **Exchange ActiveSync**。 根據預設，不會針對 Exchange ActiveSync 強制執行 Multi-Factor Authentication 和位置的條件式存取原則。 您可以設定 Exchange ActiveSync 原則直接管理，或是使用 Active Directory Federation Services (AD FS) 規則封鎖 Exchange ActiveSync 需要 tooprotect 存取 toothese 服務。
* **舊版通訊協定**。 您可以使用 AD FS 來封鎖舊版通訊協定。 這會封鎖存取 tooolder Office 用戶端，例如 Office 2013 現代化驗證已啟用，而舊版 Office。

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>使用 AD FS tooblock 舊版通訊協定
您可以使用下列範例中發行授權規則 tooblock 舊版通訊協定層級的存取 hello AD FS 的 hello。 從兩個常見的組態中進行選擇。

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>選項 1： 讓 Exchange ActiveSync，並允許將舊版應用程式，但僅 hello 內部網路
AD FS 信賴憑證者信任的 Microsoft Office 365 識別平台，Exchange ActiveSync 流量套用下列三個規則 toohello hello 和瀏覽器和新式驗證的流量，可以存取。 將舊版應用程式會從外部網路的 hello 遭到封鎖。

##### <a name="rule-1"></a>規則 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>規則 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>規則 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>選項 2︰允許 Exchange ActiveSync，並且封鎖舊版應用程式
AD FS 信賴憑證者信任的 Microsoft Office 365 識別平台，Exchange ActiveSync 流量套用下列三個規則 toohello hello 和瀏覽器和新式驗證的流量，可以存取。 來自任何位置的舊版應用程式會遭到封鎖。

##### <a name="rule-1"></a>規則 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>規則 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>規則 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>裝置型原則的支援瀏覽器 

您只能取得存取檢查的裝置原則的裝置相容性和網域加入 Azure AD 可以識別並驗證 hello 裝置時。 大部分的檢查，例如位置和 MFA 工作上大部分的裝置和瀏覽器，同時裝置原則需要 hello OS 版本與下面所列的瀏覽器。 當裝置原則已備妥，則會封鎖不受支援的瀏覽器或 hello 作業系統上的使用者存取。 

| 作業系統                     | 瀏覽器                 | 支援     |
| :--                    | :--                      | :-:         |
| Win 10                 | IE、Edge                 | ![勾選][1] |
| Win 10                 | Chrome                   | 預覽     |
| Win 8 / 8.1            | IE、Chrome               | ![勾選][1] |
| Win 7                  | IE、Chrome               | ![勾選][1] |
| iOS                    | Safari                   | ![勾選][1] |
| Android                | Chrome                   | ![勾選][1] |
| Windows Phone          | IE、Edge                 | ![勾選][1] |
| Windows Server 2016    | IE、Edge                 | ![勾選][1] |
| Windows Server 2016    | Chrome                   | 敬請期待 |
| Windows Server 2012 R2 | IE、Chrome               | ![勾選][1] |
| Windows Server 2008 R2 | IE、Chrome               | ![勾選][1] |
| Mac OS                 | Safari                   | ![勾選][1] |
| Mac OS                 | Chrome                   | 敬請期待 |

> [!NOTE]
> 如需 Chrome 支援，您必須使用 Windows 10 建立者更新並安裝到 hello 延伸模組[這裡](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)。
>
>

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


