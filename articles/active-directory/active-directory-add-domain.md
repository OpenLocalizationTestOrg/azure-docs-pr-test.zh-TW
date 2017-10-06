---
title: "您的自訂網域名稱 tooAzure Active Directory 的 aaaAdd |Microsoft 文件"
description: "如何 tooadd 貴公司的網域名稱 tooAzure Active Directory 中，並 tooverify hello 網域名稱的方式。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>新增自訂網域名稱 tooAzure Active Directory
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-domains-add-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-add-domain.md)
> 
> 

您有一或多個網域名稱，您的組織使用 toodo 商務和使用者登入 tooyour 公司網路、 使用您的公司網域名稱。 您使用 Azure Active Directory (Azure AD)，您可以新增您公司網域名稱 tooAzure AD 以及。 這可讓您在 hello 目錄 tooassign 使用者名稱，是很熟悉 tooyour 的使用者，例如 'alice@contoso.com。 ' hello 程序很簡單：

1. 新增 hello 自訂網域名稱 tooyour 目錄
2. 在 hello 網域名稱註冊機構新增 hello 網域名稱的 DNS 項目
3. 在 Azure AD 中驗證 hello 自訂網域名稱

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 針對如何 tooadd 您公司的網域名稱在 hello Azure AD 系統管理中心，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-domains-add-azure-portal.md)。

如果您計劃 tooconfigure Active Directory Federation Services (AD FS) 或您公司網路上不同的安全性權杖服務 (STS) 搭配使用您的自訂網域名稱 toobe，請依照下列中的 hello 指示[新增和設定的網域與 Azure Active Directory 同盟](active-directory-add-domain-federated.md)。 如果您計畫 toosynchronize 使用者從您的公司目錄 tooAzure AD，這非常有用，[密碼雜湊同步](active-directory-aadconnectsync-implement-password-synchronization.md)不符合您需求。

## <a name="add-a-custom-domain-name-tooyour-directory"></a>新增自訂網域名稱 tooyour 目錄
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)的 Azure AD 目錄的全域系統管理員的使用者帳戶。
2. 在**Active Directory**，開啟您的目錄並選取 hello**網域**] 索引標籤。
3. 在 [hello 命令列中，選取 [**新增**。 輸入您的自訂網域，例如 'contoso.com' hello 名稱。 請務必 tooinclude hello.com、.net 或其他最上層的延伸模組，並將 hello 核取方塊的 「 單一登入 」 （同盟） 清除。
4. 選取 [新增] 。
5. 在 hello hello 新增網域精靈的第二個頁面上，取得 hello Azure AD 將會使用 tooverify 貴組織擁有 hello 自訂網域名稱的 DNS 項目。

既然您已經加入 hello 網域名稱，Azure AD 必須確認您的組織擁有 hello 網域名稱。 Azure AD 執行這項驗證之前，您必須在 hello hello 網域名稱的 DNS 區域檔案中新增 DNS 項目。 Hello hello 網域名稱的網域名稱註冊機構的網站上執行此工作。

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>在 hello hello 網域的網域名稱註冊機構新增 hello DNS 項目
hello 您的自訂網域名稱與 Azure AD 下一個步驟 toouse 是 tooupdate hello DNS 區域檔案中的 hello 網域。 這可讓 Azure AD tooverify 貴組織擁有 hello 自訂網域名稱。

1. 登入 toohello hello 網域的網域名稱註冊機構。 如果您沒有存取 tooupdate hello DNS 項目，請要求 hello 個人或團隊具有此存取 toocomplete 步驟 2 和 toolet 您知道它完成時。
2. 加入 Azure ad 的 hello DNS 項目提供 tooyou，以更新 hello hello 網域的 DNS 區域檔案。 這個 DNS 項目可讓 Azure AD tooverify hello 網域您擁有權。 hello DNS 項目不會變更任何行為，例如郵件路由或 web 裝載。

這個新增的 hello DNS 項目說明，請參閱[指示在常用的 DNS 註冊機構加入 DNS 項目](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>驗證 Azure AD 與 hello 網域名稱
一旦您加入 hello DNS 項目，您已準備好 tooverify hello 網域名稱與 Azure AD。

如果您仍然擁有 hello**新增網域**精靈開啟時，選取**確認**hello hello 精靈第三個頁面上。 當您選取**確認**，Azure AD 會尋找 hello hello hello 網域的 DNS 區域檔案中的 DNS 項目。 Hello DNS 記錄都已傳播後，只有 azure AD 可以確認 hello 網域名稱。 通常此傳播只需要幾秒鐘，但有時可能需要一個小時以上。 如果驗證無法運作 hello 第一次，再試一次。

如果 hello**新增網域**精靈沒有仍然開啟，您可以驗證在 hello hello 網域[Azure 傳統入口網站](https://manage.windowsazure.com/):

1. 使用屬於 Azure AD 目錄全域管理員的使用者帳戶進行登入。
2. 開啟您的目錄中，而且選取 hello**網域**] 索引標籤。
3. 選取 hello 網域名稱，tooverify，然後選取**確認**hello 命令列上。
4. 選取**確認**hello 對話方塊方塊 toocomplete hello 驗證作業。

現在您可以[指派包含自訂網域名稱的使用者名稱](active-directory-add-domain-add-users.md)。

## <a name="troubleshooting"></a>疑難排解
如果您無法驗證自訂網域名稱，請嘗試下列 hello。 我們將開始 hello 最常見且向 toohello 最常見工作。

1. **等候一小時**。 Azure AD 驗證 hello 網域之前 toopropagate 需要 DNS 記錄。 這可能需要一個小時以上。
2. **確定的 hello 輸入 DNS 記錄，並確認它是否正確**。 完成此步驟在 hello hello hello 網域的網域名稱註冊機構的網站。 Azure AD 無法驗證 hello 網域名稱，如果 hello DNS 項目不存在於 hello DNS 區域檔案，或如果不是完全相符 hello DNS 項目與 Azure AD 提供給您。 如果您沒有在 hello 網域名稱註冊機構的 hello 網域存取 tooupdate DNS 記錄，與 hello 人員或小組在您組織內具有此存取權，共用 hello DNS 項目，並要求他們 tooadd hello DNS 項目。
3. **從另一個目錄中刪除 hello 網域名稱，在 Azure AD 中**。 網域名稱只能在單一目錄中確認。 如果網域名稱先前在另一個目錄中確認過，則必須先在那裡將其刪除後，才可在新的目錄中確認。 刪除網域名稱的相關 toolearn 讀取[管理自訂網域名稱](active-directory-add-manage-domain-names.md)。

## <a name="add-more-custom-domain-names"></a>新增更多的自訂網域名稱
如果您的組織使用多個自訂網域名稱，例如 'contoso.com' 和 'contosobank.com'，您可以將其加入 tooa 最大值為 900 的網域名稱註冊。 使用的 hello 這個發行項 tooadd 每個網域名稱中的相同步驟。

## <a name="next-steps"></a>後續步驟
* [指派包含自訂網域名稱的使用者名稱](active-directory-add-domain-add-users.md)
* [管理自訂網域名稱](active-directory-add-manage-domain-names.md)
* [了解 Azure AD 中的網域管理概念](active-directory-add-domain-concepts.md)
* [在您的使用者登入時顯示公司的商標](active-directory-add-company-branding.md)
* [在 Azure AD 中使用 PowerShell toomanage 網域名稱](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

