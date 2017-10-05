---
title: "將其他 Azure 儲存體帳戶新增至 HDInsight | Microsoft Docs"
description: "了解如何將其他 Azure 儲存體帳戶新增至現有的 HDInsight 叢集。"
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
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="10621-103">將其他儲存體帳戶新增至 HDInsight</span><span class="sxs-lookup"><span data-stu-id="10621-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="10621-104">了解如何使用指令碼動作，將其他 Azure 儲存體帳戶新增至 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="10621-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="10621-105">這份文件中的步驟會在現有的 Linux 架構 HDInsight 叢集中新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10621-106">本文件中的資訊是有關如何在建立叢集之後，將其他儲存體新增至叢集。</span><span class="sxs-lookup"><span data-stu-id="10621-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="10621-107">如需在叢集建立期間新增儲存體帳戶的資訊，請參閱[使用 Hadoop、Spark、Kafka 等在 HDInsight 中設定叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="10621-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="10621-108">運作方式</span><span class="sxs-lookup"><span data-stu-id="10621-108">How it works</span></span>

<span data-ttu-id="10621-109">此指令碼採用下列參數︰</span><span class="sxs-lookup"><span data-stu-id="10621-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="10621-110">__Azure 儲存體帳戶名稱__：要新增至 HDInsight 叢集的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="10621-111">執行指令碼之後，HDInsight 可以讀取和寫入此儲存體帳戶中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="10621-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="10621-112">__Azure 儲存體帳戶金鑰__︰授與存取權給儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="10621-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="10621-113">__-p__ (選用)︰若已指定，金鑰不會加密，而且會以純文字方式儲存在 core-site.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="10621-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="10621-114">在處理期間，此指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="10621-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="10621-115">如果儲存體帳戶已經存在於叢集的 core-site.xml 組態中，則指令碼會結束，不會執行任何進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="10621-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="10621-116">確認儲存體帳戶存在並可使用金鑰來存取。</span><span class="sxs-lookup"><span data-stu-id="10621-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="10621-117">使用叢集認證加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="10621-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="10621-118">將儲存體帳戶新增至 core-site.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="10621-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="10621-119">停止並重新啟動 Oozie、YARN、MapReduce2 和 HDFS 服務。</span><span class="sxs-lookup"><span data-stu-id="10621-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="10621-120">停止並啟動這些服務可讓它們使用新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="10621-121">不支援在與 HDInsight 叢集不同的位置中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="10621-122">指令碼</span><span class="sxs-lookup"><span data-stu-id="10621-122">The script</span></span>

<span data-ttu-id="10621-123">__指令碼位置__：[https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="10621-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="10621-124">__需求__：</span><span class="sxs-lookup"><span data-stu-id="10621-124">__Requirements__:</span></span>

* <span data-ttu-id="10621-125">指令碼必須套用於__前端節點__。</span><span class="sxs-lookup"><span data-stu-id="10621-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="10621-126">若要使用指令碼</span><span class="sxs-lookup"><span data-stu-id="10621-126">To use the script</span></span>

<span data-ttu-id="10621-127">您可以從 Azure 入口網站、Azure PowerShell 或 Azure CLI 1.0 使用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="10621-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="10621-128">如需詳細資訊，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)文件。</span><span class="sxs-lookup"><span data-stu-id="10621-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10621-129">在使用自訂文件中提供的步驟時，請使用下列資訊來套用此指令碼：</span><span class="sxs-lookup"><span data-stu-id="10621-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="10621-130">以這個指令碼的 URI 取代指令碼動作 URI 範例 (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)。</span><span class="sxs-lookup"><span data-stu-id="10621-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="10621-131">以即將新增至叢集的儲存體帳戶的 Azure 儲存體帳戶名稱和金鑰取代範例參數。</span><span class="sxs-lookup"><span data-stu-id="10621-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="10621-132">如果使用 Azure 入口網站，則必須以空格分隔這些參數。</span><span class="sxs-lookup"><span data-stu-id="10621-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="10621-133">您不需要將此指令碼標示為 [已保存]，因為它會直接更新叢集的 Ambari 組態。</span><span class="sxs-lookup"><span data-stu-id="10621-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="10621-134">已知問題</span><span class="sxs-lookup"><span data-stu-id="10621-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="10621-135">儲存體帳戶未顯示在 Azure 入口網站或工具中</span><span class="sxs-lookup"><span data-stu-id="10621-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="10621-136">在 Azure 入口網站中檢視 HDInsight 叢集時，選取 [屬性] 之下的 [儲存體帳戶] 項目，並不會顯示透過此指令碼動作新增的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="10621-137">Azure PowerShell 和 Azure CLI 也不會顯示其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="10621-138">沒有顯示儲存體資訊是因為指令碼只修改叢集的 core-site.xml 組態。</span><span class="sxs-lookup"><span data-stu-id="10621-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="10621-139">使用 Azure 管理 API 擷取叢集資訊時，不會使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="10621-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="10621-140">若要檢視使用此指令碼新增至叢集的儲存體帳戶資訊，請使用 Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="10621-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="10621-141">請使用下列命令，為您的叢集擷取此資訊：</span><span class="sxs-lookup"><span data-stu-id="10621-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="10621-142">將 `$clusterName` 設定為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="10621-143">將 `$storageAccountName` 設定為儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="10621-144">出現提示時，輸入叢集登入 (admin) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="10621-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="10621-145">將 `$PASSWORD` 設定為叢集登入 (admin) 帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="10621-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="10621-146">將 `$CLUSTERNAME` 設定為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="10621-147">將 `$STORAGEACCOUNTNAME` 設定為儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="10621-148">此範例會如何 [curl (http://curl.haxx.se/)](http://curl.haxx.se/) 和 [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/)，來擷取及剖析 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="10621-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="10621-149">使用此命令時，將 __CLUSTERNAME__ 替換為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="10621-150">將 __PASSWORD__ 替換為叢集的 HTTP 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="10621-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="10621-151">將 __STORAGEACCOUNT__ 替換為使用指令碼動作新增的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="10621-152">此命令傳回的資訊看起來類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="10621-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="10621-153">此文字是已加密的金鑰範例，可用來存取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="10621-154">無法在變更金鑰之後存取儲存體</span><span class="sxs-lookup"><span data-stu-id="10621-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="10621-155">如果您變更儲存體帳戶的金鑰，HDInsight 就無法再存取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="10621-156">HDInsight 在叢集的 core-site.xml 中使用金鑰的快取複本。</span><span class="sxs-lookup"><span data-stu-id="10621-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="10621-157">此快取副本必須更新以符合新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="10621-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="10621-158">再次執行指令碼動作並__不會__更新金鑰，因為指令碼會查看儲存體帳戶的項目是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="10621-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="10621-159">如果項目已經存在，就不會進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="10621-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="10621-160">若要解決這個問題，您必須移除儲存體帳戶的現有項目。</span><span class="sxs-lookup"><span data-stu-id="10621-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="10621-161">執行下列步驟以移除現有項目：</span><span class="sxs-lookup"><span data-stu-id="10621-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="10621-162">在 Web 瀏覽器中，對您的 HDInsight 叢集開啟 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="10621-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="10621-163">URI 是 https://CLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="10621-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="10621-164">將 __CLUSTERNAME__ 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="10621-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="10621-165">出現提示時，輸入您叢集的 HTTP 登入使用者和密碼。</span><span class="sxs-lookup"><span data-stu-id="10621-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="10621-166">從頁面左邊的服務清單中，選取 [HDFS]。</span><span class="sxs-lookup"><span data-stu-id="10621-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="10621-167">然後選取頁面中間的 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="10621-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="10621-168">在 [篩選...] 欄位中，輸入 __fs.azure.account__ 值。</span><span class="sxs-lookup"><span data-stu-id="10621-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="10621-169">這會傳回已新增到叢集的任何其他儲存體帳戶項目。</span><span class="sxs-lookup"><span data-stu-id="10621-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="10621-170">有兩種項目類型：__keyprovider__ 和 __key__。</span><span class="sxs-lookup"><span data-stu-id="10621-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="10621-171">兩者都會包含儲存體帳戶名稱做為金鑰名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="10621-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="10621-172">下列是名為 __mystorage__ 之儲存體帳戶的項目範例：</span><span class="sxs-lookup"><span data-stu-id="10621-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="10621-173">在您識別您需要移除之儲存體帳戶的金鑰之後，請使用項目右邊的紅色 '-' 圖示將它刪除。</span><span class="sxs-lookup"><span data-stu-id="10621-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="10621-174">然後使用 [儲存] 按鈕來儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="10621-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="10621-175">在儲存變更之後，使用指令碼動作將儲存體帳戶和新的金鑰值新增至叢集。</span><span class="sxs-lookup"><span data-stu-id="10621-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="10621-176">效能不佳</span><span class="sxs-lookup"><span data-stu-id="10621-176">Poor performance</span></span>

<span data-ttu-id="10621-177">如果儲存體帳戶位於與 HDInsight 叢集不同的區域中，您可能會遇到效能不佳。</span><span class="sxs-lookup"><span data-stu-id="10621-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="10621-178">存取不同區域中的資料會傳送 Azure 資料中心外部和跨越公用網際網路的網路流量，這可能會造成延遲。</span><span class="sxs-lookup"><span data-stu-id="10621-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="10621-179">不支援在 HDInsight 叢集以外的區域中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="10621-180">額外費用</span><span class="sxs-lookup"><span data-stu-id="10621-180">Additional charges</span></span>

<span data-ttu-id="10621-181">如果儲存體帳戶位於與 HDInsight 叢集不同的區域中，您可能會發現 Azure 帳單上出現額外輸出費用。</span><span class="sxs-lookup"><span data-stu-id="10621-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="10621-182">當資料離開區域資料中心時，就會產生輸出費用。</span><span class="sxs-lookup"><span data-stu-id="10621-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="10621-183">即使流量的目的地是不同區域中的其他 Azure 資料中心，仍會產生此費用。</span><span class="sxs-lookup"><span data-stu-id="10621-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="10621-184">不支援在 HDInsight 叢集以外的區域中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="10621-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10621-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10621-185">Next steps</span></span>

<span data-ttu-id="10621-186">您已了解如何將其他儲存體帳戶新增至現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="10621-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="10621-187">如需指令碼動作的詳細資訊，請參閱[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="10621-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
