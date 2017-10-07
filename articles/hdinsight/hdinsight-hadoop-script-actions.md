---
title: "aaaScript 與 HDInsight 的 Azure 開發動作 |Microsoft 文件"
description: "了解如何 toocustomize Hadoop 叢集以指令碼動作。 指令碼動作都可以使用的 tooinstall 應用程式安裝在叢集的 Hadoop 叢集或 toochange hello 組態上所執行的其他軟體。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="39923-104">開發 HDInsight Windows 型叢集指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="39923-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="39923-105">了解指令碼動作 toowrite hdinsight 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-105">Learn how toowrite Script Action scripts for HDInsight.</span></span> <span data-ttu-id="39923-106">如需使用指令碼動作指令碼的資訊，請參閱[使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="39923-107">Hello 同一篇文章撰寫以 Linux 為基礎的 HDInsight 叢集，請參閱[開發指令碼動作的指令碼 hdinsight](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-107">For hello same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="39923-108">hello 這個文件的唯一工作 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="39923-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="39923-109">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="39923-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="39923-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="39923-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39923-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="39923-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="39923-112">如需有關搭配 Linux 型叢集使用指令碼動作的詳細資訊，請參閱[使用 HDInsight 進行指令碼動作開發 (Linux)](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="39923-113">指令碼動作都可以使用的 tooinstall 應用程式安裝在叢集的 Hadoop 叢集或 toochange hello 組態上所執行的其他軟體。</span><span class="sxs-lookup"><span data-stu-id="39923-113">Script Action can be used tooinstall additional software running on a Hadoop cluster or toochange hello configuration of applications installed on a cluster.</span></span> <span data-ttu-id="39923-114">指令碼動作時的 HDInsight 叢集部署中，於 hello 叢集節點執行的指令碼，而且它們會執行 hello 叢集中的節點完成 HDInsight 組態之後。</span><span class="sxs-lookup"><span data-stu-id="39923-114">Script actions are scripts that run on hello cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in hello cluster complete HDInsight configuration.</span></span> <span data-ttu-id="39923-115">指令碼動作在系統管理員帳戶權限下執行，並提供完整存取權限 toohello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="39923-115">A script action is executed under system admin account privileges and provides full access rights toohello cluster nodes.</span></span> <span data-ttu-id="39923-116">每個叢集可以提供一份指令碼動作 toobe 指定中的 hello 順序執行。</span><span class="sxs-lookup"><span data-stu-id="39923-116">Each cluster can be provided with a list of script actions toobe executed in hello order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="39923-117">如果您遇到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="39923-117">If you experience hello following error message:</span></span>
>
> <span data-ttu-id="39923-118">System.Management.Automation.CommandNotFoundException;ExceptionMessage: hello 詞彙 ' 儲存 HDIFile' 無法辨識為 cmdlet、 函式、 指令碼檔案或可執行程式 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="39923-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : hello term 'Save-HDIFile' is not recognized as hello name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="39923-119">Hello hello 名稱拼字檢查，或如果包含路徑的話，請確認該 hello 路徑正確，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="39923-119">Check hello spelling of hello name, or if a path was included, verify that hello path is correct and try again.</span></span>
> <span data-ttu-id="39923-120">這是因為您未包含 hello helper 方法。</span><span class="sxs-lookup"><span data-stu-id="39923-120">It is because you didn't include hello helper methods.</span></span>  <span data-ttu-id="39923-121">請參閱 [自訂指令碼的協助程式方法](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts)。</span><span class="sxs-lookup"><span data-stu-id="39923-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="39923-122">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="39923-122">Sample scripts</span></span>
<span data-ttu-id="39923-123">在 Windows 作業系統上建立 HDInsight 叢集，hello 指令碼動作是 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-123">For creating HDInsight clusters on Windows operating system, hello Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="39923-124">hello 下列指令碼是設定 hello 站台設定檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="39923-124">hello following script is a sample for configuring hello site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="39923-125">hello 指令碼會將四個參數、 hello 組態檔名稱、 hello toomodify，hello 值 tooset，以及描述您想要的屬性。</span><span class="sxs-lookup"><span data-stu-id="39923-125">hello script takes four parameters, hello configuration file name, hello property you want toomodify, hello value you want tooset, and a description.</span></span> <span data-ttu-id="39923-126">例如：</span><span class="sxs-lookup"><span data-stu-id="39923-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="39923-127">這些參數會設定 hello hive.metastore.client.socket.timeout 值 too90 hello hive-site.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="39923-127">These parameters sets hello hive.metastore.client.socket.timeout value too90 in hello hive-site.xml file.</span></span>  <span data-ttu-id="39923-128">hello 預設值為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="39923-128">hello default value is 60 seconds.</span></span>

