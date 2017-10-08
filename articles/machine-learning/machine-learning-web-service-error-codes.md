---
title: "機器學習 REST API 錯誤碼 aaaAzure |Microsoft 文件"
description: "Azure Machine Learning Web 服務上的作業可以傳回這些錯誤碼。"
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Machine Learning REST API 錯誤碼
 
hello 下列錯誤碼可能傳回的 Azure Machine Learning web 服務上的作業。
 
## <a name="badargument-http-status-code-400"></a>BadArgument (HTTP 狀態碼 400)
 
提供的引數無效。
 
此類錯誤表示某處提供的引數無效。 這可能是認證或 Azure 儲存體 toosomething 傳遞 toohello web 服務的位置。 請查看 hello 「 錯誤碼 」 欄位中 hello 「 詳細資料 」 一節 toodiagnose 哪一個特定的引數無效。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| BadParameterValue | 所提供的 hello 參數值不符合 hello 參數中的 hello 參數規則 |
| BadSubscriptionId | hello 訂用帳戶 Id，而且使用的 tooscore 不是一個 hello 資源中的 hello |
| BadVersionCall | 無效的版本參數已傳遞 hello API 呼叫期間: {0}。 請檢查的 hello API 說明頁的傳遞 hello 正確版本，並再試一次。 |
| BatchJobInputsNotSpecified | 未指定下列必要的輸入 hello 與 hello 要求: {0}。 請確定已指定所有的輸入資料，然後再試一次。 |
| BatchJobInputsTooManySpecified | hello 要求指定比 hello 服務中定義的多個輸入。 接受的輸入清單︰{0}。 請確定已正確指定所有的輸入資料，然後再試一次。 |
| BlobNameTooLong | 針對診斷輸出提供的 Azure Blob 儲存體路徑太長︰{0}。 請縮短 hello 路徑，然後再試一次。 |
| BlobNotFound | 無法 tooaccess hello 提供 Azure blob-{0}。  Azure 錯誤訊息：{1}。 |
| ContainerIsEmpty | 未提供 Azure 儲存體容器名稱。 提供有效的容器名稱，然後再試一次。 |
| ContainerSegmentInvalid | 容器名稱無效。 提供有效的容器名稱，然後再試一次。 |
| ContainerValidationFailed | Blob 容器驗證失敗，發生下列錯誤︰{0}。 |
| DataTypeNotSupported | 提供不支援的資料類型。 提供有效的資料類型，然後再試一次。 |
| DuplicateInputInBatchCall | hello 批次要求無效。 不能指定單一和多個輸入 hello 相同的時間。 其中一個項目移除 hello 要求並再試一次。 |
| ExpiryTimeInThePast | 提供的到期時間是在過去的 hello: {0}。 提供未來的到期時間 (UTC)，然後再試一次。 toonever 到期、 設定到期時間 tooNULL。 |
| IncompleteSettings | 診斷設定不完整。 |
| InputBlobRelativeLocationInvalid | 未提供 Azure 儲存體 Blob 名稱。 提供有效的 Blob 名稱，然後再試一次。 |
| InvalidBlob | Blob 的 Blob 規格 無效：{0}。 確認連接字串 / 相對路徑或 SAS 權杖規格正確無誤，然後再試一次。 |
| InvalidBlobConnectionString | hello hello 輸入/輸出內的 blob 無效的其中一個指定的連接字串: {0}。 請更正此錯誤，然後再試一次。 |
| InvalidBlobExtension | hello blob 參考： {0} 有無效或遺漏的檔案副檔名。 此輸出類型支援的檔案副檔名為："{1}"。 |
| InvalidInputNames | 無效的服務輸入 hello 要求中指定的名稱: {0}。 請將對應 hello 輸入的資料 toohello 正確的服務輸入，然後再試一次。 |
| InvalidOutputOverrideName | 輸出覆寫名稱無效︰{0}。 hello 服務沒有使用此名稱的輸出節點。 請傳遞正確的輸出節點名稱 toooverride （適用於區分大小寫）。 |
| InvalidQueryParameter | 查詢參數 '{0}' 無效。 {1} |
| MissingInputBlobInformation | Azure 儲存體 Blob 資訊遺失。 提供有效的連接字串和相對路徑或 URI，然後再試一次。 |
| MissingJobId | 未提供作業識別碼。 工作第一次提交工作 hello 時，會傳回識別碼。 請確認 hello 作業識別碼正確無誤，然後再試。 |
| MissingKeys | 未提供任何金鑰，或未提供其中一個主要或次要金鑰。 |
| MissingModelPackage | 未提供模型套件識別碼或模型套件。 提供有效的模型套件識別碼或模型套件，然後再試一次。 |
| MissingOutputOverrideSpecification | hello 要求缺少 hello blob 規格輸出覆寫 {0}。 請指定有效的 blob 位置與 hello 要求，或移除 hello 輸出規格，如果想要使用沒有位置覆寫。 |
| MissingRequestInput | hello web 服務預期的輸入，但沒有輸入提供。 請提供有效的輸入是根據發行的 hello 輸入 hello 模型中的連接埠，並再試一次。 |
| MissingRequiredGlobalParameters | 未提供所有必要的 Web 服務參數。 請確認 hello 參數必須有的 hello 模組無誤，然後再試一次。 |
| MissingRequiredOutputOverrides | 當呼叫它是強制性 toopass 中的加密的服務端點輸出會覆寫所有 hello 服務的輸出。 這些輸出此時遺漏覆寫︰{0} |
| MissingWebServiceGroupId | 未提供 Web 服務群組識別碼。 提供有效的 Web 服務群組識別碼，然後再試一次。 |
| MissingWebServiceId | 未提供 Web 服務識別碼。 提供有效的 Web 服務識別碼，然後再試一次。 |
| MissingWebServicePackage | 未提供 Web 服務套件。 提供有效的 Web 服務套件，然後再試一次。 |
| MissingWorkspaceId | 未提供工作區識別碼。 提供有效的工作區識別碼，然後再試一次。 |
| ModelConfigurationInvalid | Hello 模型封裝中的無效的型號設定。 請確定 hello 模型組態包含輸出端點定義、 標準錯誤端點和標準端點，並再試一次。 |
| ModelPackageIdInvalid | 模型套件識別碼無效。請確認該 hello 模型封裝識別碼正確，然後再試。 |
| RequestBodyInvalid | 不提供要求主體或 hello 要求本文還原序列化時發生錯誤。 |
| RequestIsEmpty | 未提供要求。 提供有效的要求，然後再試一次。 |
| UnexpectedParameter | 提供的參數並非預期。 確認所有參數名稱的拼寫都正確無誤，只傳遞預期的參數，然後再試一次。 |
| UnknownError | 未知的錯誤。 |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | 無法變更 {0} Web 服務的並行要求需求。 |
| WebServiceIdInvalid | 提供的 Web 服務識別碼無效。 Web 服務識別碼應該是有效的 guid。 |
| WebServiceTooManyConcurrentRequestRequirement | 無法設定同時並存要求需求 toomore 比 {0}。 |
| WebServiceTypeInvalid | 提供的 Web 服務類型無效。 請確認 hello 有效的 web 服務類型正確，然後再試。 有效的 Web 服務類型：{0}。 |
 
