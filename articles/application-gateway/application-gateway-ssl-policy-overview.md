---
title: "Azure 應用程式閘道 aaaSSL 原則概觀 |Microsoft 文件"
description: "深入了解 Azure 應用程式閘道可讓您 tooconfigure SSL 原則"
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>應用程式閘道 SSL 原則概觀

應用程式閘道可讓您 toocentralize SSL 憑證管理，並降低從後端伺服器陣列的加密和解密的額外負荷。 這個集中式的 SSL 處理也可讓您 toospecify 中央 SSL 原則適合 tooyour 組織的安全性需求。 這可協助您符合法規需求，以及安全性指導方針和建議的做法。

SSL 政策包含 SSL 通訊協定版本，以及加密套件和 hello 順序 SSL 交握期間所使用的破解密碼的控制項。 向此應用程式閘道提供兩種機制 tooallow 客戶 toocontrol SSL 原則、 預先定義或自訂的原則。

## <a name="predefined-ssl-policy"></a>預先定義的 SSL 原則

應用程式閘道有三個預先定義的安全性原則。 您可以使用任何這些原則 tooget hello 適當安全性層級設定您的閘道。 hello 原則名稱加註 hello 年份和月份會以設定。 每個原則都有不同的 SSL 通訊協定版本和加密套件。 建議 toouse hello 最新 SSL 原則 tooensure hello 最佳 SSL 安全性。 應用程式閘道現在可讓使用者 toochoose 從其中一個 hello 下列預先定義。

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|屬性  |值  |
|---|---|
|名稱     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|預設值| True (如果未定義任何預先定義原則) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|屬性  |值  |
|   ---      |  ---       |
|名稱     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|預設值| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|屬性  |值  |
|---|---|
|名稱     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|預設值| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>自訂 SSL 原則

如果預先定義的 SSL 原則需要 toobe 設定為您的需求，您會有必須定義您自己自訂的 SSL 原則。 在此情況下，您已擁有 hello 最小 SSL 通訊協定版本 toosupport 的完整控制權，以及支援的加密套件，以及其優先順序。
 
SSL 通訊協定版本：

* 依預設，所有應用程式閘道都停用 SSL 2.0 和 3.0。 這些通訊協定版本無法設定。
* 自訂 SSL 原則定義可提供您選項的下列三種通訊協定為 hello SSL 通訊協定的最低版本您的閘道 TLSv1_0，TLSv1_1，TLSv1_2 hello tooselect 任何一個。
* 如果未定義任何 SSL 原則，則這三個 (TLSv1_0、TLSv1_1、TLSv1_2) 皆會啟用。

加密套件：

應用程式閘道支援下列可以從中選擇您的自訂原則的加密套件 hello。 hello 的加密套件順序 hello SSL 交涉期間判斷 hello 優先順序。

可用的加密套件：

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>後續步驟

[在應用程式閘道上設定 SSL 原則](application-gateway-configure-ssl-policy-powershell.md)
