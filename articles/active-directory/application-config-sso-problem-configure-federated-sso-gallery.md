---
title: "設定同盟單一登入 Azure AD 庫應用程式的 aaaProblem |Microsoft 文件"
description: "解決部分 hello 常見的問題，您可能會遇到當設定同盟單一登入使用 SAML hello Azure AD 應用程式庫中所列的應用程式"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>為 Azure AD 資源庫應用程式設定同盟單一登入時遇到的問題

如果您在設定應用程式時遇到問題。 請確認您已依照 hello 應用程式的 hello 教學課程中的 hello 的所有步驟。 在 hello 應用程式組態中，您必須上如何 tooconfigure hello 應用程式的內嵌文件。 此外，您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細資料的逐步指引。

## <a name="cant-add-another-instance-of-hello-application"></a>無法加入 hello 應用程式的另一個執行個體

tooadd 應用程式的第二個執行個體，您需要 toobe 能夠：

-   設定 hello 第二個執行個體的唯一識別碼。 您必須能夠 tooconfigure hello 相同識別項用於 hello 第一個執行個體。

-   設定用於 hello 第一個執行個體的 hello 與不同的憑證。

如果 hello 應用程式不支援任何上述 hello。 然後，您必須能夠 tooconfigure 第二個執行個體。

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>無法新增識別碼 hello 或 hello 回覆 URL

如果您不能 tooconfigure hello 識別碼或 hello 回覆 URL，確認 hello 識別碼，而且回覆 URL 值符合 hello 模式預先設定的 hello 應用程式。

tooknow hello 模式預先設定的 hello 應用程式：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**移 toostep 7。 如果您已經在 hello 應用程式設定 刀鋒視窗上 Azure AD。

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取**SAML 型登入**從 hello**模式**下拉式清單。

9.  移 toohello**識別碼**或**回覆 URL**文字方塊中，在 hello**網域和 Url 的區段。**

10. 有三種方式 hello 應用程式的 tooknow hello 支援模式：

   * 在 [hello] 文字方塊中，您會看到 hello 支援模式做為預留位置*範例：* <https://contoso.com>。

   * 如果不支援 hello 模式，您會看到紅色驚嘆號時 tooenter hello 文字方塊中的 hello 值再試一次。 如果您將滑鼠停留 hello 紅色驚嘆號，您會看到 hello 支援模式。

   * Hello 教學課程中的 hello 應用程式，您也可以取得支援的 hello 模式的相關資訊。 在 hello**設定 Azure AD 單一登入**> 一節。 設定的 hello 值在 hello 移 toohello 步驟**網域和 Url** > 一節。

如果 hello 值不符合使用預先設定的 Azure AD 上 hello 模式。 您可以：

-   搭配 hello 應用程式廠商 tooget 值符合預先設定的 Azure AD 上 hello 模式

-   或者，您可以連絡 Azure AD 團隊< aadapprequest@microsoft.com >或留下的 hello 應用程式的支援 hello 模式 hello 教學課程 toorequest hello 更新中的註解

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>其中將 hello EntityID （使用者識別碼） 格式的設定

您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。

Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。 如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 之下 NameIDPolicy，

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>找不到 hello Azure AD 中繼資料 toocomplete hello 組態與 hello 應用程式

toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。 根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。

Azure AD 不會提供 URL tooget hello 中繼資料。 hello 中繼資料，才能擷取為 XML 檔案。

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>不知道如何 toocustomize SAML 宣告傳送 tooan 應用程式

toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