## <a name="baduserargument-http-status-code-400"></a>BadArgument (HTTP 狀態碼 400)
 
提供的使用者引數無效。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| InputMismatchError | 輸入資料不符合輸入連接埠結構描述。 |
| InputParseError | 剖析輸入向量失敗。  請確認 hello 輸入的向量的 hello 正確的資料行和資料類型的數目。  其他詳細資料：{0}。 |
| MissingRequiredGlobalParameters | 遺失的 hello web 服務所需要的參數。 請確認 hello web 服務所需要的所有必要的 hello 參數正確，再試一次。 |
| UnexpectedParameter | 確認只有 hello 必要 hello web 服務所需要的參數傳遞，並再試一次。 |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (HTTP 狀態碼 400)
 
hello 要求 hello 目前內容中無效。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| CannotStartJob | 無法啟動 hello 作業，因為它處於 {0} 狀態。 |
| IncompatibleModel | hello 模型是與 hello 要求版本不相容。 hello 要求版本只支援單一 datatable 輸出模型。 |
| MultipleInputsNotAllowed | hello 模型不允許多個輸入。 |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (HTTP 狀態碼 400)
 
模組執行發生內部程式庫錯誤。
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (HTTP 狀態碼 400)
 
模組執行發生錯誤。
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (HTTP狀態碼 400)
 
