---
title: "應用程式 Proxy 應用程式的 aaaApplication 頁面不會正確顯示 |Microsoft 文件"
description: "Hello 網頁未正確顯示在 應用程式 Proxy 應用程式的指引您有與 Azure AD 整合"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Application Proxy 應用程式的應用程式頁面未正確顯示

本文章協助 tootroubleshoot 與 Azure Active Directory 應用程式 Proxy 應用程式的問題時您瀏覽 toohello 頁面上，但在 hello 頁面上的項目看起來不正確。

## <a name="overview"></a>概觀
當您發行應用程式 Proxy 應用程式時，只有在您的根目錄下的頁面存取 hello 應用程式時有可存取。 如果沒有正確地顯示 hello 頁面，hello 根目錄內部 URL 用於 hello 應用程式可能會遺失一些頁面資源。 tooresolve，請確定您已發行*所有*hello hello 頁面的資源做為您的應用程式的一部分。

您可以確認這是藉由開啟網路追蹤的 hello 問題 (例如 Fiddler 或 F12 工具 Internet Explorer/Edge)、 載入 hello 頁面上，並尋找 404 錯誤。 指出目前找不到，可能仍然需要 toobe 發行的 hello 頁面。

此案例的範例，假設您已經發行費用應用程式使用的內部 URL <http://myapps/expenses>，但是 hello 應用程式會使用 hello 樣式表<http://myapps/style.css>。 在此情況下，hello 樣式表不在發行您的應用程式，因此載入 hello 費用應用程式擲回時嘗試 tooload style.css 404 錯誤。 在此範例中，會解決 hello 問題發佈 hello 應用程式的內部 url <http://myapp/>改為。

## <a name="problems-with-publishing-as-one-application"></a>發佈為一個應用程式時的問題

如果不可能 toopublish 中的所有資源都 hello 相同的應用程式，您需要 toopublish 多個應用程式，並啟用它們之間的連結。

toodo 如此，我們建議使用 hello[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)方案。 不過，此解決方案需要您的網域擁有 hello 憑證，您的應用程式可使用完整的網域名稱 (Fqdn)。 如需其他選項，請參閱 hello[疑難排解中斷的連結文件](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1)。

## <a name="next-steps"></a>後續步驟
[使用 Azure AD 應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)
