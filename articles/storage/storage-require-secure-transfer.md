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
# <a name="require-secure-transfer"></a><span data-ttu-id="0e7dd-103">需要安全傳輸</span><span class="sxs-lookup"><span data-stu-id="0e7dd-103">Require secure transfer</span></span>

<span data-ttu-id="0e7dd-104">hello 「 安全傳輸需要 」 選項來加強 hello 安全性儲存體帳戶，只允許安全連線從 toohello 儲存體帳戶的要求。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="0e7dd-105">例如，在呼叫 REST Api tooaccess 儲存體帳戶時，您必須使用 HTTPS 連接。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="0e7dd-106">啟用 [需要安全傳輸] 時，會拒絕使用 HTTP 的所有要求。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="0e7dd-107">當您使用 hello Azure 檔案服務時，任何未加密時連線失敗 」 保護所需的傳輸 」 已啟用。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="0e7dd-108">這包括使用 SMB 2.1、 未加密，SMB 3.0 和 hello Linux SMB 用戶端的部分類別的案例。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="0e7dd-109">根據預設，hello 「 安全傳輸需要 」 選項已停用。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="0e7dd-110">因為 Azure 儲存體不針對自訂網域名稱支援 HTTPS，使用自訂網域名稱時不會套用此選項。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="0e7dd-111">在 hello Azure 入口網站中啟用 「 安全傳輸需要 」</span><span class="sxs-lookup"><span data-stu-id="0e7dd-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="0e7dd-112">您可以啟用 hello 「 安全傳輸所需 」 設定同時，當您建立儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)，和現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="0e7dd-113">當您建立儲存體帳戶時要求使用安全傳輸</span><span class="sxs-lookup"><span data-stu-id="0e7dd-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="0e7dd-114">開啟 hello**建立儲存體帳戶**hello Azure 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="0e7dd-115">在 [需要安全傳輸] 下，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="0e7dd-117">針對現有儲存體帳戶要求使用安全傳輸</span><span class="sxs-lookup"><span data-stu-id="0e7dd-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="0e7dd-118">在 hello Azure 入口網站中選取現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="0e7dd-119">選取**組態**下**設定**hello 儲存體帳戶功能表刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="0e7dd-120">在 [需要安全傳輸] 下，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![螢幕擷取畫面](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="0e7dd-122">以程式設計方式啟用 [需要安全傳輸]</span><span class="sxs-lookup"><span data-stu-id="0e7dd-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="0e7dd-123">hello 設定名稱是_supportsHttpsTrafficOnly_儲存體帳戶屬性中。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="0e7dd-124">可以透過 REST API、工具或程式庫啟用「需要安全傳輸」設定：</span><span class="sxs-lookup"><span data-stu-id="0e7dd-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="0e7dd-125">**REST API** (版本：2016-12-01)：[發行套件](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="0e7dd-126">**PowerShell** (版本：4.1.0)：[發行套件](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="0e7dd-127">**CLI** (版本：2.0.11)：[發行套件](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="0e7dd-128">**NodeJS** (版本：1.1.0)：[發行套件](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="0e7dd-129">**.NET SDK** (版本：6.3.0)：[發行套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="0e7dd-130">**Python SDK** (版本：1.1.0)：[發行套件](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="0e7dd-131">**Ruby SDK** (版本：0.11.0)：[發行套件](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="0e7dd-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="0e7dd-132">透過 REST API 啟用「需要安全傳輸」設定</span><span class="sxs-lookup"><span data-stu-id="0e7dd-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="0e7dd-133">toosimplify 測試透過 REST API，您可以使用[ArmClient](https://github.com/projectkudu/ARMClient) toocall 從命令列。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="0e7dd-134">您可以使用以 hello REST API 的命令列 toocheck hello 設定如下：</span><span class="sxs-lookup"><span data-stu-id="0e7dd-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="0e7dd-135">在 hello 回應，您可以找到_supportsHttpsTrafficOnly_設定。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="0e7dd-136">範例：</span><span class="sxs-lookup"><span data-stu-id="0e7dd-136">Sample:</span></span>

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

<span data-ttu-id="0e7dd-137">您可以使用以 hello REST API 的命令列 tooenable hello 設定如下：</span><span class="sxs-lookup"><span data-stu-id="0e7dd-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="0e7dd-138">Input.json 範例：</span><span class="sxs-lookup"><span data-stu-id="0e7dd-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="0e7dd-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e7dd-139">Next steps</span></span>
<span data-ttu-id="0e7dd-140">Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="0e7dd-141">如需詳細資訊，請瀏覽 hello[存放安全性指南 》](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="0e7dd-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
