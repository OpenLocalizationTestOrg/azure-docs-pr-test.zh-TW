---
title: "aaaSingle 登入與 Azure AD Application Proxy tooapps |Microsoft 文件"
description: "開啟 單一登入的 hello Azure 入口網站中的 Azure AD Application Proxy 發行內部部署的應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>使用應用程式 Proxy 進行單一登入的密碼保存庫

Azure Active Directory 應用程式 Proxy 可發佈內部部署應用程式，讓遠端員工也可以安全地存取它們，進而幫助您改進生產力。 在 hello Azure 入口網站，您也可以設定單一登入 (SSO) toothese 應用程式。 您的使用者只需要使用 Azure AD，tooauthenticate，他們可以存取您的企業應用程式無須 toosign 一次。

應用程式 Proxy 支援數個[單一登入模式](application-proxy-sso-overview.md)。 密碼型登入適用於使用使用者名稱/密碼組合進行驗證的應用程式。 當您設定密碼式登入您的應用程式，您的使用者必須 toosign 一次 toohello 在內部部署應用程式中。 在這之後，Azure Active Directory 儲存 hello 登入資訊，並自動提供它 toohello 應用程式時您的使用者從遠端存取。 

您應該已經使用應用程式 Proxy 發行並測試您的應用程式。 如果沒有，請依照下列中的 hello 步驟[使用 Azure AD Application Proxy 發行應用程式](application-proxy-publish-azure-portal.md)然後再回到這裡。 

## <a name="set-up-password-vaulting-for-your-application"></a>為應用程式設定密碼儲存庫存

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 選取 [Azure Active Directory]  >  [企業應用程式]  >  [所有應用程式]。
3. 從 hello 清單中，選取您要使用 SSO 向上 tooset hello 應用程式。  
4. 選取 [單一登入]。

   ![選取單一登入](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Hello SSO 模式中，選擇 **密碼式登入**。
6. 對於 hello 登入 URL，請輸入 hello URL hello 頁面讓使用者輸入其使用者名稱和密碼 toosign tooyour hello 公司網路外部的應用程式中。 這可能是 hello 發行 hello 透過應用程式 Proxy 的應用程式時所建立的外部 URL。 

   ![選擇密碼型登入並輸入您的 URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. 選取 [ **儲存**]。

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>測試應用程式

請您設定遠端存取 tooyour 應用程式的 tooexternal URL。 使用針對該應用程式的認證 （或 hello 認證的存取設定的測試帳戶） 登入。 一旦成功登入，您也應該能夠 tooleave hello 應用程式並返回時不需要再次輸入您的認證。 

## <a name="next-steps"></a>後續步驟

- 閱讀其他方式 tooimplement[單一登入應用程式 proxy](application-proxy-sso-overview.md)
- 深入了解[使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量](application-proxy-security-considerations.md)