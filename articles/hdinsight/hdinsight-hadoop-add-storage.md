---
title: "aaaAdd 其他 Azure 儲存體帳戶 tooHDInsight |Microsoft 文件"
description: "了解如何 tooadd 其他 Azure 儲存體帳戶 tooan 現有 HDInsight 叢集。"
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="873f4-103">加入額外的儲存體帳戶 tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="873f4-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="873f4-104">了解如何 toouse 指令碼動作 tooadd 其他 Azure 儲存體帳戶 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="873f4-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="873f4-105">hello 本文件中的步驟加入的儲存體帳戶 tooan 現有以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="873f4-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="873f4-106">本文件中的 hello 資訊是關於已建立之後，加入額外的儲存體 tooa 叢集。</span><span class="sxs-lookup"><span data-stu-id="873f4-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="873f4-107">如需在叢集建立期間新增儲存體帳戶的資訊，請參閱[使用 Hadoop、Spark、Kafka 等在 HDInsight 中設定叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="873f4-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="873f4-108">運作方式</span><span class="sxs-lookup"><span data-stu-id="873f4-108">How it works</span></span>

<span data-ttu-id="873f4-109">此指令碼採用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="873f4-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="873f4-110">__Azure 儲存體帳戶名稱__: hello hello 儲存體帳戶 tooadd toohello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="873f4-111">執行 hello 指令碼之後, HDInsight 可讀寫資料儲存在這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="873f4-112">__Azure 儲存體帳戶金鑰__： 索引鍵，會授與存取 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="873f4-113">__-p__ （選擇性）： 若指定，hello 金鑰未加密，並儲存在 hello core-site.xml 檔案做為純文字。</span><span class="sxs-lookup"><span data-stu-id="873f4-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="873f4-114">在處理期間，hello 指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="873f4-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="873f4-115">如果 hello 儲存體帳戶已經存在 hello core-site.xml hello 叢集組態中，hello 指令碼結束，並會執行任何進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="873f4-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="873f4-116">確認 hello 儲存體帳戶存在，而且可以使用 hello 索引鍵來存取。</span><span class="sxs-lookup"><span data-stu-id="873f4-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="873f4-117">Hello 使用加密金鑰 hello 叢集認證。</span><span class="sxs-lookup"><span data-stu-id="873f4-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="873f4-118">新增 hello 儲存體帳戶 toohello core-site.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="873f4-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="873f4-119">停止並重新啟動 hello Oozie、 YARN、 MapReduce2 和 HDFS 的服務。</span><span class="sxs-lookup"><span data-stu-id="873f4-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="873f4-120">停止和啟動這些服務可讓它們 toouse hello 新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="873f4-121">不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="873f4-122">hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="873f4-122">hello script</span></span>

<span data-ttu-id="873f4-123">__指令碼位置__：[https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="873f4-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="873f4-124">__需求__：</span><span class="sxs-lookup"><span data-stu-id="873f4-124">__Requirements__:</span></span>

* <span data-ttu-id="873f4-125">hello 指令碼必須套用 hello__前端節點__。</span><span class="sxs-lookup"><span data-stu-id="873f4-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="873f4-126">toouse hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="873f4-126">toouse hello script</span></span>

<span data-ttu-id="873f4-127">此指令碼可以在 hello Azure 入口網站，Azure PowerShell 中使用，或 hello Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="873f4-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="873f4-128">如需詳細資訊，請參閱 hello[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)文件。</span><span class="sxs-lookup"><span data-stu-id="873f4-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="873f4-129">當使用 hello hello 自訂文件中提供的步驟，請使用下列資訊 tooapply hello 此指令碼：</span><span class="sxs-lookup"><span data-stu-id="873f4-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="873f4-130">取代 hello URI，此指令碼 (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh) 中的任何範例指令碼動作 URI。</span><span class="sxs-lookup"><span data-stu-id="873f4-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="873f4-131">取代 hello Azure 儲存體帳戶名稱和金鑰 hello 儲存體帳戶 toobe 加入的 toohello 任何的叢集範例參數。</span><span class="sxs-lookup"><span data-stu-id="873f4-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="873f4-132">如果使用 hello Azure 入口網站，則必須以空格分隔這些參數。</span><span class="sxs-lookup"><span data-stu-id="873f4-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="873f4-133">您不需要 toomark 此指令碼做為__Persisted__，因為它會直接更新 hello Ambari hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="873f4-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="873f4-134">已知問題</span><span class="sxs-lookup"><span data-stu-id="873f4-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="873f4-135">儲存體帳戶未顯示在 Azure 入口網站或工具中</span><span class="sxs-lookup"><span data-stu-id="873f4-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="873f4-136">當檢視 hello HDInsight 叢集 hello Azure 入口網站中時，選取 hello__儲存體帳戶__下的項目__屬性__不會顯示儲存體帳戶加入到此指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="873f4-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="873f4-137">Azure PowerShell 和 Azure CLI 不會顯示 hello 額外的儲存體帳戶可能是。</span><span class="sxs-lookup"><span data-stu-id="873f4-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="873f4-138">因為 hello 指令碼只會修改 hello core-site.xml hello 叢集組態，不會顯示 hello 儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="873f4-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="873f4-139">擷取使用 Azure 管理 Api 的 hello 叢集資訊時，不會使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="873f4-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="873f4-140">tooview 儲存體帳戶資訊加入 toohello 叢集使用此指令碼，使用 hello Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="873f4-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="873f4-141">使用下列命令 tooretrieve hello 這項資訊為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="873f4-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="873f4-142">設定`$clusterName`toohello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="873f4-143">設定`$storageAccountName`toohello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="873f4-144">出現提示時，輸入 hello 叢集登入 （管理員） 和密碼。</span><span class="sxs-lookup"><span data-stu-id="873f4-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="873f4-145">設定`$PASSWORD`toohello 叢集登入 （管理員） 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="873f4-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="873f4-146">設定`$CLUSTERNAME`toohello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="873f4-147">設定`$STORAGEACCOUNTNAME`toohello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="873f4-148">這個範例會使用[curl (http://curl.haxx.se/)](http://curl.haxx.se/)和[jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve 和剖析 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="873f4-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="873f4-149">當使用這個命令，來取代__CLUSTERNAME__ hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="873f4-150">取代__密碼__hello 叢集 hello HTTP 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="873f4-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="873f4-151">取代__STORAGEACCOUNT__ hello hello 儲存體帳戶加入使用指令碼動作名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="873f4-152">此命令傳回的資訊會出現下列文字類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="873f4-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="873f4-153">此文字是已加密的金鑰，會使用的範例 tooaccess hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="873f4-154">無法 tooaccess 之後變更金鑰的儲存體</span><span class="sxs-lookup"><span data-stu-id="873f4-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="873f4-155">如果您變更儲存體帳戶的 hello 索引鍵，HDInsight 就無法再存取 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="873f4-156">HDInsight hello 叢集 hello core-site.xml 中使用快取的金鑰的副本。</span><span class="sxs-lookup"><span data-stu-id="873f4-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="873f4-157">此快取的副本必須更新的 toomatch hello 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="873f4-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="873f4-158">執行一次 hello 指令碼動作未__不__hello 金鑰時更新 hello 指令碼會檢查 toosee hello 儲存體帳戶的項目已經存在。</span><span class="sxs-lookup"><span data-stu-id="873f4-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="873f4-159">如果項目已經存在，就不會進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="873f4-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="873f4-160">toowork 解決這個問題，您必須移除 hello hello 儲存體帳戶的現有項目。</span><span class="sxs-lookup"><span data-stu-id="873f4-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="873f4-161">使用下列步驟 tooremove hello 現有項目 hello:</span><span class="sxs-lookup"><span data-stu-id="873f4-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="873f4-162">網頁瀏覽器中開啟您的 HDInsight 叢集的 hello Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="873f4-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="873f4-163">hello URI 是 https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="873f4-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="873f4-164">取代__CLUSTERNAME__與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="873f4-165">出現提示時，請針對您的叢集輸入 hello HTTP 登入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="873f4-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="873f4-166">從 hello hello 左邊 hello 頁面上的服務 清單中，選取__HDFS__。</span><span class="sxs-lookup"><span data-stu-id="873f4-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="873f4-167">然後選取 [hello __Configs__ hello hello 頁面置中的] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="873f4-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="873f4-168">在 hello__篩選...__欄位中，輸入值為__fs.azure.account__。</span><span class="sxs-lookup"><span data-stu-id="873f4-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="873f4-169">這會傳回項目已加入 toohello 叢集的任何額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="873f4-170">有兩種項目類型：__keyprovider__ 和 __key__。</span><span class="sxs-lookup"><span data-stu-id="873f4-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="873f4-171">同時包含 hello hello 索引鍵名稱的一部分的 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="873f4-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="873f4-172">hello 以下是名為儲存體帳戶的項目範例__mystorage__:</span><span class="sxs-lookup"><span data-stu-id="873f4-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="873f4-173">識別 hello 儲存體帳戶，您需要 tooremove hello 金鑰之後，使用紅色 hello '-' 權限的 hello 項目 toodelete 圖示 toohello 它。</span><span class="sxs-lookup"><span data-stu-id="873f4-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="873f4-174">然後使用 hello__儲存__按鈕 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="873f4-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="873f4-175">已儲存變更之後，使用 hello 指令碼動作 tooadd hello 儲存體帳戶和新的索引鍵值 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="873f4-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="873f4-176">效能不佳</span><span class="sxs-lookup"><span data-stu-id="873f4-176">Poor performance</span></span>

<span data-ttu-id="873f4-177">如果 hello 儲存體帳戶在 hello HDInsight 叢集以外的不同區域中，您可能會遇到效能不佳。</span><span class="sxs-lookup"><span data-stu-id="873f4-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="873f4-178">存取資料的不同區域傳送網路流量之外 hello 地區的 Azure 資料中心，並透過 hello 公用網際網路，可能會導致延遲。</span><span class="sxs-lookup"><span data-stu-id="873f4-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="873f4-179">不支援在 hello HDInsight 叢集以外的不同區域中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="873f4-180">額外費用</span><span class="sxs-lookup"><span data-stu-id="873f4-180">Additional charges</span></span>

<span data-ttu-id="873f4-181">如果 hello 儲存體帳戶是在不同的區域中，非 hello HDInsight 叢集，您可能會在您的 Azure 帳單上發現其他輸出費用。</span><span class="sxs-lookup"><span data-stu-id="873f4-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="873f4-182">當資料離開區域資料中心時，就會產生輸出費用。</span><span class="sxs-lookup"><span data-stu-id="873f4-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="873f4-183">即使 hello 流量的目的地為不同的區域中的另一個 Azure 資料中心，會套用這筆費用。</span><span class="sxs-lookup"><span data-stu-id="873f4-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="873f4-184">不支援在 hello HDInsight 叢集以外的不同區域中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="873f4-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="873f4-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="873f4-185">Next steps</span></span>

<span data-ttu-id="873f4-186">您已經學會如何 tooadd 額外的儲存體帳戶 tooan 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="873f4-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="873f4-187">如需指令碼動作的詳細資訊，請參閱[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="873f4-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
