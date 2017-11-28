---
title: "aaaAzure CLI 命令在 Resource Manager 模式 |Microsoft 文件"
description: "Azure 命令列介面 (CLI) 命令 toomanage hello Resource Manager 部署模型中的資源"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="70459-103">Resource Manager 模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="70459-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="70459-104">本文章提供語法和選項的 Azure 命令列介面 (CLI) 命令您通常會使用 toocreate 及管理在 hello Azure Resource Manager 部署模型中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="70459-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="70459-105">您可以在資源管理員 (arm) 模式中執行 hello CLI 存取這些命令。</span><span class="sxs-lookup"><span data-stu-id="70459-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="70459-106">這不是完整的參考，您的 CLI 版本可能會顯示稍微不同的命令或參數。</span><span class="sxs-lookup"><span data-stu-id="70459-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="70459-107">如需 Azure 資源及資源群組的一般概觀，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70459-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="70459-108">此文章會向資源管理員模式命令示範在 hello Azure CLI，有時也稱為 Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="70459-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="70459-109">toowork hello 資源管理員模型中的，您可以嘗試 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)下, 一個層代多重平台 CLI。</span><span class="sxs-lookup"><span data-stu-id="70459-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="70459-110">進一步了解 hello[舊的和新 Azure Cli](/cli/azure/old-and-new-clis)。</span><span class="sxs-lookup"><span data-stu-id="70459-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="70459-111">第一次 tooget 啟動[安裝 hello Azure CLI](../cli-install-nodejs.md)和[連接 tooyour Azure 訂用帳戶](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="70459-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="70459-112">如需目前的命令語法和選項在 hello Resource Manager 模式中的命令列，輸入`azure help`或特定的命令，toodisplay 說明`azure help [command]`。</span><span class="sxs-lookup"><span data-stu-id="70459-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="70459-113">建立及管理特定的 Azure 服務，也 hello 文件中找到 CLI 範例。</span><span class="sxs-lookup"><span data-stu-id="70459-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="70459-114">選用參數會以方括弧括住 (例如， `[parameter]`)。</span><span class="sxs-lookup"><span data-stu-id="70459-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="70459-115">其他所有參數皆為必要參數。</span><span class="sxs-lookup"><span data-stu-id="70459-115">All other parameters are required.</span></span>

