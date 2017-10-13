---
title: "Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證 | Microsoft Docs"
description: "示範如何在 Azure Active Directory B2C 中的取用者註冊期間停用電子郵件驗證的主題"
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證
啟用時，Azure Active Directory (Azure AD) B2C 會提供讓使用者透過提供電子郵件地址並建立本機帳戶來註冊應用程式的能力。 Azure AD B2C 可透過要求取用者在註冊程序期間驗證其身分以確保電子郵件地址的有效性。 它也會防止惡意自動化程序為應用程式產生假帳戶。

某些應用程式開發人員偏好在註冊程序期間跳過電子郵件驗證，改為讓取用者稍後在掙電子郵件地址。 為支援此方式，您可以將 Azure AD B2C 設定為停用電子郵件驗證。 這樣做可建立較為順暢的註冊程序，並提供區分已驗證電子郵件地址與未驗證電子郵件地址之取用者的彈性。

根據預設值，註冊原則會開啟電子郵件驗證。 使用下列步驟將它關閉：

1. 遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。
2. 視您要針對註冊設定的項目而定，按一下 [註冊原則] 或 [註冊或登入原則]。
3. 按一下您的原則 (例如 "B2C_1_SiUp") 以將它開啟。 按一下刀鋒視窗頂端的 [編輯] 。
4. 按一下 [頁面 UI 自訂功能]。
5. 按一下 [本機帳戶註冊頁面]。
6. 按一下 [註冊屬性] 區段下 [名稱] 欄中的 [電子郵件地址]。
7. 將 [需要驗證] 選項切換至 [否]。
8. 按一下底部的 [確定]，直到您到達 [編輯原則] 刀鋒視窗。
9. 按一下刀鋒視窗頂端的 [儲存] 。 大功告成！

> [!NOTE]
> 在註冊程序期間停用電子郵件驗證可能會導致收到垃圾郵件。 若停用預設的項目，建議您新增自己的驗證系統。
> 
> 

我們歡迎意見反應和建議！ 如果您無法完成此主題，或者有改進此內容的建議，非常歡迎您在頁面底部提供意見反應。 對於功能要求，請將它們新增到 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。