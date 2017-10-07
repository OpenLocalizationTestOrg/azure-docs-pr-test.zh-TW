---
title: "在本機以 hello Azure Cosmos DB 模擬器 aaaDevelop |Microsoft 文件"
description: "使用 hello Azure Cosmos DB 模擬器，您可以開發及測試您的應用程式在本機，而不需要建立 Azure 訂用帳戶。"
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 模擬器"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>使用本機開發及測試 hello Azure Cosmos DB 模擬器

<table>
<tr>
  <td><strong>二進位檔</strong></td>
  <td>[下載 MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker Hub](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Docker 來源</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
hello Azure Cosmos DB 模擬器提供模擬 hello Azure Cosmos 資料庫服務，供開發應用程式的本機環境。 使用 hello Azure Cosmos DB 模擬器，您可以開發及測試應用程式在本機，而不需要建立 Azure 訂用帳戶，或支付任何費用。 當您滿意 hello Azure Cosmos DB 模擬器中您的應用程式運作時，您可以切換 toousing hello 雲端中的 Azure Cosmos DB 帳戶。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 安裝模擬器 hello
> * Docker for Windows 上執行 hello 模擬器
> * 驗證要求
> * 使用 hello 模擬器中的 hello 資料總管
> * 匯出 SSL 憑證
> * 從 hello 命令列呼叫 hello 模擬器
> * 收集追蹤檔案

我們建議您藉由監看下列影片 Kirill Gavrylyuk 顯示以 hello Azure Cosmos DB 模擬器 tooget 的啟動方式 hello 開始使用。 請注意，hello 視訊參照 toohello 模擬器做 hello DocumentDB 模擬器中，但 hello 工具本身已重新命名後點選 hello 視訊 hello Azure Cosmos DB 模擬器。 Hello 視訊中的所有資訊都都仍正確 hello Azure Cosmos DB 模擬器。 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Hello 模擬器的運作方式
hello Azure Cosmos DB 模擬器提供高逼真度的模擬 hello Azure Cosmos 資料庫服務。 它支援與 Azure Cosmos DB 完全相同的功能，包括支援建立和查詢 JSON 文件、佈建和擴充集合，以及執行預存程序和觸發程序。 您可以開發和測試應用程式使用 hello Azure Cosmos DB 模擬器，及藉由只變更 Azure Cosmos DB toohello 連接端點的單一組態部署全域大規模 tooAzure。

當我們建立 hello 實際 Azure Cosmos DB 服務的高逼真度本機模擬時，hello Azure Cosmos DB 模擬器 hello 實作以不同於所 hello 服務時。 比方說，hello Azure Cosmos DB 模擬器會使用標準的作業系統元件，例如 hello 本機檔案系統的持續性和連線的 HTTPS 通訊協定堆疊。 這表示，某些功能依賴 Azure 基礎結構，例如全域複寫，讀取/寫入，以及可微調的一致性層級的單一位數毫秒延遲，無法透過 hello Azure Cosmos DB 模擬器。

> [!NOTE]
> 在此時間 hello 資料總管在 hello 模擬器只支援 hello 建立 DocumentDB API 集合和 MongoDB 集合。 hello 模擬器中的 hello 資料總管目前不支援 hello 建立資料表和圖形。 

## <a name="system-requirements"></a>系統需求
hello Azure Cosmos DB 模擬器有下列硬體和軟體需求的 hello:

* 軟體需求
  * Windows Server 2012 R2、Windows Server 2016 或 Windows 10
*   最低硬體需求
  * 2 GB RAM
  * 10 GB 可用硬碟空間

## <a name="installation"></a>安裝
您可以從下載並安裝 hello Azure Cosmos DB 模擬器 hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator)。 

> [!NOTE]
> tooinstall，設定和執行 hello Azure Cosmos DB 模擬器，您必須擁有系統管理權限 hello 電腦上。

## <a name="running-on-docker-for-windows"></a>在 Docker for Windows 上執行

可以執行 Docker for Windows hello Azure Cosmos DB 模擬器。 hello 模擬器無法在上 Docker for Oracle Linux。

