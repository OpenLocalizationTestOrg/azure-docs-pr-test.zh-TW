---
title: "aaaHow tooconfigure 密碼單一登入的非組件庫的應用程式 |Microsoft 文件"
description: "如何 tooconfigure 自訂非組件庫的應用程式時，使用安全密碼型單一登入它將不會列在 hello Azure AD 應用程式庫"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>如何 tooconfigure 密碼單一登入非組件庫的應用程式

此外 toohello 選擇找到 hello Azure AD 應用程式庫，您也可以 hello 選項 tooadd**非組件庫的應用程式**當您想要的 hello 應用程式未在此處列出。 使用這項功能，您可以新增任何應用程式已存在於您的組織或您可能會使用任何協力廠商應用程式廠商還不屬於 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)。

一旦您加入非組件庫的應用程式，您可以設定 hello 單一登入此應用程式使用的方法藉由選取 hello**單一登入**瀏覽項目在企業中的應用程式 hello [Azure 入口網站](https://portal.azure.com/).

其中一個 hello 單一登入方法提供 tooyou 為 hello[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)選項。 以 hello**加入非組件庫的應用程式**體驗，您可以整合任何應用程式可呈現 HTML 為基礎的使用者名稱和密碼會輸入欄位，即使它不在我們一組預先整合應用程式。

抓取的 hello 技術的頁面存取面板延伸模組，讓我們 tooauto hello 其運作的方式就是-偵測使用者名稱和密碼的輸入的欄位，並安全地儲存特定應用程式執行個體。 然後安全地重新執行的使用者名稱，並在使用者的密碼 toothose 欄位巡覽 toothat hello 應用程式存取面板上的應用程式。

這是很好的方式 tooget 啟動快速，將任何種類的應用程式整合至 Azure AD，並可讓您：

-   整合**任何應用程式中的 hello world**與 Azure AD 租用戶，因此只要它們呈現 HTML 使用者名稱和密碼輸入的欄位

-   啟用**單一登入您的使用者**由安全地儲存和使用者名稱和密碼的 hello 應用程式重新執行您已與 Azure AD 整合

-   **自動偵測輸入**欄位的任何應用程式，並可讓您 toomanually 偵測使用 hello 存取面板瀏覽器延伸模組，這些欄位，萬一自動偵測不到它們

-   **支援應用程式需要多個登入欄位**需要不只是使用者名稱和密碼欄位 toosign 中的應用程式

-   **自訂 hello 標籤**hello 使用者名稱和密碼輸入欄位的使用者看到上 hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)當使用者輸入其認證

-   允許您**使用者**tooprovide 他們自己的使用者名稱和它們所中手動輸入 hello 任何現有應用程式帳戶的密碼[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   允許**hello 的商務群組的成員**toospecify hello 使用者名稱和密碼使用指派給 tooa 使用者 hello[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)功能

-   允許**管理員**toospecify hello 使用者名稱和密碼使用 hello 更新認證指派給 tooa 使用者功能時[指派使用者 tooan 應用程式](#_How_to_configure_1)

-   允許**管理員**toospecify hello 共用使用者名稱或密碼一群人由使用 hello 更新認證的功能時[指派群組 tooan 應用程式](#assign-an-application-to-a-group-directly)

以下說明如何啟用[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)tooany 應用程式，您將使用 hello**加入非組件庫的應用程式**體驗。

## <a name="overview-of-steps-required"></a>所需步驟的概觀

您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：

-   [新增不在資源庫內的應用程式](#add-a-non-gallery-application)

-   [設定密碼單一登入的 hello 應用程式](#configure-the-application-for-password-single-sign-on)

-   [Hello 應用程式 tooa 使用者或群組指派](#assign-the-application-to-a-user-or-a-group)

    -   [直接指派使用者 tooan 應用程式](#assign-a-user-to-an-application-directly)

    -   [直接指派應用程式 tooa 群組](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>新增不在資源庫內的應用程式

tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗

6.  按一下 [不在資源庫內的應用程式]。

7.  輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。 選取 [新增]。

短時間，就能 toosee hello 應用程式的組態刀鋒視窗。

## <a name="configure-hello-application-for-password-single-sign-on"></a>設定密碼單一登入的 hello 應用程式

tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  輸入 hello**登入 URL**。 這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。 請確定 hello 登入欄位會顯示在 hello URL。

10. 將使用者指派 toohello 應用程式。

11. 此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。 否則，使用者在提示的 tooenter hello 認證本身在啟動。

## <a name="assign-a-user-tooan-application-directly"></a>直接指派使用者 tooan 應用程式

tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。

8.  按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。

9.  按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。

10. Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。

11. 將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。 按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。

12. **選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。

13. 當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。

14. **選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。

15. 按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。

## <a name="assign-an-application-tooa-group-directly"></a>直接指派應用程式 tooa 群組

tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。

8.  按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。

9.  按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。

10. 型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。

11. 將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。 按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。

12. **選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。

13. 當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。

14. **選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。

15. 按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。

在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)
