---
title: "產生並匯出點對站的憑證：PowerShell：Azure | Microsoft Docs"
description: "本文章包含步驟 toocreate 自我簽署的根憑證、 匯出 hello 公開金鑰，並產生使用 PowerShell 在 Windows 10 上的用戶端憑證。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>使用 Windows 10 的 PowerShell 來產生並匯出點對站連線的憑證

點對站連線使用憑證 tooauthenticate。 本文示範如何 toocreate 的自我簽署根憑證，並產生使用 PowerShell 在 Windows 10 上的用戶端憑證。 如果您要尋找的點對站台的設定步驟，例如 tooupload 根憑證，來選取其中一個 hello '設定點對站' 發行項的 hello 下列清單的方式：

> [!div class="op_single_selector"]
> * [建立自我簽署憑證 - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [建立自我簽署憑證 - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [設定點對站 - Resource Manager - Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [設定點對站 - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [設定點對站 - 傳統 - Azure 入口網站](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


您必須在本文中執行 Windows 10 的電腦上執行 hello 步驟。 您使用 toogenerate 憑證 hello PowerShell cmdlet hello Windows 10 作業系統的一部分，而且無法在其他版本的 Windows 中運作。 hello Windows 10 電腦是只有需要的 toogenerate hello 憑證。 一旦產生 hello 憑證，您可以上傳，或在任何支援的用戶端作業系統上安裝它們。 

如果您沒有存取 tooa Windows 10 電腦，您可以使用[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate 憑證。 hello 憑證，您可以產生使用哪一種方法可以安裝在任何[支援](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)用戶端作業系統。

## <a name="rootcert"></a>建立自我簽署根憑證

使用 hello New-selfsignedcertificate cmdlet toocreate 自我簽署的根憑證。 如需其他的參數資訊，請參閱 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。

1. 從執行 Windows 10 的電腦，以提高的權限開啟 Windows PowerShell 主控台。
2. 使用下列範例 toocreate hello 自我簽署的根憑證的 hello。 hello 下列範例會建立名為 'P2SRootCert'，會自動安裝在 '憑證-目前 \' 的自我簽署的根憑證。 您可以開啟來檢視 hello 憑證*certmgr.msc*，或*管理使用者憑證*。

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>匯出 hello 公開金鑰 (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

hello exported.cer 檔案必須上傳的 tooAzure。 如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-rm-ps.md#upload)。 tooadd 其他信任的根憑證，[本節](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert)hello 發行項。

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>匯出 hello 自我簽署的根憑證和公開金鑰的金鑰 toostore 它 （選擇性）

您可能想 tooexport hello 自我簽署根憑證，並將它安全地儲存。 如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。 tooexport hello 自我簽署根憑證.pfx hello 選取根憑證，使用 hello 相同的步驟中所述[用戶端憑證匯出](#clientexport)。

## <a name="clientcert"></a>產生用戶端憑證 

每個連線 tooa 的用戶端電腦使用點對站台的 VNet 必須安裝用戶端憑證。 您 hello 自我簽署的根憑證，從產生的用戶端憑證，然後匯出及安裝 hello 用戶端憑證。 如果未安裝 hello 用戶端憑證，驗證將會失敗。 

hello 下列步驟引導您完成從自我簽署的根憑證產生用戶端憑證。 您可以從 hello 產生多個用戶端憑證相同的根憑證。 當您產生用戶端憑證使用 hello 執行下列步驟時，hello 用戶端憑證會自動安裝 hello 電腦上，您會使用 toogenerate hello 憑證。 如果您想 tooinstall 另一部用戶端電腦上的用戶端憑證，您可以匯出 hello 憑證。

hello 範例會使用 hello New-selfsignedcertificate cmdlet toogenerate 一年中到期的用戶端憑證。 額外的參數資訊，例如，設定不同的到期值 hello 用戶端憑證，請參閱[New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。

### <a name="example-1"></a>範例 1

這個範例會使用 hello '$cert' hello 前一節的變數宣告。 如果建立 hello 自我簽署的根憑證，或其他用戶端憑證中，以建立新的 PowerShell 主控台工作階段之後，您可以關閉 hello PowerShell 主控台，使用中的 hello 步驟[範例 2](#ex2)。

修改並執行 hello 範例 toogenerate 用戶端憑證。 如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 'P2SChildCert' 的用戶端憑證。  如果您想 tooname hello 子憑證其他項目，修改 hello CN 值。 執行這個範例時，請勿變更 hello TextExtension。 '憑證-目前的憑證' 自動安裝 hello 您產生的用戶端憑證在電腦上。

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>範例 2

如果您要建立額外的用戶端憑證，或者不是使用 hello 相同您使用 toocreate 您的自我簽署的根憑證，下列步驟使用 hello 的 PowerShell 工作階段：

1. 識別 hello hello 電腦已安裝的自我簽署的根憑證。 此 Cmdlet 會傳回安裝於電腦上的憑證清單。

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. 找出 hello 主旨名稱 hello 傳回清單，然後複製 hello 指紋是位於 下一步 tooit tooa 文字檔案。 在下列範例的 hello，有兩個憑證。 hello CN 名稱是 hello hello 自我簽署的根憑證，您要 toogenerate 子憑證名稱。 在此例中為 'P2SRootCert'。

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. 宣告一個變數來使用 hello 先前步驟中的 hello 指紋 hello 根憑證。 憑證指紋取代 hello hello 要從中 toogenerate 子憑證的根憑證的指紋。

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  例如，使用 P2SRootCert hello 指紋 hello 上一個步驟中，hello 變數看起來像這樣：

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  修改並執行 hello 範例 toogenerate 用戶端憑證。 如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 'P2SChildCert' 的用戶端憑證。 如果您想 tooname hello 子憑證其他項目，修改 hello CN 值。 執行這個範例時，請勿變更 hello TextExtension。 '憑證-目前的憑證' 自動安裝 hello 您產生的用戶端憑證在電腦上。

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>匯出用戶端憑證   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>安裝匯出的用戶端憑證

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>後續步驟

繼續使用您的點對站設定。 

* 如**資源管理員**部署模型的步驟，請參閱[設定點對站連線 tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。 
* 如**傳統**部署模型的步驟，請參閱[設定點對站 VPN 連線 tooa VNet （傳統）](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。