<span data-ttu-id="39923-129">此範例指令碼位於 [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1)。</span><span class="sxs-lookup"><span data-stu-id="39923-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="39923-130">HDInsight 提供數個指令碼 tooinstall 其他元件在 HDInsight 叢集上：</span><span class="sxs-lookup"><span data-stu-id="39923-130">HDInsight provides several scripts tooinstall additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="39923-131">名稱</span><span class="sxs-lookup"><span data-stu-id="39923-131">Name</span></span> | <span data-ttu-id="39923-132">指令碼</span><span class="sxs-lookup"><span data-stu-id="39923-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="39923-133">**安裝 Spark**</span><span class="sxs-lookup"><span data-stu-id="39923-133">**Install Spark**</span></span> |<span data-ttu-id="39923-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1。</span><span class="sxs-lookup"><span data-stu-id="39923-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="39923-135">請參閱[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]。</span><span class="sxs-lookup"><span data-stu-id="39923-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="39923-136">**安裝 R**</span><span class="sxs-lookup"><span data-stu-id="39923-136">**Install R**</span></span> |<span data-ttu-id="39923-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1。</span><span class="sxs-lookup"><span data-stu-id="39923-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="39923-138">請參閱[在 HDInsight 叢集上安裝和使用 R][hdinsight-r-scripts]。</span><span class="sxs-lookup"><span data-stu-id="39923-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="39923-139">**安裝 Solr**</span><span class="sxs-lookup"><span data-stu-id="39923-139">**Install Solr**</span></span> |<span data-ttu-id="39923-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="39923-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="39923-141">請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="39923-142">- **安裝 Giraph**</span><span class="sxs-lookup"><span data-stu-id="39923-142">- **Install Giraph**</span></span> |<span data-ttu-id="39923-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="39923-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="39923-144">請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="39923-145">可以從 hello Azure 入口網站，Azure PowerShell 部署指令碼動作，或使用 hello HDInsight.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="39923-145">Script Action can be deployed from hello Azure portal, Azure PowerShell or by using hello HDInsight .NET SDK.</span></span>  <span data-ttu-id="39923-146">如需詳細資訊，請參閱[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]。</span><span class="sxs-lookup"><span data-stu-id="39923-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="39923-147">hello 範例指令碼工作只會與 HDInsight 叢集版本 3.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="39923-147">hello sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="39923-148">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="39923-149">自訂指令碼的協助程式方法</span><span class="sxs-lookup"><span data-stu-id="39923-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="39923-150">指令碼動作協助程式方法是您在撰寫字訂指令碼時可以使用的公用程式。</span><span class="sxs-lookup"><span data-stu-id="39923-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="39923-151">這些方法會定義在[https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)，而且可以包含在指令碼使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="39923-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using hello following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="39923-152">以下是這個指令碼所提供的 hello helper 方法：</span><span class="sxs-lookup"><span data-stu-id="39923-152">Here are hello helper methods that are provided by this script:</span></span>

