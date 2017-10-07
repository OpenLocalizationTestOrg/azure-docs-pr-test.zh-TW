---
title: "aaaBuy Azure Web 應用程式的自訂網域名稱"
description: "了解如何 toobuy 自訂網域名稱在 Azure App Service web 應用程式。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>針對 Azure Web Apps 購買自訂網域名稱

App Service 網域 (預覽) 是直接在 Azure 中管理的頂層網域。 它們可讓您輕鬆 toomanage 自訂網域[Azure Web Apps](app-service-web-overview.md)。 本教學課程會示範如何 toobuy 應用程式服務網域並指派 DNS 名稱 tooAzure Web 應用程式。

本文適用於 Azure App Service (Web Apps、API Apps、Mobile Apps、Logic Apps)。 針對 Azure VM 或 Azure 儲存體，請參閱[指派應用程式服務網域 tooAzure VM 或 Azure 儲存體](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)。 若為雲端服務，請參閱[設定 Azure 雲端服務的自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

* [建立 App Service 應用程式](/azure/app-service/)，或使用您針對另一個教學課程建立的應用程式。

## <a name="prepare-hello-app"></a>準備 hello 應用程式

在 Azure Web 應用程式，您的 web 應用程式的 toouse 自訂網域[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須付費的層 (**共用**，**基本**，**標準**，或**Premium**)。 在此步驟中，您確定該 hello web 應用程式在 hello 支援定價層。

### <a name="sign-in-tooazure"></a>登入 tooAzure

開啟 hello [Azure 入口網站](https://portal.azure.com)並以您的 Azure 帳戶登入。

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>瀏覽 toohello hello Azure 入口網站中的應用程式

從 hello 左窗格中，選取**應用程式服務**，然後選取 hello hello 應用程式名稱。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/select-app.png)

您會看到 hello hello App Service 應用程式管理頁面。  

### <a name="check-hello-pricing-tier"></a>核取 hello 定價層

在 hello 左瀏覽的 hello 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。

![相應增加功能表](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

hello 應用程式目前的階層會以藍色框線反白顯示。 請確定該 hello 應用程式不在 hello toomake**免費**層。 不支援自訂 DNS hello**免費**層。 

![檢查定價層](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

如果 hello App Service 方案不**免費**，請關閉 hello**選擇定價層**頁面上，並略過太[購買 hello 網域](#buy-the-domain)。

### <a name="scale-up-hello-app-service-plan"></a>向上擴充 hello App Service 方案

選取任何 hello 非可用層 (**共用**，**基本**，**標準**，或**Premium**)。 

按一下 [選取] 。

![檢查定價層](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

當您看到下列通知 hello 時，hello 調整規模作業已完成。

![擴充作業確認](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>購買 hello 網域

### <a name="sign-in-tooazure"></a>登入 tooAzure
開啟 hello [Azure 入口網站](https://portal.azure.com/)並以您的 Azure 帳戶登入。

### <a name="launch-buy-domains"></a>啟動購買網域
在 hello **Web 應用程式**索引標籤上，按一下您 web 應用程式，選取 hello 名稱**設定**，然後選取**自訂網域**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

在 hello**自訂網域**頁面上，按一下**購買網域**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>設定 hello 網域購買

在 hello**應用程式服務網域** 頁面的 hello**網域搜尋**中，輸入 hello 網域名稱，而您想要 toobuy 和型別`Enter`。 hello 建議可用的定義域會顯示 hello 文字 方塊的正下方。 選取您想要 toobuy 的一或多個定義域。 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

按一下 hello**連絡人資訊**並填寫 hello 網域的連絡人資訊表單。 完成後，請按一下**確定**tooreturn toohello 應用程式服務網域 頁面。
   
請務必填寫所有必要欄位，並盡可能正確填寫。 如需連絡資訊不正確的資料可能會導致失敗 toopurchase 網域。 

接下來，選取 hello 所需的選項，為您的網域。 請參閱下表說明 hello:

| 設定 | 建議的值 | 說明 |
|-|-|-|
|自動續訂 | **啟用** | 每年自動續訂 App Service 網域。 您的信用卡收取次更新的 hello hello 相同購買的價格。 |
|隱私權保護 | 啟用 | 太參加 「 隱私權保護 」，其隨附於 hello 購買價格_免費_(頂層網域登錄這類不支援隱私權保護，除了_。 co.in_， _。co.uk_等等)。 |
| 指派預設主機名稱 | **www** 和 **@** | 選取 hello 所需的主機名稱繫結，如有需要。 Hello 網域採購作業完成時，可以在 hello 選取的主機名稱存取您的 web 應用程式。 如果 hello web 應用程式是後面[Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)，您沒有看到 hello 選項 tooassign hello 根網域 (@)，因為 Traffic Manager 不支援 A 記錄。 您可以變更 toohello 主機名稱指派 hello 網域購買完成之後。 |

### <a name="accept-terms-and-purchase"></a>接受條款並購買

按一下**法律條款**tooreview hello 條款及 hello 費用，然後按一下**購買**。

> [!NOTE]
> 應用程式服務網域使用 Azure DNS toohost hello 定義域。 此外 toohello 網域註冊費，使用 Azure DNS 的費用。 如需相關資訊，請參閱 [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。
>
>

在 hello**應用程式服務網域**頁面上，按一下**確定**。 在 hello 作業正在進行中，您會看到下列通知 hello:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>測試 hello 主機名稱

如果您已指派預設主機名稱 tooyour web 應用程式，您也可以看到每個選取的主機名稱的成功通知。 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

另請參閱 hello 選取的主機名稱在 hello**自訂網域** 頁面的 hello **Hostname** > 一節。 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

tootest hello 主機名稱，瀏覽列 toohello hello 瀏覽器中的主機名稱。 Hello hello 範例中前面螢幕擷取畫面，再試一次瀏覽 too_kontoso.net_ 和_www.kontoso.net_。

## <a name="assign-hostnames-tooweb-app"></a>指定主機名稱 tooweb 應用程式

如果您選擇不 tooassign 其中一個或多個預設主機名稱 tooyour web 應用程式期間 hello 購買程序，或如果您不需要 tooassign 主機名稱列出，您可以在任何時間指派主機名稱。

您也可以指派主機名稱在 hello 應用程式服務網域 tooany 其他 web 應用程式。 hello 步驟取決於 hello 應用程式服務網域與 hello web 應用程式是否屬於 toohello 相同訂用帳戶。

- 不同的訂用帳戶： 對應 hello 應用程式服務網域 toohello web 應用程式，例如外部所購買的網域中的自訂 DNS 記錄。 有關新增自訂的 DNS 名稱 tooan 應用程式服務網域，請參閱[管理自訂 DNS 記錄](#custom)。 toomap 外部購買的網域 tooa web 應用程式，請參閱[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](app-service-web-tutorial-custom-domain.md)。 
- 相同的訂用帳戶： 使用 hello 下列步驟。

### <a name="launch-add-hostname"></a>啟動新增主機名稱
在 hello**應用程式服務**頁面、 選取 hello 想 tooassign 主機名稱、 選取您 web 應用程式名稱**設定**，然後選取**自訂網域**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

請確定您已購買的網域列在 hello**應用程式服務網域**區段，但不要選取它。 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Hello 顯示 hello web 應用程式的相同訂用帳戶中的所有應用程式服務網域**自訂網域**頁面。 如果您的網域是在 hello web 應用程式的訂用帳戶，但看不到在 hello web 應用程式的**自訂網域**頁面上，再次嘗試重新開啟 hello**自訂網域**頁面上，或重新整理 hello 網頁。 另請檢查 hello 通知鈴鐺在 hello hello Azure 入口網站頂端的進度或建立失敗。
>
>

選取 [新增主機名稱]。

### <a name="configure-hostname"></a>設定主機名稱
在 hello**新增主機名稱**對話方塊中，您的應用程式服務網域或任何子網域的型別 hello 完整的網域名稱。 例如：

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

完成之後，請選取 [驗證]。 hello 主機名稱記錄類型會自動為您選擇。

選取 [新增主機名稱]。

Hello 作業完成時，您會看到指派主機名稱的 hello 的成功通知。  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>關閉新增主機名稱
在 hello**新增主機名稱**頁面中，指派任何其他主機名稱 tooyour web 應用程式，視需要。 完成後，關閉 hello**新增 hostname**頁面。

您現在應該會在您的應用程式中看到新指派的 hello hostname(s)**自訂網域**頁面。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>測試 hello 主機名稱

瀏覽列 toohello hello 瀏覽器中的主機名稱。 在 hello hello 前面螢幕擷取畫面中的範例，請嘗試瀏覽 too_abc.kontoso.net_。

<a name="custom" />

## <a name="manage-custom-dns-records"></a>管理自訂 DNS 記錄

在 Azure 中，App Service 網域的 DNS 記錄是使用 [Azure DNS](https://azure.microsoft.com/services/dns/) 來管理。 和針對外部購買的網域一樣，您可以新增、移除及更新 DNS 記錄。

### <a name="open-app-service-domain"></a>開啟 App Service 網域

在 hello Azure 入口網站，從 hello 左窗格中，選取 **更服務** > **應用程式服務網域**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

選取 hello 網域 toomanage。 

### <a name="access-dns-zone"></a>存取 DNS 區域

在 hello 網域的左窗格中，選取  **DNS 區域**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

這個動作會開啟 hello [DNS 區域](../dns/dns-zones-records.md)Azure DNS 中的應用程式服務網域的頁面。 如需詳細資訊 tooedit DNS 記錄，請參閱[toomanage DNS 區域 hello Azure 入口網站的方式](../dns/dns-operations-dnszones-portal.md)。

## <a name="cancel-purchase-delete-domain"></a>取消購買 (刪除網域)

購買 hello 應用程式服務網域後，您有五天 toocancel 全額退款購買。 五天之後，您可以刪除 hello 應用程式服務網域，但無法獲得退款。

### <a name="open-app-service-domain"></a>開啟 App Service 網域

在 hello Azure 入口網站，從 hello 左窗格中，選取 **更服務** > **應用程式服務網域**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

選取 hello 網域 tooyou 想 toocancel 或刪除。 

### <a name="delete-hostname-bindings"></a>刪除主機名稱繫結

在 hello 網域的左窗格中，選取 **主機名稱繫結**。 以下列出 hello 從所有 Azure 服務的主機名稱繫結。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

您無法刪除 hello 應用程式服務網域，您必須刪除所有的主機名稱繫結。

請透過選取 **...** > [刪除].來刪除每個主機名稱繫結。 刪除所有 hello 繫結之後，選取**儲存**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>取消或刪除

在 hello 網域的左窗格中，選取 **概觀**。 

如果尚未經過 hello 取消期間 hello 購買網域上的，選取**取消購買**。 否則，您會看到 [刪除] 按鈕。 toodelete hello 網域不退款，選取**刪除**。

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

選取**確定**tooconfirm hello 作業。 如果您不想 tooproceed，按一下之外 hello 確認對話方塊中的任何位置。

Hello 網域 hello 作業已完成之後，會從您的訂用帳戶已釋放及可供任何人 toopurchase 一次。 
