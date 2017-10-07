---
title: "aaaHow toouse Azure Active Direcory 租用戶目錄概觀 |Microsoft 文件"
description: "說明什麼是 Azure AD 租用戶，以及如何 toomanage Azure 中使用 Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>管理 Azure AD 目錄

## <a name="what-is-an-azure-ad-tenant"></a>什麼是 Azure AD 租用戶？
在 Azure Active Directory (Azure AD) 中，租用戶是您組織在註冊 Microsoft 雲端服務 (例如 Azure 或 Office 365) 時所收到的專屬 Azure AD 目錄執行個體。 每個 Azure AD 目錄都不同，並與其他 Azure AD 目錄分開。 如同公司辦公大樓是安全資產的特定 tooonly 您的組織，Azure AD 目錄也已設計的 toobe 由您的組織使用的安全資產。 hello Azure AD 架構隔離客戶資料和識別資訊，讓使用者和一個 Azure AD 目錄的系統管理員無法意外或惡意存取其它目錄中的資料。

![管理 Azure Active Directory](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>如何取得 Azure AD 目錄？
Azure AD 提供 hello 核心目錄和身分識別管理功能的支援大部分的 Microsoft 雲端服務，包括：

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

註冊上述任何 Microsoft 雲端服務時，會收到 Azure AD 目錄。 您可以視需要建立額外的目錄。 例如，您可能會將第一個目錄維護為生產目錄，然後建立另一個目錄來進行測試或預備。

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>使用新的 Azure 訂用帳戶隨附 hello Azure AD 目錄

我們建議您使用 hello 時所使用的第一個服務註冊其他 Microsoft 服務的系統管理員帳戶。 歡迎您提供的資訊 hello 第一次您登入 Microsoft 服務是使用的 toocreate 新的 Azure AD 目錄執行個體，為您的組織。 如果您使用該目錄 tooauthenticate 登入嘗試訂閱 tooother Microsoft 服務時，他們可以使用現有的使用者帳戶、 原則、 設定或內部部署目錄整合，您的預設目錄中的 hello。

比方說，如果您簽署的 Microsoft Intune 訂閱，然後進一步同步處理您在內部部署 Active Directory 與 Azure AD 目錄，您可以註冊另一個 Microsoft 服務，例如 Office 365 並輕易地達成 hello 相同的目錄您必須使用 Microsoft Intune 的整合優點。

如需整合內部部署目錄與 Azure AD 的詳細資訊，請參閱[透過 Azure AD Connect 進行目錄整合](active-directory-aadconnect.md)。

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>關聯現有的 Azure AD 目錄與新的 Azure 訂用帳戶
您可以將新的 Azure 訂用帳戶與 hello 驗證現有 Office 365 或 Microsoft Intune 訂用帳戶的登入的相同目錄。 如需有關該狀況的詳細資訊，請參閱[的 Azure 訂用帳戶 tooanother 帳戶的擁有權轉移](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>以組織身分註冊 Microsoft 雲端服務來建立 Azure AD 目錄
如果您還沒有訂用帳戶 tooa Microsoft 雲端服務，您可以使用下列連結 toosign hello 的其中一個。 註冊第一項服務可自動建立 Azure AD 目錄。

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>如何 toochange hello 訂用帳戶的預設目錄

1. 登入 toohello [Azure 帳戶中心](https://account.windowsazure.com/Home/Index)為 hello hello 訂閱 tootransfer 訂用帳戶擁有權的帳戶管理員的帳戶。
2. 請確定您想 toobe hello 訂用帳戶擁有者為目標的 hello 目錄中的 hello 使用者。
3. 按一下 [移轉訂用帳戶]。
4. 指定 hello 收件者。 hello 收件者自動取得含有接受連結的電子郵件。
5. hello 收件者按一下 hello 連結，並遵循 hello 指示，包括輸入其付款資訊。 Hello 收件者成功時，會傳送 hello 訂用帳戶。 
6. hello hello 訂用帳戶的預設目錄變更 toohello hello 使用者的目錄是在 hello 訂用帳戶擁有權轉移是否成功。

### <a name="manage-hello-default-directory-in-azure"></a>管理在 Azure 中的 hello 預設目錄
當您註冊 Azure 時，預設 Azure AD 目錄會與您的訂用帳戶相關聯。 使用 Azure AD 不需要成本，而您的目錄為免費資源。 付費 Azure AD 服務會分開授權並提供其他功能 (例如登入時的公司商標和自助式密碼重設)。 您也可以建立自訂網域使用您自己的 DNS 名稱而非 hello 預設 *。 onmicrosoft.com 網域。

## <a name="how-can-i-manage-directory-data"></a>如何管理目錄資料？
tooadminister 其中一個或多個 Microsoft 雲端服務訂閱，您可以使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)、 hello Microsoft Intune 帳戶入口網站，或 hello [Office 365 系統管理中心](https://portal.office.com/)toomanage 您組織的目錄資料。 您也可以使用[Azure Active Directory PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/active-directory) toohelp 管理儲存在 Azure AD 中的資料。

從上述其中一個入口網站 (或 Cmdlet)，您可以：

* 建立和管理使用者和群組帳戶
* 管理您組織之訂用帳戶的相關雲端服務
* 設定與 Azure AD 身分識別和驗證服務的內部部署整合

hello Azure AD 系統管理中心、 Office 365 系統管理中心、 Microsoft Intune 帳戶入口網站和 Azure AD cmdlet hello 所有從讀寫 tooa 單一共用執行個體與貴組織的目錄相關聯的 Azure AD。 上述每個工具可做為提取或變更目錄資料的前端介面。

當您變更使用任一 hello 入口網站或 cmdlet 時的其中一個服務的 hello 內容下登入貴組織的資料時，hello 變更也會在顯示 hello 其他入口網站 hello 的下次您登入。 此資料是您訂閱 hello Microsoft 雲端服務 toowhich 之間共用的。

例如，如果您使用 hello Office 365 系統管理中心 tooblock 登入，將使用者的動作區塊 hello 使用者登入 tooany 其他服務 toowhich 貴組織目前訂閱。 如果您檢視 hello hello Microsoft Intune 帳戶入口網站中的相同使用者帳戶，您也會看到該 hello 使用者遭到封鎖。

## <a name="how-can-i-add-and-manage-multiple-directories"></a>如何新增和管理多個目錄？
您可以[hello Azure 入口網站中加入 Azure AD 目錄](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory)。 填寫 hello 資訊，然後選取**建立**。

您可以管理每個目錄當做完全獨立的資源：每個目錄都是對等、全功能且邏輯上與您所管理的其他目錄無關；目錄之間沒有任何父子關聯性。 目錄之間的這項獨立性包括資源獨立性、系統管理獨立性和同步處理獨立性。

* **資源獨立性**。 如果您建立或刪除一個目錄中的資源，它會在另一個目錄中，與 hello 外部使用者的部分例外狀況的任何資源沒有任何影響。 如果您搭配使用自訂網域 'contoso.com' 與某個目錄，則它不能與任何其他目錄搭配使用。
* **系統管理獨立性**。  如果不是 'Contoso' 目錄之系統管理員的使用者建立 'Test' 測試目錄，則：
  
  * hello 的 'Contoso' 目錄的系統管理員有沒有直接的系統管理權限 toodirectory 'Test'，除非 'Test' 的系統管理員特別授與這些權限。 'Contoso' 的系統管理員可以控制存取 toodirectory 'Test' 能藉由控制 hello 使用者帳戶的建立 'Test'。
    
  * 如果您指派或移除在一個目錄中，hello 變更使用者的系統管理員角色不會影響任何系統管理員角色的使用者有另一個目錄中。
* **同步處理獨立性**。 您可以設定每個 Azure AD 租用獨立 tooget 資料單一執行個體 hello Azure AD Connect 目錄同步作業工具從同步處理。

與其他 Azure 資源不同，您的目錄不是 Azure 訂用帳戶的子資源。 因此如果您取消，或允許您的 Azure 訂用帳戶 tooexpire，您仍然可以存取目錄資料，可使用 Azure AD PowerShell、 hello Azure Graph API 或其他介面，例如 hello Office 365 系統管理中心。 您也可以將其他訂用帳戶與 hello 目錄產生關聯。

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>如何 tooprepare toodelete Azure AD 目錄
全域管理員可以從 hello 入口網站刪除 Azure AD 目錄。 刪除目錄時，會一併刪除 hello 目錄中所包含的所有資源。 請確認，您不需要 hello 目錄然後再刪除它。

> [!NOTE]
> 如果 hello 使用者登入工作或學校帳戶，hello 使用者必須不嘗試 toodelete 其主目錄。 例如，如果 hello 使用者登入為joe@contoso.onmicrosoft.com，該使用者無法刪除具有預設網域為 contoso.onmicrosoft.com 的 hello 目錄。

Azure AD 需要某些條件是符合的 toodelete 目錄。 這樣可降低刪除目錄產生負面影響的使用者或應用程式，例如使用者 toosign 中 tooOffice 365 或 Azure 中的存取資源的 hello 能力的風險。 比方說，如果不小心刪除訂用帳戶的目錄，則使用者無法存取 hello 該訂用帳戶的 Azure 資源。

會檢查下列條件的 hello:

* hello 只有 hello 目錄中的使用者應該是 toodelete hello 目錄 hello 全域系統管理員。 必須先刪除任何其他使用者，才能刪除 hello 目錄。 如果同步處理使用者從內部部署，則同步處理，必須關閉，而且必須使用 hello 雲端目錄中刪除 hello 使用者 hello Azure 入口網站或 Azure PowerShell cmdlet。 沒有任何需求 toodelete 群組或連絡人，例如從 hello Office 365 系統管理中心新增連絡人。
* 可以在 hello 目錄中的任何應用程式。 必須先刪除任何應用程式，才能刪除 hello 目錄。
* 任何多因素驗證提供者可以不是連結的 toohello 目錄。
* 可以是任何訂用帳戶的任何 Microsoft 線上服務，例如 Microsoft Azure、 Office 365 或 Azure AD Premium 與 hello 目錄相關聯。 例如，在 Azure 中建立預設目錄時，如果您的 Azure 訂用帳戶仍然依賴此目錄來進行驗證，則無法刪除此目錄。 同樣地，如果另一位使用者擁有與目錄相關聯的訂用帳戶，您無法刪除目錄。 


## <a name="next-steps"></a>後續步驟
* [Azure AD 論壇](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Azure Multi-Factor Authentication 論壇](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Azure 問題的 Stack Overflow](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)
