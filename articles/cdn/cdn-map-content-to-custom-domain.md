---
title: "aaaMap Azure CDN 內容 tooa 自訂網域 |Microsoft 文件"
description: "了解如何 toomap Azure CDN 內容 tooa 自訂網域。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Azure CDN 內容 tooa 自訂網域對應
您可以在內容而不是使用 azureedge.net 的子網域的 Url toocached 專屬網域名稱對應順序 toouse 中的自訂網域 tooa CDN 端點。

有兩種方式 toomap 自訂網域 tooa CDN 端點：

1. [向網域註冊機構建立 CNAME 記錄，並將對應自訂網域和子網域 toohello CDN 端點](#register-a-custom-domain-for-an-azure-cdn-endpoint)。
   
    CNAME 記錄是一種 DNS 功能，例如對應來源網域`www.contosocdn.com`或`cdn.contoso.com`，tooa 目的地網域。 在此情況下，hello 來源網域是您的自訂網域和子網域 (子網域、 like **www**或**cdn**永遠是必要項)。 hello 目的地網域則是您的 CDN 端點。  
   
    對應您的自訂網域 tooyour CDN 端點的 hello 程序，不過，導致在短暫的停機時間 hello 網域在 hello Azure 入口網站中註冊 hello 網域時。
2. [使用 **cdnverify** 加入中繼註冊步驟](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    如果您的自訂網域目前支援的應用程式需要的任何停機時間，服務等級協定 (SLA)，則您可以使用 hello Azure **cdnverify**子網域 tooprovide 中繼的註冊步驟，因此使用者會無法 tooaccess 您的網域時 hello DNS 對應進行。  

註冊您的自訂網域使用其中一種 hello 上述程序之後，您會想太[確認該 hello 自訂子網域參考 CDN 端點](#verify-that-the-custom-subdomain-references-your-cdn-endpoint)。

> [!NOTE]
> 您必須建立一筆 CNAME 記錄與您的網域註冊機構 toomap 網域 toohello CDN 端點。 CNAME 記錄會對應至特定子網域 (例如 `www.contoso.com` 或 `cdn.contoso.com`)。 它不可能 toomap CNAME 記錄 tooa 根網域，例如`contoso.com`。
> 
> 一個子網域只能與一個 CDN 端點產生關聯。 hello 您所建立的 CNAME 記錄會路由傳送所有流量處理 toohello 子網域 toohello 指定端點。  例如，如果您將 `www.contoso.com` 與您的 CDN 端點產生關聯，則無法將它與其他 Azure 端點產生關聯 (例如，儲存體帳戶端點或雲端服務端點)。 不過，您可以使用不同的子網域 hello 從不同的服務端點的相同網域。 您也可以將對應不同的子網域 toohello 相同的 CDN 端點。
> 
> 如**Verizon 從 Azure CDN** （Standard 和 Premium） 端點，請注意，因此會佔用太**90 分鐘**如變更 toopropagate tooCDN 邊緣節點的自訂網域。
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>註冊 Azure CDN 端點的自訂網域
1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**瀏覽**，然後**CDN 設定檔**，然後 hello 的 CDN 設定檔想與 hello 端點 toomap tooa 自訂網域。  
3. 在 hello**的 CDN 設定檔**刀鋒視窗中，按一下您要與其 tooassociate hello 子網域的 hello CDN 端點。
4. 在 hello hello 端點刀鋒視窗頂端，按一下 hello**加入自訂網域** 按鈕。  在 hello**加入自訂網域**刀鋒視窗中，您會看到 hello 端點主機名稱，衍生自 CDN 端點，toouse 中建立新的 CNAME 記錄。 hello hello 主機名稱位址的格式將會顯示為**&lt;端點名稱 >。 azureedge.net**。  您可以複製這個主機名稱 toouse 建立 hello CNAME 記錄。  
5. 瀏覽 tooyour 網域註冊機構的網站，並找出 hello 區段，用於建立 DNS 記錄。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
6. 用於管理 Cname 尋找 hello > 一節。 您可能會有 toogo tooan 進階的設定 頁面上，並尋找 hello 文字 CNAME、 別名或子網域。
7. 建立新的 CNAME 記錄對應您所選擇的子網域 (例如， **www**或**cdn**) toohello hello 中提供的主機名稱**加入自訂網域**刀鋒視窗。 
8. 傳回 toohello**加入自訂網域**刀鋒視窗中，輸入您的自訂網域，包括 hello 子網域，在 [hello] 對話方塊中。 例如，輸入 hello 網域名稱格式為 hello`www.contoso.com`或`cdn.contoso.com`。   
   
   Azure 會確認 hello CNAME 記錄存在您所輸入的 hello 網域名稱。 如果 hello CNAME 正確無誤，則會驗證您的自訂網域。  如**Verizon 從 Azure CDN** （Standard 和 Premium） 端點，就會在 too90 分鐘的時間，自訂網域設定 toopropagate tooall CDN 邊緣節點，不過。  
   
   請注意，在某些情況下，它可能需要 hello CNAME 記錄 toopropagate tooname 伺服器 hello 網際網路上的時間。 如果您的網域並未立即通過驗證，而且您認為 hello CNAME 記錄正確，然後等候數分鐘，然後再試。

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>註冊使用 hello 中繼 cdnverify 子網域的 Azure CDN 端點的自訂網域
1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**瀏覽**，然後**CDN 設定檔**，然後 hello 的 CDN 設定檔想與 hello 端點 toomap tooa 自訂網域。  
3. 在 hello**的 CDN 設定檔**刀鋒視窗中，按一下您要與其 tooassociate hello 子網域的 hello CDN 端點。
4. 在 hello hello 端點刀鋒視窗頂端，按一下 hello**加入自訂網域** 按鈕。  在 hello**加入自訂網域**刀鋒視窗中，您會看到 hello 端點主機名稱，衍生自 CDN 端點，toouse 中建立新的 CNAME 記錄。 hello hello 主機名稱位址的格式將會顯示為**&lt;端點名稱 >。 azureedge.net**。  您可以複製這個主機名稱 toouse 建立 hello CNAME 記錄。
5. 瀏覽 tooyour 網域註冊機構的網站，並找出 hello 區段，用於建立 DNS 記錄。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
6. 用於管理 Cname 尋找 hello > 一節。 您可能會有 toogo tooan 進階的設定 頁面上，並查看 hello 文字**CNAME**，**別名**，或**子網域**。
7. 建立新的 CNAME 記錄，並提供包含 hello 的子網域別名**cdnverify**子網域。 例如，您指定的 hello 子網域會 hello 格式**cdnverify.www**或**cdnverify.cdn**。 然後 hello 主機名稱，也就是您的 CDN 端點，hello 格式提供**cdnverify。&lt;端點名稱 >。 azureedge.net**。 您的 DNS 對應看起來應該類似：`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. 傳回 toohello**加入自訂網域**刀鋒視窗中，輸入您的自訂網域，包括 hello 子網域，在 [hello] 對話方塊中。 例如，輸入 hello 網域名稱格式為 hello`www.contoso.com`或`cdn.contoso.com`。 請注意，在此步驟中，您不需要 toopreface hello 子網域與**cdnverify**。  
   
    Azure 會確認 hello CNAME 記錄存在您所輸入的 hello cdnverify 網域名稱。
9. 此時，您的自訂網域已經由 Azure 驗證，但流量 tooyour 網域但未路由的 tooyour CDN 端點。 之後等候夠長，tooallow hello 自訂網域設定 toopropagate toohello CDN 邊緣節點 (90 分鐘的時間**Verizon 從 Azure CDN**1-2 分鐘的時間、 **Akamai 從 Azure CDN**)，傳回 tooyour DNS註冊機構的網站，並建立另一個對應的子網域 tooyour CDN 端點的 CNAME 記錄。 例如，指定 hello 子網域為**www**或**cdn**，hello 做為主機名稱和**&lt;端點名稱 >。 azureedge.net**。 有了這個步驟中，您的自訂網域的 hello 註冊已完成。
10. 最後，您可以刪除 hello 使用您所建立的 CNAME 記錄**cdnverify**，因為它需要只做為中間步驟。  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>請確認該 hello 自訂子網域參考 CDN 端點
* 您已完成 hello 註冊您的自訂網域之後，您可以在您的 CDN 端點使用 hello 自訂網域存取快取的內容。
  首先，確定您擁有 hello 端點已經快取的公用內容。 例如，如果您的 CDN 端點與儲存體帳戶相關聯，hello CDN 快取公用 blob 容器中的內容。 tootest hello 自訂網域，請確定您的容器設定 tooallow 公用存取，且其包含至少一個 blob。
* 在瀏覽器中瀏覽 toohello 位址 hello blob 使用 hello 自訂網域。 例如，如果您的自訂網域為`cdn.contoso.com`，hello URL tooa 快取的 blob 將會類似下列 URL 的 toohello: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>另請參閱
[如何 tooEnable hello azure 的內容傳遞網路 (CDN)](cdn-create-new-endpoint.md)  

