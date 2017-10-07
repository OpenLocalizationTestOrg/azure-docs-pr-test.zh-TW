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
# <a name="add-additional-storage-accounts-toohdinsight"></a>加入額外的儲存體帳戶 tooHDInsight

了解如何 toouse 指令碼動作 tooadd 其他 Azure 儲存體帳戶 tooHDInsight。 hello 本文件中的步驟加入的儲存體帳戶 tooan 現有以 Linux 為基礎的 HDInsight 叢集。

> [!IMPORTANT]
> 本文件中的 hello 資訊是關於已建立之後，加入額外的儲存體 tooa 叢集。 如需在叢集建立期間新增儲存體帳戶的資訊，請參閱[使用 Hadoop、Spark、Kafka 等在 HDInsight 中設定叢集](hdinsight-hadoop-provision-linux-clusters.md)。

## <a name="how-it-works"></a>運作方式

此指令碼採用下列參數的 hello:

* __Azure 儲存體帳戶名稱__: hello hello 儲存體帳戶 tooadd toohello HDInsight 叢集名稱。 執行 hello 指令碼之後, HDInsight 可讀寫資料儲存在這個儲存體帳戶。

* __Azure 儲存體帳戶金鑰__： 索引鍵，會授與存取 toohello 儲存體帳戶。

* __-p__ （選擇性）： 若指定，hello 金鑰未加密，並儲存在 hello core-site.xml 檔案做為純文字。

在處理期間，hello 指令碼會執行下列動作的 hello:

* 如果 hello 儲存體帳戶已經存在 hello core-site.xml hello 叢集組態中，hello 指令碼結束，並會執行任何進一步的動作。

* 確認 hello 儲存體帳戶存在，而且可以使用 hello 索引鍵來存取。

* Hello 使用加密金鑰 hello 叢集認證。

* 新增 hello 儲存體帳戶 toohello core-site.xml 檔案。

* 停止並重新啟動 hello Oozie、 YARN、 MapReduce2 和 HDFS 的服務。 停止和啟動這些服務可讓它們 toouse hello 新儲存體帳戶。

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。

## <a name="hello-script"></a>hello 指令碼

__指令碼位置__：[https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__需求__：

* hello 指令碼必須套用 hello__前端節點__。

## <a name="toouse-hello-script"></a>toouse hello 指令碼

此指令碼可以在 hello Azure 入口網站，Azure PowerShell 中使用，或 hello Azure CLI 1.0。 如需詳細資訊，請參閱 hello[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)文件。

> [!IMPORTANT]
> 當使用 hello hello 自訂文件中提供的步驟，請使用下列資訊 tooapply hello 此指令碼：
>
> * 取代 hello URI，此指令碼 (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh) 中的任何範例指令碼動作 URI。
> * 取代 hello Azure 儲存體帳戶名稱和金鑰 hello 儲存體帳戶 toobe 加入的 toohello 任何的叢集範例參數。 如果使用 hello Azure 入口網站，則必須以空格分隔這些參數。
> * 您不需要 toomark 此指令碼做為__Persisted__，因為它會直接更新 hello Ambari hello 叢集組態。

## <a name="known-issues"></a>已知問題

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>儲存體帳戶未顯示在 Azure 入口網站或工具中

當檢視 hello HDInsight 叢集 hello Azure 入口網站中時，選取 hello__儲存體帳戶__下的項目__屬性__不會顯示儲存體帳戶加入到此指令碼動作。 Azure PowerShell 和 Azure CLI 不會顯示 hello 額外的儲存體帳戶可能是。

因為 hello 指令碼只會修改 hello core-site.xml hello 叢集組態，不會顯示 hello 儲存體資訊。 擷取使用 Azure 管理 Api 的 hello 叢集資訊時，不會使用這項資訊。

tooview 儲存體帳戶資訊加入 toohello 叢集使用此指令碼，使用 hello Ambari REST API。 使用下列命令 tooretrieve hello 這項資訊為您的叢集：

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> 設定`$clusterName`toohello hello HDInsight 叢集名稱。 設定`$storageAccountName`toohello hello 儲存體帳戶名稱。 出現提示時，輸入 hello 叢集登入 （管理員） 和密碼。

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> 設定`$PASSWORD`toohello 叢集登入 （管理員） 帳戶的密碼。 設定`$CLUSTERNAME`toohello hello HDInsight 叢集名稱。 設定`$STORAGEACCOUNTNAME`toohello hello 儲存體帳戶名稱。
>
> 這個範例會使用[curl (http://curl.haxx.se/)](http://curl.haxx.se/)和[jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve 和剖析 JSON 資料。

當使用這個命令，來取代__CLUSTERNAME__ hello hello HDInsight 叢集名稱。 取代__密碼__hello 叢集 hello HTTP 登入密碼。 取代__STORAGEACCOUNT__ hello hello 儲存體帳戶加入使用指令碼動作名稱。 此命令傳回的資訊會出現下列文字類似 toohello:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

此文字是已加密的金鑰，會使用的範例 tooaccess hello 儲存體帳戶。

### <a name="unable-tooaccess-storage-after-changing-key"></a>無法 tooaccess 之後變更金鑰的儲存體

如果您變更儲存體帳戶的 hello 索引鍵，HDInsight 就無法再存取 hello 儲存體帳戶。 HDInsight hello 叢集 hello core-site.xml 中使用快取的金鑰的副本。 此快取的副本必須更新的 toomatch hello 新的金鑰。

執行一次 hello 指令碼動作未__不__hello 金鑰時更新 hello 指令碼會檢查 toosee hello 儲存體帳戶的項目已經存在。 如果項目已經存在，就不會進行任何變更。

toowork 解決這個問題，您必須移除 hello hello 儲存體帳戶的現有項目。 使用下列步驟 tooremove hello 現有項目 hello:

1. 網頁瀏覽器中開啟您的 HDInsight 叢集的 hello Ambari Web UI。 hello URI 是 https://CLUSTERNAME.azurehdinsight.net。 取代__CLUSTERNAME__與 hello 叢集的名稱。

    出現提示時，請針對您的叢集輸入 hello HTTP 登入使用者名稱和密碼。

2. 從 hello hello 左邊 hello 頁面上的服務 清單中，選取__HDFS__。 然後選取 [hello __Configs__ hello hello 頁面置中的] 索引標籤。

3. 在 hello__篩選...__欄位中，輸入值為__fs.azure.account__。 這會傳回項目已加入 toohello 叢集的任何額外的儲存體帳戶。 有兩種項目類型：__keyprovider__ 和 __key__。 同時包含 hello hello 索引鍵名稱的一部分的 hello 儲存體帳戶名稱。

    hello 以下是名為儲存體帳戶的項目範例__mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. 識別 hello 儲存體帳戶，您需要 tooremove hello 金鑰之後，使用紅色 hello '-' 權限的 hello 項目 toodelete 圖示 toohello 它。 然後使用 hello__儲存__按鈕 toosave 您的變更。

5. 已儲存變更之後，使用 hello 指令碼動作 tooadd hello 儲存體帳戶和新的索引鍵值 toohello 叢集。

### <a name="poor-performance"></a>效能不佳

如果 hello 儲存體帳戶在 hello HDInsight 叢集以外的不同區域中，您可能會遇到效能不佳。 存取資料的不同區域傳送網路流量之外 hello 地區的 Azure 資料中心，並透過 hello 公用網際網路，可能會導致延遲。

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同區域中使用的儲存體帳戶。

### <a name="additional-charges"></a>額外費用

如果 hello 儲存體帳戶是在不同的區域中，非 hello HDInsight 叢集，您可能會在您的 Azure 帳單上發現其他輸出費用。 當資料離開區域資料中心時，就會產生輸出費用。 即使 hello 流量的目的地為不同的區域中的另一個 Azure 資料中心，會套用這筆費用。

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同區域中使用的儲存體帳戶。

## <a name="next-steps"></a>後續步驟

您已經學會如何 tooadd 額外的儲存體帳戶 tooan 現有 HDInsight 叢集。 如需指令碼動作的詳細資訊，請參閱[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)