| <span data-ttu-id="39923-153">協助程式方法</span><span class="sxs-lookup"><span data-stu-id="39923-153">Helper method</span></span> | <span data-ttu-id="39923-154">說明</span><span class="sxs-lookup"><span data-stu-id="39923-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39923-155">**Save-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="39923-155">**Save-HDIFile**</span></span> |<span data-ttu-id="39923-156">下載檔案，以從 hello hello 與 hello Azure VM 節點指派的 toohello 叢集相關聯的本機磁碟上指定統一資源識別元 (URI) tooa 位置。</span><span class="sxs-lookup"><span data-stu-id="39923-156">Download a file from hello specified Uniform Resource Identifier (URI) tooa location on hello local disk that is associated with hello Azure VM node assigned toohello cluster.</span></span> |
| <span data-ttu-id="39923-157">**Expand-HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="39923-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="39923-158">將壓縮檔解壓縮。</span><span class="sxs-lookup"><span data-stu-id="39923-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="39923-159">**Invoke-HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="39923-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="39923-160">從 cmd.exe 執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="39923-161">**Write-HDILog**</span><span class="sxs-lookup"><span data-stu-id="39923-161">**Write-HDILog**</span></span> |<span data-ttu-id="39923-162">將輸出寫入從 hello 自訂指令碼的指令碼動作使用。</span><span class="sxs-lookup"><span data-stu-id="39923-162">Write output from hello custom script used for a script action.</span></span> |
| <span data-ttu-id="39923-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="39923-163">**Get-Services**</span></span> |<span data-ttu-id="39923-164">取得一份 hello 指令碼的執行位置 hello 機器上執行服務。</span><span class="sxs-lookup"><span data-stu-id="39923-164">Get a list of services running on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="39923-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="39923-165">**Get-Service**</span></span> |<span data-ttu-id="39923-166">Hello 特定服務名稱做為輸入，以取得特定服務的詳細的資訊 （服務名稱、 處理序識別碼、 狀態等等） hello hello 指令碼的執行位置的電腦上。</span><span class="sxs-lookup"><span data-stu-id="39923-166">With hello specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="39923-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="39923-167">**Get-HDIServices**</span></span> |<span data-ttu-id="39923-168">取得在 hello 指令碼的執行位置 hello 電腦上執行的 HDInsight 服務的清單。</span><span class="sxs-lookup"><span data-stu-id="39923-168">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="39923-169">**Get-HDIService**</span></span> |<span data-ttu-id="39923-170">Hello 特定 HDInsight 服務的名稱做為輸入，以取得特定服務的詳細的資訊 （服務名稱、 處理序識別碼、 狀態等等） hello hello 指令碼的執行位置的電腦上。</span><span class="sxs-lookup"><span data-stu-id="39923-170">With hello specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="39923-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="39923-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="39923-172">取得電腦執行 hello hello 指令碼的執行位置的服務清單。</span><span class="sxs-lookup"><span data-stu-id="39923-172">Get a list of services that are running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="39923-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="39923-174">檢查是否特定服務 （依名稱） 電腦上執行 hello hello 指令碼執行的位置。</span><span class="sxs-lookup"><span data-stu-id="39923-174">Check if a specific service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="39923-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="39923-176">取得在 hello 指令碼的執行位置 hello 電腦上執行的 HDInsight 服務的清單。</span><span class="sxs-lookup"><span data-stu-id="39923-176">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="39923-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="39923-178">檢查是否特定的 HDInsight 服務 （依名稱） 電腦上執行 hello hello 指令碼執行的位置。</span><span class="sxs-lookup"><span data-stu-id="39923-178">Check if a specific HDInsight service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="39923-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="39923-180">取得 hello hello hello 指令碼的執行位置的電腦上安裝的 Hadoop 版本。</span><span class="sxs-lookup"><span data-stu-id="39923-180">Get hello version of Hadoop installed on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="39923-181">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="39923-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="39923-182">檢查 hello hello 指令碼的執行位置的電腦是否為前端節點。</span><span class="sxs-lookup"><span data-stu-id="39923-182">Check if hello computer where hello script executes is a head node.</span></span> |
| <span data-ttu-id="39923-183">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="39923-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="39923-184">檢查 hello hello 指令碼的執行位置的電腦是否為作用中的前端節點。</span><span class="sxs-lookup"><span data-stu-id="39923-184">Check if hello computer where hello script executes is an active head node.</span></span> |
| <span data-ttu-id="39923-185">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="39923-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="39923-186">檢查 hello hello 指令碼的執行位置的電腦是否為資料節點。</span><span class="sxs-lookup"><span data-stu-id="39923-186">Check if hello computer where hello script executes is a data node.</span></span> |
| <span data-ttu-id="39923-187">**Edit-HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="39923-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="39923-188">編輯 hello 設定檔 hive-site.xml、 core-site.xml、 hdfs-site.xml、 mapred-site.xml 或 yarn-site.xml。</span><span class="sxs-lookup"><span data-stu-id="39923-188">Edit hello config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="39923-189">指令碼開發的最佳做法</span><span class="sxs-lookup"><span data-stu-id="39923-189">Best practices for script development</span></span>
<span data-ttu-id="39923-190">當您開發的 HDInsight 叢集的自訂指令碼時，有數個最佳作法 tookeep 事項：</span><span class="sxs-lookup"><span data-stu-id="39923-190">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* <span data-ttu-id="39923-191">Hello Hadoop 版本檢查</span><span class="sxs-lookup"><span data-stu-id="39923-191">Check for hello Hadoop version</span></span>

    <span data-ttu-id="39923-192">HDInsight (Hadoop 2.4) 3.1 版和更新版本支援在叢集上使用指令碼動作 tooinstall 自訂元件。</span><span class="sxs-lookup"><span data-stu-id="39923-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action tooinstall custom components on a cluster.</span></span> <span data-ttu-id="39923-193">在自訂指令碼，您必須使用 hello **Get HDIHadoopVersion**協助程式方法 toocheck hello Hadoop 版本再繼續執行其他工作 hello 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="39923-193">In your custom script, you must use hello **Get-HDIHadoopVersion** helper method toocheck hello Hadoop version before proceeding with performing other tasks in hello script.</span></span>
