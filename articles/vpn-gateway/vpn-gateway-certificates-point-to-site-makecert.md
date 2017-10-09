---
title: "產生並匯出點對站的憑證：MakeCert：Azure | Microsoft Docs"
description: "本文章包含步驟 toocreate 自我簽署的根憑證、 匯出 hello 公開金鑰，並產生使用 MakeCert 的用戶端憑證。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>使用 MakeCert 來產生並匯出點對站連線的憑證

點對站連線使用憑證 tooauthenticate。 本文示範如何 toocreate 的自我簽署根憑證，並產生使用 MakeCert 的用戶端憑證。 如果您要尋找的點對站台的設定步驟，例如 tooupload 根憑證，來選取其中一個 hello '設定點對站' 發行項的 hello 下列清單的方式：

> [!div class="op_single_selector"]
> * [建立自我簽署憑證 - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [建立自我簽署憑證 - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [設定點對站 - Resource Manager - Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [設定點對站 - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [設定點對站 - 傳統 - Azure 入口網站](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

雖然我們建議您使用 hello [Windows 10 PowerShell 步驟](vpn-gateway-certificates-point-to-site.md)toocreate 您的憑證，我們提供這些 MakeCert 指示為選擇性的方法。 您可以產生使用哪一種方法的 hello 憑證可以安裝在[任何支援的用戶端作業系統](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)。 不過，MakeCert 有下列限制的 hello:

* MakeCert 已被取代。 這表示無法在任何時間點移除這項工具。 當無法再使用 MakeCert 時，任何您已經使用 MakeCert 所產生的憑證將不會受到影響。 MakeCert 是只使用的 toogenerate hello 憑證，不會做為驗證機制。

## <a name="rootcert"></a>建立自我簽署根憑證

hello 下列步驟顯示如何 toocreate 的自我簽署憑證使用 MakeCert。 這些並非部署模型特定的步驟。 它們同樣適用於資源管理員和傳統部署模型。

1. 下載並安裝 [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)。
2. 安裝之後，您通常可以找到 hello makecert.exe 公用程式在此路徑: ' C:\Program Files (x86) \Windows Kits\10\bin\<a c h >'。 雖然很可能已安裝的 tooanother 位置。 開啟命令提示字元，以系統管理員身分，並瀏覽 toohello hello MakeCert 公用程式位置。 您可以使用下列範例中，調整的 hello 適當的位置 hello:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. 建立及 hello 個人憑證存放區，您的電腦上安裝憑證。 hello 下列範例會建立對應*.cer*設定 P2S 時上, 傳 tooAzure 檔案。 您要 hello 憑證 toouse hello 名稱取代 'P2SRootCert' 和 'P2SRootCert.cer'。 hello 憑證位於您 '憑證-目前 \'。

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>匯出 hello 公開金鑰 (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

hello exported.cer 檔案必須上傳的 tooAzure。 如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)。 tooadd 其他信任的根憑證，請參閱[本節](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add)hello 發行項。

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>匯出 hello 自我簽署的憑證與私用金鑰 toostore 它 （選擇性）

您可能想 tooexport hello 自我簽署根憑證，並將它安全地儲存。 如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。 tooexport hello 自我簽署根憑證.pfx hello 選取根憑證，使用 hello 相同的步驟中所述[用戶端憑證匯出](#clientexport)。

## <a name="create-and-install-client-certificates"></a>建立並安裝用戶端憑證

您未直接在 hello 用戶端電腦上安裝 hello 自我簽署的憑證。 您需要 toogenerate hello 自我簽署憑證從用戶端憑證。 您接著匯出，並安裝 hello 用戶端憑證 toohello 用戶端電腦。 hello 步驟不是特定的部署模型。 它們同樣適用於資源管理員和傳統部署模型。

### <a name="clientcert"></a>產生用戶端憑證 

每個連線 tooa 的用戶端電腦使用點對站台的 VNet 必須安裝用戶端憑證。 您 hello 自我簽署的根憑證，從產生的用戶端憑證，然後匯出及安裝 hello 用戶端憑證。 如果未安裝 hello 用戶端憑證，驗證將會失敗。 

hello 下列步驟引導您完成從自我簽署的根憑證產生用戶端憑證。 您可以從 hello 產生多個用戶端憑證相同的根憑證。 當您產生用戶端憑證使用 hello 執行下列步驟時，hello 用戶端憑證會自動安裝 hello 電腦上，您會使用 toogenerate hello 憑證。 如果您想 tooinstall 另一部用戶端電腦上的用戶端憑證，您可以匯出 hello 憑證。
 
1. Hello 在同一部電腦使用 toocreate hello 的自我簽署憑證，請開啟命令提示字元，以系統管理員身分。
2. 修改並執行 hello 範例 toogenerate 用戶端憑證。
  * 變更*"P2SRootCert"* toohello hello hello 用戶端憑證，從產生的自我簽署根名稱。 請確定您使用 hello 根憑證，也就是任何 hello hello 名稱 ' CN =' 的值為您指定當您建立 hello 自我簽署的根。
  * 變更*P2SChildCert*想 toogenerate 用戶端憑證 toobe toohello 名稱。

  如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 P2SChildcert 所產生的根憑證 P2SRootCert 您個人憑證存放區中的用戶端憑證。

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>匯出用戶端憑證

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>安裝匯出的用戶端憑證

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>後續步驟

繼續使用您的點對站設定。 

* 如**資源管理員**部署模型的步驟，請參閱[設定點對站連線 tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。
* 如**傳統**部署模型的步驟，請參閱[設定點對站 VPN 連線 tooa VNet （傳統）](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。
