---
title: "aaa\"啟用 HTTPS，在 Azure 的 CDN 自訂網域 |Microsoft 文件 」"
description: "深入了解如何在您的 Azure CDN 端點的自訂網域上 tooenable HTTPS。"
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>在 Azure CDN 自訂網域上啟用 HTTPS

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Azure CDN 自訂網域的 HTTPS 支援可讓您透過 SSL 使用的資料在傳輸過程中您的網域名稱 tooimprove hello 安全性 toodeliver 安全內容。 您的自訂網域的 hello 端對端工作流程 tooenable HTTPS 已經過簡化，透過一種單鍵啟用，完成憑證管理，以及所有的任何額外的成本。

它是關鍵 tooensure hello 隱私性及您 web 應用程式的機密資料在傳輸過程中的所有資料完整性。 使用 HTTPS 通訊協定可確保您的機密資料已加密時透過傳送的嗨 hello 網際網路。 它提供信任與認證，並保護您的 Web 免於攻擊。 目前，Azure CDN 支援 CDN 端點上的 HTTPS。 舉例來說，當您從 Azure CDN (https://contoso.azureedge.net) 建立端點時，預設會啟用 HTTPS。 現在透過自訂網域 HTTPS，您也可以針對自訂網域 (如 https://www.contoso.com) 啟用安全傳遞。 

Hello 的 HTTPS 功能的索引鍵屬性的部分包括：

- 不須額外付費：取得或續約憑證不須付費，且 HTTPS 流量不另外收費。 您只需支付從 hello CDN GB 輸出。

- 簡單的啟用： 一個按一下佈建是可從 hello [Azure 入口網站](https://portal.azure.com)。 您也可以使用 REST API 或其他開發人員工具 tooenable hello 功能。

- 完整憑證管理：為您處理所有憑證採購及管理。 憑證會自動佈建及更新先前 tooexpiration。 這完全移除服務中斷，因為憑證即將到期的 hello 的風險。

>[!NOTE] 
>先前 tooenabling HTTPS 支援，您必須已經建立[Azure CDN 自訂網域](./cdn-map-content-to-custom-domain.md)。

## <a name="step-1-enabling-hello-feature"></a>步驟 1： 啟用 hello 功能 

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour Verizon 標準或進階的 CDN 設定檔。

2. 在 [hello] 清單中的端點，hello 端點包含您的自訂網域。

3. 按一下您想要的 tooenable HTTPS hello 自訂網域。

    ![端點刀鋒視窗](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. 按一下**上**tooenable HTTPS 並儲存 hello 變更。

    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>步驟 2︰網域驗證

>[!IMPORTANT] 
>必須先完成網域驗證才能在您的自訂網域上啟用 HTTPS。 您有 6 商務天 tooapprove hello 網域。 6 個工作天內沒有核准將會取消要求。  

啟用 HTTPS，在您的自訂網域之後，我們的 HTTPS 憑證提供者 DigiCert 會為您的網域，根據 WHOIS registrant 資訊，請透過 （依預設） 的電子郵件或電話連絡 hello registrant 驗證您的網域擁有權。 DigiCert 也會傳送 hello 驗證電子郵件 toohello 下方位址。 如果 WHOIS 註冊者資訊為私用，請確定您可以直接從下列其中一個地址做出核准。

>admin@<your-domain-name.com> administrator@<your-domain-name.com>  
>webmaster@<your-domain-name.com>  
>hostmaster@<your-domain-name.com>  
>postmaster@<your-domain-name.com>


在收到 hello 電子郵件時，您有兩個驗證選項：

1. 您可以為核准所有未來的訂單 hello 透過使用相同帳戶執行 hello 相同的根網域，例如 consoto.com。這是建議的方法，如果您計劃 tooadd 中的其他自訂網域 hello 未來 hello 相同的根網域。
 
2. 您只可以核准此要求中所使用的 hello 特定主機名稱。 後續的要求將需要另外核准。

    範例電子郵件：
    
    ![自訂 HTTPS 對話方塊](./media/cdn-custom-ssl/domain-validation-email-example.png)

核准之後，DigiCert 會加入您的自訂網域名稱 toohello 的 SAN 憑證。 hello 憑證一年才有效，並會自動更新已過期。

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>步驟 3： 等候 hello 傳播，然後開始使用您的功能

Hello 網域名稱驗證完成後就會在 hello 自訂網域 HTTPS 功能 toobe active too6 8 小時。 Hello 程序完成之後，hello Azure 入口網站中的 hello"自訂 HTTPS"狀態會設定太 「 已啟用 」。 您現在即可使用訂網域的 HTTPS 功能。

## <a name="frequently-asked-questions"></a>常見問題集

1. *Hello 憑證提供者，以及使用何種類型是憑證的誰？*

    我們使用 DigiCert 提供的主題別名 (SAN) 憑證。 SAN 憑證可以使用一個憑證來保護多個完整網域名稱。

2. *是否可以使用自己的憑證？*
    
    目前不可以，但其在 hello 藍圖。

3. *如果沒有收到 hello 網域驗證電子郵件從 DigiCert 嗎？*

    如果您沒有在 24 小時內收到驗證電子郵件，請連絡 Microsoft。

4. *SAN 憑證的安全性是否比專用憑證來得低？*
    
    SAN 憑證，如下所示 hello 做為專用的憑證相同的加密及安全性標準。所有核發的 SSL 憑證都使用 SHA-256 來加強伺服器安全性。

5. *是否可以搭配 Akamai 的 Azure CDN 使用自訂網域 HTTPS？*

    此功能目前只提供給 Verizon 的 Azure CDN。 我們正在 hello 未來幾個月中支援 Azure cdn Akamai 從這項功能。


## <a name="next-steps"></a>後續步驟

- 深入了解如何註冊 tooset[上您的 Azure CDN 端點的自訂網域](./cdn-map-content-to-custom-domain.md)


