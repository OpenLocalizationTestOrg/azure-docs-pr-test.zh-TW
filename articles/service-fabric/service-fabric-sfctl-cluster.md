---
title: Azure Service Fabric CLI - sfctl cluster | Microsoft Docs
description: "描述 Service Fabric CLI sfctl cluster 命令。"
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
ms.openlocfilehash: 5eeff271fea67cd859dff598cae0010cf3b8e13f
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sfctl-cluster"></a>sfctl cluster
選取、管理和操作 Service Fabric 叢集。

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
|    code-versions| 取得在 Service Fabric 叢集中佈建的網狀架構程式碼版本清單。|
|    config-versions | 取得在 Service Fabric 叢集中佈建的網狀架構組態版本清單。|
|    health       | 取得 Service Fabric 叢集的健康情況。|
|    manifest     | 取得 Service Fabric 叢集資訊清單。|
|    operation-cancel| 取消使用者引起的錯誤作業。|
|    operationgit | 取得依提供的輸入所篩選之使用者引起的錯誤作業清單。|
|    provision     | 佈建 Service Fabric 叢集的程式碼或組態封裝。|
|    recover-system  | 表示 Service Fabric 叢集應該嘗試復原目前停留在仲裁遺失的系統服務。|
|report-health   | 傳送 Service Fabric 叢集的健康情況報告。|
|    選取       | 連線到 Service Fabric 叢集端點。|
| unprovision     | 解除佈建 Service Fabric 叢集的程式碼或組態封裝。|
|    升級         | 開始升級 Service Fabric 叢集的程式碼或組態版本。|
|    upgrade-resume  | 將叢集升級移至下一個升級網域。|
|    upgrade-rollback| 復原 Service Fabric 叢集的升級。|
|    upgrade-status  | 取得目前叢集升級的進度。|
|upgrade-update  | 更新 Service Fabric 叢集升級的升級參數。|


## <a name="sfctl-cluster-health"></a>sfctl cluster health
取得 Service Fabric 叢集的健康情況。

取得 Service Fabric 叢集的健康情況。 使用 EventsHealthStateFilter 可根據健康情況狀態，篩選針對叢集所報告的健康情況事件集合。 同樣地，使用 NodesHealthStateFilter 和 ApplicationsHealthStateFilter 可根據彙總的健康情況狀態，篩選傳回的節點和應用程式集合。 

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --applications-health-state-filter| 可根據健康情況狀態來篩選叢集健康情況查詢結果中所傳回的應用程式健康情況狀態物件。 此參數的可能值包括取自成員或 HealthStateFilter 列舉成員位元運算的整數值。 只會傳回符合篩選條件的應用程式。  所有應用程式都會用來評估彙總的健康情況狀態。 如果未指定，則會傳回所有項目。 狀態值是以旗標為基礎的列舉，因此值可以是使用位元 'OR' 運算子取得的這些值的組合。 例如，如果提供的值為 6，則會傳回 HealthState 值為 OK (2) 和 Warning (4) 的應用程式健康情況狀態。 - Default - 預設值。 符合任何 HealthState。 值為零。 - None - 不符合任何 HealthState 值的篩選條件。 用來在指定狀態集合沒有任何結果時傳回。 值為 1。 - Ok - 符合輸入含 HealthState 值 Ok 的篩選條件。 值為 2。 - Warning - 符合輸入含 HealthState 值 Warning 的篩選條件。 值為 4。 - Error - 符合輸入含 HealthState 值 Error 的篩選條件。 值為 8。 - All - 符合輸入含任何 HealthState 值的篩選條件。 值為 65535。|
| --events-health-state-filter   | 可根據健康情況狀態來篩選所傳回的 HealthEvent 物件集合。 此參數的可能值包括下列其中一個健康情況狀態的整數值。 只會傳回符合篩選條件的事件。 所有事件都會用來評估彙總的健康情況狀態。 如果未指定，則會傳回所有項目。 狀態值是以旗標為基礎的列舉，因此值可以是使用位元 'OR' 運算子取得的這些值的組合。 例如，如果提供的值為 6，則會傳回 HealthState 值為 OK (2) 和 Warning (4) 的所有事件。 - Default - 預設值。 符合任何 HealthState。 值為零。 - None - 不符合任何 HealthState 值的篩選條件。 用來在指定狀態集合沒有任何結果時傳回。 值為 1。 - Ok - 符合輸入含 HealthState 值 Ok 的篩選條件。 值為 2。 - Warning - 符合輸入含 HealthState 值 Warning 的篩選條件。  值為 4。 - Error - 符合輸入含 HealthState 值 Error 的篩選條件。 值為 8。 - All - 符合輸入含任何 HealthState 值的篩選條件。 值為 65535。|
|--exclude-health-statistics                   | 表示健康情況統計資料是否傳回為查詢結果的一部分。 預設為 False。 統計資料顯示健康情況狀態為 Ok、Warning 和 Error 的子項目數目。|
 |   --include-system-application-health-statistics| 表示健康情況統計資料是否應該包含 fabric:/System 應用程式健康情況統計資料。 預設為 False。 如果 IncludeSystemApplicationHealthStatistics 設為 true，則健康情況統計資料包含的項目屬於 fabric:/System 應用程式。 否則，查詢結果只會包含使用者應用程式的健康情況統計資料。 健康情況統計資料必須包含在要套用的這個參數的查詢結果中。|
