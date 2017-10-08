---
title: "使用 Azure REST API Azure aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何 toocreate HDInsight 叢集所送出 Azure Resource Manager 範本 toohello Azure REST API。"
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
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="c4502-103">建立 Hadoop 叢集使用 hello Azure REST API</span><span class="sxs-lookup"><span data-stu-id="c4502-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="c4502-104">了解如何 toocreate 在 HDInsight 叢集使用 Azure Resource Manager 範本和 hello Azure REST API。</span><span class="sxs-lookup"><span data-stu-id="c4502-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="c4502-105">hello Azure REST API 可讓您在服務裝載於 Azure 平台，包括建立新的資源，例如 HDInsight 叢集 hello hello tooperform 管理作業。</span><span class="sxs-lookup"><span data-stu-id="c4502-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4502-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c4502-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c4502-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c4502-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="c4502-108">在此文件使用 hello 步驟 hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/)公用程式 toocommunicate 以 hello Azure REST API。</span><span class="sxs-lookup"><span data-stu-id="c4502-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="c4502-109">建立範本</span><span class="sxs-lookup"><span data-stu-id="c4502-109">Create a template</span></span>

<span data-ttu-id="c4502-110">Azure Resource Manager 範本是描述**資源群組**與其中所有資源 (例如 HDInsight) 的 JSON 文件。此範本為基礎的方法可讓您 toodefine hello 資源所需的 HDInsight 中其中一個範本。</span><span class="sxs-lookup"><span data-stu-id="c4502-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="c4502-111">hello 下列 JSON 文件是 hello 合併從範本和參數檔案[https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password)，這樣就可以建立以 Linux 為基礎使用密碼 toosecure hello SSH 使用者帳戶的叢集。</span><span class="sxs-lookup"><span data-stu-id="c4502-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

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
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
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
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
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

