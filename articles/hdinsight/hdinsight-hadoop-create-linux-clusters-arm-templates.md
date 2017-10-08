---
title: "使用範本-Azure HDInsight 叢集的 aaaCreate Hadoop |Microsoft 文件"
description: "了解 hdinsight toocreate 叢集使用的資源管理員範本如何"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

在本文中，您了解幾個方式 toocreate Azure HDInsight 叢集的 Azure Resource Manager 範本。 如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)。 toolearn 有關其他叢集建立工具和功能，按一下 [hello] 索引標籤選取器在 hello 或頂端的這個頁面，請參閱[叢集建立方法](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods)。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toofollow hello 本文中的指示，您將需要：

* [Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* Azure PowerShell 和/或 Azure CLI。

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Resource Manager 範本
資源管理員範本可讓應用程式是單一的協調作業，在下列簡單 toocreate hello:
* HDInsight 叢集和其相依的資源 （例如 hello 預設儲存體帳戶）
* 其他資源 （例如 Azure SQL Database toouse Apache Sqoop)

在 hello 範本中，您可以定義 hello 資源所需的 hello 應用程式。 您也可以指定部署參數 tooinput 值不同的環境。 hello 範本包含 JSON 和您使用您的部署 tooconstruct 值的運算式。

您可以在 [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/?term=hdinsight)中找到 HDInsight 範本範例。 使用跨平台[Visual Studio Code](https://code.visualstudio.com/#alt-downloads)以 hello[資源管理員延伸模組](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools)或文字編輯器 toosave hello 」 範本，您的工作站上的檔案。 您了解 toocall 如何 hello 範本使用不同的方法。

如需有關資源管理員範本的詳細資訊，請參閱下列文章 hello:

* [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)
* [使用 Azure Resource Manager 範本部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>產生範本

藉由使用 hello Azure 入口網站，您可以設定叢集的所有 hello 內容，並儲存 hello 範本後再進行部署。 然後，您可以重複使用 hello 範本。

**toogenerate 使用 hello Azure 入口網站的範本**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**新增**hello 左窗格中，按一下 **智慧 + 分析**，然後按一下 **HDInsight**。
3. 遵循 hello 指示 tooenter 屬性。 您可以使用任一 hello**快速建立**或 hello**自訂**選項。
4. 在 hello**摘要**索引標籤上，按一下 **下載範本和參數**:

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    您會看到一份 hello 範本檔案中，參數檔案的程式碼範例使用 toodeploy hello 範本：

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載選項](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    從這裡，您可以下載 hello 範本、 將它儲存 tooyour 樣板程式庫或部署 hello 範本。

    tooaccess 範本，以在程式庫中，按一下**更多服務**從 hello 左的功能表，然後再按一下**範本**(下 hello**其他**類別)。

    > [!Note]
    > 必須同時使用 hello 範本和參數檔案。 否則，您可能會得到非預期的結果。 比方說，hello 預設**clusterKind**屬性值一律是**hadoop**，儘管您之前，指定您下載 hello 範本。



## <a name="deploy-with-powershell"></a>使用 PowerShell 部署

此程序會在 HDInsight 中建立 Hadoop 叢集。

1. 將 hello JSON 檔案儲存在 hello[附錄](#appx-a-arm-template)tooyour 工作站。 Hello PowerShell 指令碼，在 hello 檔案名稱是`C:\HDITutorials-ARM\hdinsight-arm-template.json`。
2. 視需要設定 hello 參數和變數。
3. 使用下列 PowerShell 指令碼的 hello 執行 hello 範本：

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    hello PowerShell 指令碼會設定 hello 叢集名稱。 hello 儲存體帳戶名稱是硬式編碼 hello 範本中。 您已提示的 tooenter hello 叢集使用者密碼。 (hello 預設使用者名稱是**admin**。)您也會提示的 tooenter hello SSH 使用者密碼。 (hello 預設 SSH 使用者名稱是**sshuser**。)  

如需詳細資訊，請參閱[使用 PowerShell 進行部署](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)。

## <a name="deploy-with-cli"></a>使用 CLI 部署
hello 下列範例會使用 Azure 命令列介面 (CLI)。 它會藉由呼叫 Resource Manager 範本來建立叢集和其依存的儲存體帳戶與容器：

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

提示的 tooenter︰
* hello 叢集名稱。
* hello 叢集使用者的密碼。 (hello 預設使用者名稱是**admin**。)
* hello SSH 使用者密碼。 (hello 預設 SSH 使用者名稱是**sshuser**。)

下列程式碼的 hello 提供內嵌參數：

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>部署以 hello REST API
請參閱[hello REST API 使用部署](../azure-resource-manager/resource-group-template-deploy-rest.md)。

## <a name="deploy-with-visual-studio"></a>透過 Visual Studio 部署
 使用 Visual Studio toocreate 資源群組專案，並將其部署 tooAzure 透過 hello 使用者介面。 您可以選取資源 tooinclude hello 類型在專案中。 這些資源會自動加入 toohello Resource Manager 範本。 hello 專案也提供 PowerShell 指令碼 toodeploy hello 範本。

如簡介 toousing Visual Studio 與資源群組，請參閱[建立和部署 Azure 資源群組，透過 Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會數種方式 toocreate 的 HDInsight 叢集。 toolearn 詳細資訊，請參閱下列文章 hello:

* 如需部署透過 hello.NET 用戶端程式庫資源的範例，請參閱[使用.NET 程式庫和範本部署資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 如需部署應用程式的深入範例，請參閱 [透過可預測方式在 Azure 中佈建和部署微服務](../app-service-web/app-service-deploy-complex-application-predictably.md)。
* 如需部署解決方案 toodifferent 環境需求的指引，請參閱[Microsoft Azure 中的開發和測試環境](../solution-dev-test-environments.md)。
* toolearn 關於 hello 區段 hello Azure 資源管理員範本，請參閱[撰寫樣板](../azure-resource-manager/resource-group-authoring-templates.md)。
* 如需您可以使用 Azure Resource Manager 範本中的 hello 函式的清單，請參閱[樣板函式](../azure-resource-manager/resource-group-template-functions.md)。

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>附錄： 資源管理員範本 toocreate Hadoop 叢集
hello 下列 Azure 資源管理員範本會建立以 Linux 為基礎的 Hadoop 叢集與 hello 相依的 Azure 儲存體帳戶。

> [!NOTE]
> 此範例包括 Hive 中繼存放區和 Oozie 中繼存放區的組態資訊。 移除 hello 區段，或使用 hello 範本之前設定 hello > 一節。
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>附錄： 資源管理員範本 toocreate Spark 叢集

本節提供資源管理員範本，您可以使用 toocreate HDInsight Spark 叢集。 此範本包含 `spark-defaults` 和 `spark-thrift-sparkconf` (適用於 Spark 1.6 叢集) 與 `spark2-defaults` 和 `spark2-thrift-sparkconf` (適用於 Spark 2 叢集) 的設定。 此外 toothis，HDInsight 計算，並設定組態，例如`spark.executor.instances`， `spark.executor.memory`，和`spark.executor.cores`根據 hello 叢集大小。 

如果您設定任何一個參數區段中 hello 範本本身的一部分，HDInsight 不計算，設定 hello hello 的其他參數相同的區段。 例如，參數`spark.executor.instances`處於 hello`spark-defaults`組態。 如果您設定另一個參數 (例如， `spark.yarn.exector.memoryOverhead`) 在 hello`spark-defaults`組態中，HDInsight 不會計算和設定 hello`spark.executor.instances`參數以及。

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
