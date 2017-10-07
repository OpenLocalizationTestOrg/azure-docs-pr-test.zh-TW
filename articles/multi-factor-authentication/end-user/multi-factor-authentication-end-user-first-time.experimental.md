---
title: "註冊我的工作或學校帳戶的雙步驟驗證 aaaSet |Microsoft 文件"
description: "當您的公司設定 Azure Multi-factor Authentication 時，將會提示的 toosign 進行兩步驟驗證。 深入了解如何 tooset 它。 "
services: multi-factor-authentication
keywords: "如何 toouse azure 目錄，hello 雲端，active directory 教學課程中的 active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>對我的帳戶進行雙步驟驗證設定
雙步驟驗證是額外的安全性步驟，以協助保護您的帳戶難度中其他人 toobreak。 如果您正在閱讀這篇文章，可能會收到一封來自您工作或學校的系統管理員關於 Multi-Factor Authentication 的電子郵件。 或可能您嘗試在 toosign 和收到訊息，詢問您 tooset 其他安全性驗證設定。 如果是 hello 的情況下，**完成 hello 自動註冊程序之前，您無法登入**。

本文將協助您設定您的**工作或學校帳戶**。 如果您想要自行個人 Microsoft 帳戶 tooenable 雙步驟驗證，請參閱[需兩步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)。

## <a name="set-up-your-account"></a>設定帳戶

當您的 IT 部門需要您使用兩步驟驗證 toostart 螢幕說**系統管理員已要求您設定此帳戶的其他安全性驗證**出現：

![設定](./media/multi-factor-authentication-end-user-first-time/first.png)

啟動，tooget 選取**立即進行設定。**

如果您看不像這樣的畫面在您登入，請依照下列中的 hello 指示[管理您的設定進行兩步驟驗證](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)toofind hello 設定頁面，您可以在其中管理您的驗證選項。 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>決定您要如何 tooverify 登入

hello hello 註冊程序中的第一個問題是您要如何我們 toocontact 您。 在 hello 資料表中，看看 hello 選項，並使用 hello 連結 toogo toohello 設定步驟的每個方法。

