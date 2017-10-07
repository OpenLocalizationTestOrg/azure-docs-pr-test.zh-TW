---
title: "aaaTroubleshoot Azure 點對站連線問題 |Microsoft 文件"
description: "深入了解如何 tootroubleshoot 點對站連線問題。"
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>疑難排解：Azure 點對站連線問題

本文列出您可能遇到的常見點對站連線問題。 文中也會探討這些問題的可能原因和解決方案。

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>VPN 用戶端錯誤：找不到憑證

### <a name="symptom"></a>徵狀

當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:

**找不到可以使用這個可延伸的驗證通訊協定的憑證。(錯誤 798)**

### <a name="cause"></a>原因

如果遺漏 hello 用戶端憑證，就會發生這個問題**憑證-目前的憑證**。

### <a name="solution"></a>方案

請確定該 hello 用戶端憑證已安裝在 hello 遵循 hello 憑證存放區 (Certmgr.msc) 的位置：
 
**憑證 - 目前的使用者\個人\憑證**

如需如何 tooinstall hello 用戶端憑證的詳細資訊，請參閱[產生及匯出憑證，為點對站連線](vpn-gateway-certificates-point-to-site.md)。

> [!NOTE]
> 當您匯入 hello 用戶端憑證時，請勿選取 hello**啟用加強私密金鑰保護**選項。

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>VPN 用戶端錯誤： 收到 hello 訊息發現非預期或格式不正確

### <a name="symptom"></a>徵狀

當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:

**收到 hello 訊息發現非預期或格式不正確。(錯誤 0x80090326)**

### <a name="cause"></a>原因

如果 hello 根憑證公開金鑰不會上傳到 hello Azure VPN 閘道，就會發生這個問題。 如果 hello 金鑰已毀損或過期時，它也會發生。

### <a name="solution"></a>方案

tooresolve 這個問題，請檢查 hello 狀態的 hello 根的憑證在 Azure 入口網站 toosee hello 是否已被撤銷。 如果未被撤銷，請嘗試 toodelete hello 根憑證和 reupload。 如需詳細資訊，請參閱 [建立憑證](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts)。

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>VPN 用戶端錯誤：憑證鏈結已處理但被終止 

### <a name="symptom"></a>徵狀 

當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:

**憑證鏈結已處理，但在 hello 信任提供者所未信任的根憑證終止。**

### <a name="solution"></a>方案

1. 請確定該 hello 遵循憑證位於 hello 正確的位置：

    | 憑證 | 位置 |
    | ------------- | ------------- |
    | AzureClient.pfx  | 目前的使用者\個人\憑證 |
    | Azuregateway-*GUID*.cloudapp.net  | 目前的使用者\受信任的根憑證授權單位|
    | AzureGateway-*GUID*.cloudapp.net、AzureRoot.cer    | 本機電腦\受信任的根憑證授權單位|

2. 如果 hello 憑證已經在 hello 位置，請嘗試 toodelete hello 憑證，並將它們重新安裝。 hello  **azuregateway-*GUID*。 cloudapp.net** 憑證位於 hello VPN 用戶端組態封裝從 hello Azure 入口網站下載。 您可以使用從 hello 封裝檔案封存 tooextract hello 檔案。

## <a name="file-download-error-target-uri-is-not-specified"></a>檔案下載錯誤：未指定目標 URI

### <a name="symptom"></a>徵狀

您會收到下列錯誤訊息的 hello:

**檔案下載錯誤。未指定目標 URI。**

### <a name="cause"></a>原因 

此問題的發生原因是閘道類型不正確。 

### <a name="solution"></a>方案

hello VPN 閘道類型必須是**VPN**，而且 hello VPN 類型必須是**RouteBased**。

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>VPN 用戶端錯誤：Azure VPN 自訂指令碼失敗 

### <a name="symptom"></a>徵狀

當您使用 hello VPN 用戶端嘗試 tooconnect tooan Azure 虛擬網路時，您會收到下列錯誤訊息的 hello:

**自訂指令碼 （您的路由表 tooupdate） 失敗。(錯誤 8007026f)**

### <a name="cause"></a>原因

如果您正在使用快速鍵 tooopen hello 站對點 VPN 連線，可能會發生此問題。

### <a name="solution"></a>方案 

開啟 hello VPN 封裝直接而不是從 hello 捷徑開啟它。

## <a name="cannot-install-hello-vpn-client"></a>無法安裝 hello VPN 用戶端

### <a name="cause"></a>原因 

額外的憑證是必要的 tootrust hello VPN 閘道，您的虛擬網路。 hello 憑證包含在 hello VPN 用戶端組態封裝產生自 hello Azure 入口網站。

### <a name="solution"></a>方案

擷取 hello VPN 用戶端組態封裝，並尋找 hello.cer 檔案中。 tooinstall hello 憑證，請遵循下列步驟：

1. 開啟 mmc.exe。
2. 新增 hello**憑證**嵌入式管理單元。
3. 選取 hello**電腦**hello 本機電腦帳戶。
4. 以滑鼠右鍵按一下 hello**受信任的根憑證授權單位**節點。 按一下**全部工作** > **匯入**，和您從 hello VPN 用戶端組態封裝擷取瀏覽 toohello.cer 檔案。
5. Hello 電腦重新啟動。 
6. 嘗試使用 tooinstall hello VPN 用戶端。

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Azure 入口網站的錯誤： 無法 toosave hello VPN 閘道和 hello 資料無效

### <a name="symptom"></a>徵狀

當您嘗試在 hello Azure 入口網站中的 hello VPN 閘道的 toosave hello 變更時，您會收到下列錯誤訊息的 hello:

**失敗的 toosave 虛擬網路閘道&lt;*閘道名稱*&gt;。 憑證 &lt;*憑證識別碼*&gt; 的資料無效。**

### <a name="cause"></a>原因 

如果 hello 根憑證公開金鑰您上傳包含無效的字元，例如空格，可能會發生此問題。

### <a name="solution"></a>方案

請確定 hello 憑證中的 hello 資料不包含無效的字元，例如分行符號 （換行）。 hello 整個值應該是一行很長。 下列文字的 hello 是 hello 憑證的範例：

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Azure 入口網站的錯誤： 無法 toosave hello VPN 閘道，而且 hello 資源名稱無效

### <a name="symptom"></a>徵狀

當您嘗試在 hello Azure 入口網站中的 hello VPN 閘道的 toosave hello 變更時，您會收到下列錯誤訊息的 hello: 

**失敗的 toosave 虛擬網路閘道&lt;*閘道名稱*&gt;。 資源名稱&lt; *tooupload 再試一次的憑證名稱*&gt;是無效的 * *。

### <a name="cause"></a>原因

因為 hello hello 憑證名稱包含無效的字元，例如空格，就會發生這個問題。 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Azure 入口網站錯誤：VPN 套件檔案下載錯誤 503

### <a name="symptom"></a>徵狀

當您嘗試 toodownload hello VPN 用戶端組態封裝時，您會收到下列錯誤訊息的 hello:

**無法 toodownload hello 檔案。錯誤詳細資料： 503 錯誤。hello 伺服器太忙碌。**
 
### <a name="solution"></a>方案

此錯誤可能是由暫時性的網路問題所造成。 幾分鐘的時間之後，重試 toodownload hello VPN 封裝。

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Azure VPN 閘道升級： 所有 P2S 用戶端將無法 tooconnect

### <a name="cause"></a>原因

Hello 憑證是否超過 50%到它的存留期 hello 憑證變換。

### <a name="solution"></a>方案

tooresolve 這個問題，請建立並轉散發新憑證 toohello VPN 用戶端。 

## <a name="too-many-vpn-clients-connected-at-once"></a>一次有太多 VPN 用戶端連線

