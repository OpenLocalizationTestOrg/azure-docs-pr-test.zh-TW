---
title: "aaaClaims 感知應用程式的 Azure AD 應用程式 Proxy |Microsoft 文件"
description: "如何 toopublish 內部接受您的使用者的安全遠端存取的 ADFS 宣告的 ASP.NET 應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>在應用程式 Proxy 中使用宣告感知應用程式
[宣告感知應用程式](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx)執行重新導向 toohello 安全性權杖服務 (STS)。 hello STS hello 使用者，但是也會語彙基元要求認證，然後重新導向 hello 使用者 toohello 應用程式。 有幾個方式 tooenable 應用程式 Proxy toowork，與這些重新導向。 針對宣告感知應用程式使用此發行項 tooconfigure 您的部署。 

## <a name="prerequisites"></a>必要條件
請確定該 hello 宣告感知應用程式的 hello STS 重新導向 toois 與內部網路之外使用。 您可以提供 hello STS 公開透過 proxy，或允許外部連接。 

## <a name="publish-your-application"></a>發佈您的應用程式

1. 將根據 toohello 指示中所述的應用程式發行[發行應用程式 Proxy](application-proxy-publish-azure-portal.md)。
2. 瀏覽 toohello 應用程式頁面上，在入口網站，並選取 hello**單一登入**。
3. 如果您選擇 [Azure Active Directory] 作為您的 [預先驗證方法]，請選取 [Azure AD 單一登入已停用] 作為您的 [內部驗證方法]。 如果您選擇**通過**做為您**預先驗證方法**，您不需要 toochange 任何項目。

## <a name="configure-adfs"></a>設定 ADFS

您可以使用以下兩種方式之一為宣告感知應用程式設定 ADFS。 hello 第一個是使用自訂網域。 WS-同盟與第二個是 hello。 

### <a name="option-1-custom-domains"></a>選項 1：自訂網域

如果所有 hello 內部 Url，您的應用程式的完整網域名稱 (Fqdn)，則您可以設定[自訂網域](active-directory-application-proxy-custom-domains.md)應用程式。 使用 hello 自訂網域 toocreate 外部 Url hello 與 hello 內部 Url 相同。 當您的外部 Url 符合您的內部 Url 時，hello STS 重新導向會使用您的使用者是否在內部部署或遠端。 

### <a name="option-2-ws-federation"></a>選項 2：WS-同盟

1. 開啟 [ADFS 管理]。
2. 跳過**信賴憑證者信任**，以滑鼠右鍵按一下您要發行應用程式 proxy 的 hello 應用程式，然後選擇 **屬性**。  

   ![信賴憑證者信任 - 以滑鼠右鍵按一下應用程式名稱 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. 在 hello**端點**索引標籤，在**端點類型**，選取**WS-同盟**。
4. 下**信任 URL**，輸入您在輸入 hello 下的應用程式 Proxy 的 hello URL**外部 URL**按一下**[確定]**。  

   ![新增端點 - 設定 [信任的 URL] 值 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>後續步驟
* 對於非宣告感知的應用程式，請[啟用單一登入](application-proxy-sso-overview.md)
* [啟用原生用戶端應用程式 toointeract 與 proxy 應用程式](active-directory-application-proxy-native-client.md)


