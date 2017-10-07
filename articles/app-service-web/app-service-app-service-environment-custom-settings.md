---
title: "應用程式服務環境的 aaaCustom 設定"
description: "App Service 環境的自訂組態設定"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>App Service 環境的自訂組態設定
## <a name="overview"></a>概觀
由於應用程式服務環境隔離的 tooa 單一客戶，有一些組態設定可以套用專門 tooApp 服務環境。 此文件編號 hello 各種可用的應用程式服務環境的特定自訂。

如果您沒有 App Service 環境，請參閱[如何 tooCreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。

您可以將 App Service 環境的自訂內容儲存利用陣列中的 hello 新**clusterSettings**屬性。 這個屬性的 hello 的 hello 「 屬性 」 目錄中找到*hostingEnvironments* Azure 資源管理員實體。

hello 下列縮寫的資源管理員範本程式碼片段示範 hello **clusterSettings**屬性：

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

hello **clusterSettings**屬性可以包含在資源管理員範本 tooupdate hello App Service 環境。

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>使用 Azure 資源總管 tooupdate App Service 環境
或者，您可以藉由更新 App Service 環境的 hello [Azure 資源總管](https://resources.azure.com)。  

1. 在資源總管中，請移至 App Service 環境的 hello toohello 節點 (**訂閱** > **resourceGroups** > **提供者** > **Microsoft.Web** > **hostingEnvironments**)。 然後按一下 hello 想 tooupdate 特定 App Service 環境。
2. Hello 右窗格中，按一下 **讀/寫**hello 上方工具列 tooallow 互動式編輯在 資源總管 中。  
3. 按一下藍色 hello**編輯**按鈕 toomake hello 資源管理員範本可編輯。
4. 捲動 toohello hello 右窗格的底部。 hello **clusterSettings**屬性位於 hello 最底部，您可以在其中輸入或更新其值。
5. 您想在 hello 的組態值的類型 （或複製和貼上） hello 陣列**clusterSettings**屬性。  
6. 按一下綠色的 hello**放**按鈕，在 hello 右窗格 toocommit hello 變更 toohello App Service 環境的 hello 頂端找到。

不過您送出 hello 變更時，所花大約 30 分鐘乘以前端 hello App Service 環境的 hello 變更 tootake 作用中的 hello 數目。
例如，如果 App Service 環境有四個前端，它會使用 hello 組態更新 toofinish 約兩小時後。 雖然 hello 組態變更正在推出，沒有其他的縮放作業或組態變更作業可能需要 hello App Service 環境中的位置。

## <a name="disable-tls-10"></a>停用 TLS 1.0
來自客戶的週期性問題，特別是在處理的 PCI 合規性客戶稽核，是如何 tooexplicitly 停用 TLS 1.0 的自己的應用程式。

您可以停用 TLS 1.0 透過 hello 下列**clusterSettings**項目：

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>變更 TLS 加密套件順序
來自客戶的另一個問題就是它們可以修改其伺服器所交涉的加密方式 hello 清單，並且這可藉由修改 hello **clusterSettings**如下所示。 可以從擷取可用的加密套件 hello 清單[MSDN 本文](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx)。

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> 安全通道不了解的 hello 加密套件設定不正確的值，如果所有 TLS 通訊 tooyour 伺服器可能會都停止運作。 在此情況下，您將需要 tooremove hello *FrontEndSSLCipherSuiteOrder*項目從**clusterSettings**並送出 hello 更新資源管理員範本 toorevert 後 toohello 預設加密套件設定。  請謹慎使用這項功能。
> 
> 

## <a name="get-started"></a>開始使用
hello Azure 快速入門資源管理員範本站台包含具有 hello 基底定義的範本[建立 App Service 環境](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/)。

<!-- LINKS -->

<!-- IMAGES -->
