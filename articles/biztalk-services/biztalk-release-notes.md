---
title: "Azure BizTalk 服務的 aaaRelease 注意事項 |Microsoft 文件"
description: "列出 hello Azure BizTalk 服務的已知問題"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Azure BizTalk 服務的版本資訊

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

hello hello Microsoft Azure BizTalk 服務的版本資訊包含 hello 這個版本的已知問題。

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>在 BizTalk 服務的 hello 年 11 月更新中最新消息
* Hello BizTalk 服務入口網站中，可以啟用靜態加密。 請參閱 [在 BizTalk 服務入口網站中啟用靜態加密](https://msdn.microsoft.com/library/azure/dn874052.aspx)。

## <a name="update-history"></a>更新歷程記錄
### <a name="october-update"></a>10 月更新
* 支援組織帳戶：  
  * **情節**：您使用 Microsoft 帳戶註冊了 BizTalk 服務部署 (例如 user@live.com)。 在此案例中，只有 Microsoft 帳戶，使用者可以管理 hello BizTalk 服務使用 hello BizTalk 服務入口網站。 無法使用組織帳戶。  
  * **情節**：您使用 Azure Active Directory 中的組織帳戶註冊了 BizTalk 服務部署 (例如 user@fabrikam.com 或 user@contoso.com)。 在此案例中，只有相同組織可以管理的 hello 內的 Azure Active Directory 使用者 hello BizTalk 服務使用 hello BizTalk 服務入口網站。 無法使用 Microsoft 帳戶。  
* 當您建立 BizTalk 服務在 hello Azure 傳統入口網站中時，您會自動註冊 hello BizTalk 服務入口網站中。
  * **案例**： 您登入 hello Azure 傳統入口網站建立 BizTalk 服務，然後選取**管理**hello 第一次。 Hello BizTalk 服務入口網站開啟時，BizTalk 服務的 hello 自動註冊，並可供您的部署。  
    請參閱[註冊和更新 BizTalk 服務部署的 hello BizTalk 服務入口網站](https://msdn.microsoft.com/library/azure/hh689837.aspx)。  

### <a name="august-14-update"></a>8 月 14 日更新
* 合約與橋接器分開處理 – 交易夥伴協議和橋接器，現在分離 hello BizTalk 服務入口網站中。 您現在建立個別的合約和橋接器，並在執行階段橋接器解決 tooan hello EDI 訊息中的 hello 值為基礎的協議。 請參閱[在 Azure BizTalk 服務中建立合約](https://msdn.microsoft.com/library/azure/hh689908.aspx)、[使用 BizTalk 服務入口網站建立 EDI 橋接器](https://msdn.microsoft.com/library/azure/dn793986.aspx)、[使用 BizTalk 服務入口網站建立 AS2 橋接器](https://msdn.microsoft.com/library/azure/dn793993.aspx)和[橋接器在執行階段如何解析合約？](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* 已停用協議的 hello 選項 toocreate 範本。  
* Hello 傳送端協議中，您現在可以指定不同的分隔符號集，每個結構描述。 此設定是在傳送端合約的通訊協定設定下指定。 如需詳細資訊，請參閱[在 Azure BizTalk 服務中建立 X12 合約](https://msdn.microsoft.com/library/azure/hh689847.aspx)和[在 Azure BizTalk 服務中建立 EDIFACT合約](https://msdn.microsoft.com/library/azure/dn606267.aspx)。 也會有兩個新實體新增 toohello TPM OM API hello 相同的目的。 請參閱 [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) 和 [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx)。  
* 現在支援標準 XSD 建構，包括衍生類型。 請參閱[在您的對應中使用標準 XSD 建構](https://msdn.microsoft.com/library/azure/dn793987.aspx)和[在對應案例和範例中使用衍生類型](https://msdn.microsoft.com/library/azure/dn793997.aspx)。  
* AS2 支援用於訊息簽署的新 MIC 演算法，以及新的加密演算法。 請參閱 [在 Azure BizTalk 服務中建立 AS2合約](https://msdn.microsoft.com/library/azure/hh689890.aspx)。  
  ## <a name="know-issues"></a>已知問題

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>BizTalk 服務入口網站更新之後的連線能力問題
  如果您擁有的 hello 升級 BizTalk 服務時，BizTalk 服務入口網站開啟 tooroll 中的變更 toohello 服務，您可能會面臨 hello BizTalk 服務入口網站的連線問題。  
  因應措施，您可能會重新啟動 hello 瀏覽器、 刪除 hello 瀏覽器快取，或在私用模式中啟動 hello 入口網站。  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Visual Studio IDE 找不到 hello 成品，如果您按一下錯誤或警告，BizTalk 服務專案中
安裝 Visual Studio 2012 Update 3 RC 1 的 hello toofix hello 問題。  

### <a name="custom-binding-project-reference"></a>自訂繫結專案參考
請考慮下列情況的 BizTalk 服務專案，Visual Studio 方案中的 hello:  

* 在 hello 相同的 Visual Studio 方案，所以在 BizTalk 服務專案和自訂繫結專案。 hello BizTalk 服務專案有參考 toothis 自訂繫結專案檔。
* hello BizTalk 服務專案有參考 tooa 自訂繫結/行為 DLL。

成功，您建置 hello Visual Studio 中的方案。 然後，'Rebuild' 或者 '清除' hello 解決方案。 在這之後，當您重建或清除一次，hello 之後會發生錯誤：  
  無法 toocopy 檔案<Path tooDLL>too"bin\Debug\FileName.dll"。 hello 程序無法存取 hello 檔案 'bin\Debug\FileName.dll'，因為它正由另一個處理序。  

#### <a name="workaround"></a>因應措施
* 如果[Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305)已安裝，您有下列兩個選項的 hello:
  
  * 重新啟動 Visual Studio，或
  * 重新啟動 hello 方案。 然後，執行僅建置 hello 方案。  
* 如果[Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305)是未安裝，請開啟 [工作管理員，按一下 hello 處理程序] 索引標籤、 按一下 hello MSBuild.exe 處理程序，然後按一下hello] 按鈕結束處理程序。  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>路由 tooBasicHttpRelay 端點時，不支援從橋接器和 BizTalk 服務入口網站的不可列印字元升級為 HTTP 標頭
如果您使用不可列印字元做為升級屬性的一部分的訊息，這些訊息不能使用 hello BasicHttpRelay 繫結的路由的 toorelay 目的地。 此外，hello 升級會提供追蹤的一部分是 URL 編碼的 blob 和目的地的未編碼的屬性。  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>即使 hello 傳送非同步 MDN 選項為未選取狀態以非同步方式傳送 MDN
如果您選取 hello 考量此案例：**傳送非同步 MDN**核取方塊並指定 URL toosend hello 非同步 MDN，然後取消核取 hello**傳送非同步 MDN**核取方塊，hello MDN 仍然是即使未選取 hello 選項 toosend 非同步 Mdn 傳送的 toohello 指定的 URL。  
因應措施，您必須清除 hello 指定 URL，再取消勾選 hello**傳送非同步 MDN**核取方塊，然後部署 hello AS2 協議。  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>超出有效交換原因空的訊息傳送的 toobe toohello 空白字元暫停端點
如果 IEA 區段的空白字元，hello 解譯器會將它視為目前交換的結尾，並會查看 hello 下一組的空白字元視為下一個訊息。 由於這不是有效的交換，您可能會發現一個成功的訊息會傳送 toohello 路由目的地，以及一個空的訊息傳送嗨暫停端點。  

### <a name="tracking-in-biztalk-services-portal"></a>在 BizTalk 服務入口網站中追蹤
追蹤事件的擷取 toohello EDI 訊息處理和任何相互關聯。 如果訊息 hello 通訊協定階段之外失敗，則追蹤會顯示為成功。 在此情況下，請參閱 toohello 記錄檔區段底下 hello**詳細資料**中的資料行**追蹤**取得錯誤詳細資料。
hello X12 接收和傳送設定 ([建立 x12 協議中 Azure BizTalk 服務](https://msdn.microsoft.com/library/azure/hh689847.aspx)) 提供 hello 通訊協定階段的相關資訊。  

### <a name="update-agreement"></a>更新合約
hello BizTalk 服務入口網站可讓您 toomodify hello 身分識別的辨識符號設定協議時。 這會導致屬性不一致。 比方說，是使用 zz: 1234567 和 zz: 7654321 hello 限定詞協議。 在 hello BizTalk 服務入口網站設定檔設定中，您可以變更 zz: 1234567 toobe 01:ChangedValue。 開啟 hello 協議，而非 zz: 1234567 01:ChangedValue 顯示。
toomodify hello 限定詞身分識別，刪除 hello 協議中，更新**識別**在 hello 夥伴設定檔，然後重新建立 hello 協議。  

> AZURE.WARNING 此行為影響 X12 和 AS2。  
> 
> 

### <a name="as2-attachments"></a>AS2 附件
傳送和接收時不支援 AS2 訊息的附件。 具體來說，附件會以無訊息模式忽略，而且 hello 訊息本文會當做一般的 AS2 訊息處理。  

### <a name="resources-remembering-path"></a>資源：記住路徑
加入時**資源**，hello 對話視窗可能不記得 hello 先前使用的路徑 tooadd 資源。 tooremember hello 先前用過的路徑，再試一次 hello BizTalk 服務入口網站將網站加入太**信任的網站**Internet Explorer 中。  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>如果您要重新命名橋接器與關閉 hello 專案的 hello 實體名稱而不儲存變更，重新開啟 hello 實體產生錯誤
請考慮 hello 順序中的案例：  

* 新增橋接器 （例如 XML 單向橋接器） tooa BizTalk 服務專案  
* 重新命名 hello 橋接器，藉由指定 hello 實體名稱屬性的值。 這會重新命名 hello 相關聯的.bridgeconfig 檔案 hello 您指定的名稱。  
* 關閉 hello.bcs 檔案 （關閉 Visual Studio 中的 hello 索引標籤） 而不儲存 hello 變更。  
* 從 [方案總管] 中的 hello 再次開啟 hello.bcs 檔。  
  您會注意到 hello 相關聯的.bridgeconfig 檔案具有您指定的 hello 新名稱，而 hello hello 設計介面上的實體名稱還是 hello 舊名稱。 如果您按兩下 hello 橋接器元件嘗試 tooopen hello 橋接器組態，您會得到下列錯誤 hello:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid 執行此案例中，請確定您重新命名 BizTalk 服務專案中的 hello 實體之後儲存變更。  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>即使已經從 Visual Studio 專案中排除構件，BizTalk 服務專案仍會成功建置
請考慮案例，您新增 BizTalk 服務專案的成品 （例如，XSD 檔案） tooa、 hello 橋接器組態中包含該成品，（比方說，藉由指定它做為要求訊息類型），而且再將它從 hello Visual Studio 專案中排除。 在這種情況下，建置 hello 專案將不會發生任何錯誤，只要刪除 hello 成品磁碟上還有可用 hello hello 在其中包含 hello Visual Studio 專案中的相同位置。
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>hello BizTalk 服務專案將不會檢查結構描述可用性設定 hello 橋接器時
在 BizTalk 服務專案中，如果加入 toohello 專案的結構描述匯入另一個結構描述，hello BizTalk 服務專案不會檢查 toohello 專案時，是否要加入 hello 匯入結構描述。 如果您嘗試 toobuild 這類專案，則不會收到任何建置錯誤。
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>XML 要求-回覆橋接器的 hello 回應訊息永遠是 utf-8 字元集
此版本中，從 XML 要求-回覆橋接器 hello 回應訊息的 hello charset 一定會設定 tooUTF 8。
  
### <a name="user-defined-datatypes"></a>使用者定義的資料類型
hello BizTalk Adapter 服務功能中的 hello BizTalk Adapter Pack 配接器可以利用使用者定義的資料類型的配接器作業。
當使用使用者定義的資料類型時，複製 hello 檔案 (.dll) toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ 或裝載 hello BizTalk 配接器服務的 hello 伺服器上的 toohello 全域組件快取 (GAC)。 否則，hello 用戶端上可能會發生下列錯誤 hello:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> 它是建議的 toouse GACUtil.exe tooinstall hello 全域組件快取檔案。 GACUtil.exe 文件如何 toouse 此工具並 hello Visual Studio 命令列選項。  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>重新啟動 hello BizTalk 配接器服務網站
安裝 hello **BizTalk 配接器服務執行階段*** 建立 hello **BizTalk Adapter 服務**包含 hello 的 IIS 網站**BAService**應用程式。 **BAService**應用程式會在內部使用轉送繫結 tooextend hello 觸達的內部部署服務端點 toohello 雲端。 裝載服務內部部署，hello 對應的轉送端點將註冊 hello 服務匯流排上 hello 內部部署服務啟動時才。  

如果您停止並啟動應用程式，則不會採用 hello 組態自動啟動應用程式。 因此**BAService**已停止，您必須一律重新啟動 hello **BizTalk Adapter 服務**改為 web 站台。 無法啟動或停止 hello **BAService**應用程式。

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>LOB 元件的位址和實體名稱中不應該使用特殊字元
您不應該在 LOB 元件的位址和實體名稱中使用特殊字元。 如果您這樣做，您會部署 hello BizTalk 服務專案時收到錯誤。 針對特定的字元，例如 '%'，hello BizTalk Adapter 服務網站可能會進入停止狀態，因此您將必須 toomanually 啟動它。

### <a name="test-map-with-get-context-property"></a>使用取得內容屬性來測試對應
如果轉換包含**取得內容屬性**對應作業，**測試對應**將會失敗。 暫時的解決方法，取代 hello**取得內容屬性**字串串連對應 」 作業含有虛擬資料 」 的 「 對應 」 作業。 這將會填入 hello 目標結構描述，並讓您測試其他轉換功能。

### <a name="test-map-property-does-not-display"></a>測試對應屬性未顯示
hello**測試對應**屬性不會顯示在 Visual Studio。 這種情形 hello**屬性**視窗和 hello**方案總管 中**視窗未同時停駐。 tooresolve，停駐 hello**屬性**和 hello**方案總管 中**windows。  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>日期時間重新格式化下拉式清單變成灰色
加入日期時間重新格式化對應 」 作業時 toohello 設計介面，並設定 hello 下拉式清單可能會變成灰色的格式。這種情況 hello 電腦顯示器設**中-125%**或**大-150%**。 tooresolve，將 hello 顯示器太**小-100%（預設值）**使用 hello 執行下列步驟：  

1. 開啟 hello**控制台**按一下**外觀及個人化**。
2. 按一下 [顯示] 。
3. 按一下 [小 – 100% (預設)]，然後按一下 [套用]。

hello**格式**下拉式清單應該現在如預期般運作。

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>在 hello BizTalk 服務入口網站中的協議重複
請考慮下列案例中的 hello:

1. 建立使用 hello 交易夥伴管理 OM API 協議。
2. 在兩個不同的索引標籤中的 hello BizTalk 服務入口網站中，開啟 hello 協議。
3. 部署這兩個 [hello] 索引標籤的 hello 協議。
4. 如此一來，這兩個 hello 協議取得部署，導致 hello BizTalk 服務入口網站中的重複項目

**因應措施**。 開啟其中一個 hello 重複協議中 hello BizTalk 服務入口網站，並解除部署。  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>橋接器不會使用更新的憑證的憑證已更新 hello 成品存放區中即使
請考慮下列案例的 hello:  

**案例 1： 使用指紋型憑證來保護從橋接器 tooa 服務端點的訊息傳輸**  
假設您在 BizTalk 服務專案中使用指紋型憑證。 您可以更新 hello BizTalk 服務入口網站中的 hello 憑證以 hello 相同名稱但不同指紋，但是未據以更新 hello BizTalk 服務專案。 在這類案例中，因為 hello 較舊的憑證資料可能仍會出現在 hello 通道快取 hello 橋接器時，可能會繼續 tooprocess hello 訊息。 隨後，訊息處理就失敗。  

**因應措施**: hello BizTalk 服務專案中的 hello 憑證更新和重新部署 hello 專案。  

**案例 2： 使用名稱型行為 tooidentify 憑證來進行保護從橋接器 tooa 服務端點的訊息傳輸的安全**

假設您使用名稱型行為 tooidentify 憑證 BizTalk 服務專案中。 更新 hello BizTalk 服務入口網站中的 hello 憑證，但是未據以更新 hello BizTalk 服務專案。 在這類案例中，因為 hello 較舊的憑證資料可能仍會出現在 hello 通道快取 hello 橋接器時，可能會繼續 tooprocess hello 訊息。 隨後，訊息處理就失敗。  

**因應措施**: hello BizTalk 服務專案中的 hello 憑證更新和重新部署 hello 專案。  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>即使 hello SQL 資料庫是離線，橋接器還是繼續 tooprocess 訊息
hello BizTalk 服務橋接器會繼續 tooprocess 訊息的一段時間，即使 hello Microsoft Azure SQL Database （其中儲存 hello 執行如部署的成品和管線資訊），已離線。 這是因為 BizTalk 服務會使用快取的 hello 成品和橋接器組態。
如果您不想 hello 橋接器 tooprocess 任何訊息 hello SQL 資料庫離線時，您可以使用 hello BizTalk Services PowerShell 指令程式 toostop 或暫停 hello BizTalk 服務。 請參閱[Azure BizTalk 服務管理範例](http://go.microsoft.com/fwlink/p/?LinkID=329019)hello Windows PowerShell cmdlet toomanage 作業。  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>橋接器之自訂程式碼元件內讀取 hello XML 訊息會包含額外的 BOM 字元
假設您想要 tooread 橋接器之自訂程式碼內 XML 訊息。 如果您使用.NET API System.Text.Encoding.UTF8.GetString(bytes) hello 額外的 BOM 字元併入 hello hello hello 訊息開頭處的輸出。 因此，如果您不想 hello 輸出 tooinclude hello 額外的 BOM 字元，您必須使用```System.IO.StreamReader().ReadToEnd()```。

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>傳送訊息使用 WCF tooa 橋接器未調整
使用 WCF tooa 橋接器未調整傳送訊息。 如果您想要可調整的用戶端，則應該改為使用 HttpWebRequest。

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>升級從 BizTalk 服務預覽版 tooGeneral (GA) 上市後的升級： 語彙基元提供者錯誤
與作用中批次之間有 EDI 或 AS2 合約。 從預覽 tooGA 升級 hello BizTalk 服務時，可能會發生下列 hello:

* 錯誤： hello 權杖提供者無法 tooprovide 安全性權杖。 傳回訊息的權杖提供者： 無法解析 hello 遠端名稱。
* 批次工作已取消。

**因應措施**: hello BizTalk 服務更新的 tooGeneral (GA) 上市後，重新部署的 hello 協議。  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>升級： 工具箱會顯示 hello 舊的橋接器圖示之後升級 hello BizTalk 服務 SDK
升級舊版的 BizTalk 服務 SDK，具有代表 hello 橋接器的舊圖示，hello 之後 hello [工具箱] 會繼續 hello 橋接器的 tooshow hello 舊圖示。 不過，如果您新增橋接器 tooBizTalk 服務專案設計工具介面，hello 介面會顯示 hello 新圖示。  

**因應措施**。 正在刪除 hello 下的.tbd 檔案，可以暫時解決此問題<system drive>: \Users\<使用者 > \AppData\Local\Microsoft\VisualStudio\11.0。  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>升級： 從預覽 tooGA BizTalk 入口網站更新可能會顯示錯誤，指出該 hello EDI 功能無法使用
如果您已登入 hello BizTalk 服務入口網站，從預覽 tooGA 升級 hello BizTalk 服務時，您可能會收到下列錯誤 hello 入口網站上的 hello:  

這個版本的 Microsoft Azure BizTalk 服務中無法使用此功能。 toouse 這些功能切換 tooan 適當的版本。  

**解析**： 出 hello 入口網站、 關閉及開啟 hello 瀏覽器，然後登入 hello 入口網站中的記錄檔。  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>升級： 新的追蹤資料則不會顯示在 BizTalk 服務升級的 tooGA 之後
假設您在 BizTalk 服務預覽版訂用帳戶上已部署 XML 橋接器。 Toohello 橋接器傳送訊息，且可在 hello BizTalk 服務入口網站上取得 hello 對應追蹤資料。 現在，如果 hello BizTalk 服務入口網站和 BizTalk 服務執行階段的位元升級的 tooGA，而且您傳送訊息 toohello 先前部署相同橋接器端點，hello 追蹤資料則不會顯示在升級後所傳送的訊息。  

### <a name="pipelines-versus-bridges"></a>管線與橋接器
整份文件，會交換使用 hello 詞彙 「 管線 」 和 「 橋接器 」。 同時基本上都表示 hello 相同的作業，也就是，部署 BizTalk 服務在訊息處理單元。  

### <a name="concepts"></a>概念
[BizTalk 服務](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