| --nodes-health-state-filter    | 可根據健康情況狀態來篩選叢集健康情況查詢結果中所傳回的節點健康情況狀態物件。 此參數的可能值包括下列其中一個健康情況狀態的整數值。 只會傳回符合篩選條件的節點。 所有節點都會用來評估彙總的健康情況狀態。 如果未指定，則會傳回所有項目。 狀態值是以旗標為基礎的列舉，因此值可以是使用位元 'OR' 運算子取得的這些值的組合。 例如，如果提供的值為 "6"，則會傳回 HealthState 值為 OK (2) 和 Warning (4) 的節點健康情況狀態。 - Default - 預設值。 符合任何 HealthState。 值為零。 - None - 不符合任何 HealthState 值的篩選條件。 用來在指定狀態集合沒有任何結果時傳回。 值為 1。 - Ok - 符合輸入含 HealthState 值 Ok 的篩選條件。 值為 2。 - Warning - 符合輸入含 HealthState 值 Warning 的篩選條件。  值為 4。 - Error - 符合輸入含 HealthState 值 Error 的篩選條件。 值為 8。 - All - 符合輸入含任何 HealthState 值的篩選條件。 值為 65535。|
| --timeout -t                   | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug                        | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h                      | 顯示此說明訊息並結束。|
| --output -o                    | 輸出格式。  允許的值：json、jsonc、table、tsv。                    預設值：json。|
| --query                        | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose                      | 增加記錄詳細程度。 使用 --debug 為完整偵錯記錄。|

## <a name="sfctl-cluster-manifest"></a>sfctl cluster manifest
取得 Service Fabric 叢集資訊清單。

