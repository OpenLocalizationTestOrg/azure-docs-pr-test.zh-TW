---
title: "aaaAdd CDN tooan Azure App Service |Microsoft 文件"
description: "加入內容傳遞網路 (CDN) tooan Azure App Service toocache，並從伺服器關閉 tooyour hello 世界各地的客戶提供靜態檔案。"
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>將內容傳遞網路 (CDN) tooan Azure App Service

[Azure 內容傳遞網路 (CDN)](../cdn/cdn-overview.md)會在策略性放置的位置傳遞內容 toousers tooprovide 最大輸送量的靜態網頁內容快取。 hello CDN 也會減少伺服器負載 web 應用程式上。 本教學課程示範如何 tooadd Azure CDN tooa [Azure App Service 中的 web 應用程式](app-service-web-overview.md)。 

以下是 hello hello 範例靜態 HTML 網站首頁，您將使用：

![範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

您將學到什麼：

> [!div class="checklist"]
> * 建立 CDN 端點。
> * 重新整理快取的資產。
> * 使用查詢字串快取 toocontrol 版本。
> * 使用自訂網域 hello CDN 端點。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

- [安裝 Git](https://git-scm.com/)
- [安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>建立 hello web 應用程式

toocreate hello web 應用程式，您會使用後續 hello[靜態 HTML 快速入門](app-service-web-get-started-html.md)透過 hello**瀏覽 toohello 應用程式**步驟。

### <a name="have-a-custom-domain-ready"></a>備妥自訂網域

toocomplete hello 自訂網域步驟本教學課程中，您需要 tooown 自訂網域，並存取 tooyour DNS 登錄的網域提供者 （例如 GoDaddy)。 例如，tooadd DNS 項目`contoso.com`和`www.contoso.com`，您必須擁有存取 tooconfigure hello 的 DNS 設定 hello`contoso.com`根網域。

如果您還沒有網域名稱，請考慮下列 hello[應用程式服務網域教學課程](custom-dns-web-site-buydomains-web-app.md)toopurchase 網域使用 hello Azure 入口網站。 

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

開啟瀏覽器並瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。

## <a name="create-a-cdn-profile-and-endpoint"></a>建立 CDN 設定檔和端點

在左瀏覽 hello，選取**應用程式服務**，然後選取 hello 應用程式，您可以在 hello[靜態 HTML 快速入門](app-service-web-get-started-html.md)。

![選取在 hello 入口網站 App Service 應用程式](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

在 hello **App Service**  頁面的 hello**設定**區段中，選取**網路 > 設定您的應用程式的 Azure CDN**。

![選取在 hello 入口網站中的 CDN](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

在 hello **Azure 內容傳遞網路**頁面上，提供 hello**新端點**hello 資料表中所指定的設定。

![在 hello 入口網站中建立設定檔和端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| 設定 | 建議的值 | 說明 |
| ------- | --------------- | ----------- |
| **CDN 設定檔** | myCDNProfile | 選取**建立新**toocreate CDN 設定檔。 CDN 設定檔是以 hello 的 CDN 端點的集合，相同的定價層。 |
| **定價層** | 標準 Akamai | hello[定價層](../cdn/cdn-overview.md#azure-cdn-features)指定 hello 提供者和可用的功能。 在本教學課程中，我們會使用標準 Akamai。 |
| **CDN 端點名稱** | 任何在 hello azureedge.net 網域中為唯一的名稱 | 存取您快取的資源在 hello 網域*\<端點名稱 >。 azureedge.net*。

選取 [ **建立**]。

Azure 會建立 hello 設定檔和端點。 hello 新端點會出現在 hello**端點**清單 hello 相同頁面上，而且已佈建時 hello 狀態**執行**。

![清單中的新端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>測試 hello CDN 端點

如果您選取了 Verizon 定價層，通常需要大約 90 分鐘的時間進行端點傳播。 若為 Akamai，傳播需要幾分鐘的時間

hello 範例應用程式具有`index.html`檔案和*css*， *img*，和*js*包含其他靜態資產的資料夾。 內容的所有這些檔案的路徑是 hello hello 相同在 hello CDN 端點。 例如，這兩個 hello 下列 Url 存取 hello *bootstrap.css*檔案在 hello *css*資料夾：

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

瀏覽下列 URL 的瀏覽器 toohello:

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 提供的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 您會看到的 hello 相同頁面上您先前在 Azure web 應用程式中執行。 Azure CDN 已擷取 hello 來源 web 應用程式的資產，並為從 hello CDN 端點服務

tooensure hello CDN，重新整理 hello 頁面中，此頁面會快取。 兩個要求的 hello 相同資產有時候是必要的 hello CDN toocache hello 要求的內容。

如需建立 Azure CDN 設定檔和端點的詳細資訊，請參閱[開始使用 Azure CDN](../cdn/cdn-create-new-endpoint.md)。

## <a name="purge-hello-cdn"></a>清除 hello CDN

hello CDN 會定期重新整理其資源與 hello 來源 web 應用程式根據 hello 存留時間 (TTL) 設定。 hello 預設 TTL 是七天。

有時候您可能需要 toorefresh hello CDN 之前 hello TTL 到期-比方說，當您部署更新的內容 toohello web 應用程式。 tootrigger 重新整理，您可以手動清除 hello CDN 資源。 

在本節中的 hello 教學課程，您可以部署變更 toohello web 應用程式，並清除 hello CDN tootrigger hello CDN toorefresh 其快取。

### <a name="deploy-a-change-toohello-web-app"></a>部署變更 toohello web 應用程式

開啟 hello`index.html`檔案，然後加入"-V2"toohello H1 標題，hello 下列範例所示： 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

認可您的變更，並將它部署 toohello web 應用程式。

```bash
git commit -am "version 2"
git push azure master
```

部署完成後，請瀏覽 toohello web 應用程式 URL，並請參閱變更 hello。

```
http://<appname>.azurewebsites.net/index.html
```

![Web 應用程式標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

瀏覽 URL hello 首頁上和您看不到變更，因為 hello hello CDN 中快取的版本尚未到期的 hello toohello CDN 端點。 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中沒有 V2](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>清除 hello 入口網站中的 hello CDN

tootrigger hello CDN tooupdate 快取的版本中，清除 hello CDN。

在 hello 入口網站的左側瀏覽選取**資源群組**，然後選取您為您的 web 應用程式 (myResourceGroup) 建立的 hello 資源群組。

![選取資源群組](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

在 [hello] 清單中的資源，選取您的 CDN 端點。

![選取端點](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

頂端的 hello hello**端點**頁面上，按一下**清除**。

![選取清除](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

輸入您想 toopurge hello 內容路徑。 您可以將個別檔案或路徑區段 toopurge 所傳遞的完整檔案路徑 toopurge，並重新整理資料夾中的所有內容。 因為您變更`index.html`，確定其中一個 hello 路徑。

在 hello hello 頁面底部，選取**清除**。

![清除頁面](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>確認 CDN 會更新該 hello

等候 hello 的清除要求完成處理時，通常需要幾分鐘。 toosee hello 目前狀態，在 hello hello 頁面最上方的 hello 選取鈴鐺圖示。 

![清除通知](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

瀏覽 toohello CDN 端點 URL `index.html`，現在您會看見 hello V2 hello 首頁上，加入 toohello 標題和。 這會顯示 hello CDN 快取重新整理。

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

如需詳細資訊，請參閱[清除 Azure CDN 端點](../cdn/cdn-purge-endpoint.md)。 

## <a name="use-query-strings-tooversion-content"></a>使用查詢字串 tooversion 內容

hello Azure CDN 提供 hello 下列快取行為的選項：

* 忽略查詢字串
* 略過查詢字串的快取
* 快取每個唯一的 URL 

第一次 hello 這些是 hello 預設，這表示不論 hello 查詢字串 hello URL 中的資產只能有一個快取的版本。 

在本節中的 hello 教學課程，您可以變更 hello 快取行為 toocache 每個唯一的 URL。

### <a name="change-hello-cache-behavior"></a>變更 hello 快取行為

在 Azure 入口網站 hello **CDN 端點**頁面上，選取**快取**。

選取**快取每個唯一的 URL**從 hello**查詢字串快取行為**下拉式清單。

選取 [ **儲存**]。

![選取查詢字串快取行為](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>確認唯一的 URL 會分開快取

在瀏覽器中，瀏覽 toohello 首頁上，在 hello CDN 端點，但包含查詢字串： 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

hello CDN 傳回 hello 目前 web 應用程式內容，其中包含 「 V2"hello 標題中。 

tooensure hello CDN，重新整理 hello 頁面中，此頁面會快取。 

開啟`index.html`也變更 「 V2"和"V3"，並將部署的 hello 變更。 

```bash
git commit -am "version 3"
git push azure master
```

在瀏覽器，移 toohello CDN 端點 URL 」 包含新的查詢字串例如`q=2`。 目前的 hello CDN 取得 hello`index.html`檔並且顯示"V3"。  但是，如果您瀏覽 toohello CDN 端點以 hello`q=1`查詢字串，您會看到 「 V2"。

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN 標題中的 V3，查詢字串 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN 標題中的 V2，查詢字串 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

此輸出會顯示每個查詢字串是以不同方式處理：

* 以前使用 q=1，因此會傳回快取內容 (V2)。
* q = 2 是新的因此 hello 最新的 web 應用程式內容都會擷取並傳回 (V3)。

如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../cdn/cdn-query-string.md)。

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>對應的自訂網域 tooa CDN 端點

您會藉由建立一筆 CNAME 記錄對應您的自訂網域 tooyour CDN 端點。 CNAME 記錄是一種 DNS 功能，將來源網域 tooa 目的地定義域對應。 例如，您可能會將對應`cdn.contoso.com`或`static.contoso.com`太`contoso.azureedge.net`。

如果您沒有自訂網域，請考慮下列 hello[應用程式服務網域教學課程](custom-dns-web-site-buydomains-web-app.md)toopurchase 網域使用 hello Azure 入口網站。 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>尋找 hello hostname toouse 以 hello CNAME

Hello Azure 入口網站中**端點**頁面上，確定**概觀**已選取左瀏覽，，然後選取 hello hello **+ 自訂網域**hello hello 頁頂端的按鈕。

![選取新增自訂網域](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

在 [hello**加入自訂網域**] 頁面上，您會看到 hello 端點主機名稱 toouse 中建立 CNAME 記錄。 hello 主機名稱衍生自您的 CDN 端點 URL: **&lt;端點名稱 >。 azureedge.net**。 

![新增網域頁面](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>設定向網域註冊機構 hello CNAME

瀏覽 tooyour 網域註冊機構的網站，並找出 hello 區段，用於建立 DNS 記錄。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。

用於管理 Cname 尋找 hello > 一節。 您可能會有 toogo tooan 進階的設定 頁面上，並尋找 hello 文字 CNAME、 別名或子網域。

建立 CNAME 記錄對應您所選擇的子網域 (例如，**靜態**或**cdn**) toohello**端點主機名稱**hello 入口網站中稍早所示。 

### <a name="enter-hello-custom-domain-in-azure"></a>輸入在 Azure 中的 hello 自訂網域

傳回 toohello**加入自訂網域**頁面，然後輸入您的自訂網域，包括 hello 子網域，在 [hello] 對話方塊中。 例如，輸入 `cdn.contoso.com`。   
   
Azure 會確認 hello CNAME 記錄存在您所輸入的 hello 網域名稱。 如果 hello CNAME 正確無誤，則會驗證您的自訂網域。

可能需要 hello CNAME 記錄 toopropagate tooname 伺服器 hello 網際網路上的時間。 如果您的網域不會立即驗證，請稍候幾分鐘，然後再試一次。

### <a name="test-hello-custom-domain"></a>測試 hello 自訂網域

在瀏覽器中，瀏覽 toohello`index.html`檔案使用自訂網域 (例如， `cdn.contoso.com/index.html`) tooverify hello 結果是相同 hello 做為當您移直接太`<endpointname>azureedge.net/index.html`。

![使用自訂網域 URL 的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

如需詳細資訊，請參閱[對應 Azure CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md)。

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>後續步驟

您已了解如何︰

> [!div class="checklist"]
> * 建立 CDN 端點。
> * 重新整理快取的資產。
> * 使用查詢字串快取 toocontrol 版本。
> * 使用自訂網域 hello CDN 端點。

了解下列 hello toooptimize CDN 效能的文件：

> [!div class="nextstepaction"]
> [在 Azure CDN 中壓縮檔案以改善效能](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [在 Azure CDN 端點上預先載入資產](../cdn/cdn-preload-endpoint.md)
