---
title: "在 Azure AD Application Proxy aaaCustom 網域 |Microsoft 文件"
description: "管理 Azure AD Application Proxy 中的自訂網域，所以 hello hello 應用程式 URL 是 hello 相同不論您的使用者存取的位置。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 中的自訂網域

當您發行應用程式透過 Azure Active Directory 應用程式 Proxy 時，您會建立從遠端使用您的使用者 toogo toowhen 的外部 URL。 此 URL 取得 hello 預設網域*yourtenant.msappproxy.net*。 比方說，如果您發行應用程式名為費用，而且您的租用戶名為 Contoso，則 hello 外部 URL 將是 https://expenses-contoso.msappproxy.net。 如果您想 toouse 您自己的網域名稱，請設定您的應用程式的自訂網域。 

建議您盡可能為應用程式設定自訂網域。 自訂網域的 hello 優點包括：

- 您的使用者可以取得 toohello 應用程式與 hello 相同的 URL，是否正在內部或外部網路。
- 如果所有應用程式有 hello 相同的內部和外部 Url，一個應用程式中點 tooanother 的連結就會繼續 toowork 即使外部 hello 公司網路。 
- 您控制您的品牌，並建立您想要的 hello Url。 


## <a name="configure-a-custom-domain"></a>設定自訂網域

### <a name="prerequisites"></a>必要條件

設定自訂網域之前，請確定您有下列需求已備妥的 hello: 
- A[已驗證的網域加入 Active Directory tooAzure](active-directory-domains-add-azure-portal.md)。
- Hello 網域，請在 PFX 檔案的 hello 表單自訂的憑證。 
- [透過應用程式 Proxy 發佈](application-proxy-publish-azure-portal.md)的內部部署應用程式。

### <a name="configure-your-custom-domain"></a>設定自訂網域

當您準備這些三個需求時，請遵循這些步驟 tooset，註冊您的自訂網域：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽過**Azure Active Directory** > **企業應用程式** > **所有應用程式**選擇 hello 應用程式想 toomanage。
3. 選取 [應用程式 Proxy]。 
4. 在 [hello 外部 URL] 欄位中，使用 hello 下拉式清單 tooselect 您的自訂網域。 如果您沒有看到 hello 清單中的網域，然後它尚未經過驗證尚未。 
5. 選取 [儲存]。
5. hello**憑證**已停用的欄位會變成啟用。 選取此欄位。 

   ![按一下 tooupload 憑證](./media/active-directory-application-proxy-custom-domains/certificate.png)

   如果您已上傳此網域的憑證，憑證 [hello] 欄位會顯示 hello 憑證資訊。 

6. Hello PFX 憑證上傳，然後輸入 hello 憑證 hello 密碼。 
7. 選取**儲存**toosave 您的變更。 
8. 新增[DNS 記錄](../dns/dns-operations-recordsets-portal.md)重新導向 hello 新外部 URL toohello msappproxy.net 網域。 

>[!TIP] 
>您只需要每個自訂網域的 tooupload 一個憑證。 一旦您上傳憑證，您可以選擇 hello 自訂網域，當您發行新應用程式並沒有 toodo 除了 hello DNS 記錄的其他組態。 

## <a name="manage-certificates"></a>管理憑證

### <a name="certificate-format"></a>憑證格式
沒有任何限制 hello 憑證簽章方法上。 橢圓曲線密碼編譯 (ECC)、主體別名 (SAN) 和其他常見的憑證類型均可支援。 

只要 hello 萬用字元比對所需的 hello 外部 URL，您可以使用萬用字元憑證。 

您也可以使用自我簽署的憑證。 如果您使用私人憑證授權單位，hello CDP （憑證撤銷點發佈點） hello 憑證應該是公用的。

### <a name="changing-hello-domain"></a>變更 hello 定義域
所有已驗證的網域會出現在您的應用程式的 hello 外部 URL 下拉式清單中。 toochange hello 網域中，只需欄位 hello 應用程式的更新。 如果您想要的 hello 網域不在 hello 清單[將它新增為已驗證的網域](active-directory-domains-add-azure-portal.md)。 如果您選取的網域沒有相關聯的憑證，請依照下列步驟 5-7 tooadd hello 憑證。 接著，請確認您已更新 hello DNS 記錄 tooredirect 從 hello 新的外部 URL。 

### <a name="certificate-management"></a>憑證管理
您可以使用相同憑證的多個應用程式除非 hello 應用程式共用的外部主機的 hello。 

您會收到警告憑證過期時，告知您 tooupload 透過 hello 入口網站的另一個憑證。 如果 hello 憑證已撤銷，因為您的使用者存取 hello 應用程式時可能會看到安全性警告。 我們不會執行憑證的撤銷檢查。  tooupdate hello 憑證指定的應用程式中，瀏覽 toohello 應用程式，並遵循步驟 5-7 上發行的應用程式 tooupload 新的憑證設定自訂網域。 如果 hello 舊的憑證未由其他應用程式使用中，它會自動刪除。 

目前所有憑證管理都是透過個別的應用程式頁面，您需要 toomanage hello hello 相關應用程式內容中的憑證。 

## <a name="next-steps"></a>後續步驟
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)tooyour 發行應用程式與 Azure AD 驗證。
* [啟用條件式存取](active-directory-application-proxy-conditional-access.md)tooyour 已發佈的應用程式。
* [加入您的自訂網域名稱 tooAzure AD](active-directory-domains-add-azure-portal.md)


