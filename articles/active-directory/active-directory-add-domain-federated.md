---
title: "aaaAdd 您的自訂網域名稱和同盟登入 tooAzure Active Directory 設定 |Microsoft 文件"
description: "如何 tooadd 貴公司的網域名稱 tooAzure 組成同盟登入 Azure Active Directory 與您在內部部署的同盟解決方案之間的 Active Directory tooset"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>加入您的自訂網域名稱 tooAzure Active Directory
您可以設定自訂網域名稱，例如 'contoso.com'，如此 contoso.com 中的使用者可以從您的公司網路進行同盟單一登入。 如果您已經有 Active Directory Federation Services (AD FS) 或您的公司網路上執行的不同同盟伺服器，您可以設定 Azure AD toouse 使用 hello Azure AD Connect 工具自訂網域名稱。 您也可以使用 Azure AD Connect toodeploy 新的 AD FS 環境，並設定的同盟單一登入 tooAzure AD。

如果您不需要而且不打算 toodeploy AD FS 或另一部同盟伺服器，請遵循這些指示：[新增自訂網域名稱 tooAzure Active Directory](active-directory-add-domain.md)。

## <a name="add-a-custom-domain-name-tooyour-directory"></a>新增自訂網域名稱 tooyour 目錄
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)的 Azure AD 目錄的全域系統管理員的使用者帳戶。
2. 在**Active Directory**，開啟您的目錄並選取 hello**網域** 索引標籤。
3. 在 hello 命令列中，選取 **新增**，然後輸入 hello 您的自訂網域名稱，例如 'contoso.com'。 為確定 tooinclude hello.com、.net 或其他最上層的延伸模組。
4. 選取 hello**我計劃 tooconfigure 這個網域的單一登入使用我的本機 Active Directory**核取方塊。
5. 選取 [新增] 。

Azure AD 執行 hello Azure AD Connect 工具 tooget hello DNS 項目將會使用 tooverify hello 網域。 您會看到 hello DNS 項目在 hello **Azure AD 網域**hello 精靈中的步驟。 您可以看到哪些該步驟中看起來像 hello 精靈[這些指示中](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)。 如果您沒有 hello Azure AD Connect 工具，您可以[在此處下載](http://go.microsoft.com/fwlink/?LinkId=615771)。

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>在 hello hello 網域的網域名稱註冊機構新增 hello DNS 項目
hello 您的自訂網域名稱與 Azure AD 下一個步驟 toouse 是 tooupdate hello DNS 區域檔案中的 hello 網域。 這可讓 Azure AD tooverify 貴組織擁有 hello 自訂網域名稱。

1. 登入您的網域名稱的網域名稱註冊機構的 toohello 網站。 如果您沒有存取 toodo 這，要求 hello 個人或小組在您的組織內具有此存取 toocomplete 步驟 2 以及 toolet 您知道何時完成。
2. 加入 Azure ad 的 hello DNS 項目提供 tooyou，以更新 hello hello 網域的 DNS 區域檔案。 這個 DNS 項目可讓 Azure AD tooverify hello 網域您擁有權。 hello DNS 項目不會變更任何行為，例如郵件路由或 web 裝載。

如需此步驟的說明，請參閱 [在常用 DNS 註冊機構新增 DNS 項目的指示](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>驗證 Azure AD 與 hello 網域名稱
一旦您加入 hello DNS 項目，您已準備好 tooverify hello 網域名稱與 Azure AD。

tooverify hello 網域中，選取**下一步**上 hello **Azure AD 網域**hello Azure AD Connect 精靈 的步驟。 Azure AD 會尋找 hello hello hello 網域的 DNS 區域檔案中的 DNS 項目。 Azure AD 只能驗證 hello 網域名稱，一旦 hello DNS 記錄都已傳播。 通常傳播只需要幾秒鐘，但有時可能需要一個小時以上。 如果驗證無法運作 hello 第一次，再試一次。

Hello 剩餘 hello Azure AD Connect 精靈 中的步驟，然後再繼續。 這會同步處理您的 Windows Server AD tooAzure AD 使用者。 同步處理設定為同盟的 hello 網域中的使用者將能夠 tooget 同盟單一登入體驗，從您的公司網路 tooAzure AD。

## <a name="troubleshooting"></a>疑難排解
如果您無法驗證自訂網域名稱，請嘗試下列 hello。 我們將開始 hello 最常見且向 toohello 最常見工作。

1. **等候一小時**。 Azure AD 驗證 hello 網域之前 toopropagate 需要 DNS 記錄。 這可能需要一個小時以上。
2. **確定的 hello 輸入 DNS 記錄，並確認它是否正確**。 完成此步驟在 hello hello hello 網域的網域名稱註冊機構的網站。 Azure AD 無法驗證 hello 網域名稱，如果 hello DNS 項目不存在於 hello DNS 區域檔案，或如果不是完全相符 hello DNS 項目與 Azure AD 提供給您。 如果您沒有在 hello 網域名稱註冊機構的 hello 網域存取 tooupdate DNS 記錄，與 hello 人員或小組在您組織內具有此存取權，共用 hello DNS 項目，並要求他們 tooadd hello DNS 項目。
3. **從另一個目錄中刪除 hello 網域名稱，在 Azure AD 中**。 網域名稱只能在單一目錄中確認。 如果網域名稱先前在另一個目錄中確認過，則必須先在那裡將其刪除後，才可在新的目錄中確認。 刪除網域名稱的相關 toolearn 讀取[管理自訂網域名稱](active-directory-add-manage-domain-names.md)。

## <a name="add-more-custom-domain-names"></a>新增更多的自訂網域名稱
如果您的組織使用多個自訂網域名稱，例如 'contoso.com' 和 'contosobank.com'，您可以將其加入 tooa 最大值為 900 的網域名稱註冊。 使用的 hello 這個發行項 tooadd 每個網域名稱中的相同步驟。

## <a name="next-steps"></a>後續步驟
* [管理自訂網域名稱](active-directory-add-manage-domain-names.md)
* [了解 Azure AD 中的網域管理概念](active-directory-add-domain-concepts.md)
* [在您的使用者登入時顯示公司的商標](active-directory-add-company-branding.md)
* [在 Azure AD 中使用 PowerShell toomanage 網域名稱](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

