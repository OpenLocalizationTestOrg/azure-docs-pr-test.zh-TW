---
title: "aaaAdd SSL 憑證 tooyour Azure App Service 應用程式 |Microsoft 文件"
description: "了解如何 tooadd SSL 憑證 tooyour App Service 應用程式。"
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>購買並設定您的 Azure App Service 的 SSL 憑證

在本教學課程中，您會購買 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** 的 SSL 憑證，安全地將它儲存在 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 中，並將它與自訂網域產生關聯，藉此保護 Web 應用程式。

## <a name="step-1---log-in-tooazure"></a>步驟 1-tooAzure 中的記錄檔

登入 toohello http://portal.azure.com 在 Azure 入口網站

## <a name="step-2---place-an-ssl-certificate-order"></a>步驟 2 - 訂購 SSL 憑證

您可以訂購 SSL 憑證來建立新[應用程式的服務憑證](https://portal.azure.com/#create/Microsoft.SSL)在 hello **Azure 入口網站**。

![建立憑證](./media/app-service-web-purchase-ssl-web-site/createssl.png)

輸入好記**名稱**SSL 憑證，然後輸入 hello**網域名稱**

> [!NOTE]
> 這是一個 hello hello 採購程序的最重要的部分。 請確定 tooenter 更正您想要與此憑證 tooprotect 的主機名稱 （自訂的網域）。 **不這麼做**附加 hello 與 WWW 的主機名稱。 
>

選取 [訂用帳戶]、[資源群組] 和 [憑證 SKU]。

> [!WARNING]
> App Service 憑證只可供其他應用程式內的服務 hello 相同訂用帳戶。  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>步驟 3-hello 憑證儲存在 Azure 金鑰保存庫

> [!NOTE]
> [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 是一項 Azure 服務，可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。
>

Hello SSL 憑證購買完成之後，您需要 tooopen [App Service 憑證](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders)資源刀鋒視窗。

![插入 KV toostore 準備的映像](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

您會注意到憑證的狀態是**「 暫止發行"**還有幾個步驟之前，您可以開始使用此憑證需要 toocomplete。

按一下**憑證設定**內部憑證屬性刀鋒視窗，然後按一下 **步驟 1： 儲存區**toostore Azure 金鑰保存庫中的這個憑證。

從**金鑰保存庫狀態**刀鋒視窗中，按一下 **金鑰保存庫儲存機制**toochoose 現有的金鑰保存庫 toostore 此憑證**或建立新金鑰保存庫**toocreate 新的金鑰保存庫在相同的訂用帳戶和資源群組內。

> [!NOTE]
> Azure Key Vault 儲存此憑證會產生少許費用。
> 如需詳細資訊，請參閱 **[Azure Key Vault 定價詳細資料](https://azure.microsoft.com/pricing/details/key-vault/)**。
>

一旦您選取 hello 金鑰保存庫儲存機制 toostore 此憑證，hello**存放區**選項應該會顯示成功。

![插入在 KV 中儲存成功的影像](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>步驟 4-確認 hello 網域擁有權

> [!NOTE]
> App Service 憑證支援 3 種類型的網域驗證：網域、郵件和手動驗證。 這些說明，請參閱詳細資料請參閱 hello[進階區段](#advanced)。

從 hello 相同**憑證設定**您在步驟 3 中使用刀鋒視窗中，按一下**步驟 2： 確認**。

**網域驗證**這是 hello 最方便的程序**只当**您尚未**[購買 Azure App Service 從您的自訂網域。](custom-dns-web-site-buydomains-web-app.md)**
按一下**確認**按鈕 toocomplete 此步驟。

![插入網域驗證的影像](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

按一下後**確認**，使用 hello**重新整理**按鈕，直到 hello**確認**選項應該會顯示成功。

![插入在 KV 中驗證成功的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>步驟 5： 指定憑證 tooApp 服務應用程式

> [!NOTE]
> 在執行本節中的 hello 步驟之前, 您必須有關聯的自訂網域名稱與您的應用程式。 如需詳細資訊，請參閱**[設定 Web 應用程式的自訂網域名稱。](app-service-web-tutorial-custom-domain.md)**
>

在 hello  **[Azure 入口網站](https://portal.azure.com/)**，按一下 hello **App Service** hello 左側的 hello 頁面的選項。

按一下 hello 名稱的應用程式 toowhich 想 tooassign 此憑證。

在 hello**設定**，按一下  **SSL 憑證**。

按一下**匯入應用程式的服務憑證**和選取 hello 您購買的憑證。

![插入匯入憑證的影像](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

在 hello **ssl 繫結**區段按一下**新增繫結**，和使用 SSL，使用 hello 下拉式清單 tooselect hello 網域名稱 toosecure hello 憑證 toouse。 您也可以選取是否 toouse **[伺服器名稱指示 (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** 或 IP 為主的 SSL。

![插入 SSL 繫結的影像](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

按一下**新增繫結**toosave hello 變更並啟用 SSL。

> [!NOTE]
> 如果您選取**IP 為主的 SSL**和您的自訂網域已設定使用 A 記錄，您必須執行下列額外步驟的 hello。 這些說明，請參閱詳細資料請參閱 hello[進階區段](#Advanced)。

此時，您應該能夠 toovisit 您的應用程式使用`HTTPS://`而不是`HTTP://`hello 憑證的 tooverify 已正確設定。

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>步驟 6 - 管理工作

### <a name="azure-cli"></a>Azure CLI

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>進階

### <a name="verifying-domain-ownership"></a>驗證網域擁有權

App Service 憑證另外支援 2 種類型的網域驗證：郵件和手動驗證。

#### <a name="mail-verification"></a>郵件驗證

驗證電子郵件已經傳送的 toohello 與此自訂網域的電子郵件地址相關聯。
toocomplete hello 電子郵件驗證步驟中，開啟 hello 電子郵件，然後按一下 hello 驗證連結。

![插入電子郵件驗證的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

如果您需要 tooresend hello 驗證電子郵件，請按一下 hello**重新傳送電子郵件** 按鈕。

#### <a name="manual-verification"></a>手動驗證

> [!IMPORTANT]
> HTML 網頁驗證 (僅適用於標準憑證 SKU)
>

1. 建立名為 **"starfield.html"** 的 HTML 檔案

1. 內容的這個檔案應該 hello 的 hello 網域驗證語彙基元的確切名稱。 （您可以複製 hello 語彙基元 hello 網域驗證狀態刀鋒視窗）

1. 上傳這個檔案位於 hello hello web 伺服器裝載您的網域根目錄`/.well-known/pki-validation/starfield.html`

1. 按一下**重新整理**tooupdate hello 憑證狀態完成驗證之後。 可能需要幾分鐘，讓驗證 toocomplete。

> [!TIP]
> 確認終端機利用`curl -G http://<domain>/.well-known/pki-validation/starfield.html`hello 回應應包含 hello `<verification-token>`。

#### <a name="dns-txt-record-verification"></a>DNS TXT 記錄驗證

1. 使用 DNS 管理員中，建立 TXT 記錄上 hello`@`子網域與值相等 toohello 網域驗證語彙基元。
1. 按一下**[重新整理]** tooupdate hello 完成驗證後的憑證狀態。

> [!TIP]
> 您需要 toocreate TXT 記錄上`@.<domain>`值`<verification-token>`。

### <a name="assign-certificate-tooapp-service-app"></a>指派憑證 tooApp 服務應用程式

如果您選取**IP 為主的 SSL**和您的自訂網域已設定使用 A 記錄，您必須執行下列額外步驟的 hello:

設定之後 IP 為根據的 SSL 繫結，會指派 tooyour 應用程式的專用的 IP 位址。 您可以找到這個 IP 位址上 hello**自訂網域**頁面的 設定應用程式，上面 hello 下**Hostname** > 一節。 它會列為 [外部 IP 位址]

![插入 IP SSL 的影像](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

請注意，此 IP 位址與 hello 虛擬 IP 位址用於先前 tooconfigure hello A 記錄您的網域不同。 如果您已設定的 toouse SNI 為根據的 SSL，或不設定 toouse SSL，沒有位址會列示為此項目。

使用您網域名稱註冊機構所提供的 hello 工具，來修改 hello 您的自訂網域名稱 toopoint toohello 的 IP 位址從 hello 上一個步驟的記錄。

## <a name="rekey-and-sync-hello-certificate"></a>重設金鑰，並將同步 hello 憑證

如果您需要 tooRekey 您的憑證，選取**重設金鑰，並將同步**選項**憑證內容**刀鋒視窗。

按一下**重設金鑰**按鈕 tooinitiate hello 程序。 此程序可能需要 1-10 分鐘 toocomplete。

![插入重設 SSL 金鑰的影像](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

重設您的憑證的金鑰復原 hello 與 hello 憑證授權單位發行新憑證的憑證。

## <a name="next-steps"></a>後續步驟

* [新增內容傳遞網路](app-service-web-tutorial-content-delivery-network.md)