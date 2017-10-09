使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括區段稱為參數，其中包含所有 hello 參數值。
您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。 不會定義參數的值，會一律保持 hello 相同。 每個參數值用於 hello 範本 toodefine hello 部署的資源。 

當定義參數，使用 hello **allowedValues**欄位 toospecify 其中值的使用者可以在部署期間提供。 使用 hello **defaultValue**欄位 tooassign 值 toohello 參數，如果在部署期間未不提供任何值。

我們將說明 hello 範本中的每個參數。

### <a name="logicappname"></a>logicAppName
hello 邏輯應用程式 toocreate hello 名稱。

    "logicAppName": {
        "type": "string"
    }