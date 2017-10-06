---
title: "aaaRegister hello Azure AD v2.0 端點使用 hello 入口網站的應用程式 |Microsoft 文件"
description: "Tooregister 應用程式，但 Microsoft 來啟用登入及存取 Microsoft 服務使用 hello v2.0 端點"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>如何 tooregister 與 hello v2.0 端點的應用程式
toobuild 接受 MSA 與 Azure AD 的應用程式登入時，您必須先 tooregister 與 Microsoft 的應用程式。  此時，您將不會是能 toouse 任何現有的應用程式，您可能必須向 Azure AD 或 MSA-您將需要 toocreate 新品牌。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>請瀏覽 hello Microsoft 應用程式註冊入口網站
首要之務先瀏覽過[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。  這是新的 app 註冊入口網站，可供您管理有關 Microsoft app 的所有一切。

使用個人或公司或學校的 Microsoft 帳戶進行登入。  如果您沒有任何帳戶，請註冊新的個人帳戶。 請繼續進行，這不需要很長的時間 - 我們會在此等候。

完成了嗎？ 您現在應該看一下您的 Microsoft 應用程式清單，該清單有可能空白。  讓我們改變這點。

按一下 [新增應用程式]，並為它命名。  hello 入口網站將會指派全域唯一的應用程式識別碼，稍後在程式碼中，您將使用您的應用程式。  如果您的應用程式包含伺服器端元件，需要存取權杖呼叫應用程式開發介面 (認為： Office、 Azure 或您自己的 web 應用程式開發介面)，您會想 toocreate**應用程式密碼**也這裡。

接下來，新增 hello 將使用您的應用程式平台。

* 針對 web 架構的 app，提供可傳送登入訊息的 **重新導向 URI** 。
* 行動裝置應用程式，向下 hello 預設複製重新導向自動為您建立的 uri。

（選擇性） 您可以自訂您的登入頁面 hello 設定檔 > 一節中的 hello 外觀與風格。  請確定 tooclick**儲存**在繼續之前。

> [!NOTE]
> 當您建立應用程式使用[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，hello 應用程式將在 hello hello 帳戶，您會使用 toosign hello 入口網站的主要租用戶中登錄。  這表示您不能使用個人的 Microsoft 帳戶，在 Azure AD 租用戶中註冊應用程式。  如果您明確地想 tooregister 應用程式特定的租用戶中，使用原先建立該租用戶中的帳戶登入。
> 
> 

## <a name="build-a-quick-start-app"></a>建置快速啟動應用程式
您現在已有 Microsoft app，您可以完成我們提供的其中一個 v2.0 快速啟動教學課程。  以下是一些建議：

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