* <span data-ttu-id="39923-194">提供穩定連結 tooscript 資源</span><span class="sxs-lookup"><span data-stu-id="39923-194">Provide stable links tooscript resources</span></span>

    <span data-ttu-id="39923-195">使用者應該確定所有 hello 指令碼和用於 hello 自訂叢集的其他成品仍可在整個 hello 叢集的 hello 存留期和 hello 這些檔案的版本，不會變更 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="39923-195">Users should make sure that all hello scripts and other artifacts used in hello customization of a cluster remain available throughout hello lifetime of hello cluster and that hello versions of these files do not change for hello duration.</span></span> <span data-ttu-id="39923-196">需要 hello 重新安裝映像 hello 叢集中的節點時，這些資源是必要的。</span><span class="sxs-lookup"><span data-stu-id="39923-196">These resources are required if hello reimaging of nodes in hello cluster is required.</span></span> <span data-ttu-id="39923-197">hello 最佳作法是 toodownload 和封存 hello 使用者控制項的儲存體帳戶中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="39923-197">hello best practice is toodownload and archive everything in a Storage account that hello user controls.</span></span> <span data-ttu-id="39923-198">這可以是 hello 預設儲存體帳戶或任何 hello 自訂叢集部署的 hello 時間在指定其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="39923-198">This can be hello default Storage account or any of hello additional Storage accounts specified at hello time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="39923-199">在 hello Spark 和 R 自訂叢集範例 hello 文件，比方說，我們已經 hello 資源的本機複本中這個儲存體帳戶提供： https://hdiconfigactions.blob.core.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="39923-199">In hello Spark and R customized cluster samples provided in hello documentation, for example, we have made a local copy of hello resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="39923-200">確保 hello 叢集自訂指令碼為等冪</span><span class="sxs-lookup"><span data-stu-id="39923-200">Ensure that hello cluster customization script is idempotent</span></span>

    <span data-ttu-id="39923-201">您必須預期之 HDInsight 叢集的 hello 節點建立映像 hello 叢集存留期間。</span><span class="sxs-lookup"><span data-stu-id="39923-201">You must expect that hello nodes of an HDInsight cluster is reimaged during hello cluster lifetime.</span></span> <span data-ttu-id="39923-202">每當叢集重新安裝映像時，會執行 hello 叢集自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-202">hello cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="39923-203">此指令碼必須是設計的 toobe 等冪 hello 意義上，在重新安裝映像，hello 指令碼應該確定該 hello 叢集就會傳回的 toohello 相同自訂只在 hello 指令碼 hello 叢集是一開始的第一次執行後的狀態建立。</span><span class="sxs-lookup"><span data-stu-id="39923-203">This script must be designed toobe idempotent in hello sense that upon reimaging, hello script should ensure that hello cluster is returned toohello same customized state that it was in just after hello script ran for hello first time when hello cluster was initially created.</span></span> <span data-ttu-id="39923-204">例如，如果自訂的指令碼上安裝應用程式在 D:\AppLocation 第一個執行，然後在每個後續的執行時重新安裝映像，hello 指令碼應該檢查 hello 應用程式是否存在於 hello D:\AppLocation 位置，再繼續進行與其他hello 指令碼中的步驟。</span><span class="sxs-lookup"><span data-stu-id="39923-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, hello script should check whether hello application exists at hello D:\AppLocation location before proceeding with other steps in hello script.</span></span>
* <span data-ttu-id="39923-205">在 hello 最佳位置，安裝自訂元件</span><span class="sxs-lookup"><span data-stu-id="39923-205">Install custom components in hello optimal location</span></span>

    <span data-ttu-id="39923-206">叢集節點是映像，hello C:\ 資源磁碟機和 D:\ 系統磁碟機可以重新格式化，進而導致 hello 遺失資料與這些磁碟機已安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="39923-206">When cluster nodes are reimaged, hello C:\ resource drive and D:\ system drive can be reformatted, resulting in hello loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="39923-207">也會發生此問題如果 hello 叢集一部分的 Azure 虛擬機器 (VM) 節點關閉，且取代為新的節點。</span><span class="sxs-lookup"><span data-stu-id="39923-207">This could also happen if an Azure virtual machine (VM) node that is part of hello cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="39923-208">您可以在 hello D:\ 磁碟機上，或在 hello C:\apps 位置 hello 叢集上安裝元件。</span><span class="sxs-lookup"><span data-stu-id="39923-208">You can install components on hello D:\ drive or in hello C:\apps location on hello cluster.</span></span> <span data-ttu-id="39923-209">會保留在 hello C:\ 磁碟機上的所有其他位置。</span><span class="sxs-lookup"><span data-stu-id="39923-209">All other locations on hello C:\ drive are reserved.</span></span> <span data-ttu-id="39923-210">指定應用程式庫會安裝在 hello 叢集自訂指令碼的 toobe hello 位置。</span><span class="sxs-lookup"><span data-stu-id="39923-210">Specify hello location where applications or libraries are toobe installed in hello cluster customization script.</span></span>
