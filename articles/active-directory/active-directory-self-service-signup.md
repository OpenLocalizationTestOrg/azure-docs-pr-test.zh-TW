---
title: "aaaWhat 是 Azure 的自助註冊？ | Microsoft Docs"
description: "概觀自助式註冊 azure，toomanage hello 註冊程序，以及如何 tootake 透過 DNS 網域名稱。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>什麼是 Azure 的自助式註冊？
本主題說明 hello 自助式註冊程序和如何 tootake 透過 DNS 網域名稱。  

## <a name="why-use-self-service-signup"></a>為何使用自助式註冊？
* 取得客戶 tooservices 他們想要更快。
* 建立服務的電子郵件型供應項目。
* 建立快速允許使用者使用其容易記住的工作電子郵件別名的 toocreate 身分識別的電子郵件型註冊流程。
* 未受管理的 Azure 目錄後來可以轉換成受管理的目錄，並重複用於其他服務。

## <a name="terms-and-definitions"></a>詞彙和定義
* **自助式註冊**： 這是程式的使用者註冊的雲端服務，並將具有 Azure Active Directory (Azure AD) 中自動建立它們的身分識別根據他們的電子郵件網域的 hello 方法。
* **未受管理的 Azure 目錄**： 這是該身分識別建立所在的 hello 目錄。 未受管理的目錄是沒有全域管理員的目錄。
* **電子郵件驗證的使用者**：這是 Azure AD 中的使用者帳戶類型。 在註冊自助式供應項目後自動建立身分識別的使用者，就是所謂的電子郵件驗證的使用者。 電子郵件驗證的使用者是加上 creationmethod=EmailVerified 標記之目錄的一般成員。

## <a name="user-experience"></a>使用者體驗
例如，假設電子郵件為 Dan@BellowsCollege.com 的使用者會透過電子郵件接收機密檔案。 hello 檔案已受 Azure Rights Management (Azure RMS)。 但是 Dan 的組織 (Bellows College) 尚未註冊 Azure RMS，也未部署 Active Directory RMS。 在此情況下，Dan 可以申請免費訂用帳戶 tooRMS 順序 tooread hello 受保護的檔案中的個人。

如果 Dan hello 第一位使用者與此供應項目的自助註冊 BellowsCollege.com toosign 從電子郵件地址，然後未受管理的目錄將會建立 BellowsCollege.com 在 Azure AD 中。 如果來自 hello BellowsCollege.com 網域的其他使用者註冊此供應項目或類似的自助服務供應項目，它們也會具有電子郵件驗證建立的使用者帳戶在 hello 相同 unmanaged 在 Azure 中的目錄。

## <a name="admin-experience"></a>管理員體驗
擁有 hello DNS 網域名稱未受管理的 Azure 目錄的系統管理員可以接管或合併 hello 目錄之後證明擁有權。 hello 以下幾節說明 hello 系統管理員體驗的詳細資料，但是摘要如下：

* 當您接管的未受管理的 Azure 目錄時，您只需變得 hello hello unmanaged 目錄全域管理員。 這有時候稱為內部接管。
* 當合併未受管理的 Azure 目錄，您將 hello unmanaged 的目錄 tooyour managed Azure 目錄的 hello DNS 網域名稱和使用者資源的對應會建立讓使用者可以繼續 tooaccess 服務不中斷。 這有時候稱為外部接管。

## <a name="what-gets-created-in-azure-active-directory"></a>Azure Active Directory 中建立的項目為何？
#### <a name="directory"></a>目錄
* Hello 網域的 Azure Active Directory 目錄會建立一個目錄，每個網域。
* hello Azure AD 目錄中有任何全域管理員。

#### <a name="users"></a>使用者
* 每個使用者註冊，使用者物件建立 hello Azure AD 目錄中。
* 每個使用者物件都標示為外部。
* 每個使用者可以註冊這些簽署存取 toohello 服務。

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>如何針對我擁有的網域宣告自助式 Azure AD 目錄？
您可以執行網域驗證來宣告自助式 Azure AD 目錄。 網域驗證證明您自己的 hello 網域建立 DNS 記錄。

有兩種方式 toodo DNS 接管的 Azure AD 目錄：

