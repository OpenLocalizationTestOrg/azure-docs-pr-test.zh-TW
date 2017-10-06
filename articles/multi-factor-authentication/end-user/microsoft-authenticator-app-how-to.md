---
title: "行動電話的 aaaMicrosoft Authenticator 應用程式 |Microsoft 文件"
description: "深入了解如何 tooupgrade toohello 最新版本的 Azure Authenticator。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>開始使用 hello Microsoft 驗證器應用程式
hello Microsoft Authenticator 應用程式提供額外一層的安全性工作或學校帳戶 (例如， bsimon@contoso.com) 或您的 Microsoft 帳戶 (例如， bsimon@outlook.com)。

hello 應用程式的運作方式在兩種方式之一：

* **通知**。 hello 應用程式可協助防止未經授權的存取 tooaccounts 並停止詐騙交易將推送通知 tooyour 智慧型手機或平板電腦。 只檢視 hello 通知，如果合法，請選取**確認**。 否則，您可以選取 [拒絕] 。 
* **驗證碼**。 hello 應用程式可以做為軟體權杖 toogenerate OAuth 驗證碼。 您輸入使用者名稱和密碼之後，您會輸入 hello hello 登入畫面 hello 應用程式所提供的程式碼。 hello 驗證程式碼會提供第二種形式的驗證。

hello Microsoft 驗證器應用程式取代 hello Azure Authenticator 應用程式。 hello Azure Authenticator 應用程式仍能運作，但如果您決定 toomove toohello 新 Microsoft Authenticator 應用程式，這篇文章可協助您。  

## <a name="opt-in-for-two-step-verification"></a>選擇雙步驟驗證

hello Microsoft 驗證器應用程式並不可行的。 設定每個您輸入之後的第二個驗證方法使用您的使用者名稱和密碼登入您的帳戶 tooprompt。 

工作或學校帳戶，就無法通常取得 toochoose 這項功能自行。 相反地，安全性系統管理員選擇代表您，，然後通知您 tooregister 驗證方法，為您的帳戶。 如果此案例適用於 tooyou，進一步了解[Azure Multi-factor Authentication 什麼我](multi-factor-authentication-end-user.md)。

個人的帳戶，您必須註冊您自己的雙步驟驗證 tooset。 如果您有 Microsoft 帳戶，[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)中說明這些步驟。 

您也可以使用 Microsoft Authenticator hello 與非 Microsoft 帳戶。 它們可能會呼叫 hello 功能以外的雙步驟驗證，但是您應該能夠 toofind 在安全性 」 或 「 登入設定。 

## <a name="install-hello-app"></a>安裝 hello 應用程式
hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[iOS](http://go.microsoft.com/fwlink/?Linkid=825073)。

## <a name="add-accounts-toohello-app"></a>新增帳戶 toohello 應用程式
針對每個您想 tooadd toohello Microsoft Authenticator 應用程式的帳戶，使用其中一種 hello 下列程序：

### <a name="add-a-personal-microsoft-account-toohello-app"></a>新增個人 Microsoft 帳戶 toohello 應用程式

個人 Microsoft 帳戶 (其中一個您使用 toosign 中 tooOutlook.com Xbox、 Skype、 等)，您只需要 toodo 是登入 tooyour hello Microsoft 驗證器應用程式中的帳戶。

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>新增工作或學校帳戶 toohello 應用程式使用 hello QR 代碼掃描器
1. 移 toohello 安全性驗證設定 畫面。  如需詳細資訊 tooget toothis 畫面上，請參閱[變更安全性設定](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)。
2. 核取 hello 方塊旁太**Authenticator 應用程式**然後選取**設定**。

    ![hello hello 安全性驗證設定 畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    這會顯示有 QR 代碼的畫面。

    ![畫面，讓您 hello QR 代碼](./media/authenticator-app-how-to/barcode2.png)
3. 開啟 hello Microsoft 驗證器應用程式。 在 hello**帳戶**畫面上，選取 **+** ，然後指定您想要 tooadd 工作或學校帳戶。
4. 使用 hello 相機 tooscan hello QR 代碼，然後選取**完成**tooclose hello QR 代碼螢幕。

    如果您的相機未正常運作，您可以[手動輸入 hello QR 代碼和 URL](#add-an-account-to-the-app-manually)。

5. Hello 應用程式會顯示您的帳戶名稱，以六位數代碼其下，您已完成。 

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>手動新增帳戶 toohello 應用程式
1. 移 toohello 安全性驗證設定 畫面。  如需詳細資訊 tooget toothis 畫面上，請參閱[變更安全性設定](multi-factor-authentication-end-user-manage-settings.md)。
2. 選取 [設定] 。

    ![hello hello 安全性驗證設定 畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    這會顯示有 QR 代碼的畫面。  請注意 hello 代碼和 URL。

    ![提供 hello QR 代碼和 URL 的螢幕](./media/authenticator-app-how-to/barcode2.png)
3. 開啟 hello Microsoft 驗證器應用程式。 在 hello**帳戶**畫面上，選取 **+** ，然後指定您想要 tooadd 工作或學校帳戶。

4. 在 hello 掃描器，請選取**手動輸入程式碼**。

    ![掃描 QR 代碼的畫面](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Hello，hello 應用程式中的適當方塊中輸入 hello 代碼和 hello URL，然後選取 **完成**。

    ![輸入代碼和 URL 的畫面](./media/authenticator-app-how-to/manual.png)

6. Hello 應用程式會顯示您的帳戶名稱，以六位數代碼其下，您已完成。

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>新增帳戶 toohello 應用程式使用 Touch ID
hello Microsoft 驗證器應用程式在 iOS 上的支援 Touch ID  Azure Multi-factor Authentication 可讓組織 toorequire 裝置的 PIN。 使用 Touch ID、 iOS 使用者不需要 tooenter PIN。 相反地，他們可以掃描其指紋，並選取 [核准] 。

設定 Touch ID 搭配 Azure 驗證器很簡單。 您可以使用 PIN 碼完成一般驗證挑戰。 如果您的裝置支援 Touch ID，Microsoft Authenticator 會自動為該帳戶進行設定。

![Touch ID 安裝程式的驗證](./media/authenticator-app-how-to/touchid1.png)

從該點，當您準備 tooverify 需要您登入時，您選取 hello 接收推播通知，並掃描指紋而不是輸入 PIN。

![推播通知](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>當您登入使用 hello 應用程式

一旦您的帳戶新增 toohello 應用程式，您可能會提示的 toodo 測試驗證 toomake 確定所有項目已正確設定。 之後，就大功告成了！ 您不需要 toodo 任何其他項目直到 hello 下次您登入。

如果您選擇 toouse 驗證碼 hello 應用程式中，您會啟動 toosee 它們 hello 首頁上。 它們每 30 秒變更一次，所以當您需要時，一定可以獲得新的驗證碼。 但是您不需要 toodo 任何項目與它們直到您登入，並提示的 tooenter 驗證碼。  