<span data-ttu-id="70459-116">在加法 toocommand 特定選擇性參數記載在這裡，有三個選擇性參數可能是使用的 toodisplay 詳細的輸出，例如要求選項和狀態碼。</span><span class="sxs-lookup"><span data-stu-id="70459-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="70459-117">hello`-v`參數提供詳細資訊輸出，以及 hello`-vv`參數提供更詳細的詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="70459-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="70459-118">hello`--json`選項將未經處理的 json 格式的 hello 結果的輸出。</span><span class="sxs-lookup"><span data-stu-id="70459-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="70459-119">設定 hello Resource Manager 模式</span><span class="sxs-lookup"><span data-stu-id="70459-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="70459-120">使用下列命令 tooenable Azure CLI Resource Manager 模式命令 hello。</span><span class="sxs-lookup"><span data-stu-id="70459-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="70459-121">hello CLI Azure Resource Manager 模式和 Azure 服務管理模式互斥。</span><span class="sxs-lookup"><span data-stu-id="70459-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="70459-122">也就是一種模式中建立的資源無法在此管理 hello 其他模式。</span><span class="sxs-lookup"><span data-stu-id="70459-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="70459-123">azure account：用來管理帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="70459-123">azure account: Manage your account information</span></span>
<span data-ttu-id="70459-124">Hello 工具 tooconnect tooyour 帳戶會使用您的 Azure 訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="70459-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="70459-125">**列出 hello 匯入的訂閱**</span><span class="sxs-lookup"><span data-stu-id="70459-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="70459-126">**顯示關於訂用帳戶的詳細資料**</span><span class="sxs-lookup"><span data-stu-id="70459-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="70459-127">**設定 hello 目前訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="70459-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="70459-128">**移除訂用帳戶或環境中，或清除所有 hello 儲存帳戶和環境資訊**</span><span class="sxs-lookup"><span data-stu-id="70459-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="70459-129">**命令 toomanage 您帳戶的環境**</span><span class="sxs-lookup"><span data-stu-id="70459-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="70459-130">azure ad： 命令 toodisplay Active Directory 物件</span><span class="sxs-lookup"><span data-stu-id="70459-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="70459-131">**命令 toodisplay active directory 應用程式**</span><span class="sxs-lookup"><span data-stu-id="70459-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="70459-132">**命令 toodisplay active directory 群組**</span><span class="sxs-lookup"><span data-stu-id="70459-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="70459-133">**命令 tooprovide active directory 子群組] 或 [成員資訊**</span><span class="sxs-lookup"><span data-stu-id="70459-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="70459-134">**命令 toodisplay active directory 服務主體**</span><span class="sxs-lookup"><span data-stu-id="70459-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="70459-135">**命令 toodisplay active directory 使用者**</span><span class="sxs-lookup"><span data-stu-id="70459-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="70459-136">azure availset: toomanage 指令程式的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="70459-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="70459-137">**在資源群組內建立可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="70459-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="70459-138">**列出 hello 資源群組內的可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="70459-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="70459-139">**在資源群組內取得一個可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="70459-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="70459-140">**在資源群組內刪除一個可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="70459-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="70459-141">azure 設定： 您的本機設定命令 toomanage</span><span class="sxs-lookup"><span data-stu-id="70459-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="70459-142">**列出 Azure CLI 組態設定**</span><span class="sxs-lookup"><span data-stu-id="70459-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="70459-143">**刪除組態設定**</span><span class="sxs-lookup"><span data-stu-id="70459-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="70459-144">**更新組態設定**</span><span class="sxs-lookup"><span data-stu-id="70459-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="70459-145">**設定 hello Azure CLI 運作模式 tooeither`arm`或`asm`**</span><span class="sxs-lookup"><span data-stu-id="70459-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="70459-146">azure 功能： 命令 toomanage 帳戶功能</span><span class="sxs-lookup"><span data-stu-id="70459-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="70459-147">**列出您訂用帳戶可用的所有功能**</span><span class="sxs-lookup"><span data-stu-id="70459-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="70459-148">**顯示功能**</span><span class="sxs-lookup"><span data-stu-id="70459-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="70459-149">**註冊資源提供者的預覽功能**</span><span class="sxs-lookup"><span data-stu-id="70459-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="70459-150">azure 的群組： 命令 toomanage 資源群組</span><span class="sxs-lookup"><span data-stu-id="70459-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="70459-151">**建立資源群組**</span><span class="sxs-lookup"><span data-stu-id="70459-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="70459-152">**設定標記 tooa 資源群組**</span><span class="sxs-lookup"><span data-stu-id="70459-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="70459-153">**刪除資源群組**</span><span class="sxs-lookup"><span data-stu-id="70459-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="70459-154">**列出訂用帳戶的 hello 資源群組**</span><span class="sxs-lookup"><span data-stu-id="70459-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="70459-155">**顯示您訂用帳戶的資源群組**</span><span class="sxs-lookup"><span data-stu-id="70459-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="70459-156">**命令 toomanage 資源群組的記錄檔**</span><span class="sxs-lookup"><span data-stu-id="70459-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="70459-157">**您在資源群組中的部署命令 toomanage**</span><span class="sxs-lookup"><span data-stu-id="70459-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="70459-158">**命令 toomanage 您本機或組件庫的資源群組範本**</span><span class="sxs-lookup"><span data-stu-id="70459-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="70459-159">azure hdinsight： 命令 toomanage 您的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="70459-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="70459-160">**命令 toocreate，或加入 tooa 叢集設定檔**</span><span class="sxs-lookup"><span data-stu-id="70459-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="70459-161">範例： 建立設定檔，包含指令碼動作 toorun 時建立叢集。</span><span class="sxs-lookup"><span data-stu-id="70459-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="70459-162">**命令 toocreate 叢集資源群組中**</span><span class="sxs-lookup"><span data-stu-id="70459-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="70459-163">範例：在 Linux 叢集上建立 Storm</span><span class="sxs-lookup"><span data-stu-id="70459-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="70459-164">範例：使用指令碼動作建立叢集</span><span class="sxs-lookup"><span data-stu-id="70459-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="70459-165">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="70459-166">**命令 toodelete 叢集**</span><span class="sxs-lookup"><span data-stu-id="70459-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="70459-167">**命令 tooshow 叢集詳細資料**</span><span class="sxs-lookup"><span data-stu-id="70459-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="70459-168">**所有的命令 toolist 叢集 （在特定的資源群組中，如果提供）**</span><span class="sxs-lookup"><span data-stu-id="70459-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="70459-169">**命令 tooresize 叢集**</span><span class="sxs-lookup"><span data-stu-id="70459-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="70459-170">**命令叢集 tooenable HTTP 存取**</span><span class="sxs-lookup"><span data-stu-id="70459-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="70459-171">**命令叢集 toodisable HTTP 存取**</span><span class="sxs-lookup"><span data-stu-id="70459-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="70459-172">**叢集命令 tooenable RDP 存取**</span><span class="sxs-lookup"><span data-stu-id="70459-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="70459-173">**命令叢集 toodisable HTTP 存取**</span><span class="sxs-lookup"><span data-stu-id="70459-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="70459-174">azure insights： 命令相關 toomonitoring Insights （事件、 警示規則，自動調整規模設定、 度量）</span><span class="sxs-lookup"><span data-stu-id="70459-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="70459-175">**擷取訂用帳戶、CorrelationID、資源群組、資源或資源提供者的作業記錄**</span><span class="sxs-lookup"><span data-stu-id="70459-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="70459-176">azure 位置： 命令 tooget hello 可用位置的所有資源類型</span><span class="sxs-lookup"><span data-stu-id="70459-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="70459-177">**清單 hello 可用的位置**</span><span class="sxs-lookup"><span data-stu-id="70459-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="70459-178">azure 網路： 命令 toomanage 網路資源</span><span class="sxs-lookup"><span data-stu-id="70459-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="70459-179">**命令 toomanage 虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="70459-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="70459-180">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="70459-180">Creates a virtual network.</span></span> <span data-ttu-id="70459-181">Hello 在下列範例中我們建立虛擬網路命名 hello 美國西部區域中的資源群組 myresourcegroup newvnet。</span><span class="sxs-lookup"><span data-stu-id="70459-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="70459-182">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="70459-183">更新資源群組內的虛擬網路組態。</span><span class="sxs-lookup"><span data-stu-id="70459-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="70459-184">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="70459-185">hello 命令會列出資源群組中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="70459-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="70459-186">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="70459-187">hello 命令會顯示在資源群組中的 hello 虛擬網路屬性。</span><span class="sxs-lookup"><span data-stu-id="70459-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="70459-188">hello 命令會移除虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="70459-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="70459-189">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="70459-190">**命令 toomanage 虛擬網路子網路**</span><span class="sxs-lookup"><span data-stu-id="70459-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="70459-191">加入另一個子網路 tooan 現有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="70459-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="70459-192">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="70459-193">設定資源群組內的特定虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="70459-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="70459-194">列出所有資源群組內的特定虛擬網路的 hello 虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="70459-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="70459-195">顯示虛擬網路子網路屬性</span><span class="sxs-lookup"><span data-stu-id="70459-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="70459-196">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="70459-197">從現有的虛擬網路移除子網路。</span><span class="sxs-lookup"><span data-stu-id="70459-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="70459-198">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="70459-199">**命令 toomanage 負載平衡器**</span><span class="sxs-lookup"><span data-stu-id="70459-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="70459-200">建立負載平衡器集合。</span><span class="sxs-lookup"><span data-stu-id="70459-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="70459-201">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="70459-202">列出資源群組中負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="70459-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="70459-203">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="70459-204">顯示資源群組中特定負載平衡器的負載平衡器資訊</span><span class="sxs-lookup"><span data-stu-id="70459-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="70459-205">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="70459-206">刪除負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="70459-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="70459-207">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="70459-208">**命令 toomanage 探查的負載平衡器**</span><span class="sxs-lookup"><span data-stu-id="70459-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-209">Hello 負載平衡器中建立健全狀況狀態的 hello 探查的設定。</span><span class="sxs-lookup"><span data-stu-id="70459-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="70459-210">請注意 toorun 此命令，您的負載平衡器需要前端 ip 資源 （請查看命令 「 azure 網路前端 ip"tooassign ip 位址 tooload 平衡器）。</span><span class="sxs-lookup"><span data-stu-id="70459-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="70459-211">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-212">使用適用的新值來更新現有的負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="70459-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="70459-213">參數選項</span><span class="sxs-lookup"><span data-stu-id="70459-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="70459-214">清單 hello 負載平衡器集的探查屬性。</span><span class="sxs-lookup"><span data-stu-id="70459-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="70459-215">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-216">移除 hello 探查建立 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="70459-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="70459-217">**命令 toomanage 前端 ip 組態的負載平衡器**</span><span class="sxs-lookup"><span data-stu-id="70459-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-218">建立現有的負載平衡器集前端 IP 組態 tooan。</span><span class="sxs-lookup"><span data-stu-id="70459-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-219">更新現有組態的前端下方 IP.hello 命令加入稱為 mypubip5 tooan 現有負載平衡器前端 IP 名為 myfrontendip 公用 IP。</span><span class="sxs-lookup"><span data-stu-id="70459-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="70459-220">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="70459-221">列出 hello 負載平衡器設定所有的 hello 前端 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="70459-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="70459-222">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-223">刪除 hello 前端 IP 相關聯的物件 tooload 平衡器</span><span class="sxs-lookup"><span data-stu-id="70459-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="70459-224">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="70459-225">**命令 toomanage 後端位址集區的負載平衡器**</span><span class="sxs-lookup"><span data-stu-id="70459-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-226">建立負載平衡器的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="70459-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="70459-227">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="70459-228">列出特定資源群組的後端 IP 位址集區範圍</span><span class="sxs-lookup"><span data-stu-id="70459-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="70459-229">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="70459-230">網路 lb 位址集區刪除 [選項] < 資源群組 >< lb-n a m ><name></span><span class="sxs-lookup"><span data-stu-id="70459-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="70459-231">從負載平衡器移除 hello 後端 IP 集區範圍資源。</span><span class="sxs-lookup"><span data-stu-id="70459-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="70459-232">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="70459-233">**命令 toomanage 負載平衡器規則**</span><span class="sxs-lookup"><span data-stu-id="70459-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-234">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="70459-234">Create load balancer rules.</span></span>