Web 服務套件無效。 請確認提供的 hello web 服務封裝正確，然後再試。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| FormatError | hello web 服務封裝格式不正確。 詳細資料︰{0} |
| RuntimesError | hello web 服務封裝圖表不正確。 詳細資料︰{0} |
| ValidationError | hello web 服務封裝圖表不正確。 詳細資料︰{0} |
 
## <a name="unauthorized-http-status-code-401"></a>未經授權 (HTTP 狀態碼 401)
 
要求是未經授權的 tooaccess 資源。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| AdminRequestUnauthorized | 未經授權 |
| ManagementRequestUnauthorized | 未經授權 |
| ScoreRequestUnauthorized | 提供的認證無效。 |
 
## <a name="notfound-http-status-code-404"></a>NotFound (HTTP 狀態碼 404)
 
找不到資源。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| ModelPackageNotFound | 找不到模型套件。 請確認 hello 模型封裝識別碼正確無誤，然後再試。 |
| WebServiceIdNotFoundInWorkspace | 在此工作區下找不到 Web 服務。 沒有 hello webServiceId 與 hello 工作區識別碼不符。 請確認所提供的 hello web 服務的一部分 hello 工作區，並再試一次。 |
| WebServiceNotFound | 找不到 Web 服務。 請確認 hello web 服務識別碼正確無誤，然後再試。 |
| WorkspaceNotFound | 找不到工作區。 請確認 hello 工作區識別碼正確無誤，然後再試。 |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (HTTP 狀態碼 408)
 
hello 允許的時間內無法完成 hello 作業。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| RequestCanceled | Hello 用戶端已取消要求。 |
| ScoreRequestTimeout | 執行要求已逾時。 |
 
## <a name="conflict-http-status-code-409"></a>衝突 (HTTP 狀態碼 409)
 
資源已經存在。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| ModelOutputMetadataMismatch | 輸出參數名稱無效。 請嘗試使用 hello 中繼資料編輯器模組 toorename 資料行，並再試一次。 |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (HTTP 狀態碼 413)
 
hello 模型已超過指派 tooit hello 記憶體配額。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| OutOfMemoryLimit | hello 模型耗用更多的記憶體比已 appropriated 它。 Hello 模型允許的最大記憶體是 {0} MB。 請檢查您的模型是否有問題。 |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (HTTP 狀態碼 500)
 
執行發生內部錯誤。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | hello 容器處理序當機，系統錯誤 |
| ContainerProcessTerminatedWithUnknownError | hello 容器處理序當機發生未知的錯誤 |
| ContainerValidationFailed | Blob 容器驗證失敗，發生下列錯誤︰{0}。 |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration，ConfigValue：{0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | 未提供引數。 確認已傳遞有效的引數，然後再試一次。 |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | 連接埠識別碼 = {0} 具有不支援的資料類型：{1}。 |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Swagger 產生失敗，詳細資料︰{0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | 未知的作業狀態碼為 {0}。 |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage，詳細資料︰{0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (HTTP 狀態碼 500)
 
執行發生內部錯誤。 系統記憶體不足。 請再試一次。
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (HTTP 狀態碼 500)
 
模型套件無效。 請確認提供的 hello 模型封裝正確，然後再試。
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (HTTP 狀態碼 500)
 
Web 服務套件無效。 請確認提供的 hello web 套件正確，然後再試。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| ModuleError | hello web 服務封裝圖表不正確。 詳細資料︰{0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (HTTP 狀態碼 503)
 
hello 要求無法以 hello 容器已初始化執行。
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (HTTP 狀態碼 503)
 
服務暫時無法使用。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| NoMoreResources | 要求沒有可用的資源。 |
| RequestThrottled | 要求已針對 {0} 端點進行節流處理。 hello hello 端點的最大並行是 {1}。 |
| TooManyConcurrentRequests | 傳送的並行要求太多。 |
| TooManyHostsBeingInitialized | 太多主機在初始化 hello 相同的時間。 考慮節流 / 重試。 |
| TooManyHostsBeingInitializedPerModel | 太多主機在初始化 hello 相同的時間。 考慮節流 / 重試。 |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (HTTP 狀態碼 504)
 
hello 允許的時間內無法完成 hello 作業。
 
| 錯誤碼 | 使用者訊息 |
| ---------- |--------------|
| BackendInitializationTimeout | hello 允許的時間內無法完成 hello web 服務的初始化。 |
| BackendScoreTimeout | hello 允許的時間內無法完成 hello web 服務要求執行。 |
 
