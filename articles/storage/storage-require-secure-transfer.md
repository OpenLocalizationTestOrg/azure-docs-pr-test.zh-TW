---
title: "在 Azure 儲存體中要求使用安全傳輸 |Microsoft 文件"
description: "了解 Azure 儲存體的「需要安全傳輸」功能，以及如何啟用它。"
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
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="90982-103">需要安全傳輸</span><span class="sxs-lookup"><span data-stu-id="90982-103">Require secure transfer</span></span>

<span data-ttu-id="90982-104">「需要安全傳輸」選項透過只允許從安全連線對儲存體帳戶進行要求，來加強儲存體帳戶的安全性。</span><span class="sxs-lookup"><span data-stu-id="90982-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="90982-105">例如，呼叫 REST API 來存取儲存體帳戶時，您必須使用 HTTPS 連線。</span><span class="sxs-lookup"><span data-stu-id="90982-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="90982-106">啟用 [需要安全傳輸] 時，會拒絕使用 HTTP 的所有要求。</span><span class="sxs-lookup"><span data-stu-id="90982-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="90982-107">當您在啟用 [需要安全傳輸] 的情況下使用 Azure 檔案服務時，任何未加密的連線都會失敗。</span><span class="sxs-lookup"><span data-stu-id="90982-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="90982-108">這包括使用 SMB 2.1、無加密的 SMB 3.0 和某些 Linux SMB 用戶端類型的情況。</span><span class="sxs-lookup"><span data-stu-id="90982-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="90982-109">根據預設，[需要安全傳輸] 選項是停用的。</span><span class="sxs-lookup"><span data-stu-id="90982-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="90982-110">因為 Azure 儲存體不針對自訂網域名稱支援 HTTPS，使用自訂網域名稱時不會套用此選項。</span><span class="sxs-lookup"><span data-stu-id="90982-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="90982-111">在 Azure 入口網站中啟用 [需要安全傳輸]</span><span class="sxs-lookup"><span data-stu-id="90982-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="90982-112">不論是在 [Azure 入口網站](https://portal.azure.com)建立儲存體帳戶，或是針對現有儲存體帳戶，您都可以啟用 [需要安全傳輸] 設定。</span><span class="sxs-lookup"><span data-stu-id="90982-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="90982-113">當您建立儲存體帳戶時要求使用安全傳輸</span><span class="sxs-lookup"><span data-stu-id="90982-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="90982-114">在 Azure 入口網站中開啟 [建立儲存體帳戶] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90982-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="90982-115">在 [需要安全傳輸] 下，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="90982-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="90982-117">針對現有儲存體帳戶要求使用安全傳輸</span><span class="sxs-lookup"><span data-stu-id="90982-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="90982-118">在 Azure 入口網站中選取現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="90982-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="90982-119">在儲存體帳戶功能表刀鋒視窗的 [設定] 下選取 [組態]。</span><span class="sxs-lookup"><span data-stu-id="90982-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="90982-120">在 [需要安全傳輸] 下，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="90982-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="90982-122">以程式設計方式啟用 [需要安全傳輸]</span><span class="sxs-lookup"><span data-stu-id="90982-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="90982-123">設定名稱為儲存體帳戶屬性中的 _supportsHttpsTrafficOnly_。</span><span class="sxs-lookup"><span data-stu-id="90982-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="90982-124">可以透過 REST API、工具或程式庫啟用「需要安全傳輸」設定：</span><span class="sxs-lookup"><span data-stu-id="90982-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="90982-125">**REST API** (版本：2016-12-01)：[發行套件](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="90982-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="90982-126">**PowerShell** (版本：4.1.0)：[發行套件](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="90982-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="90982-127">**CLI** (版本：2.0.11)：[發行套件](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="90982-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="90982-128">**NodeJS** (版本：1.1.0)：[發行套件](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="90982-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="90982-129">**.NET SDK** (版本：6.3.0)：[發行套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="90982-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="90982-130">**Python SDK** (版本：1.1.0)：[發行套件](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="90982-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="90982-131">**Ruby SDK** (版本：0.11.0)：[發行套件](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="90982-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="90982-132">透過 REST API 啟用「需要安全傳輸」設定</span><span class="sxs-lookup"><span data-stu-id="90982-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="90982-133">若要透過 REST API 簡化測試，可以使用 [ArmClient](https://github.com/projectkudu/ARMClient) 從命令列呼叫。</span><span class="sxs-lookup"><span data-stu-id="90982-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="90982-134">您可以使用下列命令列透過 REST API 檢查設定：</span><span class="sxs-lookup"><span data-stu-id="90982-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="90982-135">在回應中可以找到 _supportsHttpsTrafficOnly_ 設定。</span><span class="sxs-lookup"><span data-stu-id="90982-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="90982-136">範例：</span><span class="sxs-lookup"><span data-stu-id="90982-136">Sample:</span></span>

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

<span data-ttu-id="90982-137">您可以使用下列命令列透過 REST API 啟用設定：</span><span class="sxs-lookup"><span data-stu-id="90982-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="90982-138">Input.json 範例：</span><span class="sxs-lookup"><span data-stu-id="90982-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="90982-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90982-139">Next steps</span></span>
<span data-ttu-id="90982-140">Azure 儲存體提供一組完整的安全性功能，這些功能讓開發人員能夠建置安全應用程式。</span><span class="sxs-lookup"><span data-stu-id="90982-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="90982-141">如需詳細資訊，請參閱[儲存體安全性指南](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="90982-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
