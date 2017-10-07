---
title: "設定同盟單一登入非組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "解決部分 hello hello Azure AD 應用程式庫中設定同盟單一登入 tooyour 自訂 SAML 的應用程式未列出時，可能會遇到的常見問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>為不在資源庫內的應用程式設定同盟單一登入時遇到的問題

如果您在設定應用程式時遇到問題。 請確認您已依照 hello 文件中的所有 hello 步驟[設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫中。](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>無法加入 hello 應用程式的另一個執行個體

tooadd 應用程式的第二個執行個體，您需要 toobe 能夠：

-   設定 hello 第二個執行個體的唯一識別碼。 您必須能夠 tooconfigure hello 相同識別項用於 hello 第一個執行個體。

-   設定用於 hello 第一個執行個體的 hello 與不同的憑證。

如果 hello 應用程式不支援任何上述 hello。 然後，您必須能夠 tooconfigure 第二個執行個體。

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>其中將 hello EntityID （使用者識別碼） 格式的設定

您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。

Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。 如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 之下 NameIDPolicy，

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>其中從 Azure AD 取得 hello 應用程式中繼資料或憑證

toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**SAML 簽章憑證**區段，然後按一下 [**下載**資料行值。 根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。

Azure AD 不會提供 URL tooget hello 中繼資料。 hello 中繼資料，才能擷取為 XML 檔案。

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>不知道如何 toocustomize SAML 宣告傳送 tooan 應用程式

toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
