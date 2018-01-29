---
title: "限制和設定 - Azure Logic Apps | Microsoft Docs"
description: "適用於 Azure Logic Apps 的服務限制和設定值"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 22d0ee242d18d73d1d5825567fd61638fd22cc68
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="logic-apps-limits-and-configuration"></a>Logic Apps 限制和設定

本主題說明 Azure Logic Apps 目前的限制和設定詳細資料。

## <a name="limits"></a>限制

### <a name="http-request-limits"></a>HTTP 要求限制

這些限制適用於單一 HTTP 要求或連接器呼叫。

#### <a name="timeout"></a>逾時

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 要求逾時 | 120 秒 | [非同步模式](../logic-apps/logic-apps-create-api-app.md)或 [Until 迴圈](logic-apps-loops-and-scopes.md)可以視需要抵銷 |
|||| 

#### <a name="message-size"></a>訊息大小

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 訊息大小 | 100 MB | 某些連接器和 API 可能不支援 100 MB。 | 
| 運算式評估限制 | 131,072 個字元 | `@concat()`、`@base64()``string` 的長度不能超過此限制。 | 
|||| 

#### <a name="retry-policy"></a>重試原則

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 重試次數 | 90 | 預設值為 4。 您可以使用[重試原則參數](../logic-apps/logic-apps-workflow-actions-triggers.md)來設定。 | 
| 重試延遲上限 | 1 天 | 您可以使用[重試原則參數](../logic-apps/logic-apps-workflow-actions-triggers.md)來設定。 | 
| 重試延遲下限 | 5 秒 | 您可以使用[重試原則參數](../logic-apps/logic-apps-workflow-actions-triggers.md)來設定。 |
|||| 

### <a name="run-duration-and-retention"></a>執行持續時間和保留期

這些限制適用於單一邏輯應用程式執行。

| Name | 限制 | 
| ---- | ----- | 
| 執行持續時間 | 90 天 | 
| 儲存體保留期 | 從執行開始時間算起 90 天 | 
| 最小循環間隔 | 1 秒 </br>針對搭配 App Service 方案的邏輯應用程式：15 秒 | 
| 最大循環間隔 | 500 天 | 
||| 