每個 VPN 閘道，hello 允許的連線數目上限為 128。 您可以看到連接的用戶端 hello Azure 入口網站中的 hello 總數。

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>點對站 VPN 不正確地將 10.0.0.0/8 toohello 路由表的路由

### <a name="symptom"></a>徵狀

當您撥 hello hello 點對站台的用戶端上的 VPN 連線時，hello VPN 用戶端應該加入朝 hello Azure 虛擬網路的路由。 hello IP 協助程式服務應該加入的 hello VPN 用戶端 hello 子網路的路由。 

hello VPN 用戶端範圍所屬 10.0.0.0/8，例如 10.0.12.0/24 tooa 較小的子的網路。 系統會新增較高優先順序的 10.0.0.0/8 路由，而不是 10.0.12.0/24 的路由。 

這個不正確的路由會中斷與其他內部部署網路可能屬於 tooanother 10.50.0.0/24，例如 hello 10.0.0.0/8 範圍內的子網路上沒有定義的特定路由的連線。 

### <a name="cause"></a>原因

這是針對 Windows 用戶端設計的行為。 當 hello 用戶端會使用 hello PPP IPCP 通訊協定時，它會從 hello 伺服器 （在此情況下 hello VPN 閘道） 取得 hello hello 通道介面的 IP 位址。 不過，由於 hello 通訊協定的限制，hello 用戶端並沒有 hello 子網路遮罩。 因為沒有任何其他方式 tooget hello 用戶端，它會嘗試根據 hello hello 通道介面 IP 位址類別 tooguess hello 子網路遮罩。 

因此，您已加入根據 hello 下列靜態對應的路由： 

如果位址所屬 tooclass A--> 套用/8

如果位址所屬的 tooclass B--> 套用為/16

如果位址所屬的 tooclass C--> 套用/24

## <a name="vpn-client-cannot-access-network-file-shares"></a>VPN 用戶端無法存取網路檔案共用

### <a name="symptom"></a>徵狀

hello VPN 用戶端已連線 toohello Azure 虛擬網路。 不過，hello 用戶端無法存取網路共用。

### <a name="cause"></a>原因

hello SMB 通訊協定用於存取檔案共用。 起始 hello 連線時，hello VPN 用戶端新增 hello 工作階段的認證，並發生 hello 失敗。 建立 hello 連接之後，hello 用戶端會強制 toouse hello 快取認證，Kerberos 驗證。 此程序隨即起始查詢 toohello 金鑰發佈中心 （網域控制站） tooget 語彙基元。 Hello 用戶端會從 hello 網際網路連線，因為它可能不能 tooreach hello 網域控制站。 因此，hello 用戶端無法從 Kerberos tooNTLM 容錯移轉。 

只有時間的認證是包含有效的憑證時，系統會提示該 hello 用戶端 hello （使用 SAN = UPN） 它所聯結的 hello 網域 toowhich 所發出。 hello 用戶端也必須是實體連線的 toohello 網域網路。 在此情況下，hello 用戶端會嘗試 toouse hello 憑證，並向外連 toohello 網域控制站。 然後 hello 金鑰發佈中心會傳回"KDC_ERR_C_PRINCIPAL_UNKNOWN 」 錯誤。 hello 用戶端是強制的 toofail tooNTLM。 

### <a name="solution"></a>方案

toowork hello 問題，停用 hello 快取的網域認證，從下列登錄子機碼的 hello: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>找不到 hello 點對站 VPN 連線中 Windows hello VPN 用戶端重新安裝之後

### <a name="symptom"></a>徵狀

您移除 hello 點對站 VPN 連線，然後再重新安裝 hello VPN 用戶端。 在此情況下，hello VPN 連線設定不成功。 看不到在 hello hello VPN 連線**網路連線**Windows 中的設定。

### <a name="solution"></a>方案

tooresolve hello 問題，請刪除 hello 舊 VPN 用戶端組態檔從**C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**，然後再次執行 hello VPN 用戶端安裝程式。