一旦[Docker for Windows](https://www.docker.com/docker-windows)安裝，您可以拉 hello 模擬器映像從 Docker Hub 藉由執行下列命令，從您喜愛的 shell hello (cmd.exe，PowerShell 等。)。

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
toostart hello 映像，執行下列命令的 hello。

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

hello 回應看起來類似 toohello 下列：

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Hello 模擬器已啟動一次關機 hello 模擬器的容器，請關閉 hello 互動式殼層。

在您的用戶端使用 hello 端點和從 hello 回應中的主要金鑰和 hello SSL 憑證匯入到您的主機。 請勿 hello tooimport hello SSL 憑證，系統管理員命令提示字元中的下列：

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>啟動模擬器 hello

toostart hello Azure Cosmos DB 模擬器中，選取 hello [開始] 按鈕或按 hello Windows 鍵。 開始輸入**Azure Cosmos DB 模擬器**，和選取 hello hello 清單中的應用程式的模擬器。 

![選取 hello 開始按鈕或按 hello Windows 鍵，開始輸入 * * Azure Cosmos DB 模擬器 * *，和從 hello 的應用程式的清單選取 hello 模擬器](./media/local-emulator/database-local-emulator-start.png)

當 hello 模擬器正在執行時，您會看到 hello Windows 工作列通知區域中的圖示。 ![Azure Cosmos DB 本機模擬器的工作列通知](./media/local-emulator/database-local-emulator-taskbar.png)

hello Azure Cosmos DB 模擬器預設會 hello 本機電腦 ("localhost") 上接聽連接埠 8081 上執行。

hello Cosmos DB 安裝 Azure 模擬器的預設 toohello`C:\Program Files\Azure Cosmos DB Emulator`目錄。 您也可以啟動並停止從命令列 hello hello 模擬器。 如需詳細資訊，請參閱[命令列工具參考](#command-line)。

## <a name="start-data-explorer"></a>啟動資料總管

Hello Azure Cosmos DB 模擬器啟動時就會自動開啟 hello Azure Cosmos DB Data 總管，瀏覽器中。 hello 位址將會顯示為[https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)。 如果您關閉 hello 總管 中，而且想要 toore 開啟它之後，您可以在您的瀏覽器中開啟 hello URL 或啟動從 hello Azure Cosmos DB 模擬器在 hello Windows 系統匣圖示，如下所示。

![Azure Cosmos DB 本機模擬器的資料總管啟動程式](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>檢查更新
資料總管會表示是否有新的更新可供下載。 

> [!NOTE]
> 建立在 hello Azure Cosmos DB 模擬器的其中一個版本的資料不保證 toobe 存取時使用不同版本。 如果您需要 toopersist 資料供 hello 長期，建議您在 Azure Cosmos DB 帳戶，而非 hello Azure Cosmos DB 模擬器中儲存該資料。 

## <a name="authenticating-requests"></a>驗證要求
就像 Azure Cosmos DB hello 雲端中與您進行 hello Azure Cosmos DB 模擬器針對每個要求必須進行驗證。 hello Azure Cosmos DB 模擬器主要金鑰驗證支援單一固定的帳戶及已知的驗證金鑰。 此帳戶與金鑰是 hello 僅允許以 hello Azure Cosmos DB 模擬器使用的認證。 如下：

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> hello 主要金鑰受到 hello Azure Cosmos DB 模擬器僅供 hello 模擬器只能搭配使用。 您無法使用您的生產 Azure Cosmos DB 帳戶及金鑰以 hello Azure Cosmos DB 模擬器。 

> [!NOTE] 
> 如果您已經啟動 hello 模擬器以 hello /Key 選項，然後使用 hello 產生金鑰，而不是"C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

此外，就像 hello Azure Cosmos 資料庫服務，hello Azure Cosmos DB 模擬器僅支援安全通訊透過 SSL。

## <a name="running-hello-emulator-on-a-local-network"></a>本機網路上執行 hello 模擬器

您可以執行 hello 模擬器在本機網路上。 tooenable 網路存取，指定在 hello hello /AllowNetworkAccess 選項[命令列](#command-line-syntax)，這也會要求您指定 /Key = key_string 或 /KeyFile = file_name。 您可以使用 /GenKeyFile = file_name toogenerate 檔案使用預先隨機金鑰。  然後您可以傳遞該太/KeyFile = file_name 或 /Key = contents_of_file。

第一個階段 hello 使用者 hello tooenable 的網路存取權應該關閉 hello 模擬器，然後刪除 hello 模擬器的資料目錄 (C:\Users\user_name\AppData\Local\CosmosDBEmulator)。

## <a name="developing-with-hello-emulator"></a>使用 hello 模擬器進行開發
一旦您擁有 hello 桌面上執行的 Azure Cosmos DB 模擬器，您可以使用任何支援[Azure Cosmos DB SDK](documentdb-sdk-dotnet.md)或 hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract 以 hello 模擬器。 hello Azure Cosmos DB 模擬器也包含內建的資料檔案總管，可讓您建立集合中的 hello DocumentDB 和 MongoDB Api，以及檢視和編輯文件，而不需要撰寫任何程式碼。   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

如果您使用[Azure Cosmos DB 通訊協定 support for MongoDB。](mongodb-introduction.md)，請使用下列連接字串 hello:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

您可以使用現有的工具，像是[Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB 模擬器。 您也可以移轉 hello Azure Cosmos DB 模擬器與使用 hello hello Azure Cosmos DB 服務之間的資料[Azure Cosmos DB 的資料移轉工具](https://github.com/azure/azure-documentdb-datamigrationtool)。

> [!NOTE] 
> 如果您已經啟動 hello 模擬器以 hello /Key 選項，然後使用 hello 產生金鑰，而不是"C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

依預設，使用 hello Azure Cosmos DB 模擬器中，您可以建立 too25 單一分割區集合或 1 的資料分割的集合。 如需有關如何變更此值的詳細資訊，請參閱[設定 hello PartitionCount 值](#set-partitioncount)。

## <a name="export-hello-ssl-certificate"></a>匯出 hello SSL 憑證

.NET 語言和執行階段使用 hello Windows 憑證存放區 toosecurely toohello Azure Cosmos DB 本機模擬器的連接。 其他語言則有自己管理和使用憑證的方法。 Java 使用自己的[憑證存放區](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)，而 Python 使用[通訊端包裝函式](https://docs.python.org/2/library/ssl.html)。

在訂單 tooobtain 與語言和執行階段無法與整合 hello Windows 憑證存放區與您的憑證 toouse 需要 tooexport 使用 hello Windows 憑證管理員。 您可以開始執行 certlm.msc 或依照中的 hello 逐步解說指示[匯出 hello Azure Cosmos DB 模擬器憑證](./local-emulator-export-ssl-certificates.md)。 一旦 hello 憑證管理員正常執行，如下所示，則開啟 hello 個人憑證及匯出 hello hello 易記名稱 」 DocumentDBEmulatorCertificate"憑證為 base-64 編碼 X.509 (.cer) 檔案。

![Azure Cosmos DB 本機模擬器的 SSL 憑證](./media/local-emulator/database-local-emulator-ssl_certificate.png)

hello X.509 憑證可以匯入 hello Java 憑證存放區中的 hello 指示[加入 Java CA 憑證存放區的憑證 toohello](https://docs.microsoft.com/azure/java-add-certificate-ca-store)。 一旦 hello 憑證匯入 hello 憑證存放區，則 Java 和 MongoDB 應用程式將會無法 tooconnect toohello Azure Cosmos DB 模擬器。

從 Python 和 Node.js Sdk 連接 toohello 模擬器，會停用 SSL 驗證。

## <a id="command-line"></a>命令列工具參考
從 hello 安裝位置，您可以使用 hello 命令列 toostart 和停止 hello 模擬器、 設定選項，並執行其他作業。

### <a name="command-line-syntax"></a>命令列語法

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

tooview hello 選項清單，型別`CosmosDB.Emulator.exe /?`hello 的命令提示字元。

<table>
<tr>
  <td><strong>選項</strong></td>
  <td><strong>說明</strong></td>
  <td><strong>命令</strong></td>
  <td><strong>引數</strong></td>
</tr>
<tr>
  <td>[無引數]</td>
  <td>啟動 hello Azure Cosmos DB 模擬器使用預設設定。</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[說明]</td>
  <td>顯示 hello 清單支援命令列引數。</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>關閉 hello Azure Cosmos DB 模擬器。</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>資料路徑</td>
  <td>指定在哪個 toostore 資料檔案中的 hello 路徑。 預設值為 %LocalAppdata%\CosmosDBEmulator。</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt;︰可存取的路徑</td>
</tr>
<tr>
  <td>Port</td>
  <td>指定 hello 連接埠號碼 toouse hello 模擬器。  預設值為 8081。</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;port&gt;</td>
  <td>&lt;port&gt;︰單一連接埠號碼</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>指定 hello 連接埠號碼 toouse MongoDB 相容性應用程式開發介面。 預設值為 10255。</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;︰單一連接埠號碼</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>指定直接連線的 hello 連接埠 toouse。 預設值為 10251、10252、10253、10254。</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;︰以逗號分隔的 4 個連接埠清單</td>
</tr>
<tr>
  <td>Key</td>
  <td>Hello 模擬器的授權金鑰。 索引鍵必須是 64 位元組向量的 hello base-64 編碼。</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;key&gt;</td>
  <td>&lt;索引鍵&gt;： 索引鍵必須是 hello base 64 編碼的 64 位元組向量為單位</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>指定要啟用要求率限制行為。</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>指定要停用要求率限制行為。</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>不要顯示 hello 模擬器使用者介面。</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>啟動時不要顯示文件總管。</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>指定 hello 最大的資料分割的集合。 請參閱[變更集合的 hello 數目](#set-partitioncount)如需詳細資訊。</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;：允許的單一分割區集合數目上限。 預設值為 25。 允許的上限為 250。</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>指定 hello 預設資料分割數目的資料分割的集合。</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; 預設值為 25。</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>啟用透過網路存取 toohello 模擬器。 您還必須傳遞 /Key =&lt;key_string&gt;或 /KeyFile =&lt;file_name&gt; tooenable 網路存取。</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;<br><br>或<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>當 /AllowNetworkAccess 在使用中時請勿調整防火牆規則。</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>產生新的授權金鑰並儲存 toohello 指定的檔案。 hello 產生索引鍵可以搭配 hello /Key 或 /KeyFile 選項。</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;路徑 tookey 檔案&gt;</td>
  <td></td>
</tr>
<tr>
  <td>一致性</td>
  <td>設定 hello hello 帳戶的預設一致性層級。</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;一致性&gt;： 值必須是 hello 下列其中一種[一致性層級](consistency-levels.md)： 工作階段、 強式、 Eventual 或 BoundedStaleness。  hello 預設值是工作階段。</td>
</tr>
<tr>
  <td>?</td>
  <td>顯示 hello 說明訊息。</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Hello Azure Cosmos DB 模擬器和 Azure Cosmos DB 之間的差異 
Hello Azure Cosmos DB 模擬器提供模擬的環境在本機開發人員工作站上執行，因此有一些差異功能 hello 模擬器和 Azure Cosmos DB 帳戶之間 hello 定域機組中：

* hello Azure Cosmos DB 模擬器支援只有單一固定的帳戶及已知的主索引鍵。  重新產生金鑰不能在 hello Azure Cosmos DB 模擬器。
* hello Azure Cosmos DB 模擬器不是可擴充的服務，而且不支援大量的集合。
* hello Azure Cosmos DB 模擬器不會模擬不同[Azure Cosmos DB 一致性層級](consistency-levels.md)。
* hello Azure Cosmos DB 模擬器不會模擬[多區域複寫](distribute-data-globally.md)。
* hello Azure Cosmos DB 模擬器不支援 hello 服務配額覆寫 hello Azure Cosmos DB 服務 （例如文件大小限制，增加的分割區的集合儲存體） 中可用。
* 因為 hello Azure Cosmos DB 模擬器副本可能不是向上 toodate hello 與 hello Azure Cosmos DB 服務的最新變更，請[Azure Cosmos DB 容量規劃](https://www.documentdb.com/capacityplanner)tooaccurately 估計生產輸送量 (RUs)應用程式的需求。

## <a id="set-partitioncount"></a>變更集合的 hello 數目

根據預設，您可以建立 too25 單一分割區的集合，或使用 hello Azure Cosmos DB 模擬器 1 的資料分割的集合。 藉由修改 hello **PartitionCount**值，您可以建立 too250 單一分割區集合或 10 個資料分割的集合，或任何組合的 hello 不能超過 250 單一的兩個資料分割 （位置 1 進行資料分割集合 = 25 的單一資料分割集合)。

如果超過 hello 目前資料分割計數後，您可以嘗試 toocreate 集合，hello 模擬器會擲回以 hello 下訊息 ServiceUnavailable 例外狀況。

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

集合可用 toohello Azure Cosmos DB 模擬器，toochange hello 數目不要 hello 遵循：

1. 刪除所有的本機 Azure Cosmos DB 模擬器資料，以滑鼠右鍵按一下 hello **Azure Cosmos DB 模擬器**圖示 hello 系統匣中，然後按一下**重設資料...**.
2. 刪除以下資料夾中所有的模擬器資料：C:\Users\user_name\AppData\Local\CosmosDBEmulator。
3. 結束所有開啟的執行個體，以滑鼠右鍵按一下 hello **Azure Cosmos DB 模擬器**圖示 hello 系統匣中，然後按一下**結束**。 它可能會花一分鐘的所有執行個體 tooexit。
4. 安裝 hello 最新版 hello [Azure Cosmos DB 模擬器](https://aka.ms/cosmosdb-emulator)。
5. 藉由設定值，啟動模擬器 hello PartitionCount 旗標，hello < = 250。 例如： `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`。

## <a name="troubleshooting"></a>疑難排解

使用下列秘訣 toohelp hello Azure Cosmos DB 模擬器與您遇到的問題進行疑難排解的 hello:

- 如果您安裝新版本的 hello 模擬器，並發生錯誤，請確定您重設您的資料。 您可以 hello Azure Cosmos DB 模擬器圖示上 hello 系統匣中，按一下滑鼠右鍵，然後按一下重設資料重設您的資料... 如果無法解決 hello 錯誤，您可以解除安裝然後重新安裝 hello 應用程式。 請參閱[解除安裝本機模擬器，hello](#uninstall)如需相關指示。

- 如果 hello Azure Cosmos DB 模擬器損毀，c:\Users\user_name\AppData\Local\CrashDumps 資料夾從收集傾印檔案，壓縮檔案，並且將它們附加 tooan 電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。

- 如果您遇到當機 CosmosDB.StartupEntryPoint.exe，執行下列命令，從系統管理員命令提示字元的 hello:`lodctr /R` 

- 如果您遇到連接問題，[收集追蹤檔案](#trace-files)、 壓縮，並且將它們附加 tooan 電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。

- 如果您收到**服務無法使用**訊息，hello 模擬器可能會失敗 tooinitialize hello 網路堆疊。 如果您擁有 hello Pulse 安全用戶端或 Juniper 網路用戶端安裝，因為其網路篩選器驅動程式可能會造成 hello 問題，請檢查 toosee。 解除安裝協力廠商網路篩選器驅動程式通常會修正 hello 問題。

### <a id="trace-files"></a>收集追蹤檔案

toocollect 偵錯追蹤，執行 hello 系統管理命令提示字元中的下列命令：

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`。 監看式 hello 系統匣 toomake 確定 hello 程式已關閉時，可能需要一分鐘的時間。 您也可以按一下**結束**hello Azure Cosmos DB 模擬器使用者介面中。
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. 重新產生 hello 問題。 如果資料的總管尚未運作，您只需要 toowait 的 hello 瀏覽器 tooopen 幾秒 toocatch hello 錯誤。
5. `CosmosDB.Emulator.exe /stoptraces`
6. 瀏覽過`%ProgramFiles%\Azure Cosmos DB Emulator`尋找 hello docdbemulator_000001.etl 檔案。
7. 傳送嗨.etl 檔案以及重新產生步驟太[askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com)偵錯。

### <a id="uninstall"></a>解除安裝 hello 本機模擬器

1. 結束所有開啟的執行個體的 hello 本機模擬器，以滑鼠右鍵按一下 hello Azure Cosmos DB 模擬器圖示上 hello 系統匣中，然後按一下結束。 它可能會花一分鐘的所有執行個體 tooexit。
2. 在 hello Windows 搜尋方塊中，輸入**應用程式和功能**，然後按一下 hello**應用程式和功能 （系統的設定）**結果。
3. 在 hello 清單的應用程式中，捲動太**Azure Cosmos DB 模擬器**、 選取它、 按一下**解除安裝**、 確認，然後按一下 **解除安裝**一次。
4. 解除安裝 hello 應用程式時，瀏覽 tooC:\Users\<使用者 > \AppData\Local\CosmosDBEmulator 和 delete hello 資料夾。 

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 安裝 hello 本機模擬器
> * Rand hello Docker for Windows 上的模擬器
> * 已驗證要求
> * 使用 hello 模擬器中的 hello 資料總管
> * 已匯出 SSL 憑證
> * 從 hello 命令列呼叫 hello 模擬器
> * 已收集追蹤檔案

在本教學課程中，您學到如何 toouse hello 可用的本機開發的本機模擬器。 您現在可以繼續 toohello 下一個教學課程，並了解如何 tooexport 模擬器 SSL 憑證。 

> [!div class="nextstepaction"]
> [匯出 hello Azure Cosmos DB 模擬器憑證](local-emulator-export-ssl-certificates.md)
