---
title: "Azure Stack 整合式系統的 Azure Stack 公開金鑰基礎結構憑證需求 | Microsoft Docs"
description: "說明 Azure Stack 整合式系統的 Azure Stack PKI 憑證部署需求。"
services: azure-stack
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: jeffgilb
ms.reviewer: wfayed
ms.openlocfilehash: 8f0bb2266cb3a8a869ad50c40a46eb82985d17ed
ms.sourcegitcommit: 5108f637c457a276fffcf2b8b332a67774b05981
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="azure-stack-public-key-infrastructure-certificate-requirements"></a>Azure Stack 公開金鑰基礎結構憑證需求
Azure Stack 有一個公共基礎結構網路，其使用已指派給一小組 Azure Stack 服務和可能租用戶 VM 的外部可存取公用 IP 位址。 在 Azure Stack 部署期間，這些 Azure Stack 公用基礎結構端點需要具有適當 DNS 名稱的 PKI 憑證。 本文提供以下相關資訊：

- 部署 Azure Stack 時需要哪些憑證
- 取得符合這些規格之憑證的程序
- 如何在部署期間準備、驗證及使用這些憑證

## <a name="certificate-requirements"></a>憑證需求
下列清單描述部署 Azure Stack 時所需的憑證需求： 
- 憑證必須由內部憑證授權單位或公用憑證授權單位發出。 如果使用公用憑證授權單位，它必須包含在基礎作業系統映像中成為 Microsoft 信任根授權單位方案的一部分。 您可以在這裡找到完整清單：https://gallery.technet.microsoft.com/Trusted-Root-Certificate-123665ca 
- 憑證可以是單一萬用字元憑證，其中涵蓋主體別名 (SAN) 欄位中的所有命名空間。 或者，您可以針對需要憑證的端點 (例如儲存體和 Key Vault)，使用採用萬用字元的個別憑證。 
- 憑證簽章演算法不能是 SHA1，因為它必須更強大。 
- 憑證格式必須是 PFX，因為安裝 Azure Stack 時需要公用與私密金鑰。 
- 憑證 pfx 檔案的 [金鑰使用方法] 欄位中必須有 [數位簽章] 和 [KeyEncipherment] 值。
- 部署時，所有憑證 pfx 檔案的密碼都必須相同
- 確定所有憑證的 [主體名稱] 和 [主體別名] 都必須符合本文中所述的規格，以免部署失敗。

> [!NOTE]
> 支援憑證信任鏈結 IS 中存在的中繼憑證授權單位。 

## <a name="mandatory-certificates"></a>必要憑證
本節中的表格說明 Azure AD 與 AD FS Azure Stack 部署所需的 Azure Stack 公用端點 PKI 憑證。 憑證需求會依區域以及使用的命名空間和每個命名空間所需的憑證分組。 此表格同時說明解決方案提供者在其中為每個公用端點複製不同憑證的資料夾。 

每個 Azure Stack 公用基礎結構端點需要具有適當 DNS 名稱的憑證。 每個端點的 DNS 名稱是以下列格式表示：*&lt;prefix>.&lt;region>.&lt;fqdn>*。 

針對您的部署，[region] 和 [externalfqdn] 值必須符合您為 Azure Stack 系統選擇的地區和外部網域名稱。 例如，如果區域名稱為 Redmond，而外部網域名稱為 contoso.com，則 DNS 名稱的格式會是 *&lt;prefix>.redmond.contoso.com*。Microsoft 會預先指定 *&lt;prefix>* 值，以描述憑證所保護的端點。 此外，外部基礎結構端點的 *&lt;prefix>* 值取決於使用特定端點的 Azure Stack 服務。 

|部署資料夾|必要的憑證主體和主體別名 (SAN)|範圍 (每個區域)|子網域命名空間|
|-----|-----|-----|-----|
|公用入口網站|portal.*&lt;region>.&lt;fqdn>*|入口網站|*&lt;region>.&lt;fqdn>*|
|管理入口網站|adminportal.*&lt;region>.&lt;fqdn>*|入口網站|*&lt;region>.&lt;fqdn>*|
|Azure Resource Manager (公用)|management.*&lt;region>.&lt;fqdn>*|Azure Resource Manager|*&lt;region>.&lt;fqdn>*|
|Azure Resource Manager (管理員)|adminmanagement.*&lt;region>.&lt;fqdn>*|Azure Resource Manager|*&lt;region>.&lt;fqdn>*|
|ACS<sup>1</sup>|具有主體別名的一個多重子網域萬用字元憑證：<br>&#42;.blob.*&lt;region>.&lt;fqdn>*<br>&#42;.queue.*&lt;region>.&lt;fqdn>*<br>&#42;.table.*&lt;region>.&lt;fqdn>*|儲存體|blob.*&lt;region>.&lt;fqdn>*<br>table.*&lt;region>.&lt;fqdn>*<br>queue.*&lt;region>.&lt;fqdn>*|
|KeyVault|&#42;.vault.*&lt;region>.&lt;fqdn>*<br>(萬用字元 SSL 憑證)|Key Vault|vault.*&lt;region>.&lt;fqdn>*|
|KeyVaultInternal|&#42;.adminvault.*&lt;region>.&lt;fqdn>*<br>(萬用字元 SSL 憑證)|內部金鑰保存庫|adminvault.*&lt;region>.&lt;fqdn>*|
|
<sup>1</sup> ACS 憑證要求單一憑證上有三個萬用字元 SAN。 並非所有公用憑證授權單位都支援單一憑證上有多個萬用字元 SAN。 

如果您使用 Azure AD 部署模式來部署 Azure Stack，您只需要求上表中所列的憑證。 不過，如果您使用 AD FS 部署模式來部署 Azure Stack，您也必須要求下表中所述的憑證：

|部署資料夾|必要的憑證主體和主體別名 (SAN)|範圍 (每個區域)|子網域命名空間|
|-----|-----|-----|-----|
|ADFS|adfs.*&lt;region>.&lt;fqdn>*<br>(SSL 憑證)|ADFS|*&lt;region>.&lt;fqdn>*|
|圖形|graph.*&lt;region>.&lt;fqdn>*<br>(SSL 憑證)|圖形|*&lt;region>.&lt;fqdn>*|
|

> [!IMPORTANT]
> 本章所列的所有憑證都必須都有相同的密碼。 

## <a name="optional-paas-certificates"></a>選擇性 PaaS 憑證
如果您打算在部署及設定 Azure Stack 之後，部署其他 Azure Stack PaaS 服務 (SQL、MySQL 和 App Service)，您需要要求額外的憑證來涵蓋 PaaS 服務端點。 

> [!IMPORTANT]
> 您用於 App Service、SQL 和 MySQL 資源提供者的憑證，必須具備與用於全域 Azure Stack 端點之憑證相同的根授權單位。 

下表說明 SQL 和 MySQL 配接器及 App Service 所需的端點和憑證。 您不需要將這些憑證複製到 Azure Stack 部署資料夾。 而當您安裝額外的資源提供者時，您會提供這些憑證。 

|範圍 (每個區域)|憑證|必要的憑證主體和主體別名 (SAN)|子網域命名空間|
|-----|-----|-----|-----|
|SQL、MySQL|SQL 和 MySQL|&#42;.dbadapter.*&lt;region>.&lt;fqdn>*<br>(萬用字元 SSL 憑證)|dbadapter.*&lt;region>.&lt;fqdn>*|
|App Service 方案|Web 流量預設 SSL 憑證|&#42;.appservice.*&lt;region>.&lt;fqdn>*<br>&#42;.scm.appservice.*&lt;region>.&lt;fqdn>*<br>(多重網域萬用字元 SSL 憑證<sup>1</sup>)|appservice.*&lt;region>.&lt;fqdn>*<br>scm.appservice.*&lt;region>.&lt;fqdn>*|
|App Service 方案|API|api.appservice.*&lt;region>.&lt;fqdn>*<br>(SSL 憑證<sup>2</sup>)|appservice.*&lt;region>.&lt;fqdn>*<br>scm.appservice.*&lt;region>.&lt;fqdn>*|
|App Service 方案|FTP|ftp.appservice.*&lt;region>.&lt;fqdn>*<br>(SSL 憑證<sup>2</sup>)|appservice.*&lt;region>.&lt;fqdn>*<br>scm.appservice.*&lt;region>.&lt;fqdn>*|
|App Service 方案|SSO|sso.appservice.*&lt;region>.&lt;fqdn>*<br>(SSL 憑證<sup>2</sup>)|appservice.*&lt;region>.&lt;fqdn>*<br>scm.appservice.*&lt;region>.&lt;fqdn>*|

<sup>1</sup> 需要一個具有多個萬用字元主體別名的憑證。 並非所有公用憑證授權單位都支援單一憑證上有多個萬用字元 SAN。 

<sup>2</sup> &#42;.appservice.*&lt;region>.&lt;fqdn>* 萬用字元憑證無法用來取代這三個憑證 (api.appservice.*&lt;region>.&lt;fqdn>*、ftp.appservice.*&lt;region>.&lt;fqdn>* 和 sso.appservice.*&lt;region>.&lt;fqdn>*。 應用程式服務明確要求對這些端點使用個別的憑證。 


## <a name="next-steps"></a>後續步驟
[產生適用於 Azure Stack 部署的 PKI 憑證](azure-stack-get-pki-certs.md) 