* <span data-ttu-id="39923-211">確保高可用性的 hello 叢集架構</span><span class="sxs-lookup"><span data-stu-id="39923-211">Ensure high availability of hello cluster architecture</span></span>

    <span data-ttu-id="39923-212">HDInsight 具有高可用性的主動 / 被動架構，在哪一個前端節點處於現用模式 （hello HDInsight 服務執行所在） 而且 hello 其他前端節點是在待命模式中 （在哪一個 HDInsight 服務未執行）。</span><span class="sxs-lookup"><span data-stu-id="39923-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where hello HDInsight services are running) and hello other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="39923-213">如果 HDInsight 服務會中斷主動和被動模式切換 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="39923-213">hello nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="39923-214">如果指令碼動作是使用的 tooinstall 服務兩個前端節點上的高可用性，請注意該 hello HDInsight 容錯移轉機制不是能 tooautomatically 失敗這些使用者安裝的服務。</span><span class="sxs-lookup"><span data-stu-id="39923-214">If a script action is used tooinstall services on both head nodes for high availability, note that hello HDInsight failover mechanism is not able tooautomatically fail over these user-installed services.</span></span> <span data-ttu-id="39923-215">因此使用者安裝高可用性的預期的 toobe HDInsight 前端節點上的服務必須有自己的容錯移轉機制，如果在主動 / 被動模式中，或為主動 / 主動模式中。</span><span class="sxs-lookup"><span data-stu-id="39923-215">So user-installed services on HDInsight head nodes that are expected toobe highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="39923-216">HDInsight 編寫動作的指令碼命令執行兩個前端節點上時指定 hello 前端節點角色 hello 中的值做為*ClusterRoleCollection*參數。</span><span class="sxs-lookup"><span data-stu-id="39923-216">An HDInsight Script Action command runs on both head nodes when hello head-node role is specified as a value in hello *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="39923-217">因此，當您設計自訂指令碼時，請確定您的指令碼知道這項設定。</span><span class="sxs-lookup"><span data-stu-id="39923-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="39923-218">您應該不會發生問題 hello 相同的服務會安裝並啟動這兩個 hello 前端節點上，而且他們最後彼此競爭。</span><span class="sxs-lookup"><span data-stu-id="39923-218">You should not run into problems where hello same services are installed and started on both of hello head nodes and they end up competing with each other.</span></span> <span data-ttu-id="39923-219">此外，請注意，資料會遺失期間重新安裝映像，因此透過指令碼動作所安裝的軟體具有 toobe 彈性 toosuch 事件。</span><span class="sxs-lookup"><span data-stu-id="39923-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has toobe resilient toosuch events.</span></span> <span data-ttu-id="39923-220">應用程式應該設計的 toowork 分散到多個節點的高可用性資料。</span><span class="sxs-lookup"><span data-stu-id="39923-220">Applications should be designed toowork with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="39923-221">請注意，最多 1/5 hello 叢集中的節點可以重新安裝映像在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="39923-221">Note that as many as 1/5 of hello nodes in a cluster can be reimaged at hello same time.</span></span>
* <span data-ttu-id="39923-222">設定 hello 自訂元件 toouse Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="39923-222">Configure hello custom components toouse Azure Blob storage</span></span>

    <span data-ttu-id="39923-223">hello hello 叢集節點安裝的自訂元件可能會有預設組態 toouse Hadoop 分散式檔案系統 (HDFS) 儲存體。</span><span class="sxs-lookup"><span data-stu-id="39923-223">hello custom components that you install on hello cluster nodes might have a default configuration toouse Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="39923-224">您應該改為變更 hello 組態 toouse Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="39923-224">You should change hello configuration toouse Azure Blob storage instead.</span></span> <span data-ttu-id="39923-225">在叢集重新安裝映像，取得格式化 hello HDFS 檔案系統，您就會遺失任何資料儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="39923-225">On a cluster reimage, hello HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="39923-226">改用 Azure Blob 儲存體可確保資料保留下來。</span><span class="sxs-lookup"><span data-stu-id="39923-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="39923-227">常見使用模式</span><span class="sxs-lookup"><span data-stu-id="39923-227">Common usage patterns</span></span>