若要在您的正常處理流程中超出執行持續時間或儲存體保留期的限制，請[與我們連絡](mailto://logicappsemail@microsoft.com)，以便協助滿足您的需求。

### <a name="looping-and-debatching-limits"></a>迴圈和解除批次處理限制

這些限制適用於單一邏輯應用程式執行。

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| ForEach 項目 | 100,000 | 您可以視需要使用[查詢動作](../connectors/connectors-native-query.md)來篩選較大的陣列。 | 
| 反覆運算之前 | 5,000 | | 
| SplitOn 項目 | 100,000 | | 
| ForEach 平行處理原則 | 50 | 預設值為 20。 <p>若要在 ForEach 迴圈中設定特定的平行處理原則層級，請在 `foreach` 動作中設定 `runtimeConfiguration` 屬性。 <p>若要循序執行 ForEach 迴圈，請將 `foreach` 動作中的 `operationOptions` 屬性設定為 "Sequential"。 | 
|||| 

### <a name="throughput-limits"></a>輸送量限制

這些限制適用於單一邏輯應用程式執行個體。

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 每 5 分鐘的動作執行 | 100,000 | 可以視需要將工作負載分散到多個應用程式。 | 
| 動作並行撥出電話 | ~2,500 | 視需要減少並行要求數目或縮短持續時間。 | 
| 執行階段端點：並行連入呼叫 | ~1,000 | 視需要減少並行要求數目或縮短持續時間。 | 
| 執行階段端點：每隔 5 分鐘讀取一次呼叫 | 60,000 | 可以視需要將工作負載分散到多個應用程式。 | 
| 執行階段端點：每隔 5 分鐘叫用一次呼叫 | 45,000 | 可以視需要將工作負載分散到多個應用程式。 | 
|||| 

若要在正常處理中超出這些限制，或執行可能超出這些限制的負載測試，請[與我們連絡](mailto://logicappsemail@microsoft.com)，以便協助滿足您的需求。

### <a name="logic-app-definition-limits"></a>邏輯應用程式定義限制

這些限制適用於單一邏輯應用程式定義。

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 每個工作流程的動作數目 | 500 | 若要延伸此限制，您可以視需要新增巢狀工作流程。 |
| 允許的動作巢狀深度 | 8 | 若要延伸此限制，您可以視需要新增巢狀工作流程。 | 
| 每個訂用帳戶每個區域的工作流程數目 | 1000 | | 
| 每個工作流程的觸發程序數目 | 10 | | 
| 參數範圍案例限制 | 25 | | 
| 每個工作流程的變數數目 | 250 | | 
| 每個運算式的字元數上限 | 8,192 | | 
| `trackedProperties` 大小上限 (以字元為單位) | 16,000 | 
| `action`/`trigger` 名稱限制 | 80 | | 
| `description` 長度限制 | 256 | | 
| `parameters` 限制 | 50 | | 
| `outputs` 限制 | 10 | | 
|||| 

<a name="custom-connector-limits"></a>

### <a name="custom-connector-limits"></a>自訂連接器限制

這些限制適用於您可以從 Web API 建立的自訂連接器。

| Name | 限制 | 
| ---- | ----- | 
| 您可以建立的自訂連接器數目 | 每個 Azure 訂用帳戶 1,000 個 | 
| 自訂連接器所建立之每個連線的每分鐘要求數目 | 連接器所建立的每個連線可以有 500 個要求 |
||| 

### <a name="integration-account-limits"></a>整合帳戶限制

這些限制適用於您可以新增到整合帳戶中的成品。

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 結構描述 | 8 MB | 您可以使用 [Blob URI](../logic-apps/logic-apps-enterprise-integration-schemas.md) 來上傳大於 2 MB 的檔案。 | 
| 對應 (XSLT 檔案) | 2 MB | | 
| 執行階段端點：每隔 5 分鐘讀取一次呼叫 | 60,000 | 可以視需要將工作負載分散到多個帳戶。 | 
| 執行階段端點：每隔 5 分鐘叫用一次呼叫 | 45,000 | 可以視需要將工作負載分散到多個帳戶。 | 
| 執行階段端點：每隔 5 分鐘追蹤一次呼叫 | 45,000 | 可以視需要將工作負載分散到多個帳戶。 | 
| 執行階段端點：封鎖並行呼叫 | ~1,000 | 視需要減少並行要求數目或縮短持續時間。 | 
|||| 

這些限制適用於您可以新增到整合帳戶中的成品數目。

#### <a name="free-pricing-tier"></a>免費定價層

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 合約 | 10 | | 
| 其他成品類型 | 25 |成品類型包含合作夥伴、結構描述、憑證及對應。 各類型所擁有的成品數量可達到最大上限。 | 
|||| 

#### <a name="standard-pricing-tier"></a>標準定價層

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| 任何成品類型 | 500 | 成品類型包含協議、合作夥伴、結構描述、憑證及對應。 各類型所擁有的成品數量可達到最大上限。 | 
|||| 

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a>B2B 通訊協定 (AS2、X12、EDIFACT) 訊息大小

這些限制適用於 B2B 通訊協定。

| Name | 限制 | 注意 | 
| ---- | ----- | ----- | 
| AS2 | 50 MB | 適用於解碼和編碼 | 
| X12 | 50 MB | 適用於解碼和編碼 | 
| EDIFACT | 50 MB | 適用於解碼和編碼 | 
|||| 

<a name="configuration"></a>

## <a name="configuration-ip-addresses"></a>設定：IP 位址

### <a name="logic-apps-service"></a>Logic Apps 服務

邏輯應用程式直接 (也就是透過 [HTTP](../connectors/connectors-native-http.md) 或 [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)或其他 HTTP 要求) 發出的呼叫會來自以下清單中的 IP 位址。

|Logic Apps 區域|輸出 IP|
|-----------------|-----------|
|澳洲東部|13.75.149.4, 104.210.91.55, 104.210.90.241|
|澳大利亞東南部|13.73.114.207, 13.77.3.139, 13.70.159.205|
|巴西南部|191.235.82.221, 191.235.91.7, 191.234.182.26|
|加拿大中部|52.233.29.92, 52.228.39.241, 52.228.39.244|
|加拿大東部|52.232.128.155, 52.229.120.45, 52.229.126.25|
|印度中部|52.172.154.168, 52.172.186.159, 52.172.185.79|
|美國中部|13.67.236.125, 104.208.25.27, 40.122.170.198|
|東亞|13.75.94.173, 40.83.127.19, 52.175.33.254|
|美國東部|13.92.98.111, 40.121.91.41, 40.114.82.191|
|美國東部 2|40.84.30.147, 104.208.155.200, 104.208.158.174|
|日本東部|13.71.158.3, 13.73.4.207, 13.71.158.120|
|日本西部|40.74.140.4, 104.214.137.243, 138.91.26.45|
|美國中北部|168.62.248.37, 157.55.210.61, 157.55.212.238|
|北歐|40.113.12.95, 52.178.165.215, 52.178.166.21|
|美國中南部|104.210.144.48, 13.65.82.17, 13.66.52.232|
|東南亞|13.76.133.155, 52.163.228.93, 52.163.230.166|
|印度南部|52.172.50.24, 52.172.55.231, 52.172.52.0|
|美國中西部|52.161.27.190, 52.161.18.218, 52.161.9.108|
|西歐|40.68.222.65, 40.68.209.23, 13.95.147.65|
|印度西部|104.211.164.80, 104.211.162.205, 104.211.164.136|
|美國西部|52.160.92.112, 40.118.244.241, 40.118.241.243|
|美國西部 2|13.66.210.167, 52.183.30.169, 52.183.29.132|
|英國南部|51.140.74.14, 51.140.73.85, 51.140.78.44|
|英國西部|51.141.54.185, 51.141.45.238, 51.141.47.136|
| | |

### <a name="connectors"></a>連接器

[連接器](../connectors/apis-list.md)發出的呼叫會來自以下清單中的 IP 位址。

|Logic Apps 區域|輸出 IP|
|-----------------|-----------|
|澳洲東部|40.126.251.213|
|澳大利亞東南部|40.127.80.34|
|巴西南部|191.232.38.129|
|加拿大中部|52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13|
|加拿大東部|52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52|
|印度中部|104.211.98.164|
|美國中部|40.122.49.51|
|東亞|23.99.116.181|
|美國東部|191.237.41.52|
|美國東部 2|104.208.233.100|
|日本東部|40.115.186.96|
|日本西部|40.74.130.77|
|美國中北部|65.52.218.230|
|北歐|104.45.93.9|
|美國中南部|104.214.70.191|
|東南亞|13.76.231.68|
|印度南部|104.211.227.225|
|西歐|40.115.50.13|
|印度西部|104.211.161.203|
|美國西部|104.40.51.248|
|英國南部|51.140.80.51|
|英國西部|51.141.47.105|
| | | 

## <a name="next-steps"></a>後續步驟  

* [建立第一個邏輯應用程式](../logic-apps/quickstart-create-first-logic-app-workflow.md)  
* [常見的範例和案例](../logic-apps/logic-apps-examples-and-scenarios.md)
* [影片：使用 Logic Apps 將商務程序自動化](http://channel9.msdn.com/Events/Build/2016/T694) \(英文\) 
* [影片：將您的系統與 Azure Logic Apps 整合](http://channel9.msdn.com/Events/Build/2016/P462) \(英文\)