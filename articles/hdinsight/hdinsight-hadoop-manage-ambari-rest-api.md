---
title: "aaaMonitor 和管理與 Ambari REST API Azure HDInsight Hadoop |Microsoft 文件"
description: "深入了解如何 toouse Ambari toomonitor 和管理 Azure HDInsight 中的 Hadoop 叢集。 在本文件中，您將學習如何 toouse hello Ambari REST API 包含與 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>使用 hello Ambari REST API 來管理 HDInsight 叢集

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

了解如何 toouse hello Ambari REST API toomanage 和監視 Azure HDInsight 中的 Hadoop 叢集。

Apache Ambari 簡化 hello 的管理和監視 Hadoop 叢集藉由提供簡單 toouse web UI 和 REST API。 Ambari 包含在使用 hello Linux 作業系統的 HDInsight 叢集上。 您可以使用 Ambari toomonitor hello 叢集，並進行組態變更。

## <a id="whatis"></a>什麼是 Ambari

[Apache Ambari](http://ambari.apache.org)提供 web UI，它可以是使用的 tooprovision、 管理及監視 Hadoop 叢集。 開發人員可以這些功能整合到應用程式使用 hello [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。

以 Linux 為基礎的 HDInsight 叢集預設會提供 Ambari。

## <a name="how-toouse-hello-ambari-rest-api"></a>如何 toouse hello Ambari REST API

> [!IMPORTANT]
> hello 資訊與本文件中的範例需要使用 Linux 作業系統的 HDInsight 叢集。 如需詳細資訊，請參閱[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。

這份文件中的 hello 範例提供 hello 信瑜殼層 (bash) 和 PowerShell。 範例測試與 GNU hello bash 撞 4.3.11，但應搭配其他 Unix 殼層。 hello PowerShell 範例與 PowerShell 5.0 中測試，但應該使用 PowerShell 3.0 或更高版本。

如果使用 hello__信瑜殼層__(Bash)，您必須擁有 hello 安裝下列項目：

* [cURL](http://curl.haxx.se/): cURL 是可以使用 REST Api 的使用的 toowork 從 hello 命令列公用程式。 在本文件中，會使用的 toocommunicate 以 hello Ambari REST API。

無論是使用 Bash 或 PowerShell，您也必須安裝 [jq](https://stedolan.github.io/jq/)。 Jq 是用來使用 JSON 文件的公用程式。 它用於**所有**hello Bash 範例和**一個**的 hello PowerShell 範例。

### <a name="base-uri-for-ambari-rest-api"></a>Ambari REST API 的基底 URI

hello hello Ambari REST API，在 HDInsight 上的基底 URI 是 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME，其中**CLUSTERNAME**是 hello 叢集的名稱。

> [!IMPORTANT]
> 雖然在 hello hello 叢集名稱完整限定 hello URI (CLUSTERNAME.azurehdinsight.net) 網域名稱 (FQDN) 部分不區分大小寫，出現在其他位置中 hello URI 有區分大小寫。 例如，如果您的叢集的名稱為`MyCluster`，hello 下列是有效的 Uri:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> hello 下列 Uri 會傳回錯誤，因為不是 hello hello hello 名稱的第二次出現修正案例。
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>驗證

連接 tooAmbari HDInsight 上的需要 HTTPS。 使用 hello 管理帳戶的名稱 (hello 預設值是**admin**) 和您在叢集建立期間所提供的密碼。

## <a name="examples-authentication-and-parsing-json"></a>範例︰驗證和剖析 JSON

hello 遵循範例示範如何針對 hello GET 要求 toomake 基底 Ambari REST API:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> 本文件中的 hello Bash 範例進行下列假設 hello:
>
> * hello 叢集 hello 登入名稱是 hello 預設值是`admin`。
> * `$PASSWORD`包含 hello 密碼 hello HDInsight 登入的命令。 您可以藉由使用 `PASSWORD='mypassword'` 來設定此值。
> * `$CLUSTERNAME`包含 hello hello 叢集名稱。 您可以藉由使用 `set CLUSTERNAME='clustername'` 來設定此值

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> 本文件中的 hello PowerShell 範例進行下列假設 hello:
>
> * `$creds`是包含 hello 系統管理員登入和密碼 hello 叢集的認證物件。 您可以使用來設定此值`$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"`提供 hello 提示的認證。
> * `$clusterName`是包含 hello hello 叢集名稱的字串。 您可以藉由使用 `$clusterName="clustername"` 來設定此值。

這兩個範例會傳回開頭為下列範例的資訊類似 toohello 的 JSON 文件：

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>剖析 JSON 資料

hello 下列範例會使用`jq`tooparse hello JSON 回應文件，並顯示只有 hello `health_report` hello 結果中的資訊。

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 和更新版本提供 hello `ConvertFrom-Json` cmdlet，將 hello JSON 文件轉換成更容易 toowork 與從 PowerShell 的物件。 hello 下列範例會使用`ConvertFrom-Json`toodisplay 只有 hello `health_report` hello 結果中的資訊。

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> 雖然大部分的範例，在此文件使用`ConvertFrom-Json`toodisplay 項目從 hello 回應文件，hello[更新 Ambari 組態](#example-update-ambari-configuration)範例會使用 jq。 用於此範例 tooconstruct Jq hello JSON 回應文件的新範本。

Hello REST API 的完整參考，請參閱[Ambari 應用程式開發介面參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>範例： 取得 hello 的叢集節點 FQDN

當使用 HDInsight，您可能需要 tooknow hello 完整的網域名稱 (FQDN) 的叢集節點。 您可以輕鬆地擷取 hello FQDN hello 叢集使用 hello 遵循範例中的，各種節點：

* **所有節點**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **前端節點**：

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **背景工作節點**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Zookeeper 節點**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>範例： 取得 hello 內部 IP 位址的叢集節點

> [!IMPORTANT]
> 本節中的 hello 範例所傳回的 hello IP 位址是無法直接存取 over hello 網際網路。 它們只會在 hello 包含 hello HDInsight 叢集的 Azure 虛擬網路中存取。
>
> 如需使用 HDInsight 和虛擬網路的詳細資訊，請參閱[使用自訂 Azure 虛擬網路擴充 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。

toofind hello IP 位址，您必須知道 hello 內部的完整的網域名稱 (FQDN 的 hello 叢集節點)。 一旦您擁有 hello FQDN，然後就可以 hello hello 主機 IP 位址。 hello 下列範例先查詢 Ambari hello FQDN，所有的 hello 主機節點，然後查詢 Ambari hello 的每一部主機的 IP 位址。

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>範例： 取得 hello 預設儲存體

當您建立的 HDInsight 叢集時，您必須使用 Azure 儲存體帳戶或資料湖存放區作為 hello 預設儲存體 hello 叢集。 建立 hello 叢集後，您可以使用指定 Ambari tooretrieve 這項資訊。 例如，如果您想外 HDInsight tooread/寫入資料 toohello 容器。

hello 下列範例擷取 hello 預設儲存體設定 hello 叢集：

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> 這些範例會傳回第一次套用設定 toohello 伺服器 hello (`service_config_version=1`) 包含這項資訊。 如果您擷取在叢集建立後已修改的值，您可能需要在 toolist hello 組態版本，並擷取 hello 最新版本。

hello 傳回值會是 hello 的類似 tooone 遵循範例：

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`為這個值表示該 hello 叢集使用的是 Azure 儲存體帳戶預設儲存體。 hello`ACCOUNTNAME`值為 hello hello 儲存體帳戶名稱。 hello`CONTAINER`部分是 hello hello 儲存體帳戶中的 hello blob 容器名稱。 hello 容器是 hello 根 hello hello 叢集的 HDFS 相容的存放裝置。

* `adl://home`為這個值表示該 hello 叢集使用預設儲存體的 Azure 資料湖存放區。

    toofind hello Data Lake Store 帳戶名稱，使用下列範例中的 hello:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    hello 傳回值就會類似太`ACCOUNTNAME.azuredatalakestore.net`，其中`ACCOUNTNAME`hello hello Data Lake Store 帳戶名稱。

    資料湖存放區，其中包含 hello 叢集的存放裝置 hello，下列範例使用 hello 內 toofind hello 目錄：

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    hello 傳回值就會類似太`/clusters/CLUSTERNAME/`。 此值為 hello Data Lake Store 帳戶內的路徑。 這個路徑是 hello hello hello 叢集的 HDFS 相容的檔案系統根目錄。 

> [!NOTE]
> hello`Get-AzureRmHDInsightCluster`所提供的 cmdlet [Azure PowerShell](/powershell/azure/overview)也傳回 hello hello 叢集的儲存體資訊。


## <a name="example-get-configuration"></a>範例：取得組態

1. 取得可供您的叢集 hello 設定。

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    這個範例會傳回包含 hello 目前組態的 JSON 文件 (由 hello*標記*值) hello hello 叢集上安裝的元件。 hello 下列範例是摘錄自 hello Spark 叢集類型所傳回的資料。
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. 取得您感興趣的 hello 元件的 hello 組態。 下列範例，取代在 hello`INITIAL`與 hello hello 前一個要求所傳回的標記值。

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    這個範例會傳回包含 hello hello 目前組態的 JSON 文件`core-site`元件。

## <a name="example-update-configuration"></a>範例︰更新組態

1. 收到 hello 目前組態，Ambari 將儲存為 hello 」 所需組態 >:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    這個範例會傳回包含 hello 目前組態的 JSON 文件 (由 hello*標記*值) hello hello 叢集上安裝的元件。 hello 下列範例是摘錄自 hello Spark 叢集類型所傳回的資料。
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    從這個清單中，您需要 toocopy hello hello 元件名稱 (例如， **spark\_thrift\_sparkconf**和 hello**標記**值。

2. 使用下列命令的 hello 擷取 hello 元件和標記的 hello 組態：
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > 取代**spark-thrift-sparkconf**和**初始**hello 元件與您想要針對 tooretrieve hello 設定的標記。
   
    Jq 是使用的 tooturn hello 資料從 HDInsight 擷取至新的組態範本。 具體來說，這些範例會執行下列動作的 hello:
   
    * 建立唯一的值，其中包含 hello 字串 「 版本 」 和 hello 日期，儲存在`newtag`。

    * 建立 hello 新想要設定根文件。

    * 取得 hello 的 hello 內容`.items[]`陣列，並將它加入下 hello **desired_config**項目。

    * 刪除 hello `href`， `version`，和`Config`項目，做為這些項目不是所需的 toosubmit 新組態。

    * 使用 `version#################` 的值新增 `tag` 元素。 hello 數值部分根據 hello 目前的日期。 每個組態都必須有唯一的標記。
     
    最後，hello 資料會儲存 toohello`newconfig.json`文件。 hello 文件結構應該會出現類似下列範例的 toohello:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. 開啟 hello`newconfig.json`中 hello 的文件和修改/加入值`properties`物件。 hello 下列範例會變更 hello 值`"spark.yarn.am.memory"`從`"1g"`太`"3g"`。 它也會使用 `"256m"` 的值新增 `"spark.kryoserializer.buffer.max"`。
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Hello 檔案儲存在您完成後的修改。

4. 使用下列命令 toosubmit hello 更新組態 tooAmbari hello。
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    這些命令送出 hello hello 內容**newconfig.json**檔 toohello 叢集為 hello 新增所需的組態。 hello 要求會傳回 JSON 文件。 hello **versionTag**這份文件中的項目應符合 hello 版本，將它送出，然後再 hello **configs**物件包含您所要求的 hello 組態變更。

### <a name="example-restart-a-service-component"></a>範例︰重新啟動服務元件

此時，如果您看一下 hello Ambari web UI，hello 的 Spark 服務會指出它需要 toobe 重新啟動 hello 新設定才會生效。 使用下列步驟 toorestart hello 服務的 hello。

1. 使用下列 tooenable hello 的 Spark 服務在維護模式下的 hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    這些命令會傳送 JSON 文件 toohello 伺服器，以維護模式開啟。 您可以確認 hello 服務目前處於維護模式使用 hello 下列要求：
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    hello 傳回值是`ON`。

2. 接下來，使用下列 tooturn hello 服務關閉的 hello:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    hello 回應是類似 toohello 下列範例：
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > hello`href`這個 URI 所傳回的值使用 hello 叢集節點的 hello 內部 IP 位址。 toouse 外部 hello 叢集中，從 hello '10.0.0.18:8080' 部分取代 hello hello 叢集的 FQDN。 
    
    下列命令的 hello 擷取 hello hello 要求狀態：

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    回應`COMPLETED`表示該 hello 要求已完成。

3. Hello 前一個要求完成之後，請使用下列 toostart hello 服務的 hello。
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    hello 服務正在使用 hello 新組態。

4. 最後，使用下列維護模式關閉 tooturn hello。
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>後續步驟

Hello REST API 的完整參考，請參閱[Ambari 應用程式開發介面參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。

