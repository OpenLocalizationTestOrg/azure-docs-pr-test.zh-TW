---
title: "自訂網域 tooAzure AD aaaAdd |Microsoft 文件"
description: "說明如何 tooadd Azure Active Directory 中的自訂網域。"
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>快速入門： 新增自訂網域名稱 tooAzure Active Directory

每個 Azure AD 目錄隨附 hello 形式的初始網域名稱*domainname*。 onmicrosoft.com。 hello 初始網域名稱無法變更或刪除，但是您可以加入您公司網域名稱 tooAzure AD 以及。 例如，您的組織可能有其他網域名稱使用 toodo 商務和使用者登入使用您的公司網域名稱。 加入自訂網域名稱 tooAzure AD 可讓您在 hello 目錄 tooassign 使用者名稱，是很熟悉 tooyour 的使用者，例如 'alice@contoso.com。 ' 而不是 'alice@*<domain name>*.onmicrosoft.com'。 hello 程序很簡單：

1. 新增 hello 自訂網域名稱 tooyour 目錄
2. 在 hello 網域名稱註冊機構新增 hello 網域名稱的 DNS 項目
3. 在 Azure AD 中驗證 hello 自訂網域名稱

## <a name="add-your-custom-domain"></a>新增自訂網域
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. 在 hello***目錄名稱***刀鋒視窗中，選取**網域名稱**。
4. 在 hello ***目錄名稱*-網域名稱**刀鋒視窗中，選取 hello**新增**命令。
   
   ![選取 hello Add 命令](./media/active-directory-domains-add-azure-portal/add-command.png)
5. 在 hello**網域名稱**刀鋒視窗中，在 hello 方塊中，例如 'contoso.com'，輸入 hello 您的自訂網域名稱，然後選取**新增網域**。 為確定 tooinclude hello.com、.net 或其他最上層的延伸模組。
6. 在 hello***網域名稱***刀鋒視窗 （以您的自訂網域名稱在 hello 標題），取得您的組織擁有 hello 自訂網域名稱的 DNS 項目資訊 toouse tooverify hello。
   
   ![取得 DNS 項目資訊](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> 如果您計劃 toofederate 您在內部部署 Windows Server AD 與 Azure AD，則您需要 tooselect hello**我計劃 tooconfigure 這個網域的單一登入使用我的本機 Active Directory**核取方塊，當您執行 hello Azure AD Connect 工具toosynchronize 您的目錄。 您也需要 tooregister hello 相同的網域名稱，您選取與您的內部部署目錄中 hello 聯盟**Azure AD 網域**hello 精靈中的步驟。 您可以看到哪些該步驟中看起來像 hello 精靈[這些指示中](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)。 如果您沒有 hello Azure AD Connect 工具，您可以[在此處下載](http://go.microsoft.com/fwlink/?LinkId=615771)。

既然您已經加入 hello 網域名稱，Azure AD 必須確認您的組織擁有 hello 網域名稱。 Azure AD 執行這項驗證之前，您必須在 hello hello 網域名稱的 DNS 區域檔案中新增 DNS 項目。 Hello hello 網域名稱的網域名稱註冊機構的網站上執行此工作。

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>在 hello hello 網域的網域名稱註冊機構新增 hello DNS 項目
hello 您的自訂網域名稱與 Azure AD 下一個步驟 toouse 是 tooupdate hello DNS 區域檔案中的 hello 網域。 Azure AD 接著可確認您的組織擁有 hello 自訂網域名稱。

1. 登入 toohello hello 網域的網域名稱註冊機構。 如果您沒有存取 tooupdate hello DNS 項目，請要求 hello 個人或團隊具有此存取 toocomplete 步驟 2 和 toolet 您知道它完成時。
2. 加入 Azure ad 的 hello DNS 項目提供 tooyou，以更新 hello hello 網域的 DNS 區域檔案。 這個 DNS 項目可讓 Azure AD tooverify hello 網域您擁有權。 hello DNS 項目不會變更任何行為，例如郵件路由或 web 裝載。

這個新增的 hello DNS 項目說明，請參閱[指示在常用的 DNS 註冊機構加入 DNS 項目](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>驗證 Azure AD 與 hello 網域名稱
一旦您加入 hello DNS 項目，您已準備好 tooverify hello 網域名稱與 Azure AD。

Hello DNS 記錄都已傳播後，才可以驗證網域名稱。 通常此傳播只需要幾秒鐘，但有時可能需要一個小時以上。 如果驗證無法運作 hello 第一次，再試一次。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**瀏覽**，在 [hello] 文字方塊中，輸入使用者管理，然後選取**Enter**。
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. 在 hello**使用者管理的網域名稱**刀鋒視窗中，您想 tooverify 選取 hello 未經驗證的網域名稱。
4. 在 hello***網域名稱***刀鋒視窗 （也就是 hello 刀鋒視窗中開啟 hello 標題中具有新的網域名稱），選取**確認**toocomplete hello 驗證。

> [!TIP]
> 您可以加總 too900 自訂網域名稱，但只能有一個[設為您的 Azure AD 目錄的 hello 主要網域名稱](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory)用於依預設，當您建立新帳戶。

現在您可以建立雲端式使用者帳戶，或者使用您的自訂網域名稱，更新先前已同步處理的內部部署使用者帳戶資訊。 您也可以修改先前同步處理的使用者帳戶網域尾碼資訊使用[Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)或 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)。

## <a name="troubleshooting"></a>疑難排解
如果您無法驗證自訂網域名稱，請嘗試下列疑難排解步驟的 hello:

1. **等候一小時**。 Azure AD 驗證 hello 網域之前 toopropagate 需要 DNS 記錄。 這可能需要一個小時以上。
2. **確定的 hello 輸入 DNS 記錄，並確認它是否正確**。 完成此步驟在 hello hello hello 網域的網域名稱註冊機構的網站。 Azure AD 無法驗證 hello 網域名稱，如果 hello DNS 項目不存在於 hello DNS 區域檔案，或如果不是完全相符 hello DNS 項目與 Azure AD 提供給您。 如果您沒有在 hello 網域名稱註冊機構的 hello 網域存取 tooupdate DNS 記錄，與 hello 人員或小組在您組織內具有此存取權，共用 hello DNS 項目，並要求他們 tooadd hello DNS 項目。
3. **從另一個目錄中刪除 hello 網域名稱，在 Azure AD 中**。 網域名稱只能在單一目錄中確認。 如果網域名稱先前在另一個目錄中確認過，則必須先在那裡將其刪除後，才可在新的目錄中確認。 刪除網域名稱的相關 toolearn 讀取[管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)。    

## <a name="add-more-custom-domain-names"></a>新增更多的自訂網域名稱
如果您的組織使用多個自訂網域名稱，例如 'contoso.com' 和 'contosobank.com'，您可以加總 too900 更藉由每個重複本文中的 hello 步驟。

### <a name="learn-more"></a>詳細資訊
[Azure AD 中自訂網域名稱的概念式概觀](active-directory-add-domain-concepts.md)

[管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>後續步驟
本快速入門中，您學到如何 tooadd 自訂網域 tooAzure AD。 

您可以使用 hello hello Azure 入口網站中的下列 Azure AD 中的連結 tooadd 新的自訂網域。

> [!div class="nextstepaction"]
> [新增自訂網域](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 