---
title: "登入頁面 hello Azure Active Directory aaaCustomize |Microsoft 文件"
description: "深入了解如何 tooadd 公司品牌 toohello Azure 登入頁面"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>新增公司品牌 tooyour 登入頁面 hello Azure Active Directory 中
tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。 Azure Active Directory 可讓您 toocustomize hello 外觀 hello 登入頁面與您的公司標誌自訂色彩配置，以提供這項功能。 hello 登入頁面為 hello 頁面，會出現在您登入 tooOffice 365 或其他 web 應用程式使用 Azure AD 作為身分識別提供者。 您互動此頁面 tooenter 您的認證。

如果您的公司品牌、 色彩和其他可自訂的元素，此頁面上，您會想 tooshow，請參閱下列映像 toounderstand hello hello 兩種體驗差異 hello。

下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之前**自訂：

![自訂前的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之後**自訂：

![自訂後的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>自訂 hello 登入頁面
一般而言，如果您需要瀏覽器為基礎的存取 tooyour 雲端應用程式和貴組織訂閱的服務，您可以使用 hello 登入頁面。

如果您已套用變更 tooyour 登入頁面上，就可以在 hello 變更 tooappear tooan 小時。

只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。

當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。 在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。

> [!NOTE]
> * 您的網域名稱必須為 使用出現在 hello**網域**部分 hello Azure 入口網站中您已設定的商標。 如需詳細資訊，請參閱 [新增自訂網域名稱](active-directory-domains-add-azure-portal.md)。
> * 登入頁面品牌不會延續 toohello 消費者登入的 Microsoft 的頁面。 如果您使用 Microsoft 帳戶登入，您可能會看到加上品牌的 Azure AD 所呈現的使用者磚清單，但您組織的品牌 hello 不會套用 toohello Microsoft 帳戶登入頁面。
>
>

在您登入頁面上，hello**讓我保持登**核取方塊可讓使用者 tooremain 時關閉並重新開啟瀏覽器登入。

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/01.png)

它不會影響工作階段存留期。 您可以隱藏 hello hello Azure Active Directory 登入頁面上的核取方塊。
Hello 核取方塊會顯示是否取決 hello 設定**讓我保持登停用**。

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide hello 核取方塊，設定此設定太**是**。

> [!NOTE]
> SharePoint Online 和 Office 2010 的某些功能而定的使用者可以 toocheck 此方塊。 如果您設定此設定 toohidden，您的使用者可能會看到 toosign 中其他和非預期的提示。
>
>

**tooadd 公司商標 tooyour 目錄：**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. 在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。
4. 在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**編輯**命令。

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. 修改您想 toocustomize 的 hello 項目。 所有元素都是選用的。
6. 按一下 [儲存] 。

如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。

## <a name="next-steps"></a>後續步驟
[新增語言特定公司商標](active-directory-branding-localize-azure-portal.md)
