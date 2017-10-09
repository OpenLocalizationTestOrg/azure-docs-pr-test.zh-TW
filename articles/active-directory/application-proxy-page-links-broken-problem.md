---
title: "在 hello 頁面上的 aaaLinks 不適用於應用程式 Proxy 應用程式 |Microsoft 文件"
description: "如何 tootroubleshoot 問題上您有與 Azure AD 整合的應用程式 Proxy 應用程式中斷連結"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>在 hello 頁面上的連結無法運作的應用程式 Proxy 應用程式

本文將協助您 tootroubleshoot 為什麼您的 Azure Active Directory 應用程式 Proxy 應用程式的連結無法正確運作。

## <a name="overview"></a>概觀 
之後發行的應用程式 Proxy 應用程式，工作預設會在 hello 應用程式會包含在 hello 連結 toodestinations hello 只將連結發佈根 URL。 hello 應用程式中的 hello 連結並非正在運作，hello hello 應用程式內部 URL 可能不包含所有 hello 目的地 hello 應用程式內的連結。

**為何這有關係？** 當按下應用程式中的連結，以做為其中一個內部 URL，在應用程式 Proxy 會嘗試 tooresolve hello URL hello 相同應用程式，或以做為外部使用的 URL。 如果 hello 連結指向不在 tooan 內部 URL hello 相同應用程式中，不屬於 tooeither 的這些值區，導致找不到的錯誤。

## <a name="ways-you-can-resolve-broken-links"></a>中斷連結的解決方式

有三種方式 tooresolve 此問題。 hello 以下幾個選擇是列在增加的複雜性。

1.  請確定 hello 內部 URL 是包含所有 hello 相關連結 hello 應用程式的根目錄。 這可讓所有連結 toobe 解析為發佈的內容內 hello 相同應用程式。

    如果您變更 hello 內部 URL，但不想 toochange hello 登陸頁面的使用者，變更 hello 首頁 URL toohello 先前發行的內部 URL。 作法是前往太"Azure Active Directory-"&gt;應用程式註冊-&gt;選取 hello 應用程式-&gt;屬性。 在這個內容索引標籤中，您會看到 hello 欄位 「 首頁 URL 」，您可以調整 toobe hello 預期登陸頁面。

2.  如果您的應用程式使用完整的網域名稱 (Fqdn)，使用[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)toopublish 應用程式。 這項功能可讓您同時在內部使用，相同的 URL toobe 和外部的 hello。

    此選項可確保您的應用程式中的 hello 連結是透過應用程式 Proxy 可外部存取，因為 hello 應用程式 toointernal Url 中的 hello 連結也會辨識外部。 請注意，所有的連結仍然需要 toobelong tooa 發行應用程式。 不過，使用此選項 hello 連結不需要 toobelong toohello 相同的應用程式，而且可以隸屬 toomultiple 應用程式。

3.  如果這些選項都不可行時，您將執行 URL 轉譯/重寫的新功能的 hello 預覽。 使用此選項時，內部 Url 或 hello HTML 主體的應用程式中存在的連結會轉譯，或 「 對應 」，toohello 發佈外部應用程式 Proxy Url。 這只適用於 hello HTML 或 CSS 中的連結，這無法協助如果透過 JS 產生您的連結。 

如此一來，我們強烈建議使用 hello[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)盡可能方案。 如果您想 toojoin hello 預覽，電子郵件傳送< aadapfeedback@microsoft.com >與 hello applicationId(s)。

## <a name="next-steps"></a>後續步驟
[使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)

