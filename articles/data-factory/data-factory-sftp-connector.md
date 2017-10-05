---
title: "使用 Azure Data Factory 從 SFTP 伺服器移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從內部部署或雲端 SFTP 伺服器移動資料。"
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
ms.openlocfilehash: 3a73311342489af031ed2ea1489e56292ebf2e09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="a34fd-103">使用 Azure Data Factory 從 SFTP 伺服器移動資料</span><span class="sxs-lookup"><span data-stu-id="a34fd-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="a34fd-104">本文概述如何使用 Azure Data Factory 中的複製活動，將內部部署/雲端 SFTP 伺服器中的資料移動到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a34fd-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud SFTP server to a supported sink data store.</span></span> <span data-ttu-id="a34fd-105">本文是根據 [資料移動活動](data-factory-data-movement-activities.md)一文，該文呈現使用複製活動移動資料的一般概觀以及支援作為來源/接收的資料存放區清單。</span><span class="sxs-lookup"><span data-stu-id="a34fd-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a34fd-106">資料處理站目前只支援將資料從 SFTP 伺服器移到其他資料存放區，而不支援將資料從其他資料存放區移到 SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a34fd-106">Data factory currently supports only moving data from an SFTP server to other data stores, but not for moving data from other data stores to an SFTP server.</span></span> <span data-ttu-id="a34fd-107">它支援內部部署和雲端 SFTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a34fd-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="a34fd-108">來源檔案成功複製至目的地後，「複製活動」不會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="a34fd-108">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="a34fd-109">如果您需要在成功複製後刪除來源檔案，請建立自訂活動來刪除檔案，並在管道中使用該活動。</span><span class="sxs-lookup"><span data-stu-id="a34fd-109">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="a34fd-110">支援的案例和驗證類型</span><span class="sxs-lookup"><span data-stu-id="a34fd-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="a34fd-111">您可以使用此 SFTP 連接器，從**雲端 SFTP 伺服器和內部部署 SFTP 伺服器**複製資料。</span><span class="sxs-lookup"><span data-stu-id="a34fd-111">You can use this SFTP connector to copy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="a34fd-112">連線至 SFTP 伺服器時支援 **Basic** 和 **SshPublicKey** 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="a34fd-112">**Basic** and **SshPublicKey** authentication types are supported when connecting to the SFTP server.</span></span>

