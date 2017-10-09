### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
hello **Azure 儲存體連結服務**可讓您使用 hello 的 Azure 儲存體帳戶 tooan Azure data factory toolink**帳戶金鑰**，可以提供與全域存取 toohello Azure 的 hello 資料處理站儲存體。 下表中的 hello 提供 JSON 項目特定 tooAzure 儲存體連結服務的描述。

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 類型屬性必須設定為： **AzureStorage** |是 |
| connectionString |指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。 |是 |

請參閱下列文章步驟 tooview/複製 hello 帳戶金鑰的 Azure 儲存體的 hello:[檢視、 複製和重新產生儲存體存取金鑰](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account)。

**範例：**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Azure 儲存體 SAS 連結服務
共用的存取簽章 (SAS) 提供儲存體帳戶中的委派的存取 tooresources。 它可讓 toogrant 用戶端在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects 限制而不需要 tooshare 帳戶存取金鑰。 hello SAS 是包含在其查詢參數中所有的 hello 資訊所需的已驗證的存取 tooa 儲存體資源的 URI。 tooaccess 以 hello SAS 存放裝置資源，hello 用戶端只需要 toopass hello SAS toohello 適當建構函式或方法中。 如需 SAS 的詳細資訊，請參閱[共用存取簽章： 了解 hello SAS 模型](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory 現在僅支援 **服務 SAS**，但不支援帳戶 SAS。 請參閱[共用存取簽章的型別](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures)這兩種類型的詳細資料以及如何 tooconstruct。 請注意 hello generable 從 Azure 入口網站的 SAS URL，或儲存體總管是帳戶 SAS，但不支援。
> 

hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。 它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。 下表中的 hello 提供 JSON 項目特定 tooAzure 儲存體 SAS 連結服務的描述。 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 類型屬性必須設定為： **AzureStorageSas** |是 |
| sasUri |指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。  |是 |

**範例：**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

建立時**SAS URI**，考慮下列 hello:  

* 設定適當的讀取/寫入**權限**上根據物件 hello 已連結的服務 （讀取、 寫入、 讀取/寫入） 如何用於您的 data factory。
* 設定適當的 [過期時間]。 請確定 hello hello 管線的作用中的期間內不會過期 hello 存取 tooAzure 儲存物件。
* Uri 應建立在 hello 右 「 容器 /blob 或資料表層級根據 hello 需要。 Azure blob 的 SAS Uri tooan 允許 hello Data Factory 服務 tooaccess 該特定的 blob。 SAS Uri tooan Azure blob 容器可讓 hello Data Factory 服務 tooiterate 透過該容器中的 blob。 如果您需要更大的 tooprovide 存取/較少的更新版本中，物件或更新 hello SAS URI，請記住 tooupdate hello 連結服務與 hello 新的 URI。   

