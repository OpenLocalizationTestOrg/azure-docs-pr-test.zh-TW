---
title: "您的 Azure 資源與 aaaIntegrate Azure DNS |Microsoft 文件"
description: "深入了解如何為您的 Azure 資源的 DNS tooprovide 沿著 toouse Azure DNS。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>針對一項 Azure 服務使用 Azure DNS tooprovide 自訂網域設定

Azure DNS 提供自訂網域的 DNS，可用於任何支援自訂網域或具有完整網域名稱 (FQDN) 的 Azure 資源。 範例是您 Azure web 應用程式，您想要使用者 tooaccess 它透過使用 contoso.com 或 www.contoso.com 當做 FQDN。 本文章會引導您使用 Azure DNS 設定您的 Azure 服務，以便使用自訂網域。

## <a name="prerequisites"></a>必要條件

在您的自訂網域的順序 toouse Azure DNS，您必須先委派您網域 tooAzure DNS。 請瀏覽[委派網域 tooAzure DNS](./dns-delegate-domain-azure-dns.md)如需有關指示 tooconfigure 名稱伺服器進行委派。 一旦您的網域委派的 tooyour Azure DNS 區域，您就可以 tooconfigure hello DNS 記錄所需。

您可以為 [Azure 函數應用程式](#azure-function-app)、[Azure IoT](#azure-iot)、[公用 IP 位址](#public-ip-address)、[App Service (Web Apps)](#app-service-web-apps)、[Blob 儲存體](#blob-storage)、[Azure CDN](#azure-cdn) 設定虛名或自訂網域。

## <a name="azure-function-app"></a>Azure 函數應用程式

tooconfigure Azure 函式應用程式的自訂網域，以及在 hello 函式應用程式本身的組態建立 CNAME 記錄。
 
瀏覽過**其他** > **函式應用程式**並選取您的函式應用程式。 按一下 [平台功能]，然後按一下 [網路] 下方的[自訂網域]。

![函數應用程式刀鋒視窗](./media/dns-custom-domain/functionapp.png)

請注意在 hello hello 目前 url**自訂網域**刀鋒視窗中，此位址作為 hello 別名建立 hello DNS 記錄。

![自訂網域刀鋒視窗](./media/dns-custom-domain/functionshostname.png)

瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。

|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | myFunctionApp        | Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。        |
|類型     | CNAME        | 使用 CNAME 記錄會使用別名。        |
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|Alias     | adatumfunction.azurewebsites.net        | hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 函式應用程式所提供的 hello adatumfunction.azurewebsites.net DNS 名稱。        |

瀏覽後 tooyour 函式應用程式中，按一下**平台功能**，然後在**網路**按一下**自訂網域**，然後在**Hostname**按一下**+ 加入 hostname**。

在 hello**新增主機名稱**刀鋒視窗中，輸入 hello hello CNAME 記錄**主機名稱**文字欄位，然後按一下**驗證**。 如果 hello 記錄無法找到的 toobe，hello**新增主機名稱**按鈕隨即顯示。 按一下**新增 hostname** tooadd hello 別名。

![函數應用程式的新增主機名稱刀鋒視窗](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT 沒有 hello 服務本身所需的任何自訂。 toouse 與 IoT 中樞的自訂網域的 CNAME 記錄指向 toohello 資源只需要。

瀏覽過**物聯網** > **IoT 中樞**，並選取您的 IoT 中樞。 在 hello**概觀**刀鋒視窗中，注意 hello hello IoT 中樞的 FQDN。

![IoT 中樞刀鋒視窗](./media/dns-custom-domain/iot.png)

接下來，瀏覽 tooyour DNS 區域，然後按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。


|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | myiothub        | 此值以及 hello 網域名稱標籤為 hello IoT 中樞的 hello FQDN。        |
|類型     | CNAME        | 使用 CNAME 記錄會使用別名。
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|Alias     | adatumIOT.azure-devices.net        | hello DNS 名稱建立 hello 別名，在此範例中是 hello IoT 中心所提供的 hello adatumIOT.azure devices.net 主機名稱。

一旦建立 hello 記錄時，測試與 hello CNAME 記錄使用名稱解析`nslookup`

## <a name="public-ip-address"></a>公用 IP 位址

tooconfigure 自訂網域，以服務的公用 IP 位址資源，例如應用程式閘道，負載平衡器，雲端服務，資源管理員的 Vm，並使用傳統的 Vm，CNAME 記錄。

瀏覽過**網路** > **公用 IP 位址**、 選取 hello 公用 IP 資源，然後按一下 **組態**。 Notate hello 所顯示的 IP 位址。

![公用 IP 刀鋒視窗](./media/dns-custom-domain/publicip.png)

瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。


|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | mywebserver        | Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。        |
|類型     | A        | 使用 A 記錄，因為 hello 資源是 IP 位址。        |
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|IP 位址     | <your ip address>       | hello 公用 IP 位址。|

![建立 A 記錄](./media/dns-custom-domain/arecord.png)

一旦建立 hello A 記錄時，執行`nslookup`toovalidate hello 記錄解析。

![公用 IP DNS 查閱](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Service (Web Apps)

hello 下列步驟會引導您進行設定 app service web 應用程式的自訂網域。

瀏覽過**Web 和行動裝置版** > **App Service**並選取您要設定自訂網域名稱，然後按一下 hello 資源**自訂網域**。

請注意在 hello hello 目前 url**自訂網域**刀鋒視窗中，此位址作為 hello 別名建立 hello DNS 記錄。

![自訂網域刀鋒視窗](./media/dns-custom-domain/url.png)

瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。


|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | mywebserver        | Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。        |
|類型     | CNAME        | 使用 CNAME 記錄會使用別名。 如果 hello 資源使用的 IP 位址，就會使用 A 記錄。        |
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|Alias     | webserver.azurewebsites.net        | hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello web 應用程式所提供的 hello webserver.azurewebsites.net DNS 名稱。        |


![建立 CNAME 記錄](./media/dns-custom-domain/createcnamerecord.png)

瀏覽後 toohello hello 自訂網域名稱所設定的應用程式服務。 按一下 [自訂網域] ，然後按一下 [主機名稱]。 您建立 tooadd hello CNAME 記錄，請按一下**+ 加入 hostname**。

![圖 1](./media/dns-custom-domain/figure1.png)

Hello 程序完成之後，請執行**nslookup** toovalidate 名稱解析可正常運作。

![圖 1](./media/dns-custom-domain/finalnslookup.png)

toolearn 深入了解對應自訂網域 tooApp 服務，請瀏覽[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json)。

如果您需要 toopurchase 自訂網域，請瀏覽[購買 Azure Web 應用程式的自訂網域名稱](../app-service-web/custom-dns-web-site-buydomains-web-app.md)toolearn 深入了解應用程式服務網域。

## <a name="blob-storage"></a>Blob 儲存體

hello 下列步驟會引導您進行設定 CNAME 記錄 blob 儲存體帳戶使用 hello asverify 方法。 這個方法可確保沒有任何停機時間。

瀏覽過**儲存體** > **儲存體帳戶**，選取您的儲存體帳戶，然後按一下**自訂網域**。 Notate hello FQDN 步驟 2，這個值會使用 toocreate hello 第一筆 CNAME 記錄

![Blob 儲存體自訂網域](./media/dns-custom-domain/blobcustomdomain.png)

瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。


|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | asverify.mystorageaccount        | Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。        |
|類型     | CNAME        | 使用 CNAME 記錄會使用別名。        |
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 儲存體帳戶所提供的 hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS 名稱。        |

按一下瀏覽後 tooyour 儲存體帳戶**儲存體** > **儲存體帳戶**、 選取儲存體帳戶，然後按一下**自訂網域**。 類型在您建立不含 hello asverify 前置詞在 hello] 文字方塊中，核取的別名 hello * * 使用間接 CNAME 驗證，然後按一下 [**儲存**。 一旦完成此步驟中，傳回 tooyour DNS 區域，而且建立不含 hello asverify 前置詞的 CNAME 記錄。  該時間點之後，您就 hello cdnverify 前置詞的安全 toodelete hello CNAME 記錄。

![Blob 儲存體自訂網域](./media/dns-custom-domain/indirectvalidate.png)

執行 `nslookup` 驗證 DNS 解析

關於對應自訂網域 tooa blob 儲存體端點，請瀏覽的 toolearn[設定您的 Blob 儲存體端點的自訂網域名稱](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Azure CDN

hello 下列步驟會引導您進行設定使用 hello cdnverify 方法的 CDN 端點的 CNAME 記錄。 這個方法可確保沒有任何停機時間。

瀏覽過**網路** > **CDN 設定檔**，選取您的 CDN 設定檔，然後按一下**端點**下**一般**。

選取您正在使用，然後按一下 hello 端點**+ 自訂網域**。 請注意 hello**端點主機名稱**為此值為 hello 記錄該 hello CNAME 記錄會指到。

![CDN 自訂網域](./media/dns-custom-domain/endpointcustomdomain.png)

瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。 填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。

|屬性  |值  |描述  |
|---------|---------|---------|
|名稱     | cdnverify.mycdnendpoint        | Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。        |
|類型     | CNAME        | 使用 CNAME 記錄會使用別名。        |
|TTL     | 1        | 1 為使用 1 小時        |
|TTL 單位     | 小時        | 時數會做為 hello 時間度量         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 儲存體帳戶所提供的 hello cdnverify.adatumcdnendpoint.azureedge.net DNS 名稱。        |

按一下瀏覽後 tooyour CDN 端點**網路** > **CDN 設定檔**，然後選取您的 CDN 設定檔。 按一下**+ 自訂網域**並輸入您的 CNAME 記錄別名，不含 hello cdnverify 前置詞，然後按一下**新增**。

一旦完成此步驟中，傳回 tooyour DNS 區域，而且建立不含 hello cdnverify 前置詞的 CNAME 記錄。  該時間點之後，您就 hello cdnverify 前置詞的安全 toodelete hello CNAME 記錄。 如需有關 CDN 如何 tooconfigure hello 中繼註冊步驟沒有自訂網域造訪[對應 Azure CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json)。

## <a name="next-steps"></a>後續步驟

了解如何太[設定服務在 Azure 中裝載的反向 DNS](dns-reverse-dns-for-azure-services.md)。
