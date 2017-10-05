---
title: "在 Linux 架構的 HDInsight 上使用 Hadoop 的秘訣 - Azure | Microsoft Docs"
description: "取得在 Azure 雲端中執行的熟悉 Linux 環境上使用 Linux 架構的 HDInsight (Hadoop) 叢集的實作秘訣。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8c6ff4a6b8617cda9b12be060c7c7bed62cb3f44
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a><span data-ttu-id="0d42d-103">在 Linux 上使用 HDInsight 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="0d42d-103">Information about using HDInsight on Linux</span></span>

<span data-ttu-id="0d42d-104">Azure HDInsight 叢集可在您熟悉的 Linux 環境中提供於 Azure 雲端中執行的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="0d42d-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in the Azure cloud.</span></span> <span data-ttu-id="0d42d-105">其操作大多與 Linux 安裝上的任何其他 Hadoop 相同。</span><span class="sxs-lookup"><span data-stu-id="0d42d-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span></span> <span data-ttu-id="0d42d-106">本文件會指出其中應注意的特殊不同之處。</span><span class="sxs-lookup"><span data-stu-id="0d42d-106">This document calls out specific differences that you should be aware of.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d42d-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="0d42d-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0d42d-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d42d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d42d-109">Prerequisites</span></span>

<span data-ttu-id="0d42d-110">本文件中的許多步驟都使用下列公用程式，可能需要安裝在您的系統上。</span><span class="sxs-lookup"><span data-stu-id="0d42d-110">Many of the steps in this document use the following utilities, which may need to be installed on your system.</span></span>

