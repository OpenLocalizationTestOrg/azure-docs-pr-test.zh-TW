---
title: "Azure Active Directory B2C：Multi-Factor Authentication | Microsoft Docs"
description: "如何 tooenable 消費者導向應用程式中的 Multi-factor Authentication 保護 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C：在取用者導向應用程式中啟用 Multi-Factor Authentication
直接與整合 azure Active Directory (Azure AD) B2C [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) ，讓您可以在消費者導向應用程式中新增第二層的安全性 toosign 向上鍵和登入體驗。 您連一行程式碼都不用寫，即可達成此目標。 目前我們支援撥打電話與簡訊驗證。 如果您已經建立註冊和登入原則，您仍然可以啟用 Multi-Factor Authentication。

> [!NOTE]
> Multi-Factor Authentication 也可以在建立註冊和登入原則時啟用，而非單靠編輯現有原則來啟用。
> 
> 

這項功能可協助應用程式處理 hello 如下的案例：

* 您不需要 Multi-factor Authentication tooaccess 一個應用程式，但您需要 tooaccess 另一個。 例如，hello 取用者可以登入自動保險應用程式與社交或本機帳戶，但必須驗證 hello 電話號碼，才能存取 hello 家用保險應用程式中註冊 hello 相同目錄。
* 您不需要 Multi-factor Authentication tooaccess 應用程式一般情況下，但您需要 tooaccess hello 機密部分內。 比方說，hello 取用者可以登入 tooa 銀行應用程式與社交或本機帳戶，請檢查帳戶餘額，但必須驗證 hello 電話號碼，然後再嘗試連線傳輸。

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>修改您的註冊原則 tooenable 多重要素驗證
1. [遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。
2. 按一下 [註冊原則] 。
3. 按一下 註冊原則 (例如，"B2C_1_SiUp 」) tooopen 它。
4. 按一下**multi-factor authentication**開啟 hello**狀態**太**ON**。 按一下 [確定] 。
5. 按一下**儲存**在 hello hello 刀鋒視窗最上方。

您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。 確認 hello 下列：

Hello Multi-factor Authentication 步驟之前，取得您目錄中建立取用者帳戶。 Hello 步驟期間 hello 取用者會要求他或她的電話號碼，並確認 tooprovide。 如果驗證成功時，則會附加 hello 電話號碼 toohello 消費者帳戶，供日後使用。 即使 hello 取用者取消，或卸除，他可要求的 tooverify 電話號碼再次期間 hello 下一次登入時 （使用多因素驗證啟用）。

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>修改您的登入原則 tooenable 多重要素驗證
1. [遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。
2. 按一下 [登入原則] 。
3. 按一下 登入的原則 (例如，"B2C_1_SiIn 」) tooopen 它。 按一下**編輯**在 hello hello 刀鋒視窗最上方。
4. 按一下**multi-factor authentication**開啟 hello**狀態**太**ON**。 按一下 [確定] 。
5. 按一下**儲存**在 hello hello 刀鋒視窗最上方。

您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。 確認 hello 下列：

Hello 取用者使用登入 （社交或本機帳戶），如果已驗證的電話號碼附加 toohello 消費者帳戶，他或她將被要求 tooverify 它。 如果沒有電話號碼已附加，hello 取用者要求 tooprovide 其中一個，並確認它。 在驗證成功，附加 hello 電話號碼 toohello 消費者帳戶，供日後使用。

## <a name="multi-factor-authentication-on-other-policies"></a>其他原則上的 Multi-Factor Authentication
所描述的上述的註冊和登入原則，所以也可能 tooenable 上註冊的多重要素驗證或原則登入和密碼重設原則。 很快即可用於設定檔編輯原則。

