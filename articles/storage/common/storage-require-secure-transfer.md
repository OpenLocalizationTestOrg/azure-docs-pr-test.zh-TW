---
title: "在 Azure 儲存體 aaaRequire 保護傳輸 |Microsoft 文件"
description: "了解 hello 「 需要安全的傳輸 」 功能適用於 Azure 儲存體，以及如何 tooenable 它。"
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>需要安全傳輸

hello 「 安全傳輸需要 」 選項來加強 hello 安全性儲存體帳戶，只允許安全連線從 toohello 儲存體帳戶的要求。 例如，在呼叫 REST Api tooaccess 儲存體帳戶時，您必須使用 HTTPS 連接。 啟用 [需要安全傳輸] 時，會拒絕使用 HTTP 的所有要求。

當您使用 hello Azure 檔案服務時，任何未加密時連線失敗 」 保護所需的傳輸 」 已啟用。 這包括使用 SMB 2.1、 未加密，SMB 3.0 和 hello Linux SMB 用戶端的部分類別的案例。 

根據預設，hello 「 安全傳輸需要 」 選項已停用。

> [!NOTE]
> 因為 Azure 儲存體不針對自訂網域名稱支援 HTTPS，使用自訂網域名稱時不會套用此選項。

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>在 hello Azure 入口網站中啟用 「 安全傳輸需要 」

您可以啟用 hello 「 安全傳輸所需 」 設定同時，當您建立儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)，和現有的儲存體帳戶。

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>當您建立儲存體帳戶時要求使用安全傳輸

1. 開啟 hello**建立儲存體帳戶**hello Azure 入口網站中的刀鋒視窗。
1. 在 [需要安全傳輸] 下，選取 [已啟用]。

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>針對現有儲存體帳戶要求使用安全傳輸

1. 在 hello Azure 入口網站中選取現有的儲存體帳戶。
1. 選取**組態**下**設定**hello 儲存體帳戶功能表刀鋒視窗中。
1. 在 [需要安全傳輸] 下，選取 [已啟用]。

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>以程式設計方式啟用 [需要安全傳輸]

hello 設定名稱是_supportsHttpsTrafficOnly_儲存體帳戶屬性中。 可以透過 REST API、工具或程式庫啟用「需要安全傳輸」設定：

* **REST API** (版本：2016-12-01)：[發行套件](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (版本：4.1.0)：[發行套件](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (版本：2.0.11)：[發行套件](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (版本：1.1.0)：[發行套件](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK** (版本：6.3.0)：[發行套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (版本：1.1.0)：[發行套件](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK** (版本：0.11.0)：[發行套件](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>透過 REST API 啟用「需要安全傳輸」設定

toosimplify 測試透過 REST API，您可以使用[ArmClient](https://github.com/projectkudu/ARMClient) toocall 從命令列。

 您可以使用以 hello REST API 的命令列 toocheck hello 設定如下：

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

在 hello 回應，您可以找到_supportsHttpsTrafficOnly_設定。 範例：

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

您可以使用以 hello REST API 的命令列 tooenable hello 設定如下：

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Input.json 範例：
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>後續步驟
Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。 如需詳細資訊，請瀏覽 hello[存放安全性指南 》](storage-security-guide.md)。
