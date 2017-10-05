---
title: "使用 Azure REST API 建立 Hadoop 叢集 - Azure | Microsoft Docs"
description: "了解如何將 Azure Resource Manager 範本提交至 Azure REST API 來建立 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="154f2-103">使用 Azure REST API 建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="154f2-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="154f2-104">了解如何使用 Azure Resource Manager 範本和 Azure REST API 來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="154f2-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="154f2-105">Azure REST API 可讓您對裝載於 Azure 平台的服務執行管理作業，包括建立新的資源，例如 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="154f2-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="154f2-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="154f2-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="154f2-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="154f2-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="154f2-108">本文件的步驟是使用 [curl (https://curl.haxx.se/)](https://curl.haxx.se/) 公用程式來與 Azure REST API 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="154f2-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="154f2-109">建立範本</span><span class="sxs-lookup"><span data-stu-id="154f2-109">Create a template</span></span>

<span data-ttu-id="154f2-110">Azure Resource Manager 範本是描述**資源群組**與其中所有資源 (例如 HDInsight) 的 JSON 文件。此範本型方法可讓您在一個範本中定義 HDInsight 所需的資源。</span><span class="sxs-lookup"><span data-stu-id="154f2-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="154f2-111">以下 JSON 文件是 [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password) 提供的範本和參數檔合併工具，它會使用密碼來建立以 Linux 為基礎的叢集，以保護 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="154f2-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
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
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="154f2-112">本文件中的步驟引用此範例。</span><span class="sxs-lookup"><span data-stu-id="154f2-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="154f2-113">使用您叢集的值來取代 **Parameters** 區段中的範例值。</span><span class="sxs-lookup"><span data-stu-id="154f2-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="154f2-114">本範本使用 HDInsight 叢集的背景工作節點預設數目 (4)。</span><span class="sxs-lookup"><span data-stu-id="154f2-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="154f2-115">如果您規劃 32 個以上的背景工作節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="154f2-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="154f2-116">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="154f2-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="154f2-117">登入您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="154f2-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="154f2-118">請依照[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) 所述的步驟操作，並使用 `az login` 命令連接到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="154f2-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="154f2-119">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="154f2-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="154f2-120">以下步驟是[使用 Azure CLI 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password)文件中*使用密碼建立服務主體*一節的簡易版。</span><span class="sxs-lookup"><span data-stu-id="154f2-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="154f2-121">這些步驟會建立用來驗證 Azure REST API 的服務主體。</span><span class="sxs-lookup"><span data-stu-id="154f2-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="154f2-122">從命令列中，使用下列命令列出您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="154f2-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="154f2-123">在清單中，選取您要使用的訂用帳戶，並記下 **Subscription_ID** 和 __Tenant_ID__ 資料行。</span><span class="sxs-lookup"><span data-stu-id="154f2-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="154f2-124">儲存這些值。</span><span class="sxs-lookup"><span data-stu-id="154f2-124">Save these values.</span></span>

2. <span data-ttu-id="154f2-125">使用以下命令，在 Azure Active Directory 中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="154f2-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="154f2-126">將 `--display-name`、`--homepage`、`--identifier-uris` 的值取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="154f2-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="154f2-127">為新的 Active Directory 項目提供密碼。</span><span class="sxs-lookup"><span data-stu-id="154f2-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="154f2-128">`--home-page` 和 `--identifier-uris` 值不需參考裝載於網際網路上的實際網頁。</span><span class="sxs-lookup"><span data-stu-id="154f2-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="154f2-129">它們必須是唯一的 URI。</span><span class="sxs-lookup"><span data-stu-id="154f2-129">They must be unique URIs.</span></span>

   <span data-ttu-id="154f2-130">此命令傳回的值是新應用程式的 __App ID__。</span><span class="sxs-lookup"><span data-stu-id="154f2-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="154f2-131">儲存這個值。</span><span class="sxs-lookup"><span data-stu-id="154f2-131">Save this value.</span></span>

3. <span data-ttu-id="154f2-132">使用下列命令以 **App ID** 建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="154f2-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="154f2-133">此命令傳回的值是 __Object ID__。</span><span class="sxs-lookup"><span data-stu-id="154f2-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="154f2-134">儲存這個值。</span><span class="sxs-lookup"><span data-stu-id="154f2-134">Save this value.</span></span>

4. <span data-ttu-id="154f2-135">使用 **Object ID** 值將 **Owner** 角色指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="154f2-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="154f2-136">使用稍早取得的**訂用帳戶 ID** 。</span><span class="sxs-lookup"><span data-stu-id="154f2-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="154f2-137">取得驗證權杖</span><span class="sxs-lookup"><span data-stu-id="154f2-137">Get an authentication token</span></span>

<span data-ttu-id="154f2-138">使用下列命令來擷取驗證權杖︰</span><span class="sxs-lookup"><span data-stu-id="154f2-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="154f2-139">將 `$TENANTID`、`$APPID` 和 `$PASSWORD` 設定為先前取得或使用的值。</span><span class="sxs-lookup"><span data-stu-id="154f2-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="154f2-140">如果這個要求成功，您會收到 200 系列的回應，且回應本文會包含 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="154f2-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="154f2-141">這項要求所傳回的 JSON 文件包含名為 **access_token** 的元素。</span><span class="sxs-lookup"><span data-stu-id="154f2-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="154f2-142">**access_token** 的值是用來驗證對 REST API 的要求。</span><span class="sxs-lookup"><span data-stu-id="154f2-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="154f2-143">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="154f2-143">Create a resource group</span></span>

<span data-ttu-id="154f2-144">使用下列命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="154f2-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="154f2-145">將 `$SUBSCRIPTIONID` 設定為建立服務主體時所收到的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="154f2-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="154f2-146">將 `$ACCESSTOKEN` 設定為上一個步驟中所收到的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="154f2-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="154f2-147">將 `DATACENTERLOCATION` 取代為您要在其中建立資源群組和資源的資料中心。</span><span class="sxs-lookup"><span data-stu-id="154f2-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="154f2-148">例如 'South Central US'。</span><span class="sxs-lookup"><span data-stu-id="154f2-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="154f2-149">將 `$RESOURCEGROUPNAME` 設定為您想要用於此群組的名稱︰</span><span class="sxs-lookup"><span data-stu-id="154f2-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="154f2-150">如果這個要求成功，您會收到 200 系列的回應，且回應主體會包含 JSON 文件，內含群組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="154f2-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="154f2-151">`"provisioningState"` 項目包含的值為 `"Succeeded"`。</span><span class="sxs-lookup"><span data-stu-id="154f2-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="154f2-152">建立部署</span><span class="sxs-lookup"><span data-stu-id="154f2-152">Create a deployment</span></span>

<span data-ttu-id="154f2-153">使用下列命令，將範本部署到資源群組。</span><span class="sxs-lookup"><span data-stu-id="154f2-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="154f2-154">將 `$DEPLOYMENTNAME` 設定為您想要用於此部署的名稱。</span><span class="sxs-lookup"><span data-stu-id="154f2-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="154f2-155">如果您已將範本儲存到檔案，則可使用下列命令，而不是 `-d "{ template and parameters}"`：</span><span class="sxs-lookup"><span data-stu-id="154f2-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="154f2-156">如果這個要求成功，您會收到 200 系列的回應，且回應主體會包含 JSON 文件，內含部署作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="154f2-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="154f2-157">部署已送出，但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="154f2-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="154f2-158">部署通常需要大約 15 分鐘才會完成。</span><span class="sxs-lookup"><span data-stu-id="154f2-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="154f2-159">檢查部署的狀態</span><span class="sxs-lookup"><span data-stu-id="154f2-159">Check the status of a deployment</span></span>

<span data-ttu-id="154f2-160">若要檢查部署的狀態，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="154f2-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="154f2-161">這個命令會傳回包含部署作業相關資訊的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="154f2-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="154f2-162">`"provisioningState"` 項目包含部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="154f2-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="154f2-163">如果此元素包含 `"Succeeded"` 的值，則部署已順利完成。</span><span class="sxs-lookup"><span data-stu-id="154f2-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="154f2-164">疑難排解</span><span class="sxs-lookup"><span data-stu-id="154f2-164">Troubleshoot</span></span>

<span data-ttu-id="154f2-165">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="154f2-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="154f2-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="154f2-166">Next steps</span></span>

<span data-ttu-id="154f2-167">既然您已成功建立 HDInsight 叢集，請使用下列內容來了解如何使用您的叢集。</span><span class="sxs-lookup"><span data-stu-id="154f2-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="154f2-168">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="154f2-168">Hadoop clusters</span></span>

* [<span data-ttu-id="154f2-169">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="154f2-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="154f2-170">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="154f2-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="154f2-171">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="154f2-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="154f2-172">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="154f2-172">HBase clusters</span></span>

* [<span data-ttu-id="154f2-173">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="154f2-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="154f2-174">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="154f2-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="154f2-175">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="154f2-175">Storm clusters</span></span>

* [<span data-ttu-id="154f2-176">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="154f2-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="154f2-177">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="154f2-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="154f2-178">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="154f2-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
