---
title: "Active Directory 條件式存取 aaaAzure |Microsoft 文件"
description: "使用條件式存取控制在 Azure Active Directory toocheck 特定條件的存取 tooapplications 驗證時。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Azure Active Directory 中的條件式存取

在行動裝置-首先，雲端優先世界中，Azure Active Directory 可讓單一登入 toodevices、 應用程式和服務從任何地方。 關閉公司網路中，可以使用的裝置 （包括 BYOD） 的 hello 激增，和第 3 個合作對象 SaaS 應用程式，IT 專業人員正面臨著逼近對方的兩個目標：

- 無論在何處，每當加持 hello 使用者 toobe 生產力
- 在任何階段保護 hello 公司資產

tooimprove 產能，Azure Active Directory 提供您廣泛的選項 tooaccess 的使用者，您公司的資產。 應用程式存取管理，與 Azure Active Directory 可讓您只 tooensure *hello 適當人員*可以存取您的應用程式。 如果您想 toohave 更充分掌控 hello 適當人員如何存取您在某些情況下的資源嗎？ 如果您即使有的條件下您想要 tooblock 存取 toocertain 應用程式甚至 hello*人以滑鼠右鍵*嗎？ 比方說，如果可能很確定為您 hello 適當人員要從受信任的網路; 存取特定應用程式不過，您可能不希望他們 tooaccess 這些應用程式從您不信任的網路。 您可以使用條件式存取解決這些問題。

條件式存取是 Azure Active directory，可讓您根據特定條件在環境中的 hello 存取 tooapps tooenforce 控制項的功能。 使用的控制項，可以是連接的其他需求 toohello 存取，或您可以封鎖它。 條件式存取的 hello 實作是以原則為基礎。 以原則為基礎的方法可簡化設定經驗，因為它會依照您的想法存取需求的 hello 方式。  

一般而言，您會定義您使用 hello 遵循模式為基礎的陳述式的存取需求：

![控制](./media/active-directory-conditional-access-azure-portal/10.png)

當您取代 hello 兩個 「*這*」 以真實世界的詳細資訊，您有可能已經很熟悉 tooyou 的原則陳述式的範例：

*當約聘人員嘗試 tooaccess 我們的雲端應用程式，從位於不受信任的網路時，然後封鎖存取。*

上面的 hello 原則陳述式會反白顯示 hello 電源條件式存取。 雖然您可以啟用約聘人員 toobasically 存取雲端應用程式 (**人員**)，使用條件式存取，您也可以定義在哪一個 hello 存取就可以使用條件 (**如何**)。

Azure Active Directory 條件式存取，hello 內容中

- "**When this happens**" 稱為**條件陳述式**
- "**Then do this**" 成為**控制項**

![控制](./media/active-directory-conditional-access-azure-portal/11.png)

條件陳述式與您的控制項的 hello 組合代表條件式存取原則。