<span data-ttu-id="39923-228">此章節提供指引實作某些 hello 常見的使用模式，您可能會遇到撰寫自訂指令碼時。</span><span class="sxs-lookup"><span data-stu-id="39923-228">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="39923-229">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="39923-229">Configure environment variables</span></span>
<span data-ttu-id="39923-230">通常在指令碼動作開發中，您會覺得 hello 需要 tooset 環境變數。</span><span class="sxs-lookup"><span data-stu-id="39923-230">Often in script action development, you feel hello need tooset environment variables.</span></span> <span data-ttu-id="39923-231">比方說，最可能的案例是當您從外部網站下載二進位檔案、 安裝 hello 在叢集上，並將 hello 其所在安裝的 tooyour 'PATH' 環境變數的位置。</span><span class="sxs-lookup"><span data-stu-id="39923-231">For instance, a most likely scenario is when you download a binary from an external site, install it on hello cluster, and add hello location of where it is installed tooyour ‘PATH’ environment variable.</span></span> <span data-ttu-id="39923-232">下列程式碼片段的 hello 顯示 tooset 環境變數中的 hello 自訂指令碼的方式。</span><span class="sxs-lookup"><span data-stu-id="39923-232">hello following snippet shows you how tooset environment variables in hello custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="39923-233">這個陳述式設定環境變數，hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello 值為 'true'，也設定 hello 這個變數 toobe 全機器的範圍。</span><span class="sxs-lookup"><span data-stu-id="39923-233">This statement sets hello environment variable **MDS_RUNNER_CUSTOM_CLUSTER** toohello value 'true' and also sets hello scope of this variable toobe machine-wide.</span></span> <span data-ttu-id="39923-234">有時候很重要設定環境變數時，就在 hello 適當範圍-電腦或使用者。</span><span class="sxs-lookup"><span data-stu-id="39923-234">At times it is important that environment variables are set at hello appropriate scope – machine or user.</span></span> <span data-ttu-id="39923-235">如需設定環境變數的詳細資訊，請參閱[這裡][1]。</span><span class="sxs-lookup"><span data-stu-id="39923-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="39923-236">存取的 toolocations hello 自訂指令碼的儲存位置</span><span class="sxs-lookup"><span data-stu-id="39923-236">Access toolocations where hello custom scripts are stored</span></span>
<span data-ttu-id="39923-237">使用指令碼 toocustomize 叢集需求 tooeither 是 hello 叢集 hello 預設儲存體帳戶中或在任何其他儲存體帳戶上的公用唯讀容器。</span><span class="sxs-lookup"><span data-stu-id="39923-237">Scripts used toocustomize a cluster needs tooeither be in hello default storage account for hello cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="39923-238">如果您的指令碼會存取位在其他位置的資源這些需要在可公開存取的 toobe (至少公用唯讀)。</span><span class="sxs-lookup"><span data-stu-id="39923-238">If your script accesses resources located elsewhere these need toobe in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="39923-239">例如，您可能想 tooaccess 檔案，並儲存使用 hello SaveFile HDI 命令。</span><span class="sxs-lookup"><span data-stu-id="39923-239">For instance you might want tooaccess a file and save it using hello SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="39923-240">在此範例中，您必須確定該 hello 容器儲存體帳戶 'somestorageaccount' 中的 ' somecontainer' 是可公開存取。</span><span class="sxs-lookup"><span data-stu-id="39923-240">In this example, you must ensure that hello container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="39923-241">否則，hello 指令碼擲回 「 找不到 ' 例外狀況而失敗。</span><span class="sxs-lookup"><span data-stu-id="39923-241">Otherwise, hello script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="39923-242">傳遞參數 toohello 新增 AzureRmHDInsightScriptAction cmdlet</span><span class="sxs-lookup"><span data-stu-id="39923-242">Pass parameters toohello Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="39923-243">toopass toohello 新增 AzureRmHDInsightScriptAction cmdlet 多個參數，您需要 tooformat hello 字串值 toocontain 所有參數 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-243">toopass multiple parameters toohello Add-AzureRmHDInsightScriptAction cmdlet, you need tooformat hello string value toocontain all parameters for hello script.</span></span> <span data-ttu-id="39923-244">例如：</span><span class="sxs-lookup"><span data-stu-id="39923-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="39923-245">或</span><span class="sxs-lookup"><span data-stu-id="39923-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="39923-246">對於失敗的叢集部署擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="39923-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="39923-247">如果您想要精確地收到 hello 事實 tooget 通知該叢集自訂失敗如預期般，是重要的 toothrow 例外狀況，並會 hello 叢集建立失敗。</span><span class="sxs-lookup"><span data-stu-id="39923-247">If you want tooget accurately notified of hello fact that cluster customization did not succeed as expected, it is important toothrow an exception and fail hello cluster creation.</span></span> <span data-ttu-id="39923-248">比方說，您可能會想 tooprocess 檔案，如果存在的話，並處理 hello hello 檔案不存在的錯誤情況。</span><span class="sxs-lookup"><span data-stu-id="39923-248">For instance, you might want tooprocess a file if it exists and handle hello error case where hello file does not exist.</span></span> <span data-ttu-id="39923-249">這樣會確保 hello 指令碼會依正常程序結束，且正確已知 hello hello 叢集狀態。</span><span class="sxs-lookup"><span data-stu-id="39923-249">This would ensure that hello script exits gracefully and hello state of hello cluster is correctly known.</span></span> <span data-ttu-id="39923-250">hello 下列程式碼片段會透過範例說明如何 tooachieve 這樣：</span><span class="sxs-lookup"><span data-stu-id="39923-250">hello following snippet gives an example of how tooachieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="39923-251">在此片段中，如果 hello 檔案不存在，它會導致 tooa 處於狀態下 hello 指令碼實際上正常地結束之後列印 hello 錯誤訊息： hello 叢集達到假設它是 「 成功 」 完成叢集的自訂程序的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="39923-251">In this snippet, if hello file did not exist, it would lead tooa state where hello script actually exits gracefully after printing hello error message, and hello cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="39923-252">如果您想要精確地收到 hello 事實 toobe 通知該叢集自訂基本上不成功如預期般，因為遺漏的檔案，為更適當 toothrow 例外狀況，並無法 hello 叢集自訂步驟。</span><span class="sxs-lookup"><span data-stu-id="39923-252">If you want toobe accurately notified of hello fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate toothrow an exception and fail hello cluster customization step.</span></span> <span data-ttu-id="39923-253">tooachieve 這樣您就必須使用 hello 改為下列範例程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="39923-253">tooachieve this you must use hello following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="39923-254">指令碼動作的部署檢查清單</span><span class="sxs-lookup"><span data-stu-id="39923-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="39923-255">準備 toodeploy 這些指令碼時，我們採用的 hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="39923-255">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

