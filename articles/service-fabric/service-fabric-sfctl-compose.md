---
title: Azure Service Fabric CLI - sfctl compose | Microsoft Docs
description: "描述 Service Fabric CLI sfctl compose 命令。"
services: service-fabric
documentationcenter: na
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: cli
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/22/2017
ms.author: ryanwi
ms.openlocfilehash: 0e35ac70125bc640114a4492498b12ea96800d42
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sfctl-compose"></a>sfctl compose
建立、刪除和管理 Docker Compose 部署。

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
|    create| 從 Compose 檔案部署 Service Fabric 應用程式。|
|    list  | 取得在 Service Fabric 叢集中建立的 Compose 部署清單。|
|   remove| 從叢集刪除現有的 Service Fabric Compose 部署。|
|   status| 取得 Service Fabric Compose 部署的相關資訊。|
|升級       | 開始升級 Service Fabric 叢集中的 Compose 部署。|
|    upgrade-status| 取得在此 Service Fabric Compose 部署上執行的最新升級詳細資料。|


## <a name="sfctl-compose-create"></a>sfctl compose create
建立 Service Fabric Compose 部署。

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --file-path [必要]| 目標 Docker Compose 檔案的路徑。|
 |   --deployment-name [必要]| 部署的名稱。|
|    --encrypted-pass             | 不是提示容器登錄密碼，而是使用已加密的複雜密碼。|
|    --has-pass                   | 提示使用容器登錄的密碼。|
|    --timeout -t                 | 伺服器逾時 (秒)。  預設值：60。|
 |   --user                       | 連線到容器登錄的使用者名稱。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug                 | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h               | 顯示此說明訊息並結束。|
| --output -o             | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query                 | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose               | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-compose-list"></a>sfctl compose list
取得在 Service Fabric 叢集中建立的 Compose 部署清單。

取得 Service Fabric 叢集中已建立或正在建立的 Compose 部署的相關狀態。 回應包括名稱、狀態，以及與 Compose 部署有關的其他詳細資料。 如果部署無法放入一頁，則會傳回一頁結果，以及可用來取得下一頁的接續權杖。

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --continuation-token| 接續權杖參數可用來取得下一組結果。 具有非空白值的接續權杖會在來自系統的結果無法放入單一回應中時，隨附在 API 的回應中。      當此值傳遞至下一個 API 呼叫時，API 會傳回下一組結果。 如果沒有任何進一步的結果，接續權杖就不會包含值。 此參數的值不能經過 URL 編碼。|
| --max-results    | 分頁式查詢時傳回的最大結果數目。      此參數定義傳回結果數目的上限。      如果傳回的結果無法依照組態中定義的最大訊息大小限制放入訊息中，則可能會少於指定的最大結果數目。 如果此參數為零或未指定，分頁式查詢會在傳回訊息中盡可能包含越多結果。|
| --timeout -t     | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug          | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h        | 顯示此說明訊息並結束。|
| --output -o      | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query          | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose        | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-compose-remove"></a>sfctl compose remove
從叢集刪除現有的 Service Fabric Compose 部署。

刪除現有的 Service Fabric Compose 部署。 

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --deployment-name [必要]| 部署的識別。 這通常是沒有 'fabric:' URI 配置之應用程式的完整名稱。|
| --timeout -t            | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug                 | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h               | 顯示此說明訊息並結束。|
| --output -o             | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query                 | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose               | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-compose-status"></a>sfctl compose status
取得 Service Fabric Compose 部署的相關資訊。

傳回 Service Fabric 叢集中已建立或正在建立且名稱符合參數指定之名稱的 Compose 部署狀態。 回應包括名稱、狀態，以及與應用程式有關的其他詳細資料。

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --deployment-name [必要]| 部署的識別。 |
| --timeout -t            | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug                 | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h               | 顯示此說明訊息並結束。|
| --output -o             | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query                 | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose               | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-compose-upgrade"></a>sfctl compose upgrade
開始升級 Service Fabric 叢集中的 Compose 部署。

驗證提供的升級參數，並開始升級部署。

### <a name="arguments"></a>引數
|引數|說明|
| --- | --- |
|    --file-path [必要]| 目標 Docker Compose 檔案的路徑。|
|    --deployment-name [必要]| 部署的名稱。|
|    --default-svc-type-health-map| 描述用來評估服務健康情況之健康原則的 JSON 編碼字典。|
|    --encrypted-pass             | 不是提示容器登錄密碼，而是使用已加密的複雜密碼。|
 |   --failure-action             | 可能值包括：'Invalid'、'Rollback'、'Manual'。|
|    --force-restart              | 強制重新啟動。|
 |   --has-pass                   | 提示使用容器登錄的密碼。|
|    --health-check-retry         | 健康情況檢查重試逾時 (毫秒)。|
|    --health-check-stable        | 健康情況檢查穩定持續時間 (毫秒)。|
|    --health-check-wait          | 健康情況檢查等候持續時間 (毫秒)。|
|    --replica-set-check          | 升級複本設定檢查逾時 (秒)。|
|    --svc-type-health-map        | 描述用來評估不同服務類型健康情況之健康原則的物件 JSON 編碼清單。|
|    --timeout -t                 | 伺服器逾時 (秒)。  預設值：60。|
|    --unhealthy-app              | 在報告錯誤之前，允許健康情況不良應用程式的最大百分比。        例如，若要允許 10% 的應用程式健康情況不良，這個值會是 10。 百分比表示在系統將叢集視為錯誤之前，容許應用程式健康情況不良的最大百分比。 如果未到達此百分比，但至少有一個健康情況不良的應用程式，則健康情況會評估為 Warning。 此百分比是將健康情況不良應用程式數目除以叢集中的應用程式執行個體總數計算而得。|
|    --upgrade-domain-timeout     | 升級網域逾時 (毫秒)。|
|    --upgrade-kind               | 預設值：Rolling。|
|    --upgrade-mode               | 可能值包括：'Invalid'、'UnmonitoredAuto'、'UnmonitoredManual'、'Monitored'。  預設值：UnmonitoredAuto。|
|    --upgrade-timeout            | 升級逾時 (毫秒)。|
|    --user                       | 連線到容器登錄的使用者名稱。|
|    --warning-as-error           | 具有相同嚴重性的警告會視為錯誤。|

### <a name="global-arguments"></a>全域引數
 |引數|說明|
| --- | --- |
|   --debug                      | 增加記錄詳細程度以顯示所有偵錯記錄。|
|    --help -h                    | 顯示此說明訊息並結束。|
 |   --output -o                  | 輸出格式。  允許的值：json、jsonc、table、tsv。
                                   預設值：json。|
 |   --query                      | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
 |   --verbose                    | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="next-steps"></a>後續步驟
- [設定](service-fabric-cli.md) Service Fabric CLI。
- 了解如何使用[範例指令碼](/azure/service-fabric/scripts/sfctl-upgrade-application)來使用 Service Fabric CLI。