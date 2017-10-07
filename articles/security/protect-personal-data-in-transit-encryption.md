---
title: "aaaProtect 個人資料在傳輸過程中使用 Azure 中的加密 |Microsoft 文件"
description: "在 Azure tooprotect 個人資料使用加密"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Azure 加密技術：使用加密功能來保護傳輸中的個人資料

本文將協助您了解及使用 Azure 加密技術 toosecure 資料在傳輸過程中。 

保護 hello 隱私權的個人資料傳送嗨網路跨是多層的深度防禦的安全性策略中不可或缺的一部分。 在傳輸過程中的加密 」 是設計的 tooprevent 攻擊者攔截從所能 tooview 或使用 hello 資料傳輸。

## <a name="scenario"></a>案例

大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 toosupport 努力，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國 

hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。 其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。 它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。 hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。

客戶的個人資料會輸入 hello 資料庫中，從 hello 公司遠端辦公室和位於 hello 世界各地的旅行代理程式。 包含客戶資訊的文件會透過 hello 網路 tooAzure 儲存體傳輸。

## <a name="problem-statement"></a>問題陳述

hello 公司必須保護客戶的 hello 隱私權和員工的個人資料，同時它處於傳輸 tooand 從 Azure 服務。

## <a name="company-goal"></a>公司目標

hello 公司目標 tooensure 個人資料會加密磁碟關閉時。 如果未經授權的人員攔截 hello 關閉磁碟個人資料，它必須是會轉譯無法讀取的格式。 對於使用者和系統管理員而言，套用加密應該很容易或完全透明。

## <a name="solutions"></a>解決方案

Azure 服務可提供多個工具和技術 toohelp 保護傳輸中的個人資料。

### <a name="azure-storage"></a>Azure 儲存體

Hello 雲端中儲存的資料必須周遊從 hello 用戶端，它可以是實際上都位於任何位置 hello world，toohello Azure 資料中心。 使用者所擷取的資料時，傳送一次，在 hello 相反的方向。 資料在傳輸過程中 hello 透過公用網際網路端一定是攻擊者攔截的風險。 它是重要 tooprotect hello 隱私權的個人資料使用傳輸層級加密 toosecure 做為它的位置之間移動。

hello HTTPS 通訊協定透過 hello 網際網路提供安全且加密的通訊通道。 呼叫 REST Api 時，應該使用的 tooaccess 物件在 Azure 儲存體和 HTTPS。 使用時，強制使用 hello HTTPS 通訊協定[共用存取簽章](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)(SAS) toodelegate 存取 tooAzure 儲存物件。 SAS 類型有兩種：服務 SAS 和帳戶 SAS。

#### <a name="how-do-i-construct-a-service-sas"></a>如何建構服務 SAS？

服務的 SAS 委派存取 tooa 資源中其中一個 hello 儲存體服務 （blob、 佇列、 資料表或檔案服務）。 tooconstruct 服務 SAS，請勿 hello 遵循：

1. 指定簽署版本欄位 hello

2. 指定 hello 簽章資源 （Blob 檔案服務僅與）

3. 指定查詢參數 tooOverride 回應標頭 （Blob 服務和只有檔案服務）

4. 指定 hello 資料表 （表格服務僅名稱）

5. 指定 hello 存取原則

6. 指定 hello 簽章有效性間隔

8. 指定權限

9. 指定 IP 位址或 IP 範圍

10. 指定 hello HTTP 通訊協定

11. 指定資料表存取範圍

12. 指定簽署識別碼 hello

13. 指定 hello 簽章

如需詳細指示，請參閱[建構服務 SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN)。

#### <a name="how-do-i-construct-an-account-sas"></a>如何建構帳戶 SAS？

帳戶 SAS 會將委派存取 tooresources 一或多個 hello 儲存體服務中。 您也可以委派存取 tooread、 寫入和刪除 blob 容器、 資料表、 佇列和服務的 SAS 不允許的檔案共用上的作業。 帳戶 SAS 的建構是類似的服務 SA toothat。 如需詳細指示，請參閱[建構服務 SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)。

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>呼叫 REST API 時如何強制使用 HTTPS？

tooenforce hello 使用 HTTPS 呼叫儲存體帳戶中的 REST Api tooaccess 物件時，您可以啟用安全傳輸需要 hello 儲存體帳戶。 

1. 在 hello Azure 入口網站，選取 **建立儲存體帳戶**，或現有的儲存體帳戶，請選取**設定**然後**組態**。

2. 在 [需要安全傳輸] 下，選取 [已啟用]。