1. <span data-ttu-id="39923-256">將包含 hello 自訂指令碼可在部署期間 hello 叢集節點可存取的位置中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="39923-256">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="39923-257">這可以是任何 hello 預設或其他叢集部署中或任何其他可公開存取的儲存體容器的 hello 時間在指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="39923-257">This can be any of hello default or additional Storage accounts specified at hello time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="39923-258">加入至指令碼 toomake 確定它們執行不斷地，檢查，以便 hello 指令碼可以在 hello 執行多次相同的節點。</span><span class="sxs-lookup"><span data-stu-id="39923-258">Add checks into scripts toomake sure that they execute idempotently, so that hello script can be executed multiple times on hello same node.</span></span>
3. <span data-ttu-id="39923-259">使用 hello **Write-output** Azure PowerShell cmdlet tooprint tooSTDOUT 與 STDERR。</span><span class="sxs-lookup"><span data-stu-id="39923-259">Use hello **Write-Output** Azure PowerShell cmdlet tooprint tooSTDOUT as well as STDERR.</span></span> <span data-ttu-id="39923-260">請勿使用 **Write-Host**。</span><span class="sxs-lookup"><span data-stu-id="39923-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="39923-261">使用暫存檔案資料夾，例如 $env: TEMP tookeep hello hello 指令碼所使用的下載的檔案，然後再清除它們之後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-261">Use a temporary file folder, such as $env:TEMP, tookeep hello downloaded file used by hello scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="39923-262">安裝自訂軟體，位置只能是 D:\ 或 C:\apps。</span><span class="sxs-lookup"><span data-stu-id="39923-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="39923-263">因為它們是保留，不應該使用 hello c： 磁碟機上的其他位置。</span><span class="sxs-lookup"><span data-stu-id="39923-263">Other locations on hello C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="39923-264">請注意，安裝 hello C:\apps 資料夾外部的 hello c： 磁碟機上的檔案可能會導致安裝程式失敗 reimages hello 節點的期間。</span><span class="sxs-lookup"><span data-stu-id="39923-264">Note that installing files on hello C: drive outside of hello C:\apps folder may result in setup failures during reimages of hello node.</span></span>
6. <span data-ttu-id="39923-265">萬一 hello 作業系統層級的設定或 Hadoop 服務組態檔已變更，您可能想 toorestart HDInsight 服務，讓他們可以選擇任何作業系統層級的設定，例如 hello hello 指令碼中設定的環境變數。</span><span class="sxs-lookup"><span data-stu-id="39923-265">In hello event that OS-level settings or Hadoop service configuration files were changed, you may want toorestart HDInsight services so that they can pick up any OS-level settings, such as hello environment variables set in hello scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="39923-266">偵錯自訂指令碼</span><span class="sxs-lookup"><span data-stu-id="39923-266">Debug custom scripts</span></span>
<span data-ttu-id="39923-267">儲存 hello 指令碼錯誤記錄檔，以及其他輸出，您指定在其建立 hello 叢集的 hello 預設儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="39923-267">hello script error logs are stored, along with other output, in hello default Storage account that you specified for hello cluster at its creation.</span></span> <span data-ttu-id="39923-268">hello 記錄檔會儲存在資料表中具有 hello 名稱*u < \cluster-name-fragment >< \time-stamp > setuplog*。</span><span class="sxs-lookup"><span data-stu-id="39923-268">hello logs are stored in a table with hello name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="39923-269">這些是彙總從 hello 節點 （前端節點和背景工作角色節點） 上的 hello 指令碼執行於 hello 叢集中的所有記錄的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="39923-269">These are aggregated logs that have records from all of hello nodes (head node and worker nodes) on which hello script runs in hello cluster.</span></span>
<span data-ttu-id="39923-270">輕鬆 toocheck hello 記錄檔也 toouse HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="39923-270">An easy way toocheck hello logs is toouse HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="39923-271">安裝 hello 工具，請參閱[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="39923-271">For installing hello tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="39923-272">**使用 Visual Studio toocheck hello 記錄**</span><span class="sxs-lookup"><span data-stu-id="39923-272">**toocheck hello log using Visual Studio**</span></span>

1. <span data-ttu-id="39923-273">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="39923-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="39923-274">按一下 檢視，然後按一下伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="39923-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="39923-275">以滑鼠右鍵按一下"Azure"、 按一下 連線太**Microsoft Azure 訂用帳戶**，然後輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="39923-275">Right-click "Azure", click Connect too**Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="39923-276">展開**儲存體**，依序展開 hello Azure 儲存體帳戶做為 hello 預設的檔案系統**資料表**，然後按兩下 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="39923-276">Expand **Storage**, expand hello Azure storage account used as hello default file system, expand **Tables**, and then double-click hello table name.</span></span>

<span data-ttu-id="39923-277">您可以從也遠端存取 hello 叢集節點 toosee STDOUT 和 STDERR 的自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="39923-277">You can also remote into hello cluster nodes toosee both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="39923-278">hello 記錄每個節點上的已指定唯一的 toothat 節點，並登入**C:\HDInsightLogs\DeploymentAgent.log**。</span><span class="sxs-lookup"><span data-stu-id="39923-278">hello logs on each node are specific only toothat node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="39923-279">這些記錄檔記錄從 hello 自訂指令碼的所有輸出。</span><span class="sxs-lookup"><span data-stu-id="39923-279">These log files record all outputs from hello custom script.</span></span> <span data-ttu-id="39923-280">Spark 指令碼動作的範例記錄程式碼片段看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="39923-280">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="39923-281">此記錄檔，並明確 hello 名為 HEADNODE0 VM 已執行 hello Spark 指令碼動作和 hello 執行期間所擲回任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="39923-281">In this log, it is clear that hello Spark script action has been executed on hello VM named HEADNODE0 and that no exceptions were thrown during hello execution.</span></span>

<span data-ttu-id="39923-282">Hello 執行失敗，就會發生的事件，在描述它 hello 輸出也包含在此記錄檔。</span><span class="sxs-lookup"><span data-stu-id="39923-282">In hello event that an execution failure occurs, hello output describing it is also contained in this log file.</span></span> <span data-ttu-id="39923-283">提供這些記錄檔中的 hello 資訊應在偵錯指令碼可能發生的問題很有幫助。</span><span class="sxs-lookup"><span data-stu-id="39923-283">hello information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="39923-284">另請參閱</span><span class="sxs-lookup"><span data-stu-id="39923-284">See also</span></span>
* <span data-ttu-id="39923-285">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="39923-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="39923-286">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="39923-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="39923-287">[在 HDInsight 叢集上安裝和使用 R][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="39923-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="39923-288">[在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="39923-289">[在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="39923-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
