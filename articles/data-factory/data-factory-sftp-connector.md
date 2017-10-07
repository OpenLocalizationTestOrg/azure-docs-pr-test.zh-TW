---
title: "從 SFTP 伺服器使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署或雲端 SFTP 伺服器使用 Azure Data Factory toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="11adc-103">使用 Azure Data Factory 從 SFTP 伺服器移動資料</span><span class="sxs-lookup"><span data-stu-id="11adc-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="11adc-104">本文概述如何在 Azure Data Factory toomove 資料從內部部署/雲端上的 SFTP 伺服器 tooa toouse hello 複製活動支援接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="11adc-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="11adc-105">這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。</span><span class="sxs-lookup"><span data-stu-id="11adc-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="11adc-106">資料處理站目前只支援移動資料從 SFTP 伺服器 tooother 資料存放區，但對於 tooan SFTP 伺服器會將資料從其他資料儲存。</span><span class="sxs-lookup"><span data-stu-id="11adc-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="11adc-107">它支援內部部署和雲端 SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="11adc-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="11adc-108">複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="11adc-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="11adc-109">如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="11adc-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="11adc-110">支援的案例和驗證類型</span><span class="sxs-lookup"><span data-stu-id="11adc-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="11adc-111">您可以使用此 SFTP 連接器 toocopy 資料從**這兩種雲端 SFTP 伺服器和內部部署 SFTP 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="11adc-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="11adc-112">**基本**和**SshPublicKey** toohello SFTP 伺服器連線時支援驗證類型。</span><span class="sxs-lookup"><span data-stu-id="11adc-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="11adc-113">複製資料時從 SFTP 伺服器在內部部署，您需要在 hello 在內部部署環境/Azure VM 中安裝資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="11adc-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="11adc-114">請參閱[資料管理閘道器](data-factory-data-management-gateway.md)如 hello 閘道的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11adc-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="11adc-115">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文件以取得逐步指示設定 hello 閘道並使用它。</span><span class="sxs-lookup"><span data-stu-id="11adc-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="11adc-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="11adc-116">Getting started</span></span>
<span data-ttu-id="11adc-117">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 SFTP 來源。</span><span class="sxs-lookup"><span data-stu-id="11adc-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="11adc-118">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="11adc-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="11adc-119">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="11adc-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="11adc-120">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="11adc-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="11adc-121">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="11adc-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="11adc-122">如 JSON 範例 toocopy 從 SFTP 伺服器 tooAzure Blob 儲存體的資料，請參閱 < [JSON 範例： 將資料從 SFTP 伺服器 tooAzure blob 複製](#json-example-copy-data-from-sftp-server-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="11adc-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="11adc-123">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-123">Linked service properties</span></span>
<span data-ttu-id="11adc-124">下表中的 hello 提供 JSON 項目特定 tooFTP 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="11adc-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="11adc-125">屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-125">Property</span></span> | <span data-ttu-id="11adc-126">說明</span><span class="sxs-lookup"><span data-stu-id="11adc-126">Description</span></span> | <span data-ttu-id="11adc-127">必要</span><span class="sxs-lookup"><span data-stu-id="11adc-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11adc-128">類型</span><span class="sxs-lookup"><span data-stu-id="11adc-128">type</span></span> | <span data-ttu-id="11adc-129">hello type 屬性必須設定得`Sftp`。</span><span class="sxs-lookup"><span data-stu-id="11adc-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="11adc-130">是</span><span class="sxs-lookup"><span data-stu-id="11adc-130">Yes</span></span> |
| <span data-ttu-id="11adc-131">主機</span><span class="sxs-lookup"><span data-stu-id="11adc-131">host</span></span> | <span data-ttu-id="11adc-132">Hello SFTP 伺服器的名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="11adc-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="11adc-133">是</span><span class="sxs-lookup"><span data-stu-id="11adc-133">Yes</span></span> |
| <span data-ttu-id="11adc-134">連接埠</span><span class="sxs-lookup"><span data-stu-id="11adc-134">port</span></span> |<span data-ttu-id="11adc-135">哪些 hello SFTP 伺服器正在接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="11adc-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="11adc-136">hello 預設值是： 21</span><span class="sxs-lookup"><span data-stu-id="11adc-136">hello default value is: 21</span></span> |<span data-ttu-id="11adc-137">否</span><span class="sxs-lookup"><span data-stu-id="11adc-137">No</span></span> |
| <span data-ttu-id="11adc-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="11adc-138">authenticationType</span></span> |<span data-ttu-id="11adc-139">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="11adc-139">Specify authentication type.</span></span> <span data-ttu-id="11adc-140">允許的值︰**Basic**、**SshPublicKey**。</span><span class="sxs-lookup"><span data-stu-id="11adc-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="11adc-141">請參閱太[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)分別區段上多個屬性和 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="11adc-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="11adc-142">是</span><span class="sxs-lookup"><span data-stu-id="11adc-142">Yes</span></span> |
| <span data-ttu-id="11adc-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="11adc-143">skipHostKeyValidation</span></span> | <span data-ttu-id="11adc-144">指定是否 tooskip 主機金鑰的驗證。</span><span class="sxs-lookup"><span data-stu-id="11adc-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="11adc-145">否。</span><span class="sxs-lookup"><span data-stu-id="11adc-145">No.</span></span> <span data-ttu-id="11adc-146">hello 預設值： false</span><span class="sxs-lookup"><span data-stu-id="11adc-146">hello default value: false</span></span> |
| <span data-ttu-id="11adc-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="11adc-147">hostKeyFingerprint</span></span> | <span data-ttu-id="11adc-148">指定 hello 指紋 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="11adc-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="11adc-149">是如果 hello `skipHostKeyValidation` toofalse 設定。</span><span class="sxs-lookup"><span data-stu-id="11adc-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="11adc-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="11adc-150">gatewayName</span></span> |<span data-ttu-id="11adc-151">名稱的 hello 資料管理閘道器 tooconnect tooan 內部 SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="11adc-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="11adc-152">如果從內部部署 SFTP 伺服器複製資料，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="11adc-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="11adc-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="11adc-153">encryptedCredential</span></span> | <span data-ttu-id="11adc-154">加密的認證 tooaccess hello SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="11adc-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="11adc-155">自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊中指定基本驗證 （使用者名稱 + 密碼） 或 SshPublicKey 驗證 （使用者名稱 + 私用金鑰的路徑或內容） 時。</span><span class="sxs-lookup"><span data-stu-id="11adc-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="11adc-156">否。</span><span class="sxs-lookup"><span data-stu-id="11adc-156">No.</span></span> <span data-ttu-id="11adc-157">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="11adc-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="11adc-158">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-158">Using basic authentication</span></span>