取得 Service Fabric 叢集資訊清單。 叢集資訊清單包含的叢集屬性，包括叢集上不同的節點類型、安全性組態、錯誤和升級網域拓撲等等。部署獨立叢集時，ClusterConfig.JSON 檔案中會指定這些屬性。 不過，叢集資訊清單中大部分的資訊會由服務網狀架構在其他部署案例 (例如使用 [Azure 入口網站](https://portal.azure.com)時) 的叢集部署期間以內部產生。 叢集資訊清單的內容僅供參考之用，使用者不應該依賴檔案內容或其解釋的格式。 

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --timeout -t| 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug  | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h| 顯示此說明訊息並結束。|
| --output -o | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query  | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose| 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-cluster-provision"></a>sfctl cluster provision
佈建 Service Fabric 叢集的程式碼或組態封裝。
驗證並佈建 Service Fabric 叢集的程式碼或組態封裝。

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
|--cluster-manifest-file-path| 叢集資訊清單檔案路徑。|
|    --code-file-path            | 叢集程式碼封裝檔案路徑。|
|    --timeout -t                | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h  | 顯示此說明訊息並結束。|
| --output -o| 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose  | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-cluster-select"></a>sfctl cluster select
連線到 Service Fabric 叢集端點。

如果連線到安全的叢集，請指定憑證 (.crt) 和金鑰檔案 (.key)，或者有兩者的單一檔案 (.pem)。 請勿指定兩者。 或者，如果連線到安全的叢集，也可以指定 CA 組合檔案路徑或受信任 CA 憑證的目錄路徑。

### <a name="arguments"></a>引數

|引數|說明|
| --- | --- |
| --endpoint [必要]| 叢集端點 URL，包括連接埠和 HTTP 或 HTTPS 前置詞。|
| --aad             | 使用 Azure Active Directory 進行驗證。|
| --ca              | 視為有效的 CA 憑證目錄路徑或 CA 組合檔案路徑。|
| --cert            | 用戶端憑證檔案的路徑。|
| --key             | 用戶端憑證金鑰檔案的路徑。|
| --no-verify       | 使用 HTTPS 時停用憑證的驗證。請注意：這是不安全的選項，因此不應該用於生產環境。|
| --pem             | 用戶端憑證 (.pem 檔案) 的路徑。|

### <a name="global-arguments"></a>全域引數

|引數|說明|
| --- | --- |
| --debug           | 增加記錄詳細程度以顯示所有偵錯記錄。|
| --help -h         | 顯示此說明訊息並結束。|
| --output -o       | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
| --query           | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
| --verbose         | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="sfctl-cluster-unprovision"></a>sfctl cluster unprovision
解除佈建 Service Fabric 叢集的程式碼或組態封裝。

解除佈建 Service Fabric 叢集的程式碼或組態封裝。

### <a name="arguments"></a>引數
|引數|說明|
| --- | --- |
|--code-version  | 叢集程式碼封裝版本。|
|    --config-version| 叢集資訊清單版本。|
|    --timeout -t    | 伺服器逾時 (秒)。  預設值：60。|

### <a name="global-arguments"></a>全域引數
|引數|說明|
| --- | --- |
|--debug         | 增加記錄詳細程度以顯示所有偵錯記錄。|
 |   --help -h       | 顯示此說明訊息並結束。|
 |   --output -o     | 輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。|
 |   --query         | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
 |   --verbose       | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|


## <a name="sfctl-cluster-upgrade"></a>sfctl cluster upgrade
開始升級 Service Fabric 叢集的程式碼或組態版本。
驗證提供的升級參數，如果參數有效，則開始升級 Service Fabric 叢集的程式碼或組態版本。

### <a name="arguments"></a>引數
|引數|說明|
| --- | --- |
|    --app-health-map                      | 引發錯誤之前，應用程式名稱和健康情況不良最大百分比組合的 JSON 編碼目錄。|
 |   --app-type-health-map                 | 引發錯誤之前，應用程式類型名稱和健康情況不良最大百分比組合的 JSON 編碼目錄。|
 |   --code-version                        | 叢集程式碼版本。|
 |   --config-version                      | 叢集組態版本。|
 |   --delta-health-evaluation             | 允許在完成每個升級網域之後進行差異健康狀態評估，而不是絕對健康狀態評估。|
 |   --delta-unhealthy-nodes               | 在叢集升級期間允許的節點健康情況衰退百分比上限。  預設值：10 差異是測量升級開始時節點的狀態和健康情況評估時節點的狀態之間的差異。 每次升級網域升級完成後都會執行檢查，以確保叢集的全域狀態處於容許的限制範圍內。|
 |   --failure-action                      | 可能值包括：'Invalid'、'Rollback'、'Manual'。|
 |   --force-restart                       | 強制重新啟動。|
 |   --health-check-retry                  | 健康情況檢查重試逾時 (毫秒)。|
 |   --health-check-stable                 | 健康情況檢查穩定持續時間 (毫秒)。|
  |  --health-check-wait                   | 健康情況檢查等候持續時間 (毫秒)。|
  |  --replica-set-check-timeout           | 升級複本設定檢查逾時 (秒)。|
 |   --rolling-upgrade-mode                | 可能值包括：'Invalid'、'UnmonitoredAuto'、'UnmonitoredManual'、'Monitored'。  預設值：UnmonitoredAuto。|
  |  --timeout -t                          | 伺服器逾時 (秒)。  預設值：60。|
  |  --unhealthy-applications              | 在報告錯誤之前，允許健康情況不良應用程式的最大百分比。 例如，若要允許 10% 的應用程式健康情況不良，這個值會是 10。 百分比表示在系統將叢集視為錯誤之前，容許應用程式健康情況不良的最大百分比。 如果未到達此百分比，但至少有一個健康情況不良的應用程式，則健康情況會評估為 Warning。 此計算是將健康情況不良的應用程式數目除以叢集中應用程式執行個體的總數而得，但不包括 ApplicationTypeHealthPolicyMap 所包含之應用程式類型的應用程式。 針對少量的應用程式數目，計算會四捨五入以容許一個失敗。|
 |   --unhealthy-nodes                     | 在報告錯誤之前，允許健康情況不良節點的最大百分比。 例如，若要允許 10% 的節點健康情況不良，這個值會是 10。 百分比表示在叢集被視為處於錯誤狀態之前，容許節點健康情況不良的最大百分比。 如果未到達此百分比，但至少有一個健康情況不良的節點，則健康情況會評估為 Warning。 百分比是將健康情況不良節點數目除以叢集中的節點總數計算而得。 針對較少的節點數目，計算會四捨五入以容許一個失敗。 在大型叢集中，永遠都有一些節點會關閉或需要修復，因此應設定此百分比來容許這種情形。|
 |   --upgrade-domain-delta-unhealthy-nodes| 在叢集升級期間允許的升級網域節點健康情況衰退百分比上限。 預設值：15。 差異是測量升級開始時升級網域節點的狀態和健康情況評估時升級網域節點的狀態之間的差異。 每次所有已完成升級網域的升級網域升級完成後都會執行檢查，以確保升級網域的狀態處於容許的限制範圍內。|
 |   --upgrade-domain-timeout              | 升級網域逾時 (毫秒)。|
 |   --upgrade-timeout                     | 升級逾時 (毫秒)。|
 |   --warning-as-error                    | 具有相同嚴重性的警告會視為錯誤。|

### <a name="global-arguments"></a>全域引數
|引數|說明|
| --- | --- |
|--debug                               | 增加記錄詳細程度以顯示所有偵錯記錄。|
|    --help -h                             | 顯示此說明訊息並結束。|
|    --output -o                           | 輸出格式。  允許的值：json、jsonc、table、tsv。 預設值：json。|
|    --query                               | JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 http://jmespath.org/。|
|    --verbose                             | 增加記錄詳細程度。 使用 --debug 取得完整偵錯記錄。|

## <a name="next-steps"></a>後續步驟
- [設定](service-fabric-cli.md) Service Fabric CLI。
- 了解如何使用[範例指令碼](/azure/service-fabric/scripts/sfctl-upgrade-application)來使用 Service Fabric CLI。