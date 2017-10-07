---
title: "aaaAzure MFA 登入具有雙步驟驗證 |Microsoft 文件"
description: "此頁面將提供您指引 toogo toosee hello 各種登入方法可使用 Azure MFA 的位置。"
keywords: "使用者驗證, 登入經驗, 使用行動電話登入, 使用辦公室電話登入"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>hello 登入體驗與 Azure Multi-factor Authentication
> [!NOTE]
> hello 本文的目的是 toowalk 透過典型的登入體驗。 登入，或 tootroubleshoot 問題的說明，請參閱[遇到 Azure Multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md)。

## <a name="what-will-your-sign-in-experience-be"></a>您的登入體驗將會如何？
根據您選擇的 toouse 做為您的第二個因素與您登入體驗： 電話、 驗證應用程式或文字。 選擇最能描述您進行的 hello 選項：

| 您要如何登入？ | 
| --- |
| [使用電話 toomy 行動電話或辦公室電話](#signing-in-with-a-phone-call) |
| [與文字 toomy 行動電話](#signing-in-with-a-text-message)
| [來自 hello Microsoft 驗證器應用程式通知](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [與從 hello Microsoft 驗證器應用程式的驗證碼](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [使用替代方法，因為現在無法使用我慣用的方法](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>透過撥打電話來登入
hello 下列資訊描述 hello 雙步驟驗證經驗與呼叫 tooyour 行動或辦公室電話。

1. 登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。  
2. Microsoft 打電話給您。  
3. 接聽 hello 電話並按 hello # 鍵。  

## <a name="signing-in-with-a-text-message"></a>透過簡訊登入
hello 下列資訊描述 hello 雙步驟驗證經驗，只要使用文字訊息 tooyour 行動電話：

1. 登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。 
2. Microsoft 會傳送包含數字代碼的簡訊給您。 
3. Hello 登入頁面上提供的 hello 方塊中輸入 hello 程式碼。 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>登入 hello Microsoft 驗證器應用程式 
hello 下列資訊描述 hello 體驗 hello Microsoft 驗證器應用程式使用的兩步驟驗證。 有兩個不同的方式 toouse hello 應用程式。 您可以在您的裝置上接收推播通知，或者您可以開啟 hello 應用程式 tooget 驗證碼。

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign 入是來自 hello Microsoft 驗證器應用程式通知
1. 登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。
2. Microsoft 會傳送通知 toohello Microsoft Authenticator 應用程式在裝置上。

  ![Microsoft 傳送通知](./media/multi-factor-authentication-end-user-signin/notify.png)

3. 在您的電話和選取 hello 開啟 hello 通知**確認**索引鍵。 如果貴公司要求 PIN，在此處輸入。
4. 您現在應已登入。

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign 在 hello Microsoft Authenticator 應用程式中使用驗證碼

如果您使用 hello Microsoft 驗證器應用程式 tooget 驗證碼，然後當您開啟 hello 應用程式時您看到一些在您的帳戶名稱。 這個數字變更每隔 30 秒，讓您不使用的 hello 兩次相同數字。 當詢問驗證程式碼時，開啟 hello 應用程式，並使用目前顯示的任何數字。 

1. 登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。
2. Microsoft 提示您輸入驗證碼。

  ![輸入驗證碼](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. 開啟 hello 手機上的 Microsoft 驗證器應用程式，並在您要登入的 hello 方塊中輸入 hello 程式碼。

## <a name="signing-in-with-an-alternate-method"></a>使用替代方法登入
有時候，您不需要 hello 電話或裝置，您將設定為慣用的驗證方法。 這種情況就是為什麼我們建議您為帳戶設定備份方法。 hello 下節將說明如何 toosign 使用替代方法時可能無法使用主要方法。

1. 登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。
2. 選取 [使用不同的驗證選項]。 根據您已設定的驗證選項數量而定，您會看到不同的驗證選項。
3. 選擇替代方法並且登入。

  ![使用替代方法](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>後續步驟

如果您碰到雙步驟驗證登入的問題，可從[使用 Azure Multi-Factor Authentication 時碰到困難](multi-factor-authentication-end-user-troubleshoot.md)獲得詳細資訊。

了解如何太[管理兩步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)。

了解如何太[hello Microsoft 驗證器應用程式使用者入門](microsoft-authenticator-app-how-to.md)，讓您可以使用通知 toosign 中，而不是文字和撥打電話。 
