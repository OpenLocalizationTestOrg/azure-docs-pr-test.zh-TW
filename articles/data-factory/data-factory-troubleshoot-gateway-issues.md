---
title: "資料管理閘道器會發出 aaaTroubleshoot |Microsoft 文件"
description: "提供秘訣 tootroubleshoot 問題相關的 tooData 管理閘道器。"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>使用資料管理閘道針對問題進行疑難排解
本文提供使用資料管理閘道進行疑難問題排解的相關資訊。

> [!NOTE]
> 請參閱 hello[資料管理閘道器](data-factory-data-management-gateway.md)hello 閘道的詳細資訊的發行項。 請參閱 hello[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)將資料從內部部署 SQL Server 資料庫 tooMicrosoft Azure Blob 儲存體中，使用 hello 閘道的逐步解說中的發行項。
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>失敗的 tooinstall 或註冊閘道
### <a name="1-problem"></a>1.問題
您看到此錯誤訊息時安裝並註冊閘道器，特別，下載 hello 閘道安裝檔案時。

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>原因
嘗試 tooinstall hello 閘道 hello 機器失敗 toodownload hello 最新閘道安裝檔案從 hello 下載中心到期 tooa 網路問題。

#### <a name="resolution"></a>解決方案
檢查防火牆 proxy 伺服器設定 toosee hello 設定會封鎖從 hello 電腦 toohello hello 網路連線是否[下載中心](https://download.microsoft.com/)，並更新 hello 設定據以。

或者，您可以從 hello 下載 hello hello 最新閘道的安裝檔[下載中心](https://www.microsoft.com/download/details.aspx?id=39717)在其他電腦可以存取 hello 下載中心上。 您可以複製 hello 安裝程式檔案 toohello 閘道主機電腦並手動執行 tooinstall 及更新 hello 閘道。

### <a name="2-problem"></a>2.問題
當您嘗試依序按一下 tooinstall 閘道時，您會看到此錯誤**直接在這部電腦上安裝**hello Azure 入口網站中。

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>原因
Hello 機器上已安裝閘道。

#### <a name="resolution"></a>解決方案
解除安裝現有的閘道 hello hello 機器上，按一下 hello**直接在這部電腦上安裝**重新連結。

### <a name="3-problem"></a>3.問題
註冊新的閘道時，您可能會看到此錯誤。

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>原因
您可能會看到此訊息，其中一個 hello 下列原因：

* hello hello 閘道器金鑰格式無效。
* hello 閘道器金鑰已失效。
* 從 hello 入口網站已重新產生 hello 閘道器金鑰。  

#### <a name="resolution"></a>解決方案
請確認您是否使用 hello 正確的閘道金鑰從 hello 入口網站。 如有需要重新產生金鑰，並使用 hello 金鑰 tooregister hello 閘道。

### <a name="4-problem"></a>4.問題
您可能會看到下列錯誤訊息，當您註冊閘道的 hello。

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![金鑰的內容或格式無效](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>原因
hello 內容或 hello 輸入閘道器金鑰的格式不正確。 其中一個 hello 原因可以是您從 hello 入口網站複製 hello 索引鍵的一部分，或您使用了無效的金鑰。

#### <a name="resolution"></a>解決方案
產生閘道金鑰在 hello 入口網站，並使用 hello 複製按鈕 toocopy hello 整個索引鍵。 然後將它貼到此視窗 tooregister hello 閘道器中。

### <a name="5-problem"></a>5.問題
您可能會看到下列錯誤訊息，當您註冊閘道的 hello。

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![閘道金鑰無效或是空的](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>原因
已重新產生 hello 閘道器金鑰或 hello 閘道已刪除 hello Azure 入口網站中。 它也可會發生如果 hello 資料管理閘道器安裝程式不是最新。

#### <a name="resolution"></a>解決方案
檢查是否 hello 資料管理閘道器安裝程式 hello 最新版本，您可以在 hello Microsoft 找到最新版本的 hello[下載中心](https://go.microsoft.com/fwlink/p/?LinkId=271260)。

如果安裝程式目前 / 最新，而且閘道仍存在於入口網站，重新產生 hello Azure 入口網站中的 hello 閘道器金鑰和使用 hello 複製按鈕 toocopy hello 整個索引鍵，並再將它貼入此視窗 tooregister hello 閘道中。 否則，重新建立 hello 閘道，然後再重新啟動。

### <a name="6-problem"></a>6.問題
您可能會看到下列錯誤訊息，當您註冊閘道的 hello。

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![閘道金鑰無效或是空的](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>原因
因為 hello 閘道已刪除，或已重新產生 hello 相關聯的閘道金鑰，則可能會發生此錯誤。

#### <a name="resolution"></a>解決方案
如果 hello 閘道已刪除、 重新建立 hello hello 入口網站的閘道，請按一下**註冊**、 從 hello 入口網站複製 hello 金鑰、 貼上它，然後再次嘗試 tooregister hello 閘道。

如果 hello 閘道仍然存在，但已重新產生其金鑰，請使用 hello 新金鑰 tooregister hello 閘道。 如果您沒有 hello 金鑰，重新產生 hello 再次從 hello 入口網站的索引鍵。

### <a name="7-problem"></a>7.問題
當您註冊閘道器時，您可能需要 tooenter 路徑和密碼的憑證。

![指定憑證](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>原因
hello 閘道已在之前的其他電腦上註冊。 Hello 初始註冊期間的閘道，加密憑證已與 hello 閘道相關聯。 hello 憑證可以由 hello 閘道自我產生或 hello 使用者所提供。  此憑證是使用的 tooencrypt hello 資料存放區 （連結的服務） 的認證。  

![匯出憑證](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

當還原 hello 閘道在不同的主機電腦、 hello 註冊精靈會要求的這個憑證 toodecrypt 先前認證加密的與此憑證。  如果沒有此憑證，hello 新的閘道無法解密 hello 認證而且與此新的閘道相關聯的後續複製活動執行會失敗。  

#### <a name="resolution"></a>解決方案
如果您已經從原始閘道機器 hello 匯出 hello 認證憑證，使用 hello**匯出**按鈕 hello**設定**索引標籤中的資料管理閘道組態管理員，請使用 hello此憑證。

在復原閘道時，您無法略過此階段。 如果 hello 憑證遺失，您需要從 hello 入口網站的 toodelete hello 閘道，並重新建立新的閘道。  此外，更新所有的連結的服務的相關的 toohello 閘道重新輸入其認證。

### <a name="8-problem"></a>8.問題
您可能會看到下列錯誤訊息的 hello。

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>原因
當您的閘道時需要 HTTP proxy tooaccess 網際網路資源的環境中，就會發生此錯誤或 proxy 的驗證密碼已變更，但未據以更新您的閘道中。

#### <a name="resolution"></a>解決方案
遵循 hello hello 指示[Proxy server 考量](#proxy-server-considerations)這個區段，然後設定 proxy 設定與資料管理閘道組態管理員。

## <a name="gateway-is-online-with-limited-functionality"></a>閘道在線上但功能受限
### <a name="1-problem"></a>1.問題
您看到 hello hello 閘道狀態為線上，但功能有限。

#### <a name="cause"></a>原因
具有有限的功能，其中一個 hello 下列原因與線上查看 hello hello 閘道狀態：

* 閘道無法連接 toocloud 服務透過 Azure 服務匯流排。
* 雲端服務無法透過服務匯流排連線 toogateway。

當 hello 閘道在線上且最有限的功能時，您可能無法將能 toouse hello 資料 Factory 複製精靈 toocreate 資料管線來複製資料 tooor 從內部部署資料存放區。 因應措施，您可以在 hello 入口網站，Visual Studio 或 Azure PowerShell 中使用 Data Factory 編輯器。

#### <a name="resolution"></a>解決方案
此問題解決方式 (online 具有有限功能) 根據 hello 閘道無法連接 toohello 雲端服務或 hello 另一種方式。 hello 下列各節提供這些解決方案。

### <a name="2-problem"></a>2.問題
您會看到下列錯誤 hello。

`Error: Gateway cannot connect toocloud service through service bus`

![閘道無法連接 toocloud 服務](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>原因
閘道無法透過服務匯流排連線 toohello 雲端服務。

#### <a name="resolution"></a>解決方案
請遵循這些步驟 tooget hello 閘道上線：

1. 輸出規則上 hello 閘道器電腦與 hello 公司防火牆允許的 IP 位址。 您可以找到 hello Windows 事件記錄檔中的 IP 位址 (識別碼 = = 401): 已嘗試以禁止透過其存取權限 XX 方式進行 tooaccess 通訊端。XX。XX。XX:9350。
* Hello 閘道上設定 proxy 設定。 請參閱 hello [Proxy server 考量](#proxy-server-considerations)如需詳細資訊。
* 啟用輸出連接埠 5671 與 9350-9354 上 hello 閘道器電腦與 hello 公司防火牆在這兩個 hello Windows 防火牆。 請參閱 hello[連接埠和防火牆](#ports-and-firewall)如需詳細資訊。 此步驟為選用步驟，但基於效能考量，還是建議執行。

### <a name="3-problem"></a>3.問題
您會看到下列錯誤 hello。

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>原因
暫時性網路連線錯誤。

#### <a name="resolution"></a>解決方案
請遵循這些步驟 tooget hello 閘道上線：

1. 等候數分鐘，hello 錯誤消失時自動回復 hello 連線。
* 如果 hello 錯誤持續發生，請重新啟動 hello 閘道服務。

## <a name="failed-tooauthor-linked-service"></a>失敗的 tooauthor 連結服務
### <a name="problem"></a>問題
嘗試 toouse 認證管理員中新的連結服務的 hello 入口 tooinput 認證或更新現有的連結服務的認證時，您可能會看到這個錯誤。

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

當您看到此錯誤時，hello 設定 頁面的資料管理閘道組態管理員可能會看起來像下列螢幕擷取畫面的 hello。

![無法觸達資料庫](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>原因
hello SSL 憑證可能會遺失 hello 閘道機器上。 hello 閘道電腦無法載入 hello 目前使用憑證進行 SSL 加密。 您也可能會看到類似下列訊息的 toohello 的 hello 事件記錄檔中的錯誤訊息。

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>解決方案
請遵循這些步驟 toosolve hello 問題：

1. 啟動「資料管理閘道組態管理員」。
2. 切換 toohello**設定** 索引標籤。  
3. 按一下 hello**變更**按鈕 toochange hello SSL 憑證。

   ![變更憑證按鈕](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. 選取新的憑證，做為 hello SSL 憑證。 您可以使用您自己或任何組織所產生的任何 SSL 憑證。

   ![指定憑證](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>複製活動失敗
### <a name="problem"></a>問題
您可能會注意到 hello"UserErrorFailedToConnectToSqlserver 」 失敗之後設定 hello 入口網站中的管線之後。

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>原因
發生的原因各有不同，而緩和方式也隨之而異。

#### <a name="resolution"></a>解決方案
允許輸出 TCP 連線透過 hello 資料管理閘道用戶端上的連接埠 TCP/1433年連接 tooan SQL 資料庫之前。

如果 hello 目標資料庫是 Azure SQL database，請檢查 SQL Server 的防火牆設定 Azure 以及。

請參閱下列章節 tootest hello 連接 toohello 在內部部署資料存放區的 hello。

## <a name="data-store-connection-or-driver-related-errors"></a>資料存放區連線或驅動程式相關錯誤
如果您看到資料存放區連接或驅動程式相關的錯誤，完成下列步驟的 hello:

1. Hello 閘道機器上啟動資料管理閘道組態管理員。
2. 切換 toohello**診斷** 索引標籤。
3. 在**測試連接**，新增 hello 閘道群組值。
4. 按一下**測試**toosee，如果您可以連接 toohello 內部部署資料來源從 hello 閘道機器使用 hello 連接資訊和認證。 如果之後安裝的驅動程式，仍失敗 hello 測試連接，重新啟動 hello 閘道它 toopick 向上 hello 最新變更。

![在 [診斷] 索引標籤中的測試連接](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>閘道記錄檔
### <a name="send-gateway-logs-toomicrosoft"></a>傳送閘道記錄檔 tooMicrosoft
當您連絡 Microsoft 支援服務 tooget 說明閘道的問題進行疑難排解時，可能會要求您 tooshare 您閘道記錄檔。 Hello 版的 hello 閘道，您可以共用兩個按鈕按一下在資料管理閘道組態管理員需要的閘道記錄檔。    

1. 切換 toohello**診斷**在資料管理閘道組態管理員 索引標籤。

    ![資料管理閘道診斷索引標籤](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. 按一下**傳送記錄檔**toosee hello 下列對話方塊。

    ![資料管理閘道傳送記錄檔](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. （選擇性）按一下**檢視記錄檔**tooreview 記錄 hello 事件檢視器中。
4. （選擇性）按一下**隱私權**tooreview Microsoft web services 隱私權聲明。
5. 當您滿意 tooupload 有關為何時，按一下 **傳送記錄檔**tooactually 從 hello 過去七天 tooMicrosoft 疑難排解傳送嗨記錄檔。 Hello 下列螢幕擷取畫面所示，您應該看到 hello hello 傳送記錄檔作業狀態。

    ![資料管理閘道傳送記錄檔狀態](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Hello 作業已完成之後，您會看到一個對話方塊 hello 下列螢幕擷取畫面所示。

    ![資料管理閘道傳送記錄檔狀態](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. 儲存 hello**報表識別碼**及共用向 Microsoft 支援。 使用的 toolocate hello 閘道記錄檔取得疑難排解您上傳 hello 報表 ID。  hello 報表識別碼也會儲存在 hello 事件檢視器。  您可以藉由查看 hello 事件識別碼 」 25"，找到它，並檢查 hello 日期和時間。

    ![資料管理閘道傳送記錄檔報告識別碼](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>在閘道主機電腦上封存閘道記錄檔
在某些情況下，您會有閘道問題但無法直接共用閘道記錄檔︰

* 手動安裝 hello 閘道，並註冊 hello 閘道。
* 您可以嘗試 tooregister hello 閘道使用重新產生金鑰在資料管理閘道組態管理員。
* 您嘗試 toosend 記錄檔，而且 hello 閘道器主機服務無法連線。

對於這些案例，您可以將閘道記錄檔儲存為 zip 檔案，並在連絡 Microsoft 支援服務時共用。 比方說，如果您註冊為 hello 閘道時，收到錯誤，顯示 hello 下列螢幕擷取畫面。   

![資料管理閘道註冊錯誤](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

按一下 hello**封存閘道記錄檔**連結 tooarchive 和儲存記錄檔，然後向 Microsoft 支援共用 hello zip 檔案。

![資料管理閘道封存記錄檔](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>找出閘道記錄檔
您可以在 hello Windows 事件記錄檔中找到詳細的閘道記錄檔資訊。

1. 啟動 Windows **事件檢視器**。
2. 找出記錄檔中 hello **Application and Services Logs** > **資料管理閘道器**資料夾。

 當您正在將閘道器相關的問題進行疑難排解時，查看 hello 事件檢視器中的錯誤層級事件。

![資料管理閘道事件檢視器中的記錄檔](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