<span data-ttu-id="a34fd-113">從內部部署 SFTP 伺服器複製資料時，您需要在內部部署環境/Azure VM 中安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="a34fd-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="a34fd-114">如需資料管理閘的詳細資料，請參閱[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on the gateway.</span></span> <span data-ttu-id="a34fd-115">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)一文來了解設定和使用閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a34fd-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a34fd-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="a34fd-116">Getting started</span></span>
<span data-ttu-id="a34fd-117">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 SFTP 來源。</span><span class="sxs-lookup"><span data-stu-id="a34fd-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="a34fd-118">若要建立管線，最簡單的方式就是使用**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a34fd-119">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="a34fd-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="a34fd-120">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a34fd-121">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="a34fd-122">若要將資料從 SFTP 伺服器複製到 Azure Blob 儲存體的 JSON 範例，請參閱本文的 [JSON 範例：將資料從 SFTP 伺服器複製到 Azure Blob](#json-example-copy-data-from-sftp-server-to-azure-blob)一節。</span><span class="sxs-lookup"><span data-stu-id="a34fd-122">For JSON samples to copy data from SFTP server to Azure Blob Storage, see [JSON Example: Copy data from SFTP server to Azure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a34fd-123">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-123">Linked service properties</span></span>
<span data-ttu-id="a34fd-124">下表提供 FTP 連結服務專屬 JSON 元素的說明。</span><span class="sxs-lookup"><span data-stu-id="a34fd-124">The following table provides description for JSON elements specific to FTP linked service.</span></span>

| <span data-ttu-id="a34fd-125">屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-125">Property</span></span> | <span data-ttu-id="a34fd-126">說明</span><span class="sxs-lookup"><span data-stu-id="a34fd-126">Description</span></span> | <span data-ttu-id="a34fd-127">必要</span><span class="sxs-lookup"><span data-stu-id="a34fd-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a34fd-128">類型</span><span class="sxs-lookup"><span data-stu-id="a34fd-128">type</span></span> | <span data-ttu-id="a34fd-129">類型屬性必須設為 `Sftp`。</span><span class="sxs-lookup"><span data-stu-id="a34fd-129">The type property must be set to `Sftp`.</span></span> |<span data-ttu-id="a34fd-130">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-130">Yes</span></span> |
| <span data-ttu-id="a34fd-131">主機</span><span class="sxs-lookup"><span data-stu-id="a34fd-131">host</span></span> | <span data-ttu-id="a34fd-132">SFTP 伺服器的名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a34fd-132">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="a34fd-133">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-133">Yes</span></span> |
| <span data-ttu-id="a34fd-134">連接埠</span><span class="sxs-lookup"><span data-stu-id="a34fd-134">port</span></span> |<span data-ttu-id="a34fd-135">SFTP 伺服器所接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="a34fd-135">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="a34fd-136">預設值：21</span><span class="sxs-lookup"><span data-stu-id="a34fd-136">The default value is: 21</span></span> |<span data-ttu-id="a34fd-137">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-137">No</span></span> |
| <span data-ttu-id="a34fd-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a34fd-138">authenticationType</span></span> |<span data-ttu-id="a34fd-139">指定驗證類型。</span><span class="sxs-lookup"><span data-stu-id="a34fd-139">Specify authentication type.</span></span> <span data-ttu-id="a34fd-140">允許的值︰**Basic**、**SshPublicKey**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="a34fd-141">請參閱[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)章節，分別取得更多屬性和 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="a34fd-141">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="a34fd-142">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-142">Yes</span></span> |
| <span data-ttu-id="a34fd-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="a34fd-143">skipHostKeyValidation</span></span> | <span data-ttu-id="a34fd-144">指定是否略過主機金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="a34fd-144">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="a34fd-145">否。</span><span class="sxs-lookup"><span data-stu-id="a34fd-145">No.</span></span> <span data-ttu-id="a34fd-146">預設值：false</span><span class="sxs-lookup"><span data-stu-id="a34fd-146">The default value: false</span></span> |
| <span data-ttu-id="a34fd-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="a34fd-147">hostKeyFingerprint</span></span> | <span data-ttu-id="a34fd-148">指定主機金鑰的指紋。</span><span class="sxs-lookup"><span data-stu-id="a34fd-148">Specify the finger print of the host key.</span></span> | <span data-ttu-id="a34fd-149">如果 `skipHostKeyValidation` 設為 false，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="a34fd-149">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="a34fd-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a34fd-150">gatewayName</span></span> |<span data-ttu-id="a34fd-151">要連線至內部部署 SFTP 伺服器的資料管理閘道名稱。</span><span class="sxs-lookup"><span data-stu-id="a34fd-151">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="a34fd-152">如果從內部部署 SFTP 伺服器複製資料，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="a34fd-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="a34fd-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a34fd-153">encryptedCredential</span></span> | <span data-ttu-id="a34fd-154">用來存取 SFTP 伺服器的加密認證。</span><span class="sxs-lookup"><span data-stu-id="a34fd-154">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="a34fd-155">當您在複製精靈或 ClickOnce 快顯對話方塊中指定基本驗證 (使用者名稱 + 密碼) 或 SshPublicKey 驗證 (使用者名稱 + 私密金鑰路徑或內容) 時自動產生。</span><span class="sxs-lookup"><span data-stu-id="a34fd-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="a34fd-156">否。</span><span class="sxs-lookup"><span data-stu-id="a34fd-156">No.</span></span> <span data-ttu-id="a34fd-157">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="a34fd-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="a34fd-158">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-158">Using basic authentication</span></span>

<span data-ttu-id="a34fd-159">若要使用基本驗證，將 `authenticationType` 設定為 `Basic`，然後指定上一節中介紹的 SFTP 連接器泛用以外的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="a34fd-159">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="a34fd-160">屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-160">Property</span></span> | <span data-ttu-id="a34fd-161">說明</span><span class="sxs-lookup"><span data-stu-id="a34fd-161">Description</span></span> | <span data-ttu-id="a34fd-162">必要</span><span class="sxs-lookup"><span data-stu-id="a34fd-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a34fd-163">username</span><span class="sxs-lookup"><span data-stu-id="a34fd-163">username</span></span> | <span data-ttu-id="a34fd-164">可存取 SFTP 伺服器的使用者。</span><span class="sxs-lookup"><span data-stu-id="a34fd-164">User who has access to the SFTP server.</span></span> |<span data-ttu-id="a34fd-165">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-165">Yes</span></span> |
| <span data-ttu-id="a34fd-166">password</span><span class="sxs-lookup"><span data-stu-id="a34fd-166">password</span></span> | <span data-ttu-id="a34fd-167">使用者 (使用者名稱) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="a34fd-167">Password for the user (username).</span></span> | <span data-ttu-id="a34fd-168">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="a34fd-169">範例：基本驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-169">Example: Basic authentication</span></span>
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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="a34fd-170">範例：採用加密認證的基本驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-170">Example: Basic authentication with encrypted credential</span></span>

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

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="a34fd-171">使用 SSH 公用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-171">Using SSH public key authentication</span></span>

<span data-ttu-id="a34fd-172">若要使用 SSH 公開金鑰驗證，將 `authenticationType` 設定為 `SshPublicKey`，然後指定上一節中介紹的 SFTP 連接器泛用以外的下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="a34fd-172">To use SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="a34fd-173">屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-173">Property</span></span> | <span data-ttu-id="a34fd-174">說明</span><span class="sxs-lookup"><span data-stu-id="a34fd-174">Description</span></span> | <span data-ttu-id="a34fd-175">必要</span><span class="sxs-lookup"><span data-stu-id="a34fd-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a34fd-176">username</span><span class="sxs-lookup"><span data-stu-id="a34fd-176">username</span></span> |<span data-ttu-id="a34fd-177">可存取 SFTP 伺服器的使用者</span><span class="sxs-lookup"><span data-stu-id="a34fd-177">User who has access to the SFTP server</span></span> |<span data-ttu-id="a34fd-178">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-178">Yes</span></span> |
| <span data-ttu-id="a34fd-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="a34fd-179">privateKeyPath</span></span> | <span data-ttu-id="a34fd-180">指定閘道可以存取之私密金鑰檔案的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="a34fd-180">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="a34fd-181">指定 `privateKeyPath` 或 `privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="a34fd-181">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="a34fd-182">僅當從內部部署 SFTP 伺服器複製資料時才套用。</span><span class="sxs-lookup"><span data-stu-id="a34fd-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="a34fd-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="a34fd-183">privateKeyContent</span></span> | <span data-ttu-id="a34fd-184">私密金鑰內容的序列化字串。</span><span class="sxs-lookup"><span data-stu-id="a34fd-184">A serialized string of the private key content.</span></span> <span data-ttu-id="a34fd-185">複製精靈可以讀取私密金鑰檔案，並自動解壓縮私密金鑰內容。</span><span class="sxs-lookup"><span data-stu-id="a34fd-185">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="a34fd-186">如果您使用任何其他工具/SDK，請改為使用 privateKeyPath 屬性。</span><span class="sxs-lookup"><span data-stu-id="a34fd-186">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="a34fd-187">指定 `privateKeyPath` 或 `privateKeyContent`。</span><span class="sxs-lookup"><span data-stu-id="a34fd-187">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="a34fd-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="a34fd-188">passPhrase</span></span> | <span data-ttu-id="a34fd-189">如果金鑰檔案受到複雜密碼保護，請指定複雜密碼/密碼以將私密金鑰解密。</span><span class="sxs-lookup"><span data-stu-id="a34fd-189">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="a34fd-190">如果私密金鑰檔案受到複雜密碼保護，則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="a34fd-190">Yes if the private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="a34fd-191">SFTP 連接器僅支援 OpenSSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a34fd-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="a34fd-192">請確定您的金鑰檔案格式正確。</span><span class="sxs-lookup"><span data-stu-id="a34fd-192">Make sure your key file is in the proper format.</span></span> <span data-ttu-id="a34fd-193">您可以使用 Putty 工具，從 .ppk 轉換為 OpenSSH 格式。</span><span class="sxs-lookup"><span data-stu-id="a34fd-193">You can use Putty tool to convert from .ppk to OpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="a34fd-194">範例︰使用私密金鑰 filePath 的 SshPublicKey 驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-194">Example: SshPublicKey authentication using private key filePath</span></span>

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="a34fd-195">範例︰使用私密金鑰內容的 SshPublicKey 驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-195">Example: SshPublicKey authentication using private key content</span></span>

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
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a34fd-196">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-196">Dataset properties</span></span>
<span data-ttu-id="a34fd-197">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a34fd-197">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a34fd-198">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="a34fd-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="a34fd-199">不同類型資料集的 **typeProperties** 區段不同。</span><span class="sxs-lookup"><span data-stu-id="a34fd-199">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="a34fd-200">它提供資料集類型的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="a34fd-200">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="a34fd-201">**FileShare** 資料集類型的 typeProperties 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a34fd-201">The typeProperties section for a dataset of type **FileShare** dataset has the following properties:</span></span>

| <span data-ttu-id="a34fd-202">屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-202">Property</span></span> | <span data-ttu-id="a34fd-203">說明</span><span class="sxs-lookup"><span data-stu-id="a34fd-203">Description</span></span> | <span data-ttu-id="a34fd-204">必要</span><span class="sxs-lookup"><span data-stu-id="a34fd-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a34fd-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="a34fd-205">folderPath</span></span> |<span data-ttu-id="a34fd-206">資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="a34fd-206">Sub path to the folder.</span></span> <span data-ttu-id="a34fd-207">使用逸出字元 ‘ \ ’ 當做字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a34fd-207">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="a34fd-208">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="a34fd-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="a34fd-209">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="a34fd-209">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="a34fd-210">是</span><span class="sxs-lookup"><span data-stu-id="a34fd-210">Yes</span></span> |
| <span data-ttu-id="a34fd-211">fileName</span><span class="sxs-lookup"><span data-stu-id="a34fd-211">fileName</span></span> |<span data-ttu-id="a34fd-212">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="a34fd-212">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="a34fd-213">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="a34fd-213">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="a34fd-214">若未指定輸出資料集的 fileName，所產生檔案的名稱是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="a34fd-214">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="a34fd-215">Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="a34fd-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="a34fd-216">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-216">No</span></span> |
| <span data-ttu-id="a34fd-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="a34fd-217">fileFilter</span></span> |<span data-ttu-id="a34fd-218">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a34fd-218">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="a34fd-219">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="a34fd-220">範例 1：`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="a34fd-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="a34fd-221">範例 2：`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="a34fd-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="a34fd-222">fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="a34fd-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="a34fd-223">這個屬性不支援使用 HDFS。</span><span class="sxs-lookup"><span data-stu-id="a34fd-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="a34fd-224">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-224">No</span></span> |
| <span data-ttu-id="a34fd-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="a34fd-225">partitionedBy</span></span> |<span data-ttu-id="a34fd-226">partitionedBy 可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="a34fd-226">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="a34fd-227">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="a34fd-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="a34fd-228">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-228">No</span></span> |
| <span data-ttu-id="a34fd-229">format</span><span class="sxs-lookup"><span data-stu-id="a34fd-229">format</span></span> | <span data-ttu-id="a34fd-230">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-230">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a34fd-231">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="a34fd-231">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="a34fd-232">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="a34fd-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a34fd-233">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="a34fd-233">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a34fd-234">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-234">No</span></span> |
| <span data-ttu-id="a34fd-235">compression</span><span class="sxs-lookup"><span data-stu-id="a34fd-235">compression</span></span> | <span data-ttu-id="a34fd-236">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="a34fd-236">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="a34fd-237">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a34fd-238">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a34fd-239">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a34fd-240">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-240">No</span></span> |
| <span data-ttu-id="a34fd-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="a34fd-241">useBinaryTransfer</span></span> |<span data-ttu-id="a34fd-242">指定是否使用二進位傳輸模式。</span><span class="sxs-lookup"><span data-stu-id="a34fd-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="a34fd-243">二進位模式為 true，ASCII 則為 false。</span><span class="sxs-lookup"><span data-stu-id="a34fd-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="a34fd-244">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="a34fd-244">Default value: True.</span></span> <span data-ttu-id="a34fd-245">只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="a34fd-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="a34fd-246">否</span><span class="sxs-lookup"><span data-stu-id="a34fd-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="a34fd-247">無法同時使用檔名和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="a34fd-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="a34fd-248">使用 partionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-248">Using partionedBy property</span></span>
<span data-ttu-id="a34fd-249">如上一節所述，您可以利用 partitionedBy 指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="a34fd-249">As mentioned in the previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="a34fd-250">您可以使用 Data Factory 巨集和系統變數以及可指出給定資料配量的邏輯時間週期的 SliceStart、SliceEnd 來這麼做。</span><span class="sxs-lookup"><span data-stu-id="a34fd-250">You can do so with the Data Factory macros and the system variable SliceStart, SliceEnd that indicate the logical time period for a given data slice.</span></span>

<span data-ttu-id="a34fd-251">若要了解時間序列資料集、排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)、[排程和執行](data-factory-scheduling-and-execution.md)以及[建立管線](data-factory-create-pipelines.md)等文章。</span><span class="sxs-lookup"><span data-stu-id="a34fd-251">To learn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="a34fd-252">範例 1：</span><span class="sxs-lookup"><span data-stu-id="a34fd-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="a34fd-253">在此範例中，{Slice} 會取代成 Data Factory 系統變數 SliceStart 的值 (使用指定的格式 (YYYYMMDDHH))。</span><span class="sxs-lookup"><span data-stu-id="a34fd-253">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="a34fd-254">SliceStart 是指配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="a34fd-254">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="a34fd-255">每個配量的 folderPath 都不同。</span><span class="sxs-lookup"><span data-stu-id="a34fd-255">The folderPath is different for each slice.</span></span> <span data-ttu-id="a34fd-256">範例：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。</span><span class="sxs-lookup"><span data-stu-id="a34fd-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="a34fd-257">範例 2：</span><span class="sxs-lookup"><span data-stu-id="a34fd-257">Sample 2:</span></span>

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
<span data-ttu-id="a34fd-258">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="a34fd-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a34fd-259">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="a34fd-259">Copy activity properties</span></span>
<span data-ttu-id="a34fd-260">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a34fd-260">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a34fd-261">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="a34fd-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a34fd-262">然而，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a34fd-262">Whereas, the properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="a34fd-263">就複製活動而言，類型屬性會根據來源和接收的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a34fd-263">For Copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a34fd-264">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="a34fd-264">Supported file and compression formats</span></span>
<span data-ttu-id="a34fd-265">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a34fd-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-to-azure-blob"></a><span data-ttu-id="a34fd-266">JSON 範例：將資料從 SFTP 伺服器複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a34fd-266">JSON Example: Copy data from SFTP server to Azure blob</span></span>
<span data-ttu-id="a34fd-267">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="a34fd-267">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a34fd-268">這些範例示範如何將資料從 SFTP 來源複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a34fd-268">They show how to copy data from SFTP source to Azure Blob Storage.</span></span> <span data-ttu-id="a34fd-269">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="a34fd-269">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a34fd-270">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="a34fd-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="a34fd-271">其中並不包含建立 Data Factory 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a34fd-271">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="a34fd-272">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="a34fd-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="a34fd-273">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="a34fd-273">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="a34fd-274">[sftp](#linked-service-properties) 類型的已連結服務。</span><span class="sxs-lookup"><span data-stu-id="a34fd-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="a34fd-275">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="a34fd-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="a34fd-276">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="a34fd-277">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="a34fd-278">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a34fd-279">範例會每隔一小時就把 SFTP 伺服器的資料複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="a34fd-279">The sample copies data from an SFTP server to an Azure blob every hour.</span></span> <span data-ttu-id="a34fd-280">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="a34fd-280">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a34fd-281">**SFTP 連結服務**</span><span class="sxs-lookup"><span data-stu-id="a34fd-281">**SFTP linked service**</span></span>

<span data-ttu-id="a34fd-282">此範例會利用純文字使用者名稱和密碼來使用基本驗證。</span><span class="sxs-lookup"><span data-stu-id="a34fd-282">This example uses the basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="a34fd-283">您也可以使用下列其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="a34fd-283">You can also use one of the following ways:</span></span>

* <span data-ttu-id="a34fd-284">基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="a34fd-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="a34fd-285">SSH 公用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="a34fd-285">SSH public key authentication</span></span>

<span data-ttu-id="a34fd-286">請參閱 [FTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="a34fd-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
<span data-ttu-id="a34fd-287">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="a34fd-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="a34fd-288">**SFTP 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="a34fd-288">**SFTP input dataset**</span></span>

<span data-ttu-id="a34fd-289">此資料集是指 SFTP 資料夾 `mysharedfolder` 和 `test.csv` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a34fd-289">This dataset refers to the SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="a34fd-290">管線會將檔案複製至目的地。</span><span class="sxs-lookup"><span data-stu-id="a34fd-290">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="a34fd-291">設定 "external": "true" 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="a34fd-291">Setting "external": "true" informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="a34fd-292">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="a34fd-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a34fd-293">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="a34fd-293">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a34fd-294">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="a34fd-294">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a34fd-295">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="a34fd-295">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="a34fd-296">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="a34fd-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a34fd-297">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="a34fd-297">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a34fd-298">在管線 JSON 定義中，**source** 類型設為 **FileSystemSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="a34fd-298">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span>

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

## <a name="performance-and-tuning"></a><span data-ttu-id="a34fd-299">效能和微調</span><span class="sxs-lookup"><span data-stu-id="a34fd-299">Performance and Tuning</span></span>
<span data-ttu-id="a34fd-300">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="a34fd-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a34fd-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a34fd-301">Next Steps</span></span>
<span data-ttu-id="a34fd-302">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="a34fd-302">See the following articles:</span></span>

* <span data-ttu-id="a34fd-303">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a34fd-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