<span data-ttu-id="c4502-112">這個範例用於 hello 本文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="c4502-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="c4502-113">取代 hello 範例*值*在 hello**參數**hello 值為您的叢集 > 一節。</span><span class="sxs-lookup"><span data-stu-id="c4502-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4502-114">hello 範本使用 HDInsight 叢集的背景工作節點 (4) hello 預設數目。</span><span class="sxs-lookup"><span data-stu-id="c4502-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="c4502-115">如果您規劃 32 個以上的背景工作節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="c4502-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="c4502-116">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="c4502-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="c4502-117">登入 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c4502-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="c4502-118">請依照下列中記載的 hello 步驟[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)連接 tooyour 訂用帳戶使用 hello 和`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="c4502-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="c4502-119">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="c4502-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="c4502-120">這些步驟會縮減的版的 hello*建立具有密碼的服務主體*區段 hello[使用 Azure CLI toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password)文件。</span><span class="sxs-lookup"><span data-stu-id="c4502-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="c4502-121">這些步驟會建立服務主體所使用的 tooauthenticate toohello Azure REST API。</span><span class="sxs-lookup"><span data-stu-id="c4502-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="c4502-122">從命令列使用下列命令 toolist hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4502-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="c4502-123">在 hello 清單中，選取您想 toouse，並記下 hello 的 hello 訂用帳戶**Subscription_ID**和__Tenant_ID__資料行。</span><span class="sxs-lookup"><span data-stu-id="c4502-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="c4502-124">儲存這些值。</span><span class="sxs-lookup"><span data-stu-id="c4502-124">Save these values.</span></span>

2. <span data-ttu-id="c4502-125">使用下列命令 toocreate Azure Active Directory 中的應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="c4502-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="c4502-126">Hello hello 值取代`--display-name`， `--homepage`，和`--identifier-uris`以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c4502-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="c4502-127">Hello 新 Active Directory 項目提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="c4502-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4502-128">hello`--home-page`和`--identifier-uris`值不需要實際 hello 上裝載的 web 網頁 tooreference 網際網路。</span><span class="sxs-lookup"><span data-stu-id="c4502-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="c4502-129">它們必須是唯一的 URI。</span><span class="sxs-lookup"><span data-stu-id="c4502-129">They must be unique URIs.</span></span>

   <span data-ttu-id="c4502-130">hello 從此命令傳回的值為 hello__應用程式識別碼__hello 新應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4502-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="c4502-131">儲存這個值。</span><span class="sxs-lookup"><span data-stu-id="c4502-131">Save this value.</span></span>

3. <span data-ttu-id="c4502-132">使用 hello 下列命令 toocreate 服務主體使用 hello**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="c4502-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="c4502-133">hello 從此命令傳回的值為 hello__物件識別碼__。</span><span class="sxs-lookup"><span data-stu-id="c4502-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="c4502-134">儲存這個值。</span><span class="sxs-lookup"><span data-stu-id="c4502-134">Save this value.</span></span>

4. <span data-ttu-id="c4502-135">指派 hello**擁有者**角色 toohello 服務主體使用 hello**物件識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="c4502-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="c4502-136">使用 hello**訂用帳戶 ID**您稍早取得。</span><span class="sxs-lookup"><span data-stu-id="c4502-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="c4502-137">取得驗證權杖</span><span class="sxs-lookup"><span data-stu-id="c4502-137">Get an authentication token</span></span>

<span data-ttu-id="c4502-138">使用下列命令 tooretrieve 驗證權杖的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4502-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="c4502-139">設定`$TENANTID`， `$APPID`，和`$PASSWORD`toohello 值取得或先前用過。</span><span class="sxs-lookup"><span data-stu-id="c4502-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="c4502-140">如果這個要求成功，您會收到 200 數列回應和 hello 回應主體包含 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="c4502-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="c4502-141">hello 這項要求所傳回的 JSON 文件包含的項目名稱為**access_token**。</span><span class="sxs-lookup"><span data-stu-id="c4502-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="c4502-142">hello 值**access_token**是使用的 tooauthentication 要求 toohello REST API。</span><span class="sxs-lookup"><span data-stu-id="c4502-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="c4502-143">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="c4502-143">Create a resource group</span></span>

<span data-ttu-id="c4502-144">使用下列 toocreate 資源群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="c4502-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="c4502-145">設定`$SUBSCRIPTIONID`時建立服務主體的 hello 收到 toohello 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="c4502-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="c4502-146">設定`$ACCESSTOKEN`toohello 收到 hello 上一個步驟中的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="c4502-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="c4502-147">取代`DATACENTERLOCATION`hello 資料中心您希望 toocreate hello 資源群組、 資源中。</span><span class="sxs-lookup"><span data-stu-id="c4502-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="c4502-148">例如 'South Central US'。</span><span class="sxs-lookup"><span data-stu-id="c4502-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="c4502-149">設定`$RESOURCEGROUPNAME`toohello 想 toouse 此群組的名稱：</span><span class="sxs-lookup"><span data-stu-id="c4502-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="c4502-150">如果這個要求成功，您會收到 200 數列回應和 hello 回應主體包含 JSON 文件包含 hello 群組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4502-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="c4502-151">hello`"provisioningState"`項目包含值為`"Succeeded"`。</span><span class="sxs-lookup"><span data-stu-id="c4502-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="c4502-152">建立部署</span><span class="sxs-lookup"><span data-stu-id="c4502-152">Create a deployment</span></span>

<span data-ttu-id="c4502-153">使用下列命令 toodeploy hello 範本 toohello 資源群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="c4502-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="c4502-154">設定`$DEPLOYMENTNAME`toohello 想 toouse 此部署的名稱。</span><span class="sxs-lookup"><span data-stu-id="c4502-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="c4502-155">如果您儲存 hello 範本 tooa 檔案時，您可以使用下列命令，而不是 hello `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="c4502-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="c4502-156">如果這個要求成功，您會收到 200 數列回應和 hello 回應主體包含 JSON 文件包含 hello 部署作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4502-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4502-157">hello 部署已送出，但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="c4502-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="c4502-158">可能需要幾分鐘的時間，通常大約 15 hello 部署 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="c4502-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="c4502-159">檢查部署的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="c4502-159">Check hello status of a deployment</span></span>

<span data-ttu-id="c4502-160">hello 部署中，下列命令使用 hello toocheck hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="c4502-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="c4502-161">此命令會傳回包含 hello 部署作業的相關資訊的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="c4502-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="c4502-162">hello`"provisioningState"`元素包含 hello 部署的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="c4502-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="c4502-163">如果這個項目包含值為`"Succeeded"`，然後 hello 部署已順利完成。</span><span class="sxs-lookup"><span data-stu-id="c4502-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="c4502-164">疑難排解</span><span class="sxs-lookup"><span data-stu-id="c4502-164">Troubleshoot</span></span>

<span data-ttu-id="c4502-165">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="c4502-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4502-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4502-166">Next steps</span></span>

<span data-ttu-id="c4502-167">既然您已成功建立的 HDInsight 叢集，請使用 hello 如何遵循 toolearn toowork 與您的叢集。</span><span class="sxs-lookup"><span data-stu-id="c4502-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="c4502-168">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="c4502-168">Hadoop clusters</span></span>

* [<span data-ttu-id="c4502-169">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="c4502-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c4502-170">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="c4502-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c4502-171">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="c4502-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="c4502-172">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="c4502-172">HBase clusters</span></span>

* [<span data-ttu-id="c4502-173">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="c4502-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="c4502-174">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4502-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="c4502-175">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="c4502-175">Storm clusters</span></span>

* [<span data-ttu-id="c4502-176">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="c4502-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="c4502-177">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="c4502-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="c4502-178">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="c4502-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