<span data-ttu-id="11adc-159">toouse 基本驗證時，設定`authenticationType`為`Basic`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="11adc-160">屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-160">Property</span></span> | <span data-ttu-id="11adc-161">說明</span><span class="sxs-lookup"><span data-stu-id="11adc-161">Description</span></span> | <span data-ttu-id="11adc-162">必要</span><span class="sxs-lookup"><span data-stu-id="11adc-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11adc-163">username</span><span class="sxs-lookup"><span data-stu-id="11adc-163">username</span></span> | <span data-ttu-id="11adc-164">具有存取 toohello SFTP 伺服器的使用者。</span><span class="sxs-lookup"><span data-stu-id="11adc-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="11adc-165">是</span><span class="sxs-lookup"><span data-stu-id="11adc-165">Yes</span></span> |
| <span data-ttu-id="11adc-166">password</span><span class="sxs-lookup"><span data-stu-id="11adc-166">password</span></span> | <span data-ttu-id="11adc-167">Hello 使用者 （使用者名稱） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="11adc-167">Password for hello user (username).</span></span> | <span data-ttu-id="11adc-168">是</span><span class="sxs-lookup"><span data-stu-id="11adc-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="11adc-169">範例：基本驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="11adc-170">範例：採用加密認證的基本驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="11adc-171">使用 SSH 公用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-171">Using SSH public key authentication</span></span>