* 內部接管 （管理探索未受管理的 Azure 目錄，以及想 tooturn 到受管理的目錄）
* 外部接管 （系統管理員會嘗試 tooadd 到新網域 tootheir 受管理的 Azure 目錄）

您可能會想要驗證您擁有網域，因為在使用者執行自助式註冊，或您可能會加入新網域 tooan 現有受管理的目錄之後，您就可以透過未受管理的目錄。 例如，您有名稱為 contoso.com 的網域，而且您想 tooadd contoso.co.uk 或 contoso.uk 命名新的網域。

## <a name="what-is-domain-takeover"></a>什麼是網域接管？
本章節涵蓋如何您擁有網域 toovalidate

### <a name="what-is-domain-validation-and-why-is-it-used"></a>什麼是網域驗證，以及為何使用？
在訂單 tooperform 作業在目錄中，Azure AD 會要求您驗證 hello DNS 網域的擁有權。  Hello 網域的驗證可讓您 tooclaim hello 目錄，然後升級 hello 自助目錄 tooa 管理的目錄，或合併 hello 自助服務目錄中的現有受管理的目錄。

## <a name="examples-of-domain-validation"></a>網域驗證範例
有兩種方式 toodo DNS 接管的目錄：

* 內部接管 （例如，可探索自助服務、 未受管理的目錄，而且想 tooturn 到受管理的目錄系統管理員）
* 外部接管 （例如，系統管理員會嘗試 tooadd 新網域 tooa 受管理的目錄）

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>內部接管-升級自助服務、 未受管理的目錄 toobe 受管理的目錄
當您進行內部接管時，取得會從 unmanaged 的目錄 tooa 管理目錄轉換 hello 目錄。 您需要 toocomplete DNS 網域名稱驗證，其中 hello DNS 區域中建立 MX 記錄或 TXT 記錄。 該動作：

* 驗證您擁有 hello 網域
* 可讓受管理的 hello 目錄
* 可讓您 hello hello 目錄的全域管理員

讓我們假設您的 IT 系統管理員身分從波紋管大學探索 hello 學校的使用者已註冊為自助服務供應項目。 Hello 註冊 hello DNS 的擁有者名稱 BellowsCollege.com、 hello IT 系統管理員可以驗證在 Azure 中的 hello DNS 名稱的擁有權，並再 hello 未受管理的目錄。 hello 目錄就會變成受管理的目錄，而且 hello IT 系統管理員指派 hello hello BellowsCollege.com 目錄的全域管理員角色。

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>外部接管 - 將自助式目錄合併到現有的受管理目錄
在外部的接管您已經有受管理的目錄和您想要所有使用者和群組從受管理的目錄中，未受管理的目錄 toojoin 而自己的兩個不同的目錄。

身為系統管理員的受管理的目錄中，您將加入網域，而且該網域剛好 toohave unmanaged 與它相關聯的目錄。

例如，假設您是 IT 系統管理員，而且您已經擁有的受管理的目錄，對 Contoso.com 是已註冊的 tooyour 組織的網域名稱。 您會發現貴組織的使用者已使用電子郵件網域名稱 user@contoso.co.uk (這是貴組織擁有的另一個網域名稱) 以自助方式註冊產品方案。 這些使用者目前在 contoso.co.uk 的未受管理目錄中有帳戶。

您不想 toomanage 兩個個別目錄，因此 contoso.co.uk hello unmanaged 的目錄合併到現有的受管理的 IT 目錄 contoso.com。

外部接管如下所示 hello 相同內部接管的 DNS 驗證程序。  正在執行的差異： 使用者和服務會重新對應的 toohello IT 管理的目錄。

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>執行外部接管 hello 影響為何？
透過外部的接管使用者為資源的對應會建立讓使用者可以繼續 tooaccess 服務不中斷。 許多應用程式，包括個人版，RMS，處理 hello 對應使用者的資源，而且使用者可以繼續 tooaccess 而不需要變更這些服務。 如果應用程式不會有效地處理 hello 對應的使用者-資源、 外部接管可能會明確封鎖的 tooprevent 使用者不佳的體驗。

