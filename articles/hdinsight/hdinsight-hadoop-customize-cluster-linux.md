---
title: "使用指令碼動作-Azure aaaCustomize HDInsight 叢集 |Microsoft 文件"
description: "新增自訂元件，使用指令碼動作 tooLinux 為基礎的 HDInsight 叢集。 指令碼動作是 Bash 指令碼可使用的 toocustomize hello 叢集組態或新增其他服務和公用程式，例如色調、 Solr 或。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>使用指令碼動作自訂 Linux 型 HDInsight 叢集

HDInsight 提供設定選項，呼叫**指令碼動作**自訂 hello 叢集中的自訂指令碼會叫用。 這些指令碼會使用的 tooinstall 其他元件和變更組態設定。 叢集建立期間或叢集建立之後，可以使用指令碼動作。

> [!IMPORTANT]
> hello 能力 toouse 正在執行的叢集上的指令碼動作只適用於以 Linux 為基礎的 HDInsight 叢集。
>
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

指令碼動作也可以為 HDInsight 應用程式是已發行的 toohello Azure Marketplace。 有些這份文件中的 hello 範例顯示如何安裝使用指令碼動作命令，從 PowerShell 和.NET SDK hello 的 HDInsight 應用程式。 如需 HDInsight 應用程式的詳細資訊，請參閱[hello Azure Marketplace 應用程式發行 HDInsight](hdinsight-apps-publish-applications.md)。

## <a name="permissions"></a>權限

如果您使用已加入網域的 HDInsight 叢集，有兩個使用指令碼動作與 hello 叢集時所需的 Ambari 權限：

* **AMBARI。執行\_自訂\_命令**: hello Ambari 系統管理員角色預設具有此權限。
* **叢集。執行\_自訂\_命令**： 兩者 hello HDInsight 叢集系統管理員和 Ambari 管理員預設擁有此權限。

如需使用已加入網域之 HDInsight 權限的詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。

## <a name="access-control"></a>存取控制

如果您不是 hello 管理員/擁有者的 Azure 訂用帳戶，您的帳戶必須至少有**參與者**存取 toohello 資源群組含有 hello HDInsight 叢集。

