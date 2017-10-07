---
title: "Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證 | Microsoft Docs"
description: "主題，示範如何 toodisable 電子郵件驗證期間註冊在 Azure Active Directory B2C 的取用者"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證
啟用時，Azure Active Directory (Azure AD) B2C 提供一個消費者會 hello 註冊應用程式的能力 toosign 藉由提供電子郵件地址，並建立本機帳戶。 Azure AD B2C 確保有效的電子郵件地址，藉由要求取用者 tooverify 它們 hello 註冊程序。 它也可防止惡意的自動化程序產生假 hello 應用程式的帳戶。

某些應用程式開發人員偏好 tooskip 電子郵件驗證 hello 註冊程序，並改讓取用者驗證稍後 hello 電子郵件地址。 toosupport Azure AD B2C 這可以是設定的 toodisable 電子郵件驗證。 如此一來建立更順暢的登入程序，並提供開發人員 hello 彈性 toodifferentiate hello 取用者已驗證與沒有這些取用者的電子郵件地址。

根據預設值，註冊原則會開啟電子郵件驗證。 使用 hello 下列步驟 tooturn 它關閉：

1. [遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。
2. 視您要針對註冊設定的項目而定，按一下 [註冊原則] 或 [註冊或登入原則]。
3. 按一下 原則 (例如，"B2C_1_SiUp 」) tooopen 它。 按一下**編輯**在 hello hello 刀鋒視窗最上方。
4. 按一下 [頁面 UI 自訂功能]。
5. 按一下 [本機帳戶註冊頁面]。
6. 按一下**電子郵件地址**在 hello**名稱**hello 下的資料行**註冊屬性**> 一節。
7. 切換 hello**需要驗證**太選項**否**。
8. 按一下**確定**底部 hello 直到您到達 hello**編輯原則**刀鋒視窗。
9. 按一下**儲存**在 hello hello 刀鋒視窗最上方。 大功告成！

> [!NOTE]
> 停用電子郵件驗證 hello 註冊程序中的，可能會導致 toospam。 如果您停用其中一個 hello 預設，我們建議加入您自己的驗證系統。
> 
> 

我們一定是開啟 toofeedback，以及建議 ！ 如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。 功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。