![建立儲存體帳戶](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

如需詳細指示，包括如何 tooenable 安全傳輸需要以程式設計的方式，請參閱[需要安全傳輸](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer)。

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>如何在 Azure 檔案儲存體中加密資料？

tooencrypt 資料在傳輸與[Azure 檔案儲存體](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal)，您可以使用 SMB 3.x 與 Windows 8、 8.1 及 10 和 Windows Server 2012 R2 和 Windows Server 2016。 當您使用 hello Azure 檔案服務時，任何未加密時連線失敗 」 保護所需的傳輸 」 已啟用。 這包括使用 SMB 2.1、 未加密，SMB 3.0 和 hello Linux SMB 用戶端的部分類別的案例。

#### <a name="azure-client-side-encryption"></a>Azure 用戶端加密

當個人資料在用戶端應用程式與儲存體之間傳輸時，另一個用於保護該資料的選項是[用戶端加密](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)。 hello 資料都會經過加密後再傳輸至 Azure 儲存體，並收到 hello 用戶端之後，當您擷取 hello 資料從 Azure 儲存體時，會解密 hello 資料。

### <a name="azure-site-to-site-vpn"></a>Azure 站對站 VPN

個人在公司網路或使用者與 hello Azure 虛擬網路之間傳輸資料有效地 tooprotect 是 toouse[站對站](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)或[點對站台](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)虛擬私人網路 (VPN)。 VPN 連線 hello 網際網路之間建立安全的加密的通道。

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>如何建立站對站 VPN 連線？

站對站 VPN 連線 hello 公司網路 tooAzure 上的多個使用者。 toocreate hello Azure 入口網站中的站對站連接嗎 hello 遵循：

1. 建立虛擬網路。

2. 指定 DNS 伺服器。

3. 建立 hello 閘道子網路。

4. 建立 hello VPN 閘道。 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. 建立 hello 區域網路閘道。

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. 設定 VPN 裝置。

7. 建立 hello VPN 連線。

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. 請確認 hello VPN 連線。

如需詳細指示上如何 toocreate 網站-站台連接在 hello Azure 入口網站，請參閱 [hello Azure 入口網站中建立站台間連線]。(https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>如何設定點對站 VPN 連線？

點對站 VPN 會從個別的用戶端電腦 tooa 虛擬網路建立安全連線。 當您想 tooconnect tooAzure 從遠端位置，例如從首頁，或在旅館或會議中心時，這非常有用。 toocreate hello Azure 入口網站中的點對站連接

1. 建立虛擬網路。

2. 新增閘道子網路。

3. 指定 DNS 伺服器。 (選用)

4. 建立虛擬網路閘道。

5. 產生憑證。

6. 新增 hello 用戶端位址集區。

7. 上傳 hello 根憑證的公開憑證資料。

8. 產生並安裝 hello VPN 用戶端組態封裝。

9. 安裝匯出的用戶端憑證。

10. 連接 tooAzure。

11. 確認您的連線。

如需詳細指示，請參閱[設定點對站連線 tooa VNet 使用憑證驗證： Azure 入口網站。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Microsoft 建議您一律使用 SSL/TLS 通訊協定 tooexchange 資料分散在不同的位置。 選擇 toouse 的組織[ExpressRoute](https://docs.microsoft.com/azure/expressroute/)透過專用高速 WAN 連結 toomove 大型資料集也可以加密 hello hello 為了提高保護使用 SSL/TLS 或其他通訊協定的應用程式層級的資料。

### <a name="encryption-by-default"></a>預設加密

Microsoft 會使用加密 tooprotect 資料中的 customers 與 Azure 雲端服務之間傳輸。 如果透過 hello Azure 網站互動與 Azure 儲存體，所有交易將會透過 HTTPS 都發生。

[傳輸層安全性](https://en.wikipedia.org/wiki/Transport_Layer_Security)(TLS) 是 Microsoft 資料中心內會嘗試與連接 tooMicrosoft 雲端服務的用戶端系統 toonegotiate hello 通訊協定。 TLS 提供增強式驗證、訊息隱私權、完整性 (可偵測訊息竄改、攔截和偽造)、互通性、演算法彈性，並方便部署和使用。

此外，也會運用 [完整轉寄密碼](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS)，以便客戶的用戶端系統與 Microsoft 的雲端服務之間的每個連線使用唯一金鑰。 連線 tooMicrosoft 雲端服務也充分利用基礎的 RSA 2048 位元加密金鑰長度。 hello TLS，RSA 2048 位元金鑰長度的組合和 PFS 會讓它更為困難有人 toointercept 及存取 Microsoft 雲端服務與客戶之間傳輸的資料。

傳輸中的資料一律會在 [Data Lake Store] 中加密 (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview)。 此外 tooencrypting 資料先前 toostoring toopersistent 媒體 hello 資料也都受到保護傳輸中使用 HTTPS。 HTTPS 是 hello 唯一的通訊協定支援的資料湖存放區 REST 介面的 hello。

## <a name="summary"></a>摘要

hello 公司可以完成其目標是保護這類資料的個人資料和 hello 隱私權強制使用 HTTPS 連線 tooAzure 儲存體、 使用共用存取簽章，以及啟用 hello 儲存體帳戶中的 安全傳輸需要。 他們也可藉由使用 SMB 3.0 連線並實作用戶端加密來保護個人資料。 站對站 VPN 連線，從 hello 公司網路 toohello Azure 虛擬網路和點對站 VPN 連線，從個別的使用者將會建立安全通道，透過它的個人資料可以安全地傳輸。 Microsoft 的預設加密作法會進一步保護 hello 隱私權的個人資料。

## <a name="next-steps"></a>後續步驟

- [Azure 資料安全性和加密最佳做法](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [規劃與設計 VPN 閘道](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [VPN 閘道常見問題集](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [購買及設定您的 Azure App Service 的 SSL 憑證](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
