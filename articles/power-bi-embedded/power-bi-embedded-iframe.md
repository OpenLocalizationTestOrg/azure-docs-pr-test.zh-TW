---
title: "Power BI Embedded 與其餘 aaaHow toouse |Microsoft 文件"
description: "深入了解如何 toouse Power BI Embedded 與其餘部分 "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>如何 toouse Power BI Embedded 與其餘部分

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded：了解功能與用途

Power BI Embedded 概觀述 hello 官方[Power BI Embedded 網站](https://azure.microsoft.com/services/power-bi-embedded/)，但得到 hello 詳細說明使用 REST 之前，讓我們快速瀏覽。

這其實很簡單。 您可能會想 toouse hello 動態資料視覺效果的[Power BI](https://powerbi.microsoft.com)自己的應用程式中。

大部分的自訂應用程式需要 toodeliver hello 資料他們自己的客戶，不一定是自己的組織中的使用者。 比方說，如果您提供服務給公司 A 和 B 公司，公司 A 中的使用者只能看到資料為自己的公司 a。也就是說，hello 多租用戶所需的 hello 傳遞。

hello 自訂應用程式可能也提供它自己的驗證方法，例如表單驗證、 基本驗證等等... 然後，hello 內嵌方案必須共同作業以這個現有的驗證方法安全地。 它也是必要的使用者 toobe 無法 toouse 的 ISV 應用程式不含 hello 額外採購或授權的 Power BI 訂用帳戶。

 **Power BI Embedded** 正是針對這類案例所設計。 因此，現在，我們已經超出 hello 方式的快速簡介，讓我們先進入部分詳細資料

您可以使用 hello.NET \(C#) 或 Node.js SDK，tooeasily 建置使用 Power BI Embedded 應用程式。 但是，在本文中，我們將不使用 SDK 來說明關於 Power BI 的 HTTP 流程 \(incl. AuthN)。 了解此流程，您可以建置應用程式**與程式設計語言**，而且您可以了解太深的 Power BI Embedded 的 hello 本質。

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>建立 Power BI 工作區集合，並取得存取金鑰 \(佈建)

Power BI Embedded 是其中一個 hello Azure 服務。 只有 hello ISV 會使用 Azure 入口網站則需支付使用費\(每個小時使用者工作階段)，而且檢視 hello 報表不充電或甚至 hello 使用者需要 Azure 訂用帳戶。
開始之前我們的應用程式開發，我們必須建立 hello **Power BI 工作區集合**透過 Azure 入口網站。

每個工作區的 Power BI Embedded hello 工作區中的每個客戶 （租用戶），但我們可以加入多個工作區中的每個工作區集合。 相同的存取金鑰會用在每個工作區集合中的 hello。 事實上，hello 工作區集合是 Power BI Embedded hello 安全性界限。

![](media/power-bi-embedded-iframe/create-workspace.png)

當我們完成建立 hello 工作區的集合時，請從 Azure 入口網站複製 hello 存取金鑰。

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> 我們也可以佈建 hello 工作區集合中並取得透過 REST API 的存取金鑰。 詳細資訊，請參閱 toolearn [Power BI 資源提供者 Api](https://msdn.microsoft.com/library/azure/mt712306.aspx)。

## <a name="create-pbix-file-with-power-bi-desktop"></a>使用 Power BI Desktop 建立 .pbix 檔案

接下來，我們必須建立 hello 資料連接和內嵌報表 toobe。
此工作中沒有任何程式設計或程式碼。 我們只使用 Power BI Desktop。
在本文中，我們將不會經歷 hello 詳細瞭解 toouse Power BI Desktop。 如果您在此處需要一些說明，請參閱 [開始使用 Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)。 此範例中，我們將只使用 hello[零售分析範例](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/)。

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>建立 Power BI 工作區

既然 hello 佈建所有完成，讓我們開始吧 hello 透過 REST Api 的 工作區集合中建立客戶的工作區。 hello 下列 HTTP POST 要求 (REST) 建立 hello 新的工作區中現有工作區集合。 這是 hello [POST 工作區 API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。 在本例中，為 hello 工作區集合名稱**mypbiapp**。 我們只設定 hello 存取金鑰，我們先前複製為**AppKey**。 這是非常簡單的驗證！

**HTTP 要求**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**HTTP 回應**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

傳回的 hello**工作區識別碼**用於 hello 遵循後續的 API 呼叫。 我們的應用程式必須保留這個值。

## <a name="import-pbix-file-into-hello-workspace"></a>.Pbix 檔案匯入至 hello 工作區

每個工作區中的報表對應 tooa 單一 Power BI Desktop 檔案與資料集\(包括資料來源的設定)。 我們可以匯入我們.pbix 檔案 toohello 工作區中 hello 的下列程式碼所示。 您可以看到，我們可以上傳.pbix 檔案，使用 http 以 MIME 多組件的 hello 二進位檔。

hello uri 片段**32960a09-6366-4208-a8bb-9e0678cdbb9d** hello 工作區識別碼，和查詢參數**datasetDisplayName**是 hello 資料集名稱 toocreate。 hello 建立資料集保存所有相關資料匯入資料，例如.pbix 檔案中的成品 hello 指標 toohello 資料來源等等...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

此匯入工作可能會執行一段時間。 完成時，我們的應用程式可以要求使用匯入識別碼 hello 工作狀態。在此範例中，hello 匯入 id 是**4eec64dd-533b-47c3-a72c-6508ad854659**。

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

hello 下列要求使用此匯入識別碼的狀態：

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

如果 hello 工作未完成，HTTP 回應 hello 可能像這樣：

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

如果 hello 工作已完成，HTTP 回應 hello 可能類似這樣：

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>資料來源連線 \(以及資料的多重租用)

幾乎所有的.pbix 檔案中的 hello 成品匯入至我們的工作區中，資料來源的 hello 認證並不是。 如此一來，當使用**DirectQuery 模式**，hello 內嵌的報表無法顯示正確。 但是，當使用**匯入模式**，我們可以檢視 hello 報表使用 hello 現有的匯入的資料。 在這種情況下，我們必須設定使用下列步驟透過 REST 呼叫的 hello hello 認證。

首先，我們必須取得 hello 閘道資料來源。 我們知道 hello 資料集**識別碼**hello 先前傳回識別碼。

**HTTP 要求**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**HTTP 回應**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

使用 hello 傳回閘道識別碼和資料來源識別碼\(請參閱先前的 hello **gatewayId**和**識別碼**hello 中傳回的結果)，我們可以變更這個資料來源的 hello 認證，如下所示：

**HTTP 要求**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**HTTP 回應**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

在生產環境中，我們也可以設定每個工作區中使用 REST API 的 hello 不同的連接字串。 \(亦即，我們可以區隔 hello 資料庫的每個客戶。）

hello 下列變更 hello 透過 REST 的資料來源的連接字串。

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

或者，我們可以使用資料列層級安全性，在 Power BI Embedded，而且可以區隔每個使用者在報表中的 hello 資料。 如此一來，我們就可以使用同一個 .pbix \(UI 等等) 和不同的資料來源，來佈建每個客戶報表。

> [!NOTE]
> 如果您使用**匯入模式**而不是**DirectQuery 模式**，不沒有應用程式開發介面透過任何方式 toorefresh 模型。 而且，Power BI Embedded 尚未支援透過 Power BI 閘道器內部部署資料來源。 不過，您會真的想 tookeep 落在 hello [Power BI 部落格](https://powerbi.microsoft.com/blog/)針對最新消息未來在未來發行版本。

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>在我們的網頁中驗證和裝載 (內嵌) 報表

在 hello 先前的 REST API，我們可以使用 hello 便捷鍵**AppKey**本身做為 hello 授權標頭。 這些呼叫可以 hello 後端伺服器端處理，因為它是安全的。

但是，當我們在我們的網頁中內嵌 hello 報表時，會使用 JavaScript 處理這類安全性資訊\(前端)。 然後您必須保護 hello 授權標頭值。 如果我們的存取金鑰被惡意使用者或惡意程式碼發現，他們就可以使用這個金鑰呼叫任何作業。

當我們在我們的網頁中內嵌 hello 報表時，我們必須使用 hello 計算語彙基元，而不是存取金鑰**AppKey**。 我們的應用程式必須建立 hello OAuth Json Web 權杖\(JWT) 所組成 hello 宣告與 hello 計算數位簽章。 這個 OAuth JWT 是使用點分隔符號編碼的字串權杖，如下圖所示。

![](media/power-bi-embedded-iframe/oauth-jwt.png)

首先，我們必須準備 hello 輸入的值，稍後再簽署。 此值為 hello base64 url 編碼 (rfc4648) 字串的 hello 下列 json，且這些由 hello 點分隔\(。) 字元。 更新版本中，我們將說明如何 tooget hello 報表識別碼。

> [!NOTE]
> 如果我們想 toouse 資料列層級安全性 (RLS) 與 Power BI Embedded，我們也必須指定**username**和**角色**hello 宣告中。

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

接下來，我們必須建立 hello base64 編碼字串的 HMAC \(hello 簽章) 使用 SHA256 演算法。 此帶正負號的輸入的值為 hello 先前的字串。

最後，我們就必須合併 hello 輸入的值和簽章字串的使用期限\(。) 字元。 已完成的 hello 字串是 hello hello 報表內嵌的應用程式語彙基元。 即使 hello 應用程式的權杖探索到的惡意使用者，他們無法取得 hello 原始的存取金鑰。 此應用程式權杖很快就會到期。

以下是這些步驟的 PHP 範例：

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>最後，hello 報表內嵌到 hello web 網頁

針對內嵌報表，我們必須取得 hello 內嵌 url 和報表**識別碼**使用下列 REST API 的 hello。

**HTTP 要求**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**HTTP 回應**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

我們使用 hello 先前的應用程式權杖的 web 應用程式中，我們可以內嵌 hello 報表。
如果看一下 hello 下一個範例程式碼，hello 先前部分是 hello 與 hello 前一個範例相同。 在 hello 第二個部分中，這個範例會顯示 hello **embedUrl** \(請參閱上述結果中 hello) 在 hello iframe，並張貼到 hello iframe hello 應用程式權杖。

> [!NOTE]
> 您將需要 toochange hello 報表識別碼值 tooone 您自己。 此外，因為在我們的內容管理系統 tooa bug，hello iframe hello 程式碼範例中讀取標記時常值。 如果您複製並貼上此範例程式碼，則請移除 hello 標記上限的 hello 文字。

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

我們的結果如下︰

![](media/power-bi-embedded-iframe/view-report.png)

在這個階段中，Power BI Embedded 只會顯示 hello 報表 hello iframe 中。 但是，請注意 hello [Power BI 部落格](https://powerbi.microsoft.com/blog/)。 未來的改良功能無法使用新的用戶端應用程式開發介面，將會讓我們傳送資訊到 hello iframe，以及取得資訊。令人興奮吧！

## <a name="see-also"></a>另請參閱
* [在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)

有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

