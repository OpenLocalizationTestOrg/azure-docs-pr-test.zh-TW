---
title: "開始使用 Azure CLI 批次的 aaaGet |Microsoft 文件"
description: "快速介紹 toohello 批次命令中取得 Azure CLI 管理 Azure Batch 服務資源"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>使用 Azure CLI 管理 Batch 資源

hello Azure CLI 2.0 是 Azure 的新命令列的體驗來管理 Azure 資源。 它可以用於 macOS、Linux 和 Windows。 Azure CLI 2.0 最適合用於與 hello 命令列管理 Azure 資源。 您可以使用 hello Azure CLI toomanage，您的 Azure Batch 帳戶與 toomanage 資源集區、 工作和工作等。 以 hello Azure CLI，您可以編寫指令碼的 hello 許多相同的工作，當您執行與 hello 批次應用程式開發介面、 Azure 入口網站和批次的 PowerShell cmdlet。

本文概述如何使用搭配 [Azure CLI 2.0 版](https://docs.microsoft.com/cli/azure/overview) 與 Batch。 請參閱[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)搭配 Azure 使用 hello CLI 的概觀。

Microsoft 建議使用的 hello Azure CLI 2.0 版的 hello 最新版本。 如需 2.0 版的詳細資訊，請參閱 [Azure Command Line 2.0 現已正式上市](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/)。

## <a name="set-up-hello-azure-cli"></a>Hello Azure CLI 設定

tooinstall hello Azure CLI，請依照下列所述的 hello 步驟[安裝 hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md)。

> [!TIP]
> 我們建議您更新您的 Azure CLI 安裝經常 tootake 的服務更新和增強功能的優點。
> 
> 

## <a name="command-help"></a>命令說明

您可以在 hello Azure CLI 中顯示每個命令的說明文字，藉由附加`-h`toohello 命令。 略過任何其他選項。 例如：

* hello tooget 說明`az`命令中，輸入：`az -h`
* 使用 tooget hello CLI 中的所有批次命令的清單：`az batch -h`
* tooget 說明建立批次帳戶，請輸入：`az batch account create -h`

有疑問，請使用 hello`-h`任何 Azure CLI 命令的命令列選項 tooget 說明。

> [!NOTE]
> 舊版的 hello 使用 Azure CLI `azure` toopreface CLI 命令。 在 2.0 版中，所有命令的前面現在都會加上 `az`。 為確定 tooupdate 您指令碼 toouse hello 新語法與 2.0 版。
>
>  

此外，參考 toohello Azure CLI 參考文件，如需詳細資訊，關於[Azure CLI 命令的批次](https://docs.microsoft.com/cli/azure/batch)。 

## <a name="log-in-and-authenticate"></a>登入和驗證

toouse hello Azure CLI 批次，需要在 toolog 和驗證。 有兩個簡單步驟 toofollow:

1. **登入 Azure。** 登入 Azure 可讓您存取 tooAzure 資源管理員命令，包括[批次管理服務](batch-management-dotnet.md)命令。  
2. **登入您的 Batch 帳戶。** 您登入您的批次帳戶可讓存取 tooBatch 服務命令。   

### <a name="log-in-tooazure"></a>登入 tooAzure

有幾個不同的方式 toolog 至 Azure 中有詳細, 說明[登入 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [以互動方式登入](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in)。 登入以互動方式執行時 Azure CLI 命令自行從 hello 命令列。
2. [使用服務主體來登入](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal)。 當您從指令碼或應用程式執行 Azure CLI 命令時，使用服務主體來登入。

Hello 本文的目的，我們會顯示如何 toolog 至 Azure 以互動方式。 型別[az 登入](https://docs.microsoft.com/cli/azure/#login)hello 命令列上：

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

hello`az login`命令傳回，如下所示，您可以使用 tooauthenticate，語彙基元。 請依照 hello 所提供的指示 tooopen 網頁，並送出 hello 語彙基元 tooAzure:

![登入 tooAzure](./media/batch-cli-get-started/az-login.png)

列出 hello hello 範例[範例殼層指令碼](#sample-shell-scripts)區段也顯示如何 toostart 您的 Azure CLI 工作階段，以互動方式登入 Azure。 一旦您登入，您可以呼叫命令 toowork 批次管理資源，包括批次帳戶、 金鑰、 應用程式封裝，以及配額。  

### <a name="log-in-tooyour-batch-account"></a>登入 tooyour 批次帳戶

toouse hello Azure CLI toomanage 批次資源，例如集區、 工作和工作，您需要 toolog 到您的 Batch 帳戶進行驗證。 toolog toohello 批次服務中的使用 hello [az 批次帳戶登入](https://docs.microsoft.com/cli/azure/batch/account#login)命令。 

您有兩個對 Batch 帳戶進行驗證的選項︰

- **使用 Azure Active Directory (Azure AD) 驗證。** 

    向 Azure AD 是 hello 預設值，當您使用 Azure CLI hello 與批次，並在大部分情況下建議使用。 
    
    當您登入 tooAzure，以互動方式 hello 上一節中所述時，您的認證會快取，因此 hello Azure CLI 可以讓您登入 tooyour 批次帳戶使用這些相同的認證。 如果您登入使用服務主體的 tooAzure，這些認證也會使用的 toolog tooyour 批次帳戶中。

    Azure AD 的優點就是它會提供角色型存取控制 (RBAC)。 使用 RBAC，使用者的存取權視其指派的角色，而不是他們擁有 hello 帳戶金鑰。 您可以管理 RBAC 角色，並且讓 Azure AD 處理存取和驗證，而不用管理帳戶金鑰。  

    使用 Azure AD 進行驗證時需要您建立您的 Azure 批次帳戶的集區配置模式下設定 too'User 訂用帳戶 '。 

    toolog tooyour 批次中的使用 Azure AD 的帳戶，請呼叫 hello [az 批次帳戶登入](https://docs.microsoft.com/cli/azure/batch/account#login)命令： 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **使用共用金鑰驗證。**

    [共用的金鑰驗證](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key)的批次服務會使用您的帳戶存取金鑰 hello tooauthenticate Azure CLI 命令。

    如果您正在建立 Azure CLI 指令碼 tooautomate 呼叫的批次命令，您可以使用共用金鑰驗證或 Azure AD 服務主體。 在某些情況下，使用共用金鑰驗證可能會比建立服務主體簡單。  

    在使用共用金鑰驗證 toolog 包含 hello `--shared-key-auth` hello 命令列選項：

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

列出 hello hello 範例[範例殼層指令碼](#sample-shell-scripts)一節說明如何 toolog 到您的 Batch 帳戶與 hello Azure CLI 兩者都使用 Azure AD 和共用金鑰。

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>使用 Azure Batch CLI 範本和檔案傳輸 (預覽)

您可以使用 hello Azure CLI toorun 批次作業端對端，而不需要撰寫程式碼。 批次範本檔案支援建立集區、 工作和工作以 hello Azure CLI。 您也可以使用 hello Azure CLI tooupload 作業輸入的檔 toohello hello 與相關聯的 Azure 儲存體帳戶的批次帳戶，並下載作業輸出檔。 如需詳細資訊，請參閱[使用 Azure Batch CLI 範本和檔案傳輸 (預覽)](batch-cli-templates.md)。

## <a name="sample-shell-scripts"></a>範例 shell 指令碼

hello 範例指令碼列出下列表格顯示 hello toouse Azure CLI 命令搭配 hello 批次服務和批次管理服務 tooaccomplish 一般工作的方式。 這些範例指令碼，涵蓋許多 hello Azure CLI 批次中可用的 hello 命令。 

| 指令碼 | 注意事項 |
|---|---|
| [建立 Batch 帳戶](./scripts/batch-cli-sample-create-account.md) | 建立 Batch 帳戶並將它與儲存體帳戶產生關聯。 |
| [新增應用程式](./scripts/batch-cli-sample-add-application.md) | 新增應用程式，並上傳封裝的二進位檔。|
| [管理 Batch 集區](./scripts/batch-cli-sample-manage-pool.md) | 示範建立、調整大小和管理集區。 |
| [使用 Batch 執行工作和作業](./scripts/batch-cli-sample-run-job.md) | 示範執行工作及新增作業。 |

## <a name="json-files-for-resource-creation"></a>用於建立資源的 JSON 檔案

當您建立批次資源，例如集區和工作時，您可以指定包含 hello 新資源的設定，而不是它的參數傳遞做為命令列選項在 JSON 檔案。 例如：

```azurecli
az batch pool create my_batch_pool.json
```

雖然您可以建立最多使用只有命令列選項的批次資源，某些功能需要您指定 JSON 格式的檔案，其中包含 hello 資源詳細資料。 例如，您必須使用 JSON 檔案，如果您想要啟動工作的 toospecify 資源檔案。

toosee hello JSON 語法需 toocreate 資源，請參閱 toohello[批次 REST API 參考][ rest_api]文件。 每個 「 新增*資源類型*"hello REST API 參考資料中的主題包含範例 JSON 指令碼來建立該資源。 您可以使用這些範例 JSON 指令碼做為範本，如 JSON 檔案 toouse 以 hello Azure CLI。 例如，toosee hello 集區建立的 JSON 語法，請參閱太[加入集區 tooan 帳戶][rest_add_pool]。

如需可指定 JSON 檔案的範例指令碼，請參閱[使用 Batch 執行作業和工作](./scripts/batch-cli-sample-run-job.md)。

> [!NOTE]
> 如果當您建立的資源，您會指定 JSON 檔案，則會忽略您在該資源的 hello 命令列指定的任何其他參數。
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>有效率的 Batch 資源查詢

每個 Batch 資源類型都支援 `list` 命令，已查詢 Batch 帳戶並列出該類型的資源。 例如，您可以列出 hello 集區中您的帳戶和 hello 工作中的工作：

```azurecli
az batch pool list
az batch task list --job-id job001
```

當您查詢與 hello 批次服務`list`作業，您可以指定 OData 子句 toolimit hello 傳回的資料量。 因為所有的篩選發生伺服器端，所以只會 hello 您要求的資料不符合 hello 網路。 使用這些子句 toosave 頻寬 （並因此時間） 當您執行的作業清單。

hello 下表描述支援的 hello 批次服務的 hello OData 子句：

| 子句 | 說明 |
|---|---|
| `--select-clause [select-clause]` | 傳回每個實體的屬性子集。 |
| `--filter-clause [filter-clause]` | 傳回符合 hello 的唯一實體指定的 OData 運算式。 |
| `--expand-clause [expand-clause]` | 取得基礎的單一 REST 呼叫中的 hello 實體資訊。 hello expand 的子句目前支援僅 hello`stats`屬性。 |

如需範例指令碼如何 toouse OData 子句中，請參閱該顯示[與批次執行工作和工作](./scripts/batch-cli-sample-run-job.md)。

如需有關如何執行有效率的清單以 OData 子句的查詢的詳細資訊，請參閱[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)。

## <a name="troubleshooting-tips"></a>疑難排解秘訣

hello 下列秘訣可以協助您疑難排解 Azure CLI 問題時：

* 使用`-h`tooget**說明文字**任何 CLI 命令
* 使用`-v`和`-vv`toodisplay **verbose**命令輸出。 當 hello`-vv`旗標之後，hello Azure CLI 顯示 hello 實際 REST 要求和回應。 這些參數方便用於顯示完整的錯誤輸出。
* 您可以檢視**命令為 JSON 輸出**以 hello`--json`選項。 例如， `az batch pool show pool001 --json` 會以 JSON 格式顯示 pool001 的屬性。 您可以複製並修改在此輸出 toouse `--json-file` (請參閱[JSON 檔案](#json-files)稍早在本文章)。
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* hello [Batch 論壇][ batch_forum]監視的批次小組成員。 如果您遇到問題或需要特定作業的協助，您可以在此張貼您的問題。

## <a name="next-steps"></a>後續步驟

* 如需 hello Azure CLI 的詳細資訊，請參閱 hello [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。
* 如需 Batch 資源的詳細資訊，請參閱[適用於開發人員的 Azure Batch 概觀](batch-api-basics.md)。
* 如需使用批次範本 toocreate 集區、 工作和工作，而不需要撰寫程式碼的詳細資訊，請參閱[使用 Azure 批次 CLI 範本和檔案傳輸 （預覽）](batch-cli-templates.md)。

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