![控制](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>控制

在條件式存取原則中，控制項定義滿足條件陳述式時所應發生的狀況。  
利用控制項，您可以封鎖存取，或允許有額外需求的存取。
當您設定的原則允許存取時，您需要 tooselect 至少一項需求。   

### <a name="grant-controls"></a>授與控制
hello 目前的 Azure Active Directory 的實作可讓您 tooconfigure hello 遵循授與控制需求：

![控制](./media/active-directory-conditional-access-azure-portal/05.png)

- **Multi-Factor Authentication** - 您可以透過 Multi-Factor Authentication 來要求增強式驗證。 身為提供者，您可以使用 Azure Multi-Factor Authentication，或使用結合 Active Directory Federation Services (AD FS) 的內部部署多重要素驗證提供者。 使用多因素驗證，可協助防止未經授權的使用者，可能會獲得了存取 toohello 認證是有效的使用者所存取資源。

- **相容的裝置**-您可以在 hello 裝置層級設定條件式存取原則。 您可以設定相容，原則 tooonly 啟用電腦或行動裝置的行動裝置管理 tooaccess 中註冊您的組織資源。 比方說，您可以使用 Intune toocheck 裝置相容性，並再回報 tooAzure 強制 AD hello 使用者嘗試 tooaccess 應用程式時。 如需如何 toouse Intune tooprotect 應用程式和資料，請參閱詳細指引[使用 Microsoft Intune 保護應用程式和資料](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune)。 您也可以使用 Intune tooenforce 資料保護遺失或遭竊的裝置。 如需詳細資訊，請參閱 [使用 Microsoft Intune 搭配完整或選擇性抹除協助保護您的資料](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)。

- **已加入網域裝置**– 您可以要求您已經使用 tooconnect tooAzure Active Directory toobe 已加入網域的 tooyour hello 裝置內部部署 Active Directory (AD)。 此原則適用於 tooWindows 桌上型電腦、 膝上型電腦和企業平板電腦。 

如果您選取多個控制項，也可以設定在處理您的原則時是否全都為必要。

![控制](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>工作階段控制項
工作階段控制項可讓您限制雲端應用程式內的體驗。 hello 工作階段控制項強制執行的雲端應用程式，而且依賴 hello 工作階段的相關的 Azure AD toohello 應用程式所提供的其他資訊。

![控制](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>使用應用程式強制執行限制
您可以使用此控制 toorequire Azure AD toopass hello 裝置資訊 toohello 雲端應用程式。 這有助於 hello 知道如果 hello 使用者來自相容的裝置或已加入網域裝置的雲端應用程式。 此控制項是目前僅支援 SharePoint 當做 hello 雲端應用程式。 SharePoint 會使用 hello 裝置資訊 tooprovide 使用者有限或完整的經驗視 hello 裝置狀態而定。
深入了解如何 toorequire 限制存取 SharePoint toolearn 移[這裡](https://aka.ms/spolimitedaccessdocs)。

## <a name="condition-statement"></a>條件陳述式

hello 上一節介紹了 toosupported 選項 tooblock 或限制存取 tooyour 資源中表單的控制項。 在條件式存取原則中，您可以定義 hello 準則，針對您在條件陳述式的格式中套用的控制項 toobe toobe 符合。  

您可以包含下列工作分派到您的條件陳述式的 hello:

![控制](./media/active-directory-conditional-access-azure-portal/07.png)


- **誰**-要在許多情況下，您的控制項 toobe 套用 tooa 特定一組使用者。 條件陳述式中您可以選取 hello 使用者和群組原則套用至定義這個集合。 如有必要，您也可以明確豁免一組使用者，進行從您的原則中排除這些使用者。  
選取使用者和群組，您可以定義您的原則套用至使用者 hello 範圍。    

    ![控制](./media/active-directory-conditional-access-azure-portal/08.png)



- **什麼** - 從保護的觀點而言，有些在您的環境中執行的應用程式通常需要更多關注 (相較於其他應用程式)。 這會影響，例如，具有存取 toosensitive 資料應用程式。
藉由選取的雲端應用程式，您可以定義您的原則套用至雲端應用程式 hello 範圍。 如有必要，您也可以從您的原則中明確排除一組應用程式。

    ![控制](./media/active-directory-conditional-access-azure-portal/09.png)


- **如何**-只要存取 tooyour 應用程式會在您可以控制，不需要諸額外的控制項上如何雲端應用程式存取您的使用者有可能的情況下執行。 不過，畫面可能看起來不同，如果存取 tooyour 雲端應用程式執行時，比方說，不受信任的網路或不相容的裝置。 在條件陳述式中，您可以定義特定存取條件會有存取 tooyour 應用程式的執行方式的其他需求。

    ![條件](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>條件

在 hello 目前實作中的 Azure Active Directory，您可以定義下列區域的 hello 的條件：

- 登入風險
- 裝置平台
- 位置
- 用戶端應用程式

![條件](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>登入風險

登入的風險是物件，可由 Azure Active Directory tootrack hello 可能性 hello 合法的使用者帳戶擁有者未執行的登入嘗試。 此物件，在 hello 可能性 （高、 中或低） 會儲存在表單的屬性稱為[登入風險層級](active-directory-reporting-risk-events.md#risk-level)。 如果 Azure Active Directory 偵測到登入風險，則會在使用者登入期間產生此物件。 如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。  
您可以使用計算的 hello 登入風險層級做為條件式存取原則中的條件。 

![條件](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>裝置平台

hello 您裝置執行作業系統的特點在於 hello 裝置平台：

- Android
- iOS
- Windows Phone
- Windows
- macOS (預覽)。 

![條件](./media/active-directory-conditional-access-azure-portal/02.png)

您可以定義包含會豁免原則的裝置平台以及 hello 裝置平台。  
toouse hello 原則中的裝置平台，第一個變更 hello 設定切換太**是**，然後選取所有或個別的裝置平台 hello 原則會套用至。 如果您選取個別的裝置平台，hello 原則會在這些平台上有只影響。 在此情況下，登入 tooother 支援平台不會受到 hello 原則。


### <a name="locations"></a>位置

hello 位置識別 hello hello 用戶端的 IP 位址，您已使用 tooconnect tooAzure Active Directory。 這種情況需要您熟悉 toobe**名為位置**和**MFA 可信任 Ip**。  

**名為位置**是 Azure Active Directory 可讓您的組織中的 toolabel 受信任的 IP 位址範圍的功能。 在您的環境，您可以使用具名的位置 hello 內容中的 hello 偵測[風險事件](active-directory-reporting-risk-events.md)以及條件式存取。 如需有關在 Azure Active Directory 中設定具名位置的詳細資訊，請參閱 [Azure Active Directory 中的具名位置](active-directory-named-locations.md)。

在 Azure AD 中位置可以設定的 hello 數目受到 hello hello 相關物件的大小。 您可以設定：
 
 - 其中一個名為向上 too500 IP 範圍的位置
 - 使用其中一個 IP 範圍指派 tooeach 最多 60 具名位置 （預覽） 


**MFA 可信任 Ip**是一項功能可讓您 toodefine 受信任的 IP 位址範圍代表您組織的近端內部網路的多重要素驗證。 當您設定位置條件時，信任的 Ip 可讓您 toodistinguish 之間進行從您的組織網路和所有其他位置的連線。 如需詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。  



您可以包含所有位置或所有信任的 IP，也可以排除所有信任的 IP。

![條件](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>用戶端應用程式

hello 用戶端應用程式可以是泛型的層級 hello 的應用程式的網頁瀏覽器、 行動裝置應用程式 （桌面用戶端） 上使用 tooconnect tooAzure Active Directory 或您可以明確選取 Exchange Active Sync。  
舊有的驗證是指 tooclients 使用基本驗證，例如不使用新式驗證的舊版 Office 用戶端。 舊式驗證目前不支援條件式存取。

![條件](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>常見案例

### <a name="requiring-multi-factor-authentication-for-apps"></a>應用程式需要 Multi-Factor Authentication

許多環境中有其他人需要比 hello 較高的保護層級的應用程式。
這種，例如 hello 擁有存取 toosensitive 資料的應用程式。
如果您想 tooadd 另一層保護 toothese 應用程式，您可以設定條件式存取原則，當使用者同時存取這些應用程式要求多重要素驗證。


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>從不受信任的網路存取時需要 Multi-Factor Authentication

此案例中是類似 toohello 前一個案例，因為它會增加多因素驗證的需求。
不過，hello 主要差異是這項需求的 hello 條件。  
當應用程式存取 toosensitve 資料與已 hello 焦點的 hello 前一個案例時，這種情況的 hello 焦點是受信任的位置。  
換句話說，如果使用者從您不信任的網路存取應用程式，您可能需要 Multi-Factor Authentication。


### <a name="only-trusted-devices-can-access-office-365-services"></a>只有受信任的裝置可以存取 Office 365 服務

如果您使用 Intune 在您的環境中，您可以立即開始使用 hello Azure 主控台中的 hello 條件式存取原則介面。

許多 Intune 客戶使用條件式存取 tooensure 只有受信任的裝置才可以存取 Office 365 服務。 這表示，行動裝置向 Intune 註冊並符合相容性原則的需求，Windows 電腦會聯結的 tooan 在內部部署網域。 重要的改進是，您不需要 tooset hello hello Office 365 服務的每個相同的原則。  當您建立新的原則時，設定 hello 雲端應用程式 tooinclude 每個您想使用 tooprotect 使用條件式存取的 hello O365 應用程式。

## <a name="next-steps"></a>後續步驟

如果您想如何 tooconfigure 條件式存取原則，請參閱的 tooknow[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。

如果您針對您的環境準備好 tooconfigure 條件式存取原則，請參閱 hello [Azure Active Directory 中的條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。 