<span data-ttu-id="11adc-172">toouse SSH 公開金鑰驗證、 設定`authenticationType`為`SshPublicKey`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="11adc-173">屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-173">Property</span></span> | <span data-ttu-id="11adc-174">說明</span><span class="sxs-lookup"><span data-stu-id="11adc-174">Description</span></span> | <span data-ttu-id="11adc-175">必要</span><span class="sxs-lookup"><span data-stu-id="11adc-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11adc-176">username</span><span class="sxs-lookup"><span data-stu-id="11adc-176">username</span></span> |<span data-ttu-id="11adc-177">使用者具有存取 toohello SFTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="11adc-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="11adc-178">是</span><span class="sxs-lookup"><span data-stu-id="11adc-178">Yes</span></span> |
| <span data-ttu-id="11adc-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="11adc-179">privateKeyPath</span></span> | <span data-ttu-id="11adc-180">指定絕對路徑 toohello 私密金鑰檔案可以存取該閘道。</span><span class="sxs-lookup"><span data-stu-id="11adc-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="11adc-181">指定任一個 hello`privateKeyPath`或`privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="11adc-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="11adc-182">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="11adc-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="11adc-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="11adc-183">privateKeyContent</span></span> | <span data-ttu-id="11adc-184">Hello 私用的索引鍵內容的序列化的字串。</span><span class="sxs-lookup"><span data-stu-id="11adc-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="11adc-185">hello 複製精靈可以讀取 hello 私密金鑰檔案，並自動擷取 hello 私用的索引鍵內容。</span><span class="sxs-lookup"><span data-stu-id="11adc-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="11adc-186">如果您使用任何其他工具/SDK，請改為使用 hello privateKeyPath 屬性。</span><span class="sxs-lookup"><span data-stu-id="11adc-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="11adc-187">指定任一個 hello`privateKeyPath`或`privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="11adc-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="11adc-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="11adc-188">passPhrase</span></span> | <span data-ttu-id="11adc-189">指定 hello 傳遞片語/密碼 toodecrypt hello 私密金鑰如果 hello 金鑰檔受複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="11adc-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="11adc-190">[是] 如果 hello 私密金鑰檔案受複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="11adc-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="11adc-191">SFTP 連接器僅支援 OpenSSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="11adc-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="11adc-192">請確定您的金鑰檔 hello 正確的格式。</span><span class="sxs-lookup"><span data-stu-id="11adc-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="11adc-193">您可以使用 Putty 工具 tooconvert 從.ppk tooOpenSSH 格式。</span><span class="sxs-lookup"><span data-stu-id="11adc-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="11adc-194">範例︰使用私密金鑰 filePath 的 SshPublicKey 驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="11adc-195">範例︰使用私密金鑰內容的 SshPublicKey 驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="11adc-196">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-196">Dataset properties</span></span>
<span data-ttu-id="11adc-197">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="11adc-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="11adc-198">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="11adc-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="11adc-199">hello **typeProperties**區段是不同的資料集的每個型別。</span><span class="sxs-lookup"><span data-stu-id="11adc-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="11adc-200">它提供特定 toohello 資料集類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="11adc-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="11adc-201">hello typeProperties 區段類型的資料集**FileShare**資料集具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="11adc-202">屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-202">Property</span></span> | <span data-ttu-id="11adc-203">說明</span><span class="sxs-lookup"><span data-stu-id="11adc-203">Description</span></span> | <span data-ttu-id="11adc-204">必要</span><span class="sxs-lookup"><span data-stu-id="11adc-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11adc-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="11adc-205">folderPath</span></span> |<span data-ttu-id="11adc-206">子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="11adc-206">Sub path toohello folder.</span></span> <span data-ttu-id="11adc-207">使用逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="11adc-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="11adc-208">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="11adc-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="11adc-209">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="11adc-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="11adc-210">是</span><span class="sxs-lookup"><span data-stu-id="11adc-210">Yes</span></span> |
| <span data-ttu-id="11adc-211">fileName</span><span class="sxs-lookup"><span data-stu-id="11adc-211">fileName</span></span> |<span data-ttu-id="11adc-212">在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="11adc-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="11adc-213">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="11adc-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="11adc-214">檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="11adc-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="11adc-215">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="11adc-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="11adc-216">否</span><span class="sxs-lookup"><span data-stu-id="11adc-216">No</span></span> |
| <span data-ttu-id="11adc-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="11adc-217">fileFilter</span></span> |<span data-ttu-id="11adc-218">指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="11adc-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="11adc-219">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="11adc-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="11adc-220">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="11adc-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="11adc-221">範例 2：`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="11adc-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="11adc-222">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="11adc-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="11adc-223">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="11adc-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="11adc-224">否</span><span class="sxs-lookup"><span data-stu-id="11adc-224">No</span></span> |
| <span data-ttu-id="11adc-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="11adc-225">partitionedBy</span></span> |<span data-ttu-id="11adc-226">partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="11adc-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="11adc-227">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="11adc-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="11adc-228">否</span><span class="sxs-lookup"><span data-stu-id="11adc-228">No</span></span> |
| <span data-ttu-id="11adc-229">format</span><span class="sxs-lookup"><span data-stu-id="11adc-229">format</span></span> | <span data-ttu-id="11adc-230">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="11adc-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="11adc-231">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="11adc-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="11adc-232">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="11adc-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="11adc-233">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="11adc-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="11adc-234">否</span><span class="sxs-lookup"><span data-stu-id="11adc-234">No</span></span> |
| <span data-ttu-id="11adc-235">compression</span><span class="sxs-lookup"><span data-stu-id="11adc-235">compression</span></span> | <span data-ttu-id="11adc-236">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="11adc-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="11adc-237">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="11adc-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="11adc-238">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="11adc-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="11adc-239">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="11adc-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="11adc-240">否</span><span class="sxs-lookup"><span data-stu-id="11adc-240">No</span></span> |
| <span data-ttu-id="11adc-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="11adc-241">useBinaryTransfer</span></span> |<span data-ttu-id="11adc-242">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="11adc-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="11adc-243">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="11adc-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="11adc-244">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="11adc-244">Default value: True.</span></span> <span data-ttu-id="11adc-245">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="11adc-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="11adc-246">否</span><span class="sxs-lookup"><span data-stu-id="11adc-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="11adc-247">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="11adc-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="11adc-248">使用 partionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-248">Using partionedBy property</span></span>
<span data-ttu-id="11adc-249">如 hello 前一節中所述，您可以指定動態 folderPath，與 partitionedBy 時間序列資料的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="11adc-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="11adc-250">您可以使用 hello Data Factory 巨集和 hello 系統變數 SliceStart，顯示 hello 給定的資料配量的邏輯時間期間的 SliceEnd。</span><span class="sxs-lookup"><span data-stu-id="11adc-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="11adc-251">toolearn 有關時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程及執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)文件。</span><span class="sxs-lookup"><span data-stu-id="11adc-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="11adc-252">範例 1：</span><span class="sxs-lookup"><span data-stu-id="11adc-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="11adc-253">在此範例與 hello 指定 hello 格式 (YYYYMMDDHH) 中的 Data Factory 系統變數 SliceStart 的值取代 {Slice}。</span><span class="sxs-lookup"><span data-stu-id="11adc-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="11adc-254">hello SliceStart 是指 toostart hello 配量時間。</span><span class="sxs-lookup"><span data-stu-id="11adc-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="11adc-255">hello folderPath 是不同的每個配量。</span><span class="sxs-lookup"><span data-stu-id="11adc-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="11adc-256">範例：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。</span><span class="sxs-lookup"><span data-stu-id="11adc-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="11adc-257">範例 2：</span><span class="sxs-lookup"><span data-stu-id="11adc-257">Sample 2:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="11adc-258">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="11adc-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="11adc-259">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="11adc-259">Copy activity properties</span></span>
<span data-ttu-id="11adc-260">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="11adc-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="11adc-261">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="11adc-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="11adc-262">而 hello hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="11adc-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="11adc-263">複製活動，根據 hello 類型的來源與接收 hello 類型屬性而有所不同。</span><span class="sxs-lookup"><span data-stu-id="11adc-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="11adc-264">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="11adc-264">Supported file and compression formats</span></span>
<span data-ttu-id="11adc-265">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11adc-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="11adc-266">JSON 範例： 從 SFTP 伺服器 tooAzure blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="11adc-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="11adc-267">hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="11adc-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="11adc-268">它們會顯示如何 toocopy 資料從 SFTP 來源 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="11adc-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="11adc-269">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="11adc-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11adc-270">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="11adc-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="11adc-271">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="11adc-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="11adc-272">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="11adc-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="11adc-273">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="11adc-274">[sftp](#linked-service-properties) 類型的已連結服務。</span><span class="sxs-lookup"><span data-stu-id="11adc-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="11adc-275">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="11adc-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="11adc-276">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="11adc-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="11adc-277">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="11adc-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="11adc-278">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="11adc-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="11adc-279">hello 範例將資料從 Azure blob 的 SFTP 伺服器 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="11adc-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="11adc-280">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="11adc-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="11adc-281">**SFTP 連結服務**</span><span class="sxs-lookup"><span data-stu-id="11adc-281">**SFTP linked service**</span></span>

<span data-ttu-id="11adc-282">這個範例會使用 hello 基本驗證的使用者名稱和密碼以純文字。</span><span class="sxs-lookup"><span data-stu-id="11adc-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="11adc-283">您也可以使用下列方式 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="11adc-284">基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="11adc-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="11adc-285">SSH 公用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="11adc-285">SSH public key authentication</span></span>

<span data-ttu-id="11adc-286">請參閱 [FTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="11adc-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="11adc-287">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="11adc-287">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="11adc-288">**SFTP 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="11adc-288">**SFTP input dataset**</span></span>

<span data-ttu-id="11adc-289">此資料集是指 toohello SFTP 資料夾`mysharedfolder`和檔案`test.csv`。</span><span class="sxs-lookup"><span data-stu-id="11adc-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="11adc-290">hello 管線複製 hello 檔案 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="11adc-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="11adc-291">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="11adc-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="11adc-292">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="11adc-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="11adc-293">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="11adc-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="11adc-294">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="11adc-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="11adc-295">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="11adc-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="11adc-296">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="11adc-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="11adc-297">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="11adc-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="11adc-298">在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="11adc-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="11adc-299">效能和微調</span><span class="sxs-lookup"><span data-stu-id="11adc-299">Performance and Tuning</span></span>
<span data-ttu-id="11adc-300">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="11adc-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11adc-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11adc-301">Next Steps</span></span>
<span data-ttu-id="11adc-302">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="11adc-302">See hello following articles:</span></span>

* <span data-ttu-id="11adc-303">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="11adc-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
