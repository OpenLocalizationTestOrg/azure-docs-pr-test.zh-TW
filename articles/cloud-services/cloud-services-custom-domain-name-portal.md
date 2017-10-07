---
title: "aaaConfigure 雲端服務中的自訂網域名稱 |Microsoft 文件"
description: "深入了解如何 tooexpose Azure 應用程式或資料 toohello 網際網路上設定 DNS 設定自訂網域。  這些範例使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>設定 Azure 雲端服務的自訂網域名稱
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-custom-domain-name-portal.md)
> * [Azure 傳統入口網站](cloud-services-custom-domain-name.md)
> 
> 

當您建立雲端服務時，Azure 將指派其 tooa 子網域的**.cloudapp.net**。 例如，如果您的雲端服務名稱為"contoso"，您的使用者將會無法 tooaccess http://contoso.cloudapp.net 之類的 URL 上的應用程式。 Azure 也會指派虛擬 IP 位址。

不過，您也可以在自己的網域名稱 (例如 **contoso.com**) 上公開您的應用程式。這篇文章說明如何 tooreserve 或設定自訂網域名稱的雲端服務 web 角色。

您已經了解什麼是 CNAME 和 A 記錄嗎？ [跳過 hello 說明](#add-a-cname-record-for-your-custom-domain)。

> [!NOTE]
> 在這項工作的 hello 程序適用於 tooAzure 雲端服務。 如需應用程式服務的資訊，請參閱 [這裡](../app-service-web/web-sites-custom-domain-name.md)。 如需儲存體帳戶的資訊，請參閱 [這裡](../storage/blobs/storage-custom-domain-name.md)。
> 
> 

<p/>

> [!TIP]
> 更快-開始使用新的 Azure hello[引導式逐步解說](http://support.microsoft.com/kb/2990804)！  在彈指之間完成自訂網域名稱的關聯，以及與 Azure 雲端服務或 Azure 網站之間的通訊 (SSL) 保護。
> 
> 

## <a name="understand-cname-and-a-records"></a>了解 CNAME 和 A 記錄
CNAME （或別名記錄） 和記錄同時 tooassociate 與特定伺服器的網域名稱可讓您 （或在此情況下，服務） 但是以不同的方式運作。 與 Azure 雲端服務，您應該先決定哪些 toouse 考慮使用 A 記錄時，也會產生一些特定的考量。

### <a name="cname-or-alias-record"></a>CNAME 或別名記錄
CNAME 記錄對應*特定*網域，例如**contoso.com**或**www.contoso.com**，tooa 正式網域名稱。 在此情況下，hello 正式網域名稱為 hello **[myapp].cloudapp.net**網域名稱，您的 Azure 託管應用程式。 Hello CNAME 建立之後，建立一個別名 hello **[myapp].cloudapp.net**。 hello 的 CNAME 項目將 toohello IP 位址，解析您**[myapp].cloudapp.net**自動服務，因此 hello hello 雲端服務 IP 位址變更時，如果您不需要 tootake 任何動作。

> [!NOTE]
> 一些網域註冊機構只允許您 toomap 子網域時使用的 CNAME 記錄，例如 www.contoso.com，而不根名稱，例如 contoso.com。如需有關 CNAME 記錄的詳細資訊，請參閱您的註冊機構所提供的 hello 文件[hello 維基百科項目上的 CNAME 記錄](http://en.wikipedia.org/wiki/CNAME_record)，或使用 hello [IETF 網域名稱-實作和規格](http://tools.ietf.org/html/rfc1035)文件。
> 
> 

### <a name="a-record"></a>A 記錄
*A*記錄將定義域對應，例如**contoso.com**或**www.contoso.com**，*或萬用字元網域*例如 **\*。 contoso.com**，tooan IP 位址。 在 Azure 雲端服務的 hello 情況下，hello hello 服務的虛擬 IP。 因此 hello 的 A 記錄透過 CNAME 記錄的主要優點是，您可以擁有一個項目使用萬用字元，例如\* **。 contoso.com**，這會處理要求有多個子網域，例如**mail.contoso.com**， **login.contoso.com**，或**www.contso.com**。

> [!NOTE]
> 由於 A 記錄對應 tooa 靜態 IP 位址，無法自動解決您的雲端服務的變更 toohello IP 位址。 使用您的雲端服務的 hello IP 位址被配置 hello 首次部署 tooan 空的插槽 （生產或預備環境。）如果您刪除 hello 插槽的 hello 部署，hello IP address 已釋放由 Azure 和任何未來的部署 toohello 位置提供新的 IP 位址。
> 
> 為了方便起見，預備和生產部署或執行就地升級的現有部署之間交換時，會保存 hello IP 位址的指定的部署位置 （生產或預備環境）。 如需有關如何執行這些動作的詳細資訊，請參閱[toomanage 雲端服務的方式](cloud-services-how-to-manage.md)。
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>新增自訂網域的 CNAME 記錄
toocreate CNAME 記錄，您必須新增新的項目 hello DNS 資料表中的自訂網域註冊機構所提供的 hello 工具。 每個註冊機構有相似但稍微不同的方法指定 CNAME 記錄，但概念的 hello hello 相同。

1. 使用其中一個這些方法 toofind hello **。.cloudapp.net**指派 tooyour 雲端服務的網域名稱。
   
   * 登入 toohello [Azure 入口網站]、 選取您的雲端服務、 查看 hello **Essentials**區段，並找出 hello**網站 URL**項目。
     
       ![快速概覽區段，顯示 hello 網站 URL][csurl]
     
       **或**
   * 安裝和設定[Azure Powershell](/powershell/azure/overview)，，然後使用 hello 下列命令：
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     儲存會建立一筆 CNAME 記錄時需要使用任一種方法，所傳回的 hello URL 中的 hello 網域名稱。
2. 登入 tooyour DNS 註冊機構的網站，並移至 toohello 管理 DNS 的頁面。 查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。
3. 現在找出可選取或輸入 CNAME 的地方。 您可能必須從下拉式清單，輸入或瀏覽 tooan 進階設定 頁面上，tooselect hello 記錄。 您應該尋找 hello 文字**CNAME**，**別名**，或**子網域**。
4. 您也必須提供 hello 網域或子網域別名 hello CNAME，例如**www**如果您想 toocreate 別名**www.customdomain.com**。如果您想 toocreate 別名 hello 根網域時，它可能被列為 hello '**@**' 註冊機構的 DNS 工具中的符號。
5. 接著，您必須提供正式主機名稱，在此案例中為應用程式的 **cloudapp.net** 網域。

比方說，hello 下列 CNAME 記錄會轉送所有流量**www.contoso.com**太**contoso.cloudapp.net**，應用程式已部署的 hello 自訂網域名稱：

| 別名/主機名稱/子網域 | 正式網域 |
| --- | --- |
| www |contoso.cloudapp.net |

> [!NOTE]
> 在訪客的**www.contoso.com** hello 轉送程序是不可見的 toothe 終端使用者，則不會看到 hello，則為 true 的主機 (contoso.cloudapp.net)。
> 
> hello 上述範例只適用於在 hello tootraffic **www**子網域。 因為 CNAME 記錄不能使用萬用字元，所以您必須為每一個網域/子網域建立一個 CNAME。 如果想 toodirect 流量從子網域，例如 *。 contoso.com、 tooyour.cloudapp.net 位址，您可以設定**URL 重新導向**或**向前 URL** DNS 設定中的項目或建立 A 記錄。
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>新增自訂網域的 A 記錄
toocreate A 記錄，您必須先找到您的雲端服務的 hello 虛擬 IP 位址。 使用您的註冊機構所提供的 hello 工具，然後您的自訂網域的 hello DNS 資料表中加入新項目。 每個註冊機構具有相似但稍微不同的方法，指定 A 記錄，但概念的 hello hello 相同。

1. 使用下列方法 tooget hello 的雲端服務的 IP 位址的 hello 之一。
   
   * 登入 toohello [Azure 入口網站]、 選取您的雲端服務、 查看 hello **Essentials**區段，並找出 hello**公用 IP 位址**項目。
     
       ![快速概覽區段，顯示 hello VIP][vip]
     
       **或**
   * 安裝和設定[Azure Powershell](/powershell/azure/overview)，，然後使用 hello 下列命令：
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     儲存 hello IP 位址，您將需要建立 A 記錄時。
2. 登入 tooyour DNS 註冊機構的網站，並移至 toohello 管理 DNS 的頁面。 查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。
3. 現在找出可選取或輸入 A 記錄的地方。 您可能必須從下拉式清單，輸入或瀏覽 tooan 進階設定 頁面上，tooselect hello 記錄。
4. 選取或輸入 hello 網域或將使用此 A 記錄的子網域。 例如，選取**www**如果您想 toocreate 別名**www.customdomain.com**。如果您想要所有子網域 toocreate 萬用字元項目，請輸入 ' * '。 這將會涵蓋所有子網域，例如 **mail.customdomain.com**、**login.customdomain.com** 和 **www.customdomain.com**。
   
    如果您想 toocreate A 記錄 hello 根網域時，它可能被列為 hello '**@**' 註冊機構的 DNS 工具中的符號。
5. Hello 提供欄位中輸入您的雲端服務的 hello IP 位址。 這樣會將關聯 hello 網域項目用於 hello 與您的雲端服務部署的 hello IP 位址的 A 記錄。

比方說，hello 下列記錄會轉送所有流量**contoso.com**太**137.135.70.239**，hello 已部署應用程式的 IP 位址：

| 主機名稱/子網域 | IP 位址 |
| --- | --- |
| @ |137.135.70.239 |

這個範例將示範如何建立 hello 根網域的 A 記錄。 如果您想 toocreate 萬用字元項目 toocover 所有子網域，您會輸入 '*' 為 hello 子網域。

> [!WARNING]
> 依預設，Azure 中的 IP 位址是動態的。 您可能會想 toouse[保留的 IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md)tooensure 不會變更您的 IP 位址。
> 
> 

## <a name="next-steps"></a>後續步驟
* [如何 tooManage 雲端服務](cloud-services-how-to-manage.md)
* [如何 tooMap CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md)
* [雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[Azure 入口網站]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
