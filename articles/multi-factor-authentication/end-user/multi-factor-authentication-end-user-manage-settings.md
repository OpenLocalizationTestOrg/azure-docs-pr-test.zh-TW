---
title: "aaaManage 雙步驟驗證設定 |Microsoft 文件"
description: "管理您使用 Azure Multi-Factor Authentication 的方式，包括變更您的連絡資訊或是設定您的裝置。"
services: multi-factor-authentication
keywords: "多重要素驗證用戶端, 驗證的問題, 相互關聯識別碼"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>管理您的雙步驟驗證設定
本文回答有關的問題 tooupdate 設定進行兩步驟驗證或多重要素驗證。 如果您有登入 tooyour 帳戶的問題，請參閱太[遇到雙步驟驗證](multi-factor-authentication-end-user-troubleshoot.md)的疑難排解說明。

## <a name="where-toofind-hello-settings-page"></a>其中 toofind hello 設定 頁面
視您的公司使用 Azure Multi-Factor Authentication 的方式而定，有一些地方可讓您變更如電話號碼等設定。

如果您的 IT 管理員送出特定的 URL 或步驟 toomanage 雙步驟驗證，請遵循這些指示。 否則，請遵循指示 hello 應該適用其他人。 如果您遵循這些步驟，但看不到 hello 相同的選項，這表示您的工作或學校自訂自己的入口網站。 您的系統管理員尋求 hello 連結 tooyour Azure Multi-factor Authentication 入口網站。

1. 登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Hello 右上方，選取您的帳戶名稱，然後選取**設定檔**。  
3. 選取 [其他安全性驗證]。  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. hello 其他安全性驗證頁面載入的設定。

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>我想 toochange 我的電話號碼，或新增次要號碼
它是重要 tooconfigure 次要驗證電話號碼。  因為您的主要電話號碼和您的行動裝置應用程式都可能在 hello 相同電話，hello 次要的電話號碼是 hello 唯一的方式，您將會無法 tooget 回您的帳戶，如果您的手機遺失或遭竊。

> [!NOTE]
> 如果您不具有存取 tooyour 主要電話號碼，而需要取得 tooyour 帳戶中的說明，請參閱我們的說明主題中[遇到雙步驟驗證](multi-factor-authentication-end-user-troubleshoot.md)。  

**toochange 您的主要電話號碼：**  

1. 在 hello 其他安全性驗證 頁面上，選取與您目前的電話號碼的 hello 文字方塊中，編輯與新的電話號碼。  
2. 選取 [ **儲存**]。  
3. 如果這是您使用您的慣用的驗證選項的 hello 數目時，才可儲存有 tooverify hello 新數字。  

**tooadd 次要的電話號碼：**  

1. 在 hello 其他安全性驗證 頁面上，核取 hello 方塊旁太**替代驗證電話。**  
2. 在 hello 文字方塊中輸入您的第二個電話號碼。  
3. 選取 [儲存] 您的變更即完成。  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>需要在已標示為受信任的裝置上再次進行雙步驟驗證

根據您組織的設定，當您在您的瀏覽器上執行雙步驟驗證時，您可能會看到核取方塊指出「**X** 天內不要再問我」。 如果您核取此方塊，然後遺失裝置或認為您的帳戶遭到洩露時，您應該還原兩步驟驗證 tooall 您的裝置。 

1. 在 hello 其他安全性驗證 頁面上，選取 **先前所信任的裝置上還原多重要素驗證**。
2. hello 下次您任何裝置登入，您將會提示的 tooperform 雙步驟驗證。 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>如何從我的舊裝置清除 Microsoft Authenticator 和移動 tooa 新？
當您解除 hello 應用程式安裝從您的裝置或重設的 hello 裝置時，它不會移除 hello 啟用 hello 後端。 如需詳細資訊，請參閱 [Microsoft Authenticator](microsoft-authenticator-app-how-to.md)。

## <a name="next-steps"></a>後續步驟
* 取得疑難排解提示以及[使用雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)的說明。
* 針對不支援雙步驟驗證的任何應用程式，設定[應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。