此外，如果您建立的 HDInsight 叢集，具備至少**參與者**存取 toohello Azure 訂用帳戶必須先前已登錄 hello HDInsight 的提供者。 提供者註冊會在使用者與參與者存取 toohello 訂用帳戶建立時的資源，hello 第一次 hello 訂用帳戶。 透過[使用 REST 註冊提供者](https://msdn.microsoft.com/library/azure/dn790548.aspx)，也可以不需要建立資源就完成註冊作業。

如需有關使用存取管理的詳細資訊，請參閱下列文件的 hello:

* [開始使用 hello Azure 入口網站中存取管理](../active-directory/role-based-access-control-what-is.md)
* [使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>了解指令碼動作

指令碼動作只是一個您會提供 URI 和參數的 Bash 指令碼。 在 hello HDInsight 叢集節點上執行 hello 指令碼。 hello 以下是特性與功能的指令碼動作。

* 必須儲存在可從 hello HDInsight 叢集存取的 URI。 hello 以下是可能的儲存體位置：

    * **Azure Data Lake Store** hello HDInsight 叢集可以存取的帳戶。 如需使用 Azure Data Lake Store 與 HDInsight 的相關資訊，請參閱[建立使用 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。

        使用儲存在資料湖存放區中的指令碼，hello URI 格式時`adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`。

        > [!NOTE]
        > hello 服務主體 HDInsight 使用 tooaccess 資料湖存放區必須有讀取權限 toohello 指令碼。

    * 中的 blob **Azure 儲存體帳戶**也就是說 hello HDInsight 叢集的任一個 hello 主要或其他儲存體帳戶。 HDInsight 是在叢集建立期間，授與存取 tooboth 這些類型的儲存體帳戶。

    * 公用檔案共用服務，例如 Azure Blob、GitHub、OneDrive、Dropbox 等。

        Uri，例如看到 hello[範例指令碼動作的指令碼](#example-script-action-scripts)> 一節。

        > [!WARNING]
        > HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。 它目前不支援 hello __Blob 儲存體__帳戶類型。

* 也可以限制太**只有特定節點型別上執行**，範例前端節點或背景工作節點。

  > [!NOTE]
  > HDInsight Premium 搭配使用時，您可以指定應透過 hello 邊緣節點上 hello 指令碼。

* 可以是**持續性**或**臨時性**。

    **保存**hello 指令碼執行後指令碼都是套用的 tooworker 節點加入的 toohello 叢集。 例如，當向上擴充 hello 叢集。

    保存的指令碼也可能會套用變更 tooanother 節點類型，例如前端節點。

  > [!IMPORTANT]
  > 持續性指令碼動作必須有唯一的名稱。

    **臨時性**指令碼不會持續留存。 它們不是套用的 tooworker 節點加入的 toohello 叢集之後 hello 指令碼已執行。 您可以接著升級臨機操作指令碼 tooa 保存指令碼，或降級保存的指令碼 tooan 臨機操作指令碼。

  > [!IMPORTANT]
  > 建立叢集期間使用的指令碼動作會自動保存下來。
  >
  > 即使您特別指出應予保存，仍然不會保存失敗的指令碼。

* 可以接受**參數**所使用的 hello 指令碼執行期間。
* 使用執行**根層級權限**hello 叢集節點上。
* 可以用於透過 hello **Azure 入口網站**， **Azure PowerShell**， **Azure CLI**，或**HDInsight.NET SDK**

hello 叢集會保留所有已執行的指令碼。 hello 歷程記錄時，您需要升級或降級作業的指令碼的 toofind hello 識別碼。

> [!IMPORTANT]
> 沒有任何自動的方式 tooundo hello 指令碼動作所做的變更。 請手動反轉 hello 變更，或提供的指令碼，將其序列反轉。


### <a name="script-action-in-hello-cluster-creation-process"></a>Hello 叢集建立程序中的指令碼動作

在叢集建立期間使用的指令碼動作與在現有叢集上執行的指令碼動作稍微不同︰

* hello 指令碼是**自動保存**。
* A**失敗**hello 在指令碼可能會導致 hello 叢集建立程序 toofail。

hello 下列圖表說明 hello 建立程序期間執行指令碼動作時：

![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]

正在設定 HDInsight 時，就會執行 hello 指令碼。 在這個階段，hello 指令碼會以平行方式在所有 hello hello 叢集和 hello 節點上執行的根權限與指定的節點。

> [!NOTE]
> 因為 hello 指令碼是 hello 叢集節點上執行的根層級權限，您可以執行作業，例如停止和啟動服務，包括 Hadoop 相關服務。 如果您停止服務，您必須確定確認 hello Ambari 服務與其他相關的 Hadoop 服務已啟動並執行 hello 指令碼完成執行之前完成。 這些服務所需 toosuccessfully 判斷 hello 健全狀況和狀態的 hello 叢集在建立時。


在叢集建立期間，您可以同時使用多個指令碼動作。 這些指令碼會叫用 hello 所指定的順序。

> [!IMPORTANT]
> 指令碼動作必須在 60 分鐘內完成，否則就會逾時。 在叢集佈建，hello 指令碼會執行與其他安裝及設定處理程序。 競爭資源，例如 CPU 時間和網路頻寬可能會導致 hello 指令碼 tootake 長 toofinish 不同於您的開發環境。
>
> toominimize hello 次採用 toorun hello 指令碼，例如下載及編譯來源的應用程式的工作。 先行編譯應用程式，並儲存在 Azure 儲存體中的 hello 二進位檔。


### <a name="script-action-on-a-running-cluster"></a>執行中叢集上的指令碼動作

不同於正在執行的叢集執行的叢集建立期間，指令碼中的失敗動作的指令碼並不會自動導致 hello 叢集 toochange tooa 失敗狀態。 指令碼完成之後，hello 叢集應該會傳回 tooa 「 執行 」 狀態。

> [!IMPORTANT]
> 即使 hello 叢集的 「 執行中 」 狀態，hello 失敗的指令碼可能會有中斷作業。 例如，指令碼無法刪除 hello 叢集所需的檔案。
>
> 根權限，因此您應該確定您了解指令碼會執行之後才套用 tooyour 叢集執行指令碼動作。

當套用指令碼 tooa 叢集，hello 叢集狀態變更 toofrom**執行**太**接受**，然後**HDInsight 組態**，以及最後回太**執行**成功的指令碼。 hello 指令碼狀態來登入 hello 指令碼動作記錄，而且您可以使用此資訊 toodetermine hello 指令碼成功或失敗。 例如，hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell 指令程式可以使用的 tooview hello 狀態的指令碼。 它會傳回資訊的類似 toohello 下列文字：

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> 如果您變更 hello 叢集使用者 (admin) 密碼建立 hello 叢集之後，動作執行對此叢集的指令碼可能會失敗。 如果您有任何保存的指令碼動作的目標背景工作節點，這些指令碼可能會失敗，當您擴充 hello 叢集時。

## <a name="example-script-action-scripts"></a>範例指令碼動作指令碼

指令碼動作的指令碼可以用於透過下列公用程式的 hello:

* Azure 入口網站
* Azure PowerShell
* Azure CLI
* HDInsight .NET SDK

HDInsight 提供下列元件在 HDInsight 叢集上的指令碼 tooinstall hello:

| 名稱 | 指令碼 |
| --- | --- |
| **新增 Azure 儲存體帳戶** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh。請參閱[新增額外的儲存體 tooan HDInsight 叢集](hdinsight-hadoop-add-storage.md)。 |
| **安裝色調** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh。請參閱 [在 HDInsight 叢集上安裝及使用色調](hdinsight-hadoop-hue-linux.md)。 |
| **安裝 Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh。請參閱[在 HDInsight 叢集上安裝和使用 Presto](hdinsight-hadoop-install-presto.md)。 |
| **安裝 Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install-linux.md)。 |
| **安裝 Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh。請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install-linux.md)。 |
| **預先載入 Hive 程式庫** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh。請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)。 |
| **安裝或更新 Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash。 請參閱[在 HDInsight 上安裝或更新 Mono](hdinsight-hadoop-install-mono.md)。 |

## <a name="use-a-script-action-during-cluster-creation"></a>在建立叢集期間使用指令碼動作

本節提供範例 hello 不同的方式，建立的 HDInsight 叢集時，您可以使用指令碼動作。

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>使用指令碼動作在叢集建立 hello Azure 入口網站的期間

1. 依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。 在到達 hello 時停止__叢集摘要__> 一節。

2. 從 hello__叢集摘要__區段中，選取 hello__編輯__連結__進階設定__。

    ![[Advanced settings] \(進階設定\) 連結](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. 從 hello__進階設定__區段中，選取__編寫指令碼動作__。 從 hello__編寫指令碼動作__區段中，選取__+ 新送出__

    ![送出新的指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. 使用 hello__選取指令碼__項目 tooselect 預先製作的指令碼。 toouse 自訂指令碼中，選取__自訂__，然後提供 hello__名稱__和__撞指令碼 URI__指令碼。

    ![Hello 選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    hello 下表描述 hello 表單上的 hello 元素：

    | 屬性 | 值 |
    | --- | --- |
    | 選取指令碼 | toouse 自己的指令碼，選取__自訂__。 否則，請選取其中一個提供的 hello 指令碼。 |
    | 名稱 |指定 hello 指令碼動作的名稱。 |
    | Bash 指令碼 URI |指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。 |
    | Head/Worker/Zookeeper |指定 hello 節點 (**Head**，**工作者**，或**動物園管理員**) 執行哪些 hello 自訂指令碼。 |
    | 參數 |指定 hello 參數，如果 hello 指令碼所需。 |

    使用 hello__保存此指令碼動作__hello 指令碼的項目 tooensure 縮放作業期間套用。

5. 選取__建立__toosave hello 指令碼。 然後您可以使用__+ 送出新__tooadd 另一個指令碼。

    ![多個指令碼動作](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    當您完成新增指令碼時，使用 hello__選取__按鈕，然後再 hello__下一步__按鈕 tooreturn toohello__叢集摘要__> 一節。

3. toocreate hello 叢集上，選取__建立__從 hello__叢集摘要__選取項目。

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>從 Azure 資源管理員範本使用指令碼動作

本節中的 hello 範例示範如何 toouse 指令碼動作的 Azure 資源管理員範本。

#### <a name="before-you-begin"></a>開始之前

* 設定工作站 toorun HDInsight Powershell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。
* 如需有關指示 toocreate 範本，請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。
* 如果您之前未曾搭配使用Azure PowerShell 與資源管理員，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../azure-resource-manager/powershell-azure-resource-manager.md)。

#### <a name="create-clusters-using-script-action"></a>使用指令碼動作建立叢集

1. 複製下列範本 tooa 位置在電腦上的 hello。 此範本安裝 Giraph hello 叢集中的 hello headnodes 和背景工作節點上。 您也可以確認 hello JSON 範本是否有效。 將您的範本內容貼至 [JSONLint](http://jsonlint.com/)，這是一個線上 JSON 驗證器工具。

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. 啟動 Azure PowerShell，並登入 tooyour Azure 帳戶。 提供您的認證之後，hello 命令會傳回您的帳戶相關的資訊。

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. 如果您有多個訂用帳戶，提供 hello 訂用帳戶 ID 想 toouse 部署。

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > 您可以使用`Get-AzureRmSubscription`tooget 與您的帳戶，其中包含針對每個 hello 訂用帳戶 ID 相關聯的所有訂閱的清單。

4. 如果您沒有現有資源群組，請建立新的資源群組。 提供 hello 名稱 hello 資源群組及您需要為您的方案的位置。 會傳回 hello 新資源群組的摘要。

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. 部署您的資源群組，執行 hello toocreate**新增 AzureRmResourceGroupDeployment**命令，並提供 hello 必要參數。 hello 參數包括下列資料的 hello:

    * 部署的名稱
    * hello 的資源群組的名稱
    * hello 路徑或 URL toohello 範本所建立。

  如果您的範本需要任何參數，您也必須傳遞這些參數。 在此情況下，hello 指令碼動作 tooinstall R hello 叢集上的不需要任何參數。

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    您會提示的 tooprovide hello 範本中定義的 hello 參數值。

1. 當已部署 hello 資源群組時，則會顯示 hello 部署的摘要。

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. 如果您的部署失敗，您可以使用下列 cmdlet tooget 資訊有關 hello 失敗 hello。

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>在建立叢集期間從 Azure PowerShell 使用指令碼動作

在本節中，我們使用 hello[新增 AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx)使用指令碼動作 toocustomize 叢集 cmdlet tooinvoke 指令碼。 在繼續之前，請確認您已安裝和設定 Azure PowerShell。 設定工作站 toorun HDInsight PowerShell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

hello 下列指令碼示範如何 tooapply script 動作時使用 PowerShell 建立叢集：

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

可能需要幾分鐘後才建立 hello 叢集。

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>使用指令碼動作在叢集建立時，從 hello HDInsight.NET SDK

hello HDInsight.NET SDK 提供可讓您更輕鬆 toowork 與 HDInsight.NET 應用程式的用戶端程式庫。 如需程式碼範例，請參閱[建立 linux 叢集使用 HDInsight 中的 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)。

## <a name="apply-a-script-action-tooa-running-cluster"></a>適用於執行叢集的指令碼動作 tooa

這一節，了解如何 tooapply 指令碼動作 tooa 執行叢集。

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>適用於執行叢集 hello Azure 入口網站從指令碼動作 tooa

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。

2. 從 hello HDInsight 叢集的概觀，請選取 hello**指令碼動作**磚。

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > 您也可以選取**所有設定**，然後選取 [**指令碼動作**從 hello 設定] 區段。

3. 從 hello hello 指令碼動作 區段頂端，選取**送出新**。

    ![新增指令碼 tooa 執行叢集](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. 使用 hello__選取指令碼__項目 tooselect 預先製作的指令碼。 toouse 自訂指令碼中，選取__自訂__，然後提供 hello__名稱__和__撞指令碼 URI__指令碼。

    ![Hello 選取指令碼表單中加入指令碼](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    hello 下表描述 hello 表單上的 hello 元素：

    | 屬性 | 值 |
    | --- | --- |
    | 選取指令碼 | toouse 自己的指令碼，選取__自訂__。 否則，請選取提供的指令碼。 |
    | 名稱 |指定 hello 指令碼動作的名稱。 |
    | Bash 指令碼 URI |指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。 |
    | Head/Worker/Zookeeper |指定 hello 節點 (**Head**，**工作者**，或**動物園管理員**) 執行哪些 hello 自訂指令碼。 |
    | 參數 |指定 hello 參數，如果 hello 指令碼所需。 |

    使用 hello__保存此指令碼動作__縮放作業期間套用項目 toomake 確定 hello 指令碼。

5. 最後，使用 hello**建立**按鈕 tooapply hello 指令碼 toohello 叢集。

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>適用於執行叢集從 Azure PowerShell 指令碼動作 tooa

在繼續之前，請確認您已安裝和設定 Azure PowerShell。 設定工作站 toorun HDInsight PowerShell cmdlet 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

hello 下列範例會示範如何 tooapply 指令碼動作 tooa 執行叢集：

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Hello 作業完成之後，您會收到下列文字的資訊類似 toohello:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>適用於執行叢集 hello Azure CLI 從指令碼動作 tooa

繼續之前，請確定您已安裝並設定 hello Azure CLI。 如需詳細資訊，請參閱[安裝 hello Azure CLI](../cli-install-nodejs.md)。

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure Resource Manager 模式會使用下列命令在 hello 命令列的 hello:

        azure config mode arm

2. 使用下列 tooauthenticate tooyour Azure 訂用帳戶的 hello。

        azure login

3. 使用下列命令 tooapply 執行叢集的指令碼動作 tooa hello

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    如果省略這個命令的參數，系統會提示您使用。 如果您使用指定的指令碼的 hello`-u`接受參數，您可以指定它們使用 hello`-p`參數。

    有效的節點類型為 `headnode``workernode` 和 `zookeeper`。 如果 hello 指令碼應該套用的 toomultiple 節點型別，指定以分隔 hello 類型 ';'。 例如： `-n headnode;workernode`。

    toopersist hello 指令碼中，加入 hello `--persistOnSuccess`。 您可以也保存 hello 指令碼稍後使用`azure hdinsight script-action persisted set`。

    一旦 hello 作業完成時，您會收到下列文字的輸出類似 toohello:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>適用於執行叢集使用 REST API 的指令碼動作 tooa

請參閱 [在執行中的叢集執行指令碼動作](https://msdn.microsoft.com/library/azure/mt668441.aspx)。

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>適用於從 hello HDInsight.NET SDK 執行叢集的指令碼動作 tooa

如需使用 hello.NET SDK tooapply 指令碼 tooa 叢集的範例，請參閱[https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。

## <a name="view-history-promote-and-demote-script-actions"></a>檢視歷程記錄、升級和降級指令碼動作

### <a name="using-hello-azure-portal"></a>使用 hello Azure 入口網站

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。

2. 從 hello HDInsight 叢集的概觀，請選取 hello**指令碼動作**磚。

    ![指令碼動作磚](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > 您也可以選取**所有設定**，然後選取 [**指令碼動作**從 hello 設定] 區段。

4. 對此叢集的指令碼的歷程記錄會顯示在 hello 指令碼動作 > 一節。 此資訊包含持續性指令碼清單。 在 hello 以下螢幕擷取畫面，您可以看到此叢集執行的指令碼已的 Solr 該 hello。 hello 螢幕擷取畫面不會顯示任何持續性的指令碼。

    ![指令碼動作區段](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. 選取指令碼從 hello 歷程記錄顯示 hello 這個指令碼的內容 > 一節。 從 hello 囉 」 畫面頂端，您可以重新執行 hello 指令碼，或將它升級。

    ![指令碼動作屬性](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. 您也可以使用 hello **...** toohello 方 hello 指令碼動作 > 一節 tooperform 動作上的項目。

    ![指令碼動作...使用情況](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>使用 Azure PowerShell

| 使用下列 hello... | 太... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |擷取持續性指令碼動作的資訊 |
| Get-AzureRmHDInsightScriptActionHistory |擷取指令碼動作套用 toohello 叢集或特定的指令碼的詳細資料的歷程記錄 |
| Set-AzureRmHDInsightPersistedScriptAction |升級特定指令碼動作 tooa 保存的指令碼動作 |
| Remove-AzureRmHDInsightPersistedScriptAction |將保存的指令碼動作 tooan 臨機操作動作降級 |

> [!IMPORTANT]
> 使用`Remove-AzureRmHDInsightPersistedScriptAction`不復原 hello 指令碼所執行的動作。 此 cmdlet 只會移除 hello 保存旗標。

下列範例指令碼的 hello 示範如何使用 hello cmdlet toopromote，然後再降級指令碼。

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>使用 Azure CLI hello

| 使用下列 hello... | 太... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |擷取保存的指令碼動作清單 |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |擷取特定的保存指令碼動作資訊 |
| `azure hdinsight script-action history list <clustername>` |擷取指令碼動作套用 toohello 叢集歷程的記錄 |
| `azure hdinsight script-action history show <clustername> <scriptname>` |擷取特定指令碼動作的資訊 |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |升級特定指令碼動作 tooa 保存的指令碼動作 |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |將保存的指令碼動作 tooan 臨機操作動作降級 |

> [!IMPORTANT]
> 使用`azure hdinsight script-action persisted delete`不復原 hello 指令碼所執行的動作。 此 cmdlet 只會移除 hello 保存旗標。

### <a name="using-hello-hdinsight-net-sdk"></a>使用 hello HDInsight.NET SDK

如需使用 hello.NET SDK tooretrieve 從叢集的指令碼記錄的範例，請升級或降級指令碼，請參閱[https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)。

> [!NOTE]
> 此範例也示範如何 tooinstall HDInsight 應用程式使用 hello.NET SDK。

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>支援在 HDInsight 叢集上使用開放原始碼軟體

hello Microsoft Azure HDInsight 服務會使用開放原始碼技術 Hadoop 周圍形成的生態系統。 Microsoft Azure 可為開放原始碼技術提供一般層級的支援。 如需詳細資訊，請參閱 hello**支援範圍**區段 hello [Azure 支援常見問題集網站，](https://azure.microsoft.com/support/faq/)。 hello HDInsight 服務的內建的元件，提供一層額外的支援。

有兩種可用在 hello HDInsight 服務的開放原始碼元件類型：

* **內建元件**-HDInsight 叢集上已預先安裝這些元件，並提供 hello 叢集的核心功能。 例如，YARN ResourceManager、 hello Hive 查詢語言 (HiveQL) 及 hello 砲象兵程式庫屬於 toothis 類別目錄。 叢集元件的完整清單位於[hello HDInsight 所提供的 Hadoop 叢集版本的新](hdinsight-component-versioning.md)。
* **自訂元件**-您為 hello 叢集的使用者可以安裝或使用您的工作負載中用於 hello 社群或您所建立的任何元件。

> [!WARNING]
> 完全支援元件時附上 hello HDInsight 叢集。 Microsoft 支援服務可協助 tooisolate，並解決問題的相關的 toothese 元件。
>
> 自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 Microsoft 支援服務可能無法 tooresolve hello 問題，或它們可能會要求您 tooengage 可用頻道 hello 開放原始碼技術，找到深層的專業知識，針對該項技術。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。

hello HDInsight 服務提供數種方式 toouse 自訂元件。 hello 套用相同層級支援，無論是使用還是 hello 叢集上安裝元件。 hello 下列清單將描述 hello 最常見方式，可以使用自訂元件的 HDInsight 叢集上：

1. 提交作業-Hadoop 或其他類型的執行，或使用自訂元件的工作可以提交的 toohello 叢集。

2. 叢集自訂-叢集建立期間，您可以指定其他設定及自訂 hello 叢集節點已安裝的元件。

3. 範例-常用的自訂元件、 Microsoft 和其他人可能會提供如何使用這些元件在 hello HDInsight 叢集上的範例。 提供這些範例，但是沒有支援。

## <a name="troubleshooting"></a>疑難排解

您可以使用指令碼動作所記錄的 Ambari web UI tooview 資訊。 如果 hello 指令碼無法在叢集建立期間，hello 記錄檔也會提供 hello 與 hello 叢集相關聯的預設儲存體帳戶中的。 本節提供資訊 tooretrieve hello 記錄使用這兩個選項的方式。

### <a name="using-hello-ambari-web-ui"></a>使用 hello Ambari Web UI

1. 在瀏覽器中瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net。 CLUSTERNAME 取代 hello 的 HDInsight 叢集的名稱。

    出現提示時，輸入 hello 叢集 hello 管理帳戶名稱 （管理員） 和密碼。 Web 表單中，您可能必須 tooreenter hello 系統管理員認證。

2. 在 hello 頁面頂端的 hello hello 列中，選取 hello **ops**項目。 會顯示目前和舊版上執行的作業透過 Ambari hello 叢集清單。

    ![Ambari Web UI 列與選取的 ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. 尋找 hello 的項目**執行\_customscriptaction**在 hello**作業**資料行。 Hello 指令碼動作執行時，會建立這些項目。

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT 和 STDERR 輸出選取 hello run\customscriptaction 項目，然後向下鑽研 hello 連結。 Hello 指令碼執行時，不會產生此輸出，而且可能包含有用的資訊。

### <a name="access-logs-from-hello-default-storage-account"></a>從 hello 預設儲存體帳戶的存取記錄檔

如果 hello 叢集建立失敗，因為 tooa 指令碼動作錯誤，可以從 hello 叢集儲存體帳戶存取 hello 記錄檔。

* hello 儲存體記錄位於`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`。

    ![作業的螢幕擷取畫面](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    在此目錄中，hello 記錄檔會分別叢集前端節點、 workernode，和動物園管理員節點組織。 部分範例如下：

    * **前端節點** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **背景工作節點** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper 節點** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* 所有 stdout 和 stderr 的 hello 對應主機都是上傳 toohello 儲存體帳戶。 每個指令碼動作分別有一個 **output-\*.txt** 和 **errors-\*.txt**。 hello 輸出 *.txt 檔案包含 hello URI 中的 hello 收到 hello 主機執行的指令碼資訊。 例如

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* 您可使用 hello 重複建立指令碼動作叢集相同的名稱。 在這種情況下，您可以區分 hello hello 日期資料夾名稱為基礎的相關記錄。 例如，hello 資料夾結構上不同的日期所建立的叢集 (mycluster) 會出現類似 toohello 下列記錄項目：

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* 如果您以 hello 建立指令碼動作叢集名稱相同的 hello 相同天，您可以使用 hello 唯一的前置詞 tooidentify hello 相關記錄檔。

* 如果您建立叢集附近上午 12:00 （午夜），很可能 hello 記錄檔跨越兩天。 在這種情況下，您會看到兩個不同的日期資料夾 hello 相同叢集中。

* 正在上傳記錄檔 toohello 預設容器可能會佔用 too5 分鐘，特別是針對大型叢集。 因此，如果您想 tooaccess hello 記錄檔，您不應該立即刪除 hello 叢集的指令碼動作失敗時。

### <a name="ambari-watchdog"></a>Ambari 看門狗

> [!WARNING]
> 請勿變更 hello hello Ambari 監視 (hdinsightwatchdog) 以 Linux 為基礎的 HDInsight 叢集上的密碼。 變更此帳戶的 hello 密碼中斷 hello 能力 toorun 新指令碼動作在 hello HDInsight 叢集上。

### <a name="cant-import-name-blobservice"></a>無法匯入名稱 BlobService

__徵兆__: hello 指令碼動作會失敗。 當您檢視 Ambari hello 作業時，會顯示文字類似 toohello 下列錯誤：

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__可能的原因__： 如果您升級 hello Python Azure 儲存體用戶端所包含的 hello HDInsight 叢集，就會發生這個錯誤。 HDInsight 需要 Azure 儲存體用戶端 0.20.0。

__解析__: tooresolve 這個錯誤，請手動連接 tooeach 叢集節點使用`ssh`並使用 hello 遵循命令 tooreinstall hello 正確的儲存體用戶端版本：

```
sudo pip install azure-storage==0.20.0
```

透過 SSH 的連接 toohello 叢集上的資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>歷程記錄不會顯示在叢集建立期間使用的指令碼

如果您在 2016 年 3 月 15 日之前建立叢集，您可能不會在動作歷程記錄中看到任何項目。 如果您在 2016 年 3 月 15 日之後調整 hello 叢集 hello 在叢集建立期間使用的指令碼出現的歷程記錄會套用 toonew hello 一部分的 hello 叢集中節點的調整大小作業。

有兩種例外狀況：

* 如果您的叢集在 2015 年 9 月 1 日之前建立。 此日期是引進指令碼動作的日期。 在此日期之前建立的任何叢集可能都未使用指令碼動作建立叢集。

* 如果您使用多個指令碼動作在叢集建立期間，並使用相同名稱的多個指令碼，或 hello 的 hello 名稱相同，但不同參數的多個指令碼的相同 URI。 在這些情況下，您會收到下列錯誤 hello:

    動作可以是任何新指令碼已 tooconflicting 指令碼名稱，在現有的指令碼因為此叢集上不執行。 建立叢集時所提供的指令碼名稱全都必須是唯一的名稱。 既有的指令碼會在調整大小時執行。

## <a name="next-steps"></a>後續步驟

* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions-linux.md)
* [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install-linux.md)
* [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [新增額外的儲存體 tooan HDInsight 叢集](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "叢集建立期間的階段"