<span data-ttu-id="70459-235">您可以建立負載平衡器規則設定 hello 負載平衡器和 hello 後端位址集區範圍 tooreceive hello 連入網路流量的 hello 前端端點。</span><span class="sxs-lookup"><span data-stu-id="70459-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="70459-236">設定也會包含 hello 前端 IP 端點的連接埠和連接埠 hello 後端位址集區範圍。</span><span class="sxs-lookup"><span data-stu-id="70459-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="70459-237">hello 下列範例示範如何 toocreate 負載平衡器法則 hello 前端端點接聽 tooport 80 TCP 和負載平衡的網路流量傳送 hello 後端位址集區範圍 tooport 8080。</span><span class="sxs-lookup"><span data-stu-id="70459-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-238">更新特定資源群組中的現有負載平衡器規則設定。</span><span class="sxs-lookup"><span data-stu-id="70459-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="70459-239">在下列範例的 hello，我們會從 mylbrule toomynewlbrule 變更 hello 規則名稱。</span><span class="sxs-lookup"><span data-stu-id="70459-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="70459-240">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="70459-241">列出特定資源群組中針對負載平衡器所設定的所有負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="70459-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="70459-242">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-243">刪除負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="70459-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="70459-244">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="70459-245">**命令 toomanage 負載平衡器輸入 NAT 規則**</span><span class="sxs-lookup"><span data-stu-id="70459-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-246">建立負載平衡器的輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="70459-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="70459-247">在 hello 我們建立 NAT 規則從前端 IP (先前已定義使用 hello azure 網路前端-ip 命令） 輸入的接聽連接埠與輸出連接埠的 hello 負載平衡器的下列範例會使用 toosend hello 網路流量。</span><span class="sxs-lookup"><span data-stu-id="70459-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="70459-248">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="70459-249">更新現有的輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="70459-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="70459-250">在下列範例的 hello，我們變更 hello 輸入從 80 too81 接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="70459-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="70459-251">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="70459-252">列出負載平衡器的所有輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="70459-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="70459-253">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="70459-254">刪除特定的資源群組中的 hello 負載平衡器 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="70459-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="70459-255">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="70459-256">**命令 toomanage 公用 ip 位址**</span><span class="sxs-lookup"><span data-stu-id="70459-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="70459-257">建立公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="70459-257">Creates a public ip resource.</span></span> <span data-ttu-id="70459-258">您將建立 hello 公用 ip 資源，並將 tooa 網域名稱產生關聯。</span><span class="sxs-lookup"><span data-stu-id="70459-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="70459-259">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="70459-260">更新現有的公用 ip 資源 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="70459-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="70459-261">Hello 下列範例中我們會從動態 tooStatic 變更 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="70459-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="70459-262">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="70459-263">network public-ip list [options] &lt;resource-group&gt; 列出資源群組中的所有公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="70459-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="70459-264">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="70459-265">網路的公用 ip 會顯示 [選項] < 資源群組 ><name></span><span class="sxs-lookup"><span data-stu-id="70459-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="70459-266">顯示資源群組中公用 IP 資源的公用 IP 屬性。</span><span class="sxs-lookup"><span data-stu-id="70459-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="70459-267">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="70459-268">刪除公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="70459-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="70459-269">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="70459-270">**命令 toomanage 網路介面**</span><span class="sxs-lookup"><span data-stu-id="70459-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="70459-271">建立稱為網路介面 (NIC) 可用於負載平衡器或關聯 tooa 虛擬機器的資源。</span><span class="sxs-lookup"><span data-stu-id="70459-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="70459-272">參數選項：</span><span class="sxs-lookup"><span data-stu-id="70459-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="70459-273">**命令 toomanage 網路安全性群組**</span><span class="sxs-lookup"><span data-stu-id="70459-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="70459-274">**命令 toomanage 網路安全性群組規則**</span><span class="sxs-lookup"><span data-stu-id="70459-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="70459-275">**命令 toomanage 流量管理員設定檔**</span><span class="sxs-lookup"><span data-stu-id="70459-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="70459-276">**命令 toomanage 流量管理員端點**</span><span class="sxs-lookup"><span data-stu-id="70459-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="70459-277">**命令 toomanage 虛擬網路閘道**</span><span class="sxs-lookup"><span data-stu-id="70459-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="70459-278">azure 提供者： 命令 toomanage 資源提供者登錄</span><span class="sxs-lookup"><span data-stu-id="70459-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="70459-279">**列出 Resource Manager 中目前已註冊的提供者**</span><span class="sxs-lookup"><span data-stu-id="70459-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="70459-280">**顯示詳細資料，關於 hello 要求提供者命名空間**</span><span class="sxs-lookup"><span data-stu-id="70459-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="70459-281">**登錄提供者與 hello 訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="70459-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="70459-282">**取消註冊提供者與 hello 訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="70459-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="70459-283">azure 資源： 命令 toomanage 資源</span><span class="sxs-lookup"><span data-stu-id="70459-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="70459-284">**建立資源群組中的資源**</span><span class="sxs-lookup"><span data-stu-id="70459-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="70459-285">**更新資源群組中的資源而不使用任何範本或參數**</span><span class="sxs-lookup"><span data-stu-id="70459-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="70459-286">**列出 hello 資源**</span><span class="sxs-lookup"><span data-stu-id="70459-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="70459-287">**取得資源群組或訂用帳戶中的一項資源**</span><span class="sxs-lookup"><span data-stu-id="70459-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="70459-288">**刪除資源群組中的資源**</span><span class="sxs-lookup"><span data-stu-id="70459-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="70459-289">azure 角色： 命令 toomanage 您的 Azure 角色</span><span class="sxs-lookup"><span data-stu-id="70459-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="70459-290">**取得所有可用的角色定義**</span><span class="sxs-lookup"><span data-stu-id="70459-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="70459-291">**取得一項可用的角色定義**</span><span class="sxs-lookup"><span data-stu-id="70459-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="70459-292">**命令 toomanage 您的角色指派**</span><span class="sxs-lookup"><span data-stu-id="70459-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="70459-293">azure 儲存體： 命令 toomanage 儲存物件</span><span class="sxs-lookup"><span data-stu-id="70459-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="70459-294">**命令 toomanage 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="70459-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="70459-295">**命令 toomanage 儲存體帳戶金鑰**</span><span class="sxs-lookup"><span data-stu-id="70459-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="70459-296">**命令 tooshow 您儲存體連接字串**</span><span class="sxs-lookup"><span data-stu-id="70459-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="70459-297">**命令 toomanage 儲存體容器**</span><span class="sxs-lookup"><span data-stu-id="70459-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="70459-298">**命令 toomanage 共用存取簽章的儲存體容器**</span><span class="sxs-lookup"><span data-stu-id="70459-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="70459-299">**命令 toomanage 預存存取原則的儲存體容器**</span><span class="sxs-lookup"><span data-stu-id="70459-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="70459-300">**命令 toomanage 儲存體 blob**</span><span class="sxs-lookup"><span data-stu-id="70459-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="70459-301">**命令 toomanage 您的 blob 複製作業**</span><span class="sxs-lookup"><span data-stu-id="70459-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="70459-302">**命令 toomanage 共用的存取簽章，您的儲存體 blob**</span><span class="sxs-lookup"><span data-stu-id="70459-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="70459-303">**命令 toomanage 您存放裝置檔案共用**</span><span class="sxs-lookup"><span data-stu-id="70459-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="70459-304">**命令 toomanage 儲存體檔案**</span><span class="sxs-lookup"><span data-stu-id="70459-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="70459-305">**命令 toomanage 您儲存體的檔案目錄**</span><span class="sxs-lookup"><span data-stu-id="70459-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="70459-306">**命令 toomanage 儲存體佇列**</span><span class="sxs-lookup"><span data-stu-id="70459-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="70459-307">**您的儲存體佇列命令 toomanage 共用存取簽章**</span><span class="sxs-lookup"><span data-stu-id="70459-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="70459-308">**命令 toomanage 預存存取原則的儲存體佇列**</span><span class="sxs-lookup"><span data-stu-id="70459-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="70459-309">**命令 toomanage 您的儲存體記錄屬性**</span><span class="sxs-lookup"><span data-stu-id="70459-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="70459-310">**命令 toomanage 您儲存體度量屬性**</span><span class="sxs-lookup"><span data-stu-id="70459-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="70459-311">**命令 toomanage 儲存體資料表**</span><span class="sxs-lookup"><span data-stu-id="70459-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="70459-312">**命令 toomanage 共用存取簽章的儲存體資料表**</span><span class="sxs-lookup"><span data-stu-id="70459-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="70459-313">**命令 toomanage 預存存取原則的儲存體資料表**</span><span class="sxs-lookup"><span data-stu-id="70459-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="70459-314">azure 的標記： 命令 toomanage 資源管理員索引標籤</span><span class="sxs-lookup"><span data-stu-id="70459-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="70459-315">**新增標記**</span><span class="sxs-lookup"><span data-stu-id="70459-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="70459-316">**移除整個標記或標記值**</span><span class="sxs-lookup"><span data-stu-id="70459-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="70459-317">**列出 hello 標記資訊**</span><span class="sxs-lookup"><span data-stu-id="70459-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="70459-318">**取得標記**</span><span class="sxs-lookup"><span data-stu-id="70459-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="70459-319">azure vm： 命令 toomanage 的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="70459-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="70459-320">**建立 VM**</span><span class="sxs-lookup"><span data-stu-id="70459-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="70459-321">**建立使用預設資源的 VM**</span><span class="sxs-lookup"><span data-stu-id="70459-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="70459-322">CLI 版本 0.10 從開始，您可以提供簡短的別名，例如"UbuntuLTS"或"Win2012R2Datacenter 」 為 hello`image-urn`一些受歡迎的 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="70459-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="70459-323">執行 `azure help vm quick-create` 以取得選項。</span><span class="sxs-lookup"><span data-stu-id="70459-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="70459-324">此外，開頭為 0.10，版本`azure vm quick-create`如果有的話 hello 所選資料區域中，依預設採用高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="70459-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="70459-325">**列出 hello 虛擬機器內的帳戶**</span><span class="sxs-lookup"><span data-stu-id="70459-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="70459-326">**取得資源群組中的一個虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="70459-327">**刪除資源群組中的一個虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="70459-328">**關閉資源群組中的一個虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="70459-329">**重新啟動資源群組中的一個虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="70459-330">**啟動資源群組中的一個虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="70459-331">**資源群組和版本 hello 內關閉一部虛擬機器計算資源**</span><span class="sxs-lookup"><span data-stu-id="70459-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="70459-332">**列出可用的虛擬機器大小**</span><span class="sxs-lookup"><span data-stu-id="70459-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="70459-333">**擷取 hello 做為作業系統映像的 VM 或 VM 映像**</span><span class="sxs-lookup"><span data-stu-id="70459-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="70459-334">**設定 hello VM tooGeneralized hello 狀態**</span><span class="sxs-lookup"><span data-stu-id="70459-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="70459-335">**取得執行個體檢視的 hello VM**</span><span class="sxs-lookup"><span data-stu-id="70459-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="70459-336">**讓您在虛擬機器與 hello 帳戶具有系統管理員或 sudo 授權 tooreset hello 密碼 tooreset 遠端桌面存取或 SSH 設定**</span><span class="sxs-lookup"><span data-stu-id="70459-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="70459-337">**以新資料更新 VM**</span><span class="sxs-lookup"><span data-stu-id="70459-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="70459-338">**命令 toomanage 您虛擬機器的資料磁碟**</span><span class="sxs-lookup"><span data-stu-id="70459-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="70459-339">**命令 toomanage VM 資源擴充功能**</span><span class="sxs-lookup"><span data-stu-id="70459-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="70459-340">**命令 toomanage Docker 虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="70459-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="70459-341">**命令 toomanage VM 映像**</span><span class="sxs-lookup"><span data-stu-id="70459-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