| 連絡方法 | 說明 |
| --- | --- |
| [行動應用程式](#use-a-mobile-app-as-the-contact-method) |- **收到驗證的通知。** 此選項會將通知 toohello authenticator 應用程式推入您的智慧型手機或平板電腦。 檢視 hello 通知，如果合法，請選取**驗證**hello 應用程式中。 您的工作或學校可能會要求您輸入 PIN 後才能進行驗證。<br>- **驗證碼。** 在此模式中，hello 驗證器應用程式會產生驗證碼，以更新每隔 30 秒。 Hello 登入介面中輸入 hello 最新的驗證碼。<br>hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。 |
| [行動電話通話或文字](#use-your-mobile-phone-as-the-contact-method) |- **通話**會將您提供自動的語音電話 toohello 電話號碼。 接聽 hello 電話並按 # hello 電話數字鍵台 tooauthenticate 中。<br>- **簡訊**傳送包含驗證碼的簡訊。 下列 hello 提示字元中的 hello 文字，請回覆 toohello 簡訊，或輸入 hello hello 登入介面提供的驗證碼。 |
| [辦公室電話通話](#use-your-office-phone-as-the-contact-method) |將您提供自動的語音電話 toohello 電話號碼。 回應 hello 呼叫，並在 hello 電話數字鍵台 tooauthenticate 中按下 #。 |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>使用行動裝置應用程式做為 hello 連絡方法
使用此方法會要求您在手機或平板電腦上安裝驗證器應用程式。 hello 本文章中的步驟根據 hello Microsoft 驗證器應用程式，可供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。

1. 選取**行動裝置應用程式**hello 下拉式清單中。
2. 選取 [接收驗證的通知] 或 [使用驗證碼]，然後選取 [設定]。

   ![[其他安全性驗證] 畫面](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. 您的電話或平板電腦，開啟 hello 應用程式，並選取** + ** tooadd 帳戶。 (Android 裝置上，選取 hello 三個點，然後**將帳戶加入**。)
4. 指定您要 tooadd 工作或學校帳戶。 hello QR 代碼掃描器，在手機上的開啟。 如果您的相機未正常運作，您可以選取 tooenter 您公司的資訊以手動方式。 如需詳細資訊，請參閱 [手動新增帳戶](#add-an-account-manually)。  
5. 掃描 hello QR 程式碼的圖片與囉 」 畫面設定 hello 行動裝置應用程式出現。  選取**完成**tooclose hello QR 代碼螢幕。  

   ![QR 代碼畫面](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. 當啟用完成 hello 電話上時，選取**與我連絡**。  此步驟會傳送通知或驗證碼 tooyour 電話。 選取 [驗證] 。  
7. 如果貴公司需要 PIN 來核准登入驗證，請輸入它。

   ![輸入 PIN 的方塊](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. 輸入完 PIN 之後，請選取 [關閉] 。 此時，您的驗證應會成功。
9. 我們建議您輸入您的行動電話號碼，以備在遺失存取 tooyour 行動裝置應用程式。 指定您的國家/地區，從 [hello] 下拉式清單中，並在 hello 方塊下一步 toohello 國家 （地區） 名稱中輸入您的行動電話號碼。 選取 [下一步] 。
10. 此時，您會設定非瀏覽器應用程式，例如 Outlook 2010 或更舊或 hello Apple 裝置上的原生電子郵件應用程式的應用程式密碼的提示的 tooset。 此動作是因為某些應用程式不支援雙步驟驗證。 如果您不使用這些應用程式，按一下**完成**和略過這些步驟 hello 其餘部分。
11. 如果您使用這些應用程式，將密碼複製 hello 應用程式提供，並將它貼到您的應用程式，而非一般密碼。 您可以使用 hello 的多個應用程式的相同應用程式密碼。 如需詳細資訊，[應用程式密碼協助]。
12. 按一下 [完成] 。

### <a name="add-an-account-manually"></a>手動新增帳戶
如果您想 tooadd 帳戶 toohello 行動裝置應用程式以手動方式，而不是使用 hello QR 讀卡機，請遵循下列步驟。

1. 選取 hello**手動輸入帳戶**] 按鈕。  
2. 輸入 hello 程式碼和 hello URL 所提供 hello 上相同的頁面，其中顯示 hello 條碼。 此資訊則是放在 hello**程式碼**和**URL** hello 行動裝置應用程式上的方塊。

    ![設定](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Hello 啟動完成時，選取**與我連絡**。 此步驟會傳送通知或驗證碼 tooyour 電話。 選取 [驗證] 。

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>使用您的行動電話作為連絡方式的 hello
1. 選取**驗證電話**hello 下拉式清單中。  

    ![設定](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. 從 hello 下拉式清單中，選擇您的國家/地區，並輸入您的行動電話號碼。
3. 選取您想與您的行動電話-簡訊還是通話 toouse hello 方法。
4. 選取**與我連絡**tooverify 您的電話號碼。 根據您選取的 hello 模式，我們會傳送給您的文字或撥打電話給您。 依照 hello 提供指示，在 [hello] 畫面中，然後選取 [**確認**。
5. 此時，您會設定非瀏覽器應用程式，例如 Outlook 2010 或更舊或 hello Apple 裝置上的原生電子郵件應用程式的應用程式密碼的提示的 tooset。 此動作是因為某些應用程式不支援雙步驟驗證。 如果您不使用這些應用程式，按一下**完成**並略過其餘步驟，hello hello。
6. 如果您使用這些應用程式，將密碼複製 hello 應用程式提供，並將它貼到您的應用程式，而非一般密碼。 您可以使用 hello 的多個應用程式的相同應用程式密碼。 如需詳細資訊，[應用程式密碼協助]。
7. 按一下 [完成] 。

## <a name="use-your-office-phone-as-hello-contact-method"></a>使用您的辦公室電話作為連絡方式的 hello
1. 選取**辦公室電話**從 hello] 下拉式清單  

    ![設定](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. hello 電話號碼] 方塊會自動填入您的公司連絡資訊。 如果 hello 編號錯誤或遺失，請 toomake 變更系統管理員。
3. 選取**與我連絡**tooverify 您的電話號碼，我們會撥打您的號碼。 依照 hello 提供指示，在 [hello] 畫面中，然後選取 [**確認**。
4. 此時，您會設定非瀏覽器應用程式，例如 Outlook 2010 或更舊或 hello Apple 裝置上的原生電子郵件應用程式的應用程式密碼的提示的 tooset。 此動作是因為某些應用程式不支援雙步驟驗證。 如果您不使用這些應用程式，按一下**完成**並略過其餘步驟，hello hello。
5. 如果您使用這些應用程式，將密碼複製 hello 應用程式提供，並將它貼到您的應用程式，而非一般密碼。 您可以使用 hello 的多個應用程式的相同應用程式密碼。 如需詳細資訊，請參閱 [什麼是應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。
6. 按一下 [完成] 。

## <a name="next-steps"></a>後續步驟
* 變更您慣用的選項並[管理您雙步驟驗證的設定](multi-factor-authentication-end-user-manage-settings.md)
* 針對不支援雙步驟驗證的原生裝置應用程式，設定[應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。
* 簽出 hello [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)快速、 安全驗證即使您沒有儲存格的服務。

