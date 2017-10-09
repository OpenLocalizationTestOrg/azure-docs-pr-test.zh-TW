使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括區段稱為參數，其中包含所有 hello 參數值。
您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。 不會定義參數的值，會一律保持 hello 相同。 每個參數值用於 hello 範本 toodefine hello 資源部署。 

當定義參數，使用 hello **allowedValues**欄位 toospecify 其中值的使用者可以在部署期間提供。 使用 hello **defaultValue**欄位 tooassign 值 toohello 參數，如果在部署期間未不提供任何值。

我們將說明 hello 範本中的每個參數。

### <a name="sitename"></a>siteName
hello，您會希望 toocreate hello web 應用程式名稱。

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
hello 名稱 hello 應用程式服務計劃 toouse 裝載 hello web 應用程式。

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
定價層裝載計劃的 hello。

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

hello 範本定義此參數，以允許的 hello 值，並指派的預設值 (S1)，如果未不指定任何值。

### <a name="workersize"></a>workerSize
hello hello 裝載計劃 （小型、 中型或大型） 的執行個體大小。

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

hello 範本可定義 hello （0、 1 或 2），此參數允許的值，並指派的預設值 (0)，如果未不指定任何值。 hello 值相對應 toosmall 中型和大型。