* <span data-ttu-id="0d42d-111">[cURL](https://curl.haxx.se/) - 用來與 Web 型服務通訊</span><span class="sxs-lookup"><span data-stu-id="0d42d-111">[cURL](https://curl.haxx.se/) - used to communicate with web-based services</span></span>
* <span data-ttu-id="0d42d-112">[jq](https://stedolan.github.io/jq/) - 用來剖析 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="0d42d-112">[jq](https://stedolan.github.io/jq/) - used to parse JSON documents</span></span>
* <span data-ttu-id="0d42d-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (預覽) - 用來從遠端管理 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="0d42d-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used to remotely manage Azure services</span></span>

## <a name="users"></a><span data-ttu-id="0d42d-114">使用者</span><span class="sxs-lookup"><span data-stu-id="0d42d-114">Users</span></span>

<span data-ttu-id="0d42d-115">除非[已加入網域](hdinsight-domain-joined-introduction.md)，否則應將 HDInsight 視為**單一使用者**系統。</span><span class="sxs-lookup"><span data-stu-id="0d42d-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span></span> <span data-ttu-id="0d42d-116">叢集中會建立一個具有系統管理員層級權限的 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d42d-116">A single SSH user account is created with the cluster, with administrator level permissions.</span></span> <span data-ttu-id="0d42d-117">您可以建立其他 SSH 帳戶，但這些帳戶也會擁有叢集的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0d42d-117">Additional SSH accounts can be created, but they also have administrator access to the cluster.</span></span>

<span data-ttu-id="0d42d-118">已加入網域的 HDInsight 可支援多個使用者和更細微的權限和角色設定。</span><span class="sxs-lookup"><span data-stu-id="0d42d-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span></span> <span data-ttu-id="0d42d-119">如需詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="domain-names"></a><span data-ttu-id="0d42d-120">網域名稱</span><span class="sxs-lookup"><span data-stu-id="0d42d-120">Domain names</span></span>

<span data-ttu-id="0d42d-121">從網際網路連接到叢集時所要使用的完整網域名稱 (FQDN) 是 **&lt;clustername>.azurehdinsight.net** 或 (僅適用於 SSH) **&lt;clustername-ssh>.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="0d42d-121">The fully qualified domain name (FQDN) to use when connecting to the cluster from the internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span></span>

<span data-ttu-id="0d42d-122">就內部而言，叢集中的每個節點都具有在叢集組態期間指派的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d42d-122">Internally, each node in the cluster has a name that is assigned during cluster configuration.</span></span> <span data-ttu-id="0d42d-123">若要尋找叢集名稱，請參閱 Ambari Web UI 上的 [主機] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0d42d-123">To find the cluster names, see the **Hosts** page on the Ambari Web UI.</span></span> <span data-ttu-id="0d42d-124">您也可以使用下列命令從 Ambari REST API 傳回主機清單︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-124">You can also use the following to return a list of hosts from the Ambari REST API:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

<span data-ttu-id="0d42d-125">將 **PASSWORD** 取代為系統管理員帳戶的密碼，並且將 **CLUSTERNAME** 取代為叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0d42d-125">Replace **PASSWORD** with the password of the admin account, and **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="0d42d-126">此命令會傳回包含叢集中主機清單的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="0d42d-126">This command returns a JSON document that contains a list of the hosts in the cluster.</span></span> <span data-ttu-id="0d42d-127">Jq 用來擷取每部主機的 `host_name` 元素值。</span><span class="sxs-lookup"><span data-stu-id="0d42d-127">Jq is used to extract the `host_name` element value for each host.</span></span>

<span data-ttu-id="0d42d-128">如果您需要針對特定服務尋找節點的名稱，您可以查詢 Ambari 有無該元件。</span><span class="sxs-lookup"><span data-stu-id="0d42d-128">If you need to find the name of the node for a specific service, you can query Ambari for that component.</span></span> <span data-ttu-id="0d42d-129">例如，若要尋找主機有無 HDFS 名稱節點，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="0d42d-129">For example, to find the hosts for the HDFS name node, use the following command:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

<span data-ttu-id="0d42d-130">此命令會傳回描述服務的 JSON 文件，然後 jq 只會針對主機提取 `host_name` 值。</span><span class="sxs-lookup"><span data-stu-id="0d42d-130">This command returns a JSON document describing the service, and then jq pulls out only the `host_name` value for the hosts.</span></span>

## <a name="remote-access-to-services"></a><span data-ttu-id="0d42d-131">遠端存取服務</span><span class="sxs-lookup"><span data-stu-id="0d42d-131">Remote access to services</span></span>

* <span data-ttu-id="0d42d-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="0d42d-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span></span>

    <span data-ttu-id="0d42d-133">使用叢集系統管理員使用者和密碼進行驗證，然後登入 Ambari 。</span><span class="sxs-lookup"><span data-stu-id="0d42d-133">Authenticate by using the cluster administrator user and password, and then log in to Ambari.</span></span>

    <span data-ttu-id="0d42d-134">驗證是純文字的 - 請一律使用 HTTPS 來協助確保連線的安全性。</span><span class="sxs-lookup"><span data-stu-id="0d42d-134">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0d42d-135">透過 Ambari 使用的一些 Web UI 會使用內部網域名稱存取節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-135">Some of the web UIs available through Ambari access nodes using an internal domain name.</span></span> <span data-ttu-id="0d42d-136">內部網域名稱無法透過網際網路公開存取。</span><span class="sxs-lookup"><span data-stu-id="0d42d-136">Internal domain names are not publicly accessible over the internet.</span></span> <span data-ttu-id="0d42d-137">在嘗試透過網際網路存取某些功能時可能會收到「找不到伺服器」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d42d-137">You may receive "server not found" errors when trying to access some features over the Internet.</span></span>
    >
    > <span data-ttu-id="0d42d-138">若要使用 Ambari Web UI 的完整功能，請使用 SSH 通道將 Web 流量以 Proxy 處理傳輸到叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-138">To use the full functionality of the Ambari web UI, use an SSH tunnel to proxy web traffic to the cluster head node.</span></span> <span data-ttu-id="0d42d-139">請參閱[使用 SSH 通道來存取 Ambari Web UI、ResourceManager、JobHistory、NameNode、Oozie 及其他 Web UI](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="0d42d-139">See [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

* <span data-ttu-id="0d42d-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span><span class="sxs-lookup"><span data-stu-id="0d42d-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d42d-141">使用叢集系統管理員使用者和密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0d42d-141">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="0d42d-142">驗證是純文字的 - 請一律使用 HTTPS 來協助確保連線的安全性。</span><span class="sxs-lookup"><span data-stu-id="0d42d-142">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="0d42d-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span><span class="sxs-lookup"><span data-stu-id="0d42d-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d42d-144">使用叢集系統管理員使用者和密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0d42d-144">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="0d42d-145">驗證是純文字的 - 請一律使用 HTTPS 來協助確保連線的安全性。</span><span class="sxs-lookup"><span data-stu-id="0d42d-145">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="0d42d-146">**SSH** - 連接埠 22 或 23 上的 &lt;clustername>-ssh.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="0d42d-146">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span></span> <span data-ttu-id="0d42d-147">連接埠 22 用來連接至主要前端節點，而 23 用來連接至次要前端節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-147">Port 22 is used to connect to the primary headnode, while 23 is used to connect to the secondary.</span></span> <span data-ttu-id="0d42d-148">如需前端節點的詳細資訊，請參閱 [HDInsight 上 Hadoop 叢集的可用性和可靠性](hdinsight-high-availability-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-148">For more information on the head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d42d-149">您只能從用戶端電腦透過 SSH 存取叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-149">You can only access the cluster head nodes through SSH from a client machine.</span></span> <span data-ttu-id="0d42d-150">然後在連線後，再從前端節點使用 SSH 存取背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-150">Once connected, you can then access the worker nodes by using SSH from a headnode.</span></span>

## <a name="file-locations"></a><span data-ttu-id="0d42d-151">檔案位置</span><span class="sxs-lookup"><span data-stu-id="0d42d-151">File locations</span></span>

<span data-ttu-id="0d42d-152">Hadoop 相關檔案可以在叢集節點的 `/usr/hdp`上找到。</span><span class="sxs-lookup"><span data-stu-id="0d42d-152">Hadoop-related files can be found on the cluster nodes at `/usr/hdp`.</span></span> <span data-ttu-id="0d42d-153">此目錄包含下列子目錄：</span><span class="sxs-lookup"><span data-stu-id="0d42d-153">This directory contains the following subdirectories:</span></span>

* <span data-ttu-id="0d42d-154">**2.2.4.9-1**︰目錄名稱是 HDInsight 所使用的 Hortonworks Data Platform 版本。</span><span class="sxs-lookup"><span data-stu-id="0d42d-154">**2.2.4.9-1**: The directory name is the version of the Hortonworks Data Platform used by HDInsight.</span></span> <span data-ttu-id="0d42d-155">叢集上的數字可能不同於此處所列的數字。</span><span class="sxs-lookup"><span data-stu-id="0d42d-155">The number on your cluster may be different than the one listed here.</span></span>
* <span data-ttu-id="0d42d-156">**current**︰此目錄包含 **2.2.4.9-1** 目錄下的子目錄連結。</span><span class="sxs-lookup"><span data-stu-id="0d42d-156">**current**: This directory contains links to subdirectories under the **2.2.4.9-1** directory.</span></span> <span data-ttu-id="0d42d-157">因為有此目錄，您就不必記住版本號碼。</span><span class="sxs-lookup"><span data-stu-id="0d42d-157">This directory exists so that you don't have to remember the version number.</span></span>

<span data-ttu-id="0d42d-158">在 Hadoop 分散式檔案系統的 `/example` 和 `/HdiSamples` 可取得範例資料和 JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d42d-158">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span></span>

## <a name="hdfs-azure-storage-and-data-lake-store"></a><span data-ttu-id="0d42d-159">HDFS、Azure 儲存體和 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0d42d-159">HDFS, Azure Storage, and Data Lake Store</span></span>

<span data-ttu-id="0d42d-160">在大部分的 Hadoop 散發套件中，是以叢集機器上的本機儲存體支援 HDFS 的運作。</span><span class="sxs-lookup"><span data-stu-id="0d42d-160">In most Hadoop distributions, HDFS is backed by local storage on the machines in the cluster.</span></span> <span data-ttu-id="0d42d-161">針對雲端解決方案使用本機儲存體的成本可能相當高，因為計算資源是以每小時或每分鐘為單位來計費。</span><span class="sxs-lookup"><span data-stu-id="0d42d-161">Using local storage can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span></span>

<span data-ttu-id="0d42d-162">HDInsight 使用 Azure 儲存體或 Azure Data Lake Store 中的 Blob 做為預設存放區。</span><span class="sxs-lookup"><span data-stu-id="0d42d-162">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as the default store.</span></span> <span data-ttu-id="0d42d-163">這些服務提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0d42d-163">These services provide the following benefits:</span></span>

* <span data-ttu-id="0d42d-164">長期儲存成本低廉</span><span class="sxs-lookup"><span data-stu-id="0d42d-164">Cheap long-term storage</span></span>
* <span data-ttu-id="0d42d-165">可從各種外部服務進行存取，例如網站、檔案上傳/下載公用程式、各種語言的 SDK 和網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="0d42d-165">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span></span>

> [!WARNING]
> <span data-ttu-id="0d42d-166">HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d42d-166">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="0d42d-167">目前不支援 __Blob 儲存體__帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="0d42d-167">It does not currently support the __Blob storage__ account type.</span></span>

<span data-ttu-id="0d42d-168">Azure 儲存體帳戶可以保存多達 4.75 TB 的資料，但個別 Blob (或檔案，從 HDInsight 觀點來看) 只能保存到達 195 GB 的資料。</span><span class="sxs-lookup"><span data-stu-id="0d42d-168">An Azure Storage account can hold up to 4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up to 195 GB.</span></span> <span data-ttu-id="0d42d-169">Azure Data Lake Store 可以動態地成長來保存數兆的檔案，個別檔案可大於 PB。</span><span class="sxs-lookup"><span data-stu-id="0d42d-169">Azure Data Lake Store can grow dynamically to hold trillions of files, with individual files greater than a petabyte.</span></span> <span data-ttu-id="0d42d-170">如需詳細資訊，請參閱[了解 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 和[Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-170">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span>

<span data-ttu-id="0d42d-171">使用 Azure 儲存體或 Data Lake Store 時，您不需要從 HDInsight 進行任何特殊動作就能存取資料。</span><span class="sxs-lookup"><span data-stu-id="0d42d-171">When using either Azure Storage or Data Lake Store, you don't have to do anything special from HDInsight to access the data.</span></span> <span data-ttu-id="0d42d-172">例如，下列命令列出 `/example/data` 資料夾中的檔案，不論其儲存在 Azure 儲存體或 Data Lake Store 中：</span><span class="sxs-lookup"><span data-stu-id="0d42d-172">For example, the following command lists files in the `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span></span>

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a><span data-ttu-id="0d42d-173">URI 和配置</span><span class="sxs-lookup"><span data-stu-id="0d42d-173">URI and scheme</span></span>

<span data-ttu-id="0d42d-174">有些命令可能需要您在存取檔案時於 URI 中指定配置。</span><span class="sxs-lookup"><span data-stu-id="0d42d-174">Some commands may require you to specify the scheme as part of the URI when accessing a file.</span></span> <span data-ttu-id="0d42d-175">例如，Storm-HDFS 元件就需要您指定配置。</span><span class="sxs-lookup"><span data-stu-id="0d42d-175">For example, the Storm-HDFS component requires you to specify the scheme.</span></span> <span data-ttu-id="0d42d-176">在使用非預設儲存體 (新增為叢集「其他」儲存體的儲存體) 時，您一律必須在 URI 中使用配置。</span><span class="sxs-lookup"><span data-stu-id="0d42d-176">When using non-default storage (storage added as "additional" storage to the cluster), you must always use the scheme as part of the URI.</span></span>

<span data-ttu-id="0d42d-177">使用 __Azure 儲存體__時，可使用下列其中一種 UI 配置︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-177">When using __Azure Storage__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="0d42d-178">`wasb:///`︰使用未加密通訊存取預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="0d42d-178">`wasb:///`: Access default storage using unencrypted communication.</span></span>

* <span data-ttu-id="0d42d-179">`wasbs:///`︰使用加密通訊存取預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="0d42d-179">`wasbs:///`: Access default storage using encrypted communication.</span></span>  <span data-ttu-id="0d42d-180">HDInsight 3.6 版和更新版本才會支援 wasbs 配置。</span><span class="sxs-lookup"><span data-stu-id="0d42d-180">The wasbs scheme is supported only from HDInsight version 3.6 onwards.</span></span>

* <span data-ttu-id="0d42d-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`︰以非預設儲存體帳戶進行通訊時使用。</span><span class="sxs-lookup"><span data-stu-id="0d42d-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span></span> <span data-ttu-id="0d42d-182">例如，當您有其他儲存體帳戶，或在可公開存取的儲存體帳戶中存取儲存的資料時。</span><span class="sxs-lookup"><span data-stu-id="0d42d-182">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span></span>

<span data-ttu-id="0d42d-183">使用 __Data Lake Store__ 時，可使用下列其中一種 UI 配置︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-183">When using __Data Lake Store__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="0d42d-184">`adl:///`︰存取叢集的預設 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="0d42d-184">`adl:///`: Access the default Data Lake Store for the cluster.</span></span>

* <span data-ttu-id="0d42d-185">`adl://<storage-name>.azuredatalakestore.net/`：用來與非預設 Data Lake Store 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0d42d-185">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store.</span></span> <span data-ttu-id="0d42d-186">也用來存取 HDInsight 叢集根目錄之外的資料。</span><span class="sxs-lookup"><span data-stu-id="0d42d-186">Also used to access data outside the root directory of your HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d42d-187">使用 Data Lake Store 做為 HDInsight 的預設存放區時，您必須在存放區內指定要做為 HDInsight 儲存體根目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="0d42d-187">When using Data Lake Store as the default store for HDInsight, you must specify a path within the store to use as the root of HDInsight storage.</span></span> <span data-ttu-id="0d42d-188">預設路徑為 `/clusters/<cluster-name>/`。</span><span class="sxs-lookup"><span data-stu-id="0d42d-188">The default path is `/clusters/<cluster-name>/`.</span></span>
>
> <span data-ttu-id="0d42d-189">使用 `/` 或 `adl:///` 存取資料時，您只可以存取儲存在叢集根目錄 (例如，`/clusters/<cluster-name>/`) 中的資料。</span><span class="sxs-lookup"><span data-stu-id="0d42d-189">When using `/` or `adl:///` to access data, you can only access data stored in the root (for example, `/clusters/<cluster-name>/`) of the cluster.</span></span> <span data-ttu-id="0d42d-190">若要存取存放區中任何位置的資料，請使用 `adl://<storage-name>.azuredatalakestore.net/` 格式。</span><span class="sxs-lookup"><span data-stu-id="0d42d-190">To access data anywhere in the store, use the `adl://<storage-name>.azuredatalakestore.net/` format.</span></span>

### <a name="what-storage-is-the-cluster-using"></a><span data-ttu-id="0d42d-191">叢集使用什麼儲存體</span><span class="sxs-lookup"><span data-stu-id="0d42d-191">What storage is the cluster using</span></span>

<span data-ttu-id="0d42d-192">您可以使用 Ambari 來擷取叢集的預設儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="0d42d-192">You can use Ambari to retrieve the default storage configuration for the cluster.</span></span> <span data-ttu-id="0d42d-193">請使用下列命令和 CURL 來擷取 HDFS 組態資訊，並使用 [jq](https://stedolan.github.io/jq/)加以篩選：</span><span class="sxs-lookup"><span data-stu-id="0d42d-193">Use the following command to retrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span></span>

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> <span data-ttu-id="0d42d-194">這個方法會傳回套用至伺服器的第一個組態 (`service_config_version=1`)，其包含這項資訊。</span><span class="sxs-lookup"><span data-stu-id="0d42d-194">This returns the first configuration applied to the server (`service_config_version=1`), which contains this information.</span></span> <span data-ttu-id="0d42d-195">您可能需要列出所有組態版本來找出最新的版本。</span><span class="sxs-lookup"><span data-stu-id="0d42d-195">You may need to list all configuration versions to find the latest one.</span></span>

<span data-ttu-id="0d42d-196">此命令會傳回類似下列 URI 的值：</span><span class="sxs-lookup"><span data-stu-id="0d42d-196">This command returns a value similar to the following URIs:</span></span>

* <span data-ttu-id="0d42d-197">`wasb://<container-name>@<account-name>.blob.core.windows.net`，若使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d42d-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span></span>

    <span data-ttu-id="0d42d-198">帳戶名稱是 Azure 儲存體帳戶的名稱，容器名稱則是叢集儲存體根目錄的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="0d42d-198">The account name is the name of the Azure Storage account, while the container name is the blob container that is the root of the cluster storage.</span></span>

* <span data-ttu-id="0d42d-199">`adl://home`，若使用 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="0d42d-199">`adl://home` if using Azure Data Lake Store.</span></span> <span data-ttu-id="0d42d-200">若要取得 Data Lake Store 名稱，請使用下列 REST 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-200">To get the Data Lake Store name, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    <span data-ttu-id="0d42d-201">此命令會傳回下列主機名稱：`<data-lake-store-account-name>.azuredatalakestore.net`。</span><span class="sxs-lookup"><span data-stu-id="0d42d-201">This command returns the following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span></span>

    <span data-ttu-id="0d42d-202">若要取得 HDInsight 根目錄存放區內的目錄，請使用下列 REST 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-202">To get the directory within the store that is the root for HDInsight, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    <span data-ttu-id="0d42d-203">此命令會傳回類似下列路徑的路徑：`/clusters/<hdinsight-cluster-name>/`。</span><span class="sxs-lookup"><span data-stu-id="0d42d-203">This command returns a path similar to the following path: `/clusters/<hdinsight-cluster-name>/`.</span></span>

<span data-ttu-id="0d42d-204">您也可以使用 Azure 入口網站，以下列步驟尋找儲存體資訊︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-204">You can also find the storage information using the Azure portal by using the following steps:</span></span>

1. <span data-ttu-id="0d42d-205">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0d42d-205">In the [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="0d42d-206">從 [屬性] 區段中，選取 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="0d42d-206">From the **Properties** section, select **Storage Accounts**.</span></span> <span data-ttu-id="0d42d-207">隨即會顯示叢集的儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="0d42d-207">The storage information for the cluster is displayed.</span></span>

### <a name="how-do-i-access-files-from-outside-hdinsight"></a><span data-ttu-id="0d42d-208">如何從 HDInsight 外部存取檔案</span><span class="sxs-lookup"><span data-stu-id="0d42d-208">How do I access files from outside HDInsight</span></span>

<span data-ttu-id="0d42d-209">有各種不同的方式可從 HDInsight 叢集之外存取資料。</span><span class="sxs-lookup"><span data-stu-id="0d42d-209">There are a various ways to access data from outside the HDInsight cluster.</span></span> <span data-ttu-id="0d42d-210">以下是幾個可用來處理資料之公用程式和 SDK 的連結︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-210">The following are a few links to utilities and SDKs that can be used to work with your data:</span></span>

<span data-ttu-id="0d42d-211">如果使用 __Azure 儲存體__，請參閱下列連結，以取得可供存取資料的方式︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-211">If using __Azure Storage__, see the following links for ways that you can access your data:</span></span>

* <span data-ttu-id="0d42d-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)：適用於 Azure 的命令列介面命令。</span><span class="sxs-lookup"><span data-stu-id="0d42d-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span></span> <span data-ttu-id="0d42d-213">安裝好後，請使用 `az storage` 命令以協助使用儲存體，或是針對 Blob 特有命令使用 `az storage blob`。</span><span class="sxs-lookup"><span data-stu-id="0d42d-213">After installing, use the `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span></span>
* <span data-ttu-id="0d42d-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage)：python 指令碼，用於 Azure 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="0d42d-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span></span>
* <span data-ttu-id="0d42d-215">各種 SDK：</span><span class="sxs-lookup"><span data-stu-id="0d42d-215">Various SDKs:</span></span>

    * [<span data-ttu-id="0d42d-216">Java</span><span class="sxs-lookup"><span data-stu-id="0d42d-216">Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
    * [<span data-ttu-id="0d42d-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="0d42d-217">Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
    * [<span data-ttu-id="0d42d-218">PHP</span><span class="sxs-lookup"><span data-stu-id="0d42d-218">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
    * [<span data-ttu-id="0d42d-219">Python</span><span class="sxs-lookup"><span data-stu-id="0d42d-219">Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
    * [<span data-ttu-id="0d42d-220">Ruby</span><span class="sxs-lookup"><span data-stu-id="0d42d-220">Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)
    * [<span data-ttu-id="0d42d-221">.NET</span><span class="sxs-lookup"><span data-stu-id="0d42d-221">.NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
    * [<span data-ttu-id="0d42d-222">儲存體 REST API</span><span class="sxs-lookup"><span data-stu-id="0d42d-222">Storage REST API</span></span>](https://msdn.microsoft.com/library/azure/dd135733.aspx)

<span data-ttu-id="0d42d-223">如果使用 __Azure Data Lake Store__，請參閱下列連結，以取得可供存取資料的方式︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-223">If using __Azure Data Lake Store__, see the following links for ways that you can access your data:</span></span>

* [<span data-ttu-id="0d42d-224">Web 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="0d42d-224">Web browser</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* [<span data-ttu-id="0d42d-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d42d-225">PowerShell</span></span>](../data-lake-store/data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="0d42d-226">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d42d-226">Azure CLI 2.0</span></span>](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [<span data-ttu-id="0d42d-227">WebHDFS REST API</span><span class="sxs-lookup"><span data-stu-id="0d42d-227">WebHDFS REST API</span></span>](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="0d42d-228">Visual Studio 適用的 Data Lake 工具</span><span class="sxs-lookup"><span data-stu-id="0d42d-228">Data Lake Tools for Visual Studio</span></span>](https://www.microsoft.com/download/details.aspx?id=49504)
* [<span data-ttu-id="0d42d-229">.NET</span><span class="sxs-lookup"><span data-stu-id="0d42d-229">.NET</span></span>](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="0d42d-230">Java</span><span class="sxs-lookup"><span data-stu-id="0d42d-230">Java</span></span>](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="0d42d-231">Python</span><span class="sxs-lookup"><span data-stu-id="0d42d-231">Python</span></span>](../data-lake-store/data-lake-store-get-started-python.md)

## <span data-ttu-id="0d42d-232"><a name="scaling"></a>調整您的叢集規模</span><span class="sxs-lookup"><span data-stu-id="0d42d-232"><a name="scaling"></a>Scaling your cluster</span></span>

<span data-ttu-id="0d42d-233">叢集調整功能可讓您動態變更叢集所用的資料節點數目。</span><span class="sxs-lookup"><span data-stu-id="0d42d-233">The cluster scaling feature allows you to dynamically change the number of data nodes used by a cluster.</span></span> <span data-ttu-id="0d42d-234">正在叢集上執行其他工作或處理序時，您可以執行調整作業。</span><span class="sxs-lookup"><span data-stu-id="0d42d-234">You can perform scaling operations while other jobs or processes are running on a cluster.</span></span>

<span data-ttu-id="0d42d-235">不同的叢集類型會受調整影響，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0d42d-235">The different cluster types are affected by scaling as follows:</span></span>

* <span data-ttu-id="0d42d-236">**Hadoop**︰相應減少叢集中的節點數目時，會重新啟動叢集中的部分服務。</span><span class="sxs-lookup"><span data-stu-id="0d42d-236">**Hadoop**: When scaling down the number of nodes in a cluster, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="0d42d-237">調整作業可能會導致執行中或擱置的工作在調整作業完成時失敗。</span><span class="sxs-lookup"><span data-stu-id="0d42d-237">Scaling operations can cause jobs running or pending to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="0d42d-238">您可以在作業完成後重新提交這些工作。</span><span class="sxs-lookup"><span data-stu-id="0d42d-238">You can resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="0d42d-239">**HBase**︰區域伺服器會在完成調整作業的數分鐘之內自動取得平衡。</span><span class="sxs-lookup"><span data-stu-id="0d42d-239">**HBase**: Regional servers are automatically balanced within a few minutes after completion of the scaling operation.</span></span> <span data-ttu-id="0d42d-240">若要手動平衡區域伺服器，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d42d-240">To manually balance regional servers, use the following steps:</span></span>

    1. <span data-ttu-id="0d42d-241">使用 SSH 連線到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0d42d-241">Connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="0d42d-242">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-242">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    2. <span data-ttu-id="0d42d-243">使用下列命令來啟動 HBase Shell：</span><span class="sxs-lookup"><span data-stu-id="0d42d-243">Use the following to start the HBase shell:</span></span>

            hbase shell

    3. <span data-ttu-id="0d42d-244">載入 HBase Shell 後，使用下列命令來手動平衡區域伺服器︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-244">Once the HBase shell has loaded, use the following to manually balance the regional servers:</span></span>

            balancer

* <span data-ttu-id="0d42d-245">**Storm**︰執行調整作業之後，您應該重新平衡任何執行中的 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="0d42d-245">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span></span> <span data-ttu-id="0d42d-246">重新平衡可讓拓撲根據叢集中的新節點數目，重新調整平行處理原則設定。</span><span class="sxs-lookup"><span data-stu-id="0d42d-246">Rebalancing allows the topology to readjust parallelism settings based on the new number of nodes in the cluster.</span></span> <span data-ttu-id="0d42d-247">若要重新平衡執行中的拓撲，請使用下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="0d42d-247">To rebalance running topologies, use one of the following options:</span></span>

    * <span data-ttu-id="0d42d-248">**SSH**︰連接到伺服器並使用下列命令來重新平衡拓撲：</span><span class="sxs-lookup"><span data-stu-id="0d42d-248">**SSH**: Connect to the server and use the following command to rebalance a topology:</span></span>

            storm rebalance TOPOLOGYNAME

        <span data-ttu-id="0d42d-249">您也可以指定參數來覆寫拓撲原先提供的平行處理原則提示。</span><span class="sxs-lookup"><span data-stu-id="0d42d-249">You can also specify parameters to override the parallelism hints originally provided by the topology.</span></span> <span data-ttu-id="0d42d-250">例如，`storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` 會將拓撲重新設定為 5 個背景工作角色處理序、適用於 blue-spout 元件的 3 個執行程式，以及適用於 yellow-bolt 元件的 10 個執行程式。</span><span class="sxs-lookup"><span data-stu-id="0d42d-250">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures the topology to 5 worker processes, 3 executors for the blue-spout component, and 10 executors for the yellow-bolt component.</span></span>

    * <span data-ttu-id="0d42d-251">**Storm UI**︰使用下列步驟來重新平衡使用 Storm UI 的拓撲。</span><span class="sxs-lookup"><span data-stu-id="0d42d-251">**Storm UI**: Use the following steps to rebalance a topology using the Storm UI.</span></span>

        1. <span data-ttu-id="0d42d-252">在網頁瀏覽器中開啟 **https://CLUSTERNAME.azurehdinsight.net/stormui**，其中 CLUSTERNAME 是 Storm 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d42d-252">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is the name of your Storm cluster.</span></span> <span data-ttu-id="0d42d-253">出現提示時，輸入建立叢集時所指定的 HDInsight 叢集系統管理員 (管理員) 名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0d42d-253">If prompted, enter the HDInsight cluster administrator (admin) name and password you specified when creating the cluster.</span></span>
        2. <span data-ttu-id="0d42d-254">選取您要重新平衡的拓撲，然後選取 [重新平衡] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d42d-254">Select the topology you wish to rebalance, then select the **Rebalance** button.</span></span> <span data-ttu-id="0d42d-255">在執行重新平衡作業之前輸入延遲。</span><span class="sxs-lookup"><span data-stu-id="0d42d-255">Enter the delay before the rebalance operation is performed.</span></span>

<span data-ttu-id="0d42d-256">如需有關調整 HDInsight 叢集的特定資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0d42d-256">For specific information on scaling your HDInsight cluster, see:</span></span>

* [<span data-ttu-id="0d42d-257">使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="0d42d-257">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="0d42d-258">使用 Azure PowerShell 管理 HDInsight 上的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="0d42d-258">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a><span data-ttu-id="0d42d-259">如何安裝 Hue (或其他 Hadoop 元件)？</span><span class="sxs-lookup"><span data-stu-id="0d42d-259">How do I install Hue (or other Hadoop component)?</span></span>

<span data-ttu-id="0d42d-260">HDInsight 是受管理的服務。</span><span class="sxs-lookup"><span data-stu-id="0d42d-260">HDInsight is a managed service.</span></span> <span data-ttu-id="0d42d-261">如果 Azure 偵測到叢集問題，它可能會刪除失敗節點並建立要取代它的節點。</span><span class="sxs-lookup"><span data-stu-id="0d42d-261">If Azure detects a problem with the cluster, it may delete the failing node and create a node to replace it.</span></span> <span data-ttu-id="0d42d-262">如果您以手動方式在叢集上安裝項目，此作業發生時，不會保存這些項目。</span><span class="sxs-lookup"><span data-stu-id="0d42d-262">If you manually install things on the cluster, they are not persisted when this operation occurs.</span></span> <span data-ttu-id="0d42d-263">請改用 [HDInsight 指令碼動作](hdinsight-hadoop-customize-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-263">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="0d42d-264">指令碼動作可用來進行下列變更︰</span><span class="sxs-lookup"><span data-stu-id="0d42d-264">A script action can be used to make the following changes:</span></span>

* <span data-ttu-id="0d42d-265">安裝及設定服務或網站，例如 Spark 或 Hue。</span><span class="sxs-lookup"><span data-stu-id="0d42d-265">Install and configure a service or web site such as Spark or Hue.</span></span>
* <span data-ttu-id="0d42d-266">安裝及設定需要在叢集中的多個節點上進行組態變更的元件。</span><span class="sxs-lookup"><span data-stu-id="0d42d-266">Install and configure a component that requires configuration changes on multiple nodes in the cluster.</span></span> <span data-ttu-id="0d42d-267">例如，必要的環境變數、建立記錄目錄或建立組態檔。</span><span class="sxs-lookup"><span data-stu-id="0d42d-267">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span></span>

<span data-ttu-id="0d42d-268">指令碼動作是 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d42d-268">Script Actions are Bash scripts.</span></span> <span data-ttu-id="0d42d-269">指令碼會在叢集佈建期間執行，而且可用來在叢集上安裝並設定其他元件。</span><span class="sxs-lookup"><span data-stu-id="0d42d-269">The scripts run during cluster provisioning, and can be used to install and configure additional components on the cluster.</span></span> <span data-ttu-id="0d42d-270">範例指令碼可供安裝下列元件：</span><span class="sxs-lookup"><span data-stu-id="0d42d-270">Example scripts are provided for installing the following components:</span></span>

* [<span data-ttu-id="0d42d-271">Hue</span><span class="sxs-lookup"><span data-stu-id="0d42d-271">Hue</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="0d42d-272">Giraph</span><span class="sxs-lookup"><span data-stu-id="0d42d-272">Giraph</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="0d42d-273">Solr</span><span class="sxs-lookup"><span data-stu-id="0d42d-273">Solr</span></span>](hdinsight-hadoop-solr-install-linux.md)

<span data-ttu-id="0d42d-274">如需開發您自己的指令碼動作相關資訊，請參閱 [使用 HDInsight 開發指令碼動作](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-274">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

### <a name="jar-files"></a><span data-ttu-id="0d42d-275">JAR 檔案</span><span class="sxs-lookup"><span data-stu-id="0d42d-275">Jar files</span></span>

<span data-ttu-id="0d42d-276">獨立的 jar 檔案中提供了一些 Hadoop 技術，其中包含可用來做為 MapReduce 工作一部分的函式，或者來自 Pig 或 Hive 內部的函式。</span><span class="sxs-lookup"><span data-stu-id="0d42d-276">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span></span> <span data-ttu-id="0d42d-277">使用指令碼動作安裝這些項目時，它們通常不需要任何設定，並且可以在佈建之後上傳到叢集並直接使用。</span><span class="sxs-lookup"><span data-stu-id="0d42d-277">While these can be installed using Script Actions, they often don't require any setup and can be uploaded to the cluster after provisioning and used directly.</span></span> <span data-ttu-id="0d42d-278">如果您想要確定元件會在重新安裝叢集的映像後保存下來，則可將 jar 檔案儲存於叢集的預設儲存體 (WASB 或 ADL) 中。</span><span class="sxs-lookup"><span data-stu-id="0d42d-278">If you want to make sure the component survives reimaging of the cluster, you can store the jar file in the default storage for your cluster (WASB or ADL).</span></span>

<span data-ttu-id="0d42d-279">例如，如果您想要使用最新版本的 [DataFu](http://datafu.incubator.apache.org/)，則可下載包含專案的 jar，並將它上傳至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0d42d-279">For example, if you want to use the latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing the project and upload it to the HDInsight cluster.</span></span> <span data-ttu-id="0d42d-280">接著遵循 DataFu 文件中，如何從 Pig 或 Hive 中使用它的指示進行。</span><span class="sxs-lookup"><span data-stu-id="0d42d-280">Then follow the DataFu documentation on how to use it from Pig or Hive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d42d-281">有一些屬於獨立 jar 檔案的元件是透過 HDInsight 來提供，但它們不在路徑中。</span><span class="sxs-lookup"><span data-stu-id="0d42d-281">Some components that are standalone jar files are provided with HDInsight, but are not in the path.</span></span> <span data-ttu-id="0d42d-282">如果您正在尋找特定元件，可在叢集上使用下列內容來搜尋：</span><span class="sxs-lookup"><span data-stu-id="0d42d-282">If you are looking for a specific component, you can use the follow to search for it on your cluster:</span></span>
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> <span data-ttu-id="0d42d-283">此命令會傳回任何相符 jar 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="0d42d-283">This command returns the path of any matching jar files.</span></span>

<span data-ttu-id="0d42d-284">若要使用不同版本的元件，請上傳您需要的版本並在工作中使用。</span><span class="sxs-lookup"><span data-stu-id="0d42d-284">To use a different version of a component, upload the version you need and use it in your jobs.</span></span>

> [!WARNING]
> <span data-ttu-id="0d42d-285">透過 HDInsight 叢集提供的元件會受到完整支援，且 Microsoft 支援服務會協助釐清與解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="0d42d-285">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="0d42d-286">自訂元件則獲得商務上合理的支援，協助您進一步疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="0d42d-286">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="0d42d-287">如此可能會進而解決問題，或要求您利用可用管道，以找出開放原始碼技術，從中了解該技術的深度專業知識。</span><span class="sxs-lookup"><span data-stu-id="0d42d-287">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="0d42d-288">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-288">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="0d42d-289">另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="0d42d-289">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d42d-290">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d42d-290">Next steps</span></span>

* [<span data-ttu-id="0d42d-291">從以 Windows 為基礎的 HDInsight 移轉至以 Linux 為基礎的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d42d-291">Migrate from Windows-based HDInsight to Linux-based</span></span>](hdinsight-migrate-from-windows-to-linux.md)
* [<span data-ttu-id="0d42d-292">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="0d42d-292">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0d42d-293">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="0d42d-293">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0d42d-294">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="0d42d-294">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
