---
title: "將 Azure CDN 內容對應至自訂網域 | Microsoft Docs"
description: "了解如何將 Azure CDN 內容對應至自訂網域。"
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
ms.openlocfilehash: cd6db44f7776859d1e6a893543cf0666182ca41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="map-azure-cdn-content-to-a-custom-domain"></a>將 Azure CDN 內容對應至自訂網域
您可以將自訂網域對應至 CDN 端點，以在所快取內容的 URL 中使用您自己的網域名稱，而不是使用 azureedge.net 的子網域。

有兩種方式可將您的自訂網域對應至 CDN 端點：

1. [向網域註冊機構建立 CNAME 記錄，並將您的自訂網域和子網域對應至 CDN 端點](#register-a-custom-domain-for-an-azure-cdn-endpoint)。
   
    CNAME 記錄是將 `www.contosocdn.com` 或 `cdn.contoso.com` 等來源網域對應至目的地網域的 DNS 功能。 在這種情況下，來源網域是您的自訂網域和子網域 (像是 **www** 或 **cdn** 的子網域一律是必要項目)。 目的地網域是 CDN 端點。  
   
    然而，在將自訂網域對應至 CDN 端點的過程中，會由於您在 Azure 入口網站中註冊網域而導致網域短暫停擺。
2. [使用 **cdnverify** 加入中繼註冊步驟](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    如果自訂網域目前支援不得發生停機的服務等級協定 (SLA) 的應用程式，您可以使用 Azure **cdnverify** 子網域提供中繼註冊步驟，使用者就能在 DNS 對應發生時存取網域。  

您使用上述其中一個程序註冊自訂網域之後，您會想要 [確認自訂子網域參照您的 CDN 端點](#verify-that-the-custom-subdomain-references-your-cdn-endpoint)。

> [!NOTE]
> 您必須向網域註冊機構建立 CNAME 記錄，以將網域對應至 CDN 端點。 CNAME 記錄會對應至特定子網域 (例如 `www.contoso.com` 或 `cdn.contoso.com`)。 CNAME 記錄無法對應至根網域 (例如 `contoso.com`)。
> 
> 一個子網域只能與一個 CDN 端點產生關聯。 您所建立的 CNAME 記錄會將所有定址至子網域的流量路由傳送至指定的端點。  例如，如果您將 `www.contoso.com` 與您的 CDN 端點產生關聯，則無法將它與其他 Azure 端點產生關聯 (例如，儲存體帳戶端點或雲端服務端點)。 不過，針對不同的服務端點，您可以使用來自相同網域的不同子網域。 您也可以將不同的子網域對應至相同的 CDN 端點。
> 
> 若為**來自 Verizon 的 Azure CDN** (標準與進階) 端點，請注意，最多需要 **90 分鐘**的時間，才能將自訂網域變更傳播至 CDN 邊緣節點。
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>註冊 Azure CDN 端點的自訂網域
1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 依序按一下 [瀏覽] 和 [CDN 設定檔]，接著按一下包含要對應到自訂網域之端點的 CDN 設定檔。  
3. 在 [CDN 設定檔]  刀鋒視窗中，按一下要與子網域產生關聯的 CDN 端點。
4. 在 [端點] 刀鋒視窗頂端，按一下 [新增自訂網域] 按鈕。  在 [新增自訂網域] 刀鋒視窗中，您會看到衍生自 CDN 端點的端點主機名稱，其可用來建立新的 CNAME 記錄。 主機名稱位址的格式會顯示為 **&lt;EndpointName>.azureedge.net**。  您可以複製這個主機名稱，以用於建立 CNAME 記錄。  
5. 瀏覽至您網域註冊機構的網站，並找出用於建立 DNS 記錄的區段。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
6. 尋找管理 CNAME 的區段。 您可能需要移至進階設定頁面，並尋找 CNAME、Alias 或 Subdomains 單字。
7. 建立新的 CNAME 記錄，將您選擇的子網域 (例如 **www** 或 **cdn**) 對應到 [新增自訂網域] 刀鋒視窗中提供的主機名稱。 
8. 返回 [新增自訂網域]  刀鋒視窗，在對話方塊中輸入您的自訂網域 (包括子網域)。 例如，以 `cdn.contoso.com` 或 `www.contoso.com` 格式輸入網域名稱。   
   
   Azure 會確認您所輸入的網域名稱存在 CNAME 記錄。 如果 CNAME 正確，您的自訂網域就會驗證。  然而，若為 **來自 Verizon 的 Azure CDN** (標準與進階) 端點，最多可能需要 90 分鐘的時間，自訂網域設定才能傳播至 CDN 邊緣節點。  
   
   請注意，在某些情況下，可能需要時間讓 CNAME 記錄傳播到網際網路上的名稱伺服器。 如果未立即驗證您的網域，但您確信 CNAME 記錄正確，則請等待數分鐘的時間，然後再試一次。

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain"></a>註冊使用中繼 cdnverify 子網域的 Azure CDN 端點的自訂網域
1. 登入 [Azure 入口網站](https://portal.azure.com/)。
2. 依序按一下 [瀏覽] 和 [CDN 設定檔]，接著按一下包含要對應到自訂網域之端點的 CDN 設定檔。  
3. 在 [CDN 設定檔]  刀鋒視窗中，按一下要與子網域產生關聯的 CDN 端點。
4. 在 [端點] 刀鋒視窗頂端，按一下 [新增自訂網域] 按鈕。  在 [新增自訂網域] 刀鋒視窗中，您會看到衍生自 CDN 端點的端點主機名稱，其可用來建立新的 CNAME 記錄。 主機名稱位址的格式會顯示為 **&lt;EndpointName>.azureedge.net**。  您可以複製這個主機名稱，以用於建立 CNAME 記錄。
5. 瀏覽至您網域註冊機構的網站，並找出用於建立 DNS 記錄的區段。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
6. 尋找管理 CNAME 的區段。 您可能需要移至進階設定頁面，並尋找 **CNAME**、**Alias** 或 **Subdomains** 單字。
7. 建立新的 CNAME 記錄，並提供包含 **cdnverify** 子網域的子網域別名。 例如，您指定的子網域格式會是 **cdnverify.www** 或 **cdnverify.cdn**。 接著以格式 **cdnverify.&lt;EndpointName>.azureedge.net** 提供主機名稱，也就是您的 CDN 端點。 您的 DNS 對應看起來應該類似：`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. 返回 [新增自訂網域]  刀鋒視窗，在對話方塊中輸入您的自訂網域 (包括子網域)。 例如，以 `cdn.contoso.com` 或 `www.contoso.com` 格式輸入網域名稱。 請注意，在此步驟中，您不需要在子網域的前方加上 **cdnverify**。  
   
    Azure 會確認您所輸入的 cdnverify 網域名稱存在 CNAME 記錄。
9. 此時，自訂網域已通過 Azure 的驗證，不過前往網域的流量尚未路由傳送至 CDN 端點。 當等候的時間足以讓自訂網域設定傳播至 CDN 邊緣節點 (90 分鐘用於**來自 Verizon 的 Azure CDN**，1-2 分鐘用於**來自 Akamai 的 Azure CDN**) 之後，返回 DNS 註冊機構的網站，並建立另一個 CNAME 記錄，將子網域對應至您的 CDN 端點。 例如，將子網域指定為 **www** 或 **cdn**，並將主機名稱指定為 **&lt;EndpointName>.azureedge.net**。 待這個步驟完成後，自訂網域的註冊作業也宣告完成。
10. 最後，您可以透過 **cdnverify**刪除您建立的 CNAME 記錄，因為只有在中繼步驟才需要此記錄。  

## <a name="verify-that-the-custom-subdomain-references-your-cdn-endpoint"></a>確認自訂子網域參照您的 CDN 端點
* 完成註冊您的自訂網域之後，即可使用自訂網域存取 CDN 端點所快取的內容。
  請先確定您有端點上所快取的公用內容。 例如，如果您的 CDN 端點與儲存體帳戶相關聯，則 CDN 會快取公用 Blob 容器中的內容。 若要測試自訂網域，請確定您的容器設定為允許公用存取，而且它包含至少一個 Blob。
* 在瀏覽器中，使用自訂網域瀏覽至 Blob 位址。 例如，如果您的自訂網域是 `cdn.contoso.com`，快取 Blob 的 URL 會和下列 URL 類似：http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>另請參閱
[如何啟用 Azure 內容傳遞網路 (CDN)](cdn-create-new-endpoint.md)  

