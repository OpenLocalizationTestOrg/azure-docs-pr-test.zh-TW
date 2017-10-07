---
title: "aaaCloud 服務和管理憑證 |Microsoft 文件"
description: "了解如何 toocreate 和使用憑證搭配 Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Azure 雲端服務的憑證概觀
憑證可用於在 Azure 中雲端服務 ([服務憑證](#what-are-service-certificates)) 以及使用 hello 管理 API 進行驗證 ([管理憑證](#what-are-management-certificates)時使用 hello Azure 傳統入口網站而非hello 非傳統 Azure 入口網站）。 本主題提供這兩種憑證類型，一般概觀如何太[建立](#create)和[部署](#deploy)它們 tooAzure。

在 Azure 中使用的憑證是 x.509 v3 憑證，而且可以由其他受信任的憑證簽署，或者可以自我簽署。 自我簽署的憑證是由自己的建立者簽署，因此預設不受到信任。 大部分的瀏覽器都可以忽略這個問題。 您應該僅在開發和測試雲端服務時使用自我簽署的憑證。 

Azure 所使用的憑證可以包含私密或公開金鑰。 憑證具有指紋提供表示 tooidentify 它們模稜兩可的方式。 Hello Azure 會使用此憑證指紋[組態檔](cloud-services-configure-ssl-certificate.md)tooidentify 其中一項雲端服務的憑證應該使用。 

## <a name="what-are-service-certificates"></a>什麼是服務憑證？
服務憑證是附加的 toocloud 服務，以及啟用安全通訊 tooand 從 hello 服務。 例如，如果您部署 web 角色，您會想 toosupply 可以驗證公開的 HTTPS 端點的憑證。 服務憑證，定義在服務定義中，會執行您的角色執行個體的自動部署的 toohello 虛擬機器。 

您可以上傳服務憑證 tooAzure 傳統入口網站使用 hello Azure 傳統入口網站，或使用 hello 傳統部署模型。 服務憑證是與特定的雲端服務相關聯。 它們會指派 tooa hello 服務定義檔中的部署。

服務憑證可以與您的服務分開管理，而且可以由不同的人員管理。 例如，開發人員，可能是指，IT 管理員先前上傳 tooAzure tooa 憑證將服務套件上傳。 IT 管理員可以管理和更新 （變更 hello hello 服務組態） 該憑證，而不需要 tooupload 新的服務封裝。 沒有新的服務封裝更新可能會是因為 hello 邏輯名稱、 商店名稱和位置 hello 憑證的正在 hello 服務定義檔中時 hello 服務組態檔中指定 hello 憑證指紋。 tooupdate hello 憑證，它是只需要 tooupload hello 服務組態檔中的新憑證及變更 hello 指紋值。

>[!Note]
>hello [Cloud Services 常見問題集](cloud-services-faq.md)發行項有一些很有幫助憑證的相關資訊。

## <a name="what-are-management-certificates"></a>什麼是管理憑證？
管理憑證可讓您 tooauthenticate 與 hello 傳統部署模型。 許多程式和工具 （例如 Visual Studio 或 Azure SDK hello） 使用這些憑證 tooautomate 組態和各種 Azure 服務的部署。 這些不是真的相關的 toocloud 服務。 

> [!WARNING]
> 請務必小心！ 這些憑證類型允許驗證它們的任何人 toomanage hello 訂用帳戶相關聯。 
> 
> 

### <a name="limitations"></a>限制
每個訂用帳戶有 100 個管理憑證的限制。 此外，在特定服務管理員的使用者識別碼底下的所有訂用帳戶也有 100 個管理憑證的限制。 如果 hello hello 帳戶管理員的使用者識別碼已經用的 tooadd 100 管理憑證，而且需要更多的憑證，您可以加入共同管理員 tooadd hello 其他憑證。 

加入超過 100 個憑證之前，請查看您是否可以重複使用現有的憑證。 使用共同管理員加入可能不必要的複雜性 tooyour 憑證管理程序。

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>建立新的自我簽署憑證
您可以使用任何工具可用 toocreate 自我簽署憑證，只要遵守 toothese 設定：

* X.509 憑證。
* 包含一個私密金鑰。
* 針對金鑰交換 (.pfx 檔案) 而建立。
* 主體名稱必須符合 hello 用網域 tooaccess hello 雲端服務。

    > 您無法取得 hello.cloudapp.net 的 SSL 憑證 (或任何 Azure 相關) 網域。hello 憑證的主體名稱必須符合您的應用程式的 hello 自訂網域名稱使用 tooaccess。 例如，**contoso.net**，而非 **contoso.cloudapp.net**。

* 至少為 2048 位元加密。
* **只有服務憑證**： 用戶端憑證必須位於 hello*個人*憑證存放區。

有兩個簡單的方法 toocreate 憑證在 Windows 中，以 hello`makecert.exe`公用程式或 IIS。

### <a name="makecertexe"></a>Makecert.exe
此公用程式已被取代，此處不再說明。 如需詳細資訊，請參閱[此 MSDN 文章](https://msdn.microsoft.com/library/windows/desktop/aa386968)。

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> 如果您想 toouse hello 憑證，而不是網域的 IP 位址，請在 hello-DnsName 參數中使用 hello IP 位址。


如果您要 toouse [hello 管理入口網站憑證](../azure-api-management-certs.md)，將它匯出 tooa **.cer**檔案：

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>網際網路資訊服務 (IIS)
Hello 上有許多網頁網際網路，其中涵蓋如何 toodo 這與 IIS。 [這裡](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) 是我找到的其中一個我認為說明得很好的網頁。 

### <a name="java"></a>Java
您也可以使用 Java[建立憑證](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate)。

### <a name="linux"></a>Linux
[這](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)文章說明 toocreate 透過 SSH 的憑證。

## <a name="next-steps"></a>後續步驟
[上傳您的服務憑證 toohello Azure 傳統入口網站](cloud-services-configure-ssl-certificate.md)(或 hello [Azure 入口網站](cloud-services-configure-ssl-certificate-portal.md))。

上傳[管理 API 憑證](../azure-api-management-certs.md)toohello Azure 傳統入口網站。 hello Azure 入口網站不使用管理憑證進行驗證。