#### <a name="directory-takeover-support-by-service"></a>服務支援的目錄接管
目前 hello 下列服務支援接管：

* RMS

下列服務的 hello 將很快就會支援接管：

* PowerBI

hello 下列外部接管之後需要額外的管理動作 toomigrate 使用者資料，並不相符。

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>如何 tooperform DNS 網域名稱接管
您有幾個選項，供 tooperform 網域驗證 （和執行接管，如果您想）：

1. Azure 管理入口網站

   接管是由執行網域新增所觸發。  如果目錄已經存在 hello 網域，您將有 hello 選項 tooperform 外部接管。

   登入 toohello Azure 入口網站使用您的認證。  瀏覽 tooyour 現有目錄，然後太**新增網域**。
2. Office 365

   您可以使用 hello hello 選項[管理網域](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/)Office 365 toowork 與您的網域和 DNS 記錄中的頁面。 請參閱 [在 Office 365 中驗證您的網域](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)。
3. Windows PowerShell

   hello 步驟是必要的 tooperform 驗證，使用 Windows PowerShell。

   | 步驟 | Cmdlet toouse |
   | --- | --- |
   | 建立認證物件 |Get-Credential |
   | 連接 tooAzure AD |Connect-MsolService |
   | 取得網域清單 |Get-MsolDomain |
   | 建立挑戰 |Get-MsolDomainVerificationDns |
   | 建立 DNS 記錄 |在您的 DNS 伺服器上執行這項操作 |
   | 確認 hello 挑戰 |Confirm-MsolEmailVerifiedDomain |

例如：

1. 連接 tooAzure AD 使用 hello 認證所使用的 toorespond toohello 自助服務供應項目：

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. 取得網域清單：

    Get-MsolDomain
3. 然後執行 hello Get-msoldomainverificationdns cmdlet toocreate 一項挑戰：

    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord

    例如：

    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
4. 複製此命令會傳回 hello 值 （hello 挑戰）。

    例如：

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. 在公用 DNS 命名空間，建立 DNS txt 記錄，其中包含您在 hello 上一個步驟中複製的 hello 值。

    這個記錄的 hello 名稱是 hello hello 父系網域的名稱，因此如果您使用 Windows 伺服器 hello DNS 角色建立此資源記錄，將 hello 記錄名稱保留空白，而且只要 hello 值貼到 [hello] 文字方塊中
6. 執行 hello Confirm-msoldomain cmdlet tooverify hello 挑戰：

    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*

    例如：

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

成功挑戰會傳回 toohello 提示字元，且未產生錯誤。

## <a name="how-do-i-control-self-service-settings"></a>如何控制自助式設定？
系統管理員目前有兩個自助式控制項。 可以控制：

* 是否使用者可以加入 hello 目錄，透過電子郵件。
* 使用者是否可以自行授權應用程式和服務。

### <a name="how-can-i-control-these-capabilities"></a>如何控制這些功能？
系統管理員可以使用下列 Azure AD Cmdlet Set-MsolCompanySettings 參數設定這些功能：

* **AllowEmailVerifiedUsers** 控制使用者是否可以建立或加入未受管理的目錄。 如果您將該參數太 $false，則沒有電子郵件驗證的使用者可以加入 hello 目錄。
* **AllowAdHocSubscriptions**控制 hello tooperform 自助登入使用者的能力。 如果您將該參數太 $false，沒有任何使用者可以執行自助式註冊。

### <a name="how-do-hello-controls-work-together"></a>Hello 控制項如何一起？
這兩個參數可以用於搭配 toodefine 更精確地控制自助登入。 比方說，下列命令的 hello 可讓使用者 tooperform 自助式註冊，但僅限於如果這些使用者已經有 Azure AD 的帳戶 （亦即，使用者必須建立電子郵件驗證帳戶 toobe 無法將自助登執行向上）：

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

hello 以下流程圖說明對這些參數的 hello 不同組合與 hello 產生條件 hello 目錄和自助式註冊。

![][1]

如需詳細資訊和範例的方式 toouse 這些參數，請參閱[Set-msolcompanysettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)。

## <a name="see-also"></a>另請參閱
* [如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet 參考](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
