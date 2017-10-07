---
title: "註冊入口網站說明主題 aaaApp |Microsoft 文件"
description: "Hello Microsoft 應用程式註冊入口網站中的各種功能的描述。"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>App 註冊參考
本文件提供內容和 hello Microsoft 應用程式註冊入口網站中找到的各種功能的描述[https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。

## <a name="my-applications"></a>我的應用程式
此清單包含所有應用程式註冊為用於 hello Azure AD v2.0 端點。  有兩個 Microsoft 帳戶和工作/學校帳戶，從 Azure Active Directory 的個人帳戶的使用者 hello 能力 toosign 這些應用程式。  toolearn 進一步了解 Azure AD hello v2.0 端點，請參閱我們[v2.0 概觀](active-directory-appmodel-v2-overview.md)。  這些應用程式也可以使用與 hello Microsoft 帳戶驗證端點 toointegrate `https://login.live.com`。

## <a name="live-sdk-applications"></a>Live SDK 應用程式
此清單包含所有已註冊且只能與 Microsoft 帳戶搭配使用的應用程式。  在任何情況下，它們都不會啟用來與 Azure Active Directory 搭配使用。  這是您可以在其中找到任何先前已與 hello MSA 開發人員入口網站，在已註冊的應用程式`https://account.live.com/developers/applications`。  您先前曾在 `https://account.live.com/developers/applications` 執行的所有函式現在均可在這個新的入口網站 `https://apps.dev.microsoft.com` 中執行。  如果您有任何進一步有關 Microsoft 帳戶應用程式的問題，請與我們連絡。

## <a name="application-secrets"></a>應用程式密碼
應用程式密碼是認證可讓您的應用程式 tooperform 可靠[用戶端驗證](http://tools.ietf.org/html/rfc6749#section-2.3)與 Azure AD。  在 OAuth 和 OpenID Connect，應用程式密碼是通常參照的 tooas `client_secret`。  Hello v2.0 通訊協定，接收到安全性權杖，web 可定址位置的任何應用程式中 (使用`https`配置) 必須使用該安全性權杖的兌換時 tooAzure AD 應用程式密碼 tooidentify 本身。  此外，在裝置上的將收到權杖會禁止使用應用程式密碼 tooperform 用戶端驗證，toodiscourage 任何原生用戶端 hello 不安全的環境中的機密資料的儲存的體。

每個 app 最後都能在任何指定時間點包含兩個有效的應用程式密碼。  藉由維護兩個密碼，您會跨應用程式的整個環境有 hello ablilty tooperform 定期金鑰變換。  一旦您已移轉 hello 整個 tooa 新應用程式的密碼，您可以刪除 hello 舊的密碼，並佈建一個新。

此時，只有兩種類型的應用程式密碼才允許 hello 應用程式註冊入口網站。  選擇**產生新的密碼**將會產生並儲存在 hello 各自的資料存放區，您可以在您的應用程式中使用的共用的密碼。  選擇**產生新的金鑰組**會建立新的公用/私用金鑰組，可以下載和使用的用戶端驗證 tooAzure AD。

## <a name="profile"></a>設定檔
hello 設定檔區段的 hello 應用程式註冊入口網站可以是 toocustomize hello 登用於您的應用程式的頁面。  在這個階段中，您可以變更 hello 登入網頁的應用程式標誌、 服務 URL 和隱私權聲明的條款。  hello 的標誌必須是 15 KB 的 GIF、 PNG 或 JPEG 檔案中透明 48 x 48 或 50 x 50 像素影像或變小。  請嘗試變更 hello 值和產生登入頁面上檢視 hello ！

## <a name="live-sdk-support"></a>Live SDK 支援
當您啟用 「 即時 SDK 支援 」 時，會儲存您所建立的密碼將會佈建到 hello Azure AD 與 Microsoft 帳戶資料的任何應用程式。  這可讓您的應用程式 toointegrate 直接與 hello Microsoft 帳戶服務 (login.live.com)。  如果您想 toobuild 直接 （相對於的 toousing hello Azure AD v2.0 端點） 以使用 Microsoft 帳戶應用程式，您應該確定已啟用 Live SDK 支援。

停用 Live SDK 支援可確保該 hello 應用程式密碼只會寫入 hello Azure AD 資料存放區。  hello Azure AD 資料存放區合併，允許它 toomeet 企業等級規定某些標準，例如 FISMA 相容性。  如果您啟用 Live SDK 支援，您的應用程式可能不會遵守這其中的部分標準。

如果您只有計劃 toouse hello Azure AD v2.0 端點，您可以安全地停用 Live SDK 支援。

