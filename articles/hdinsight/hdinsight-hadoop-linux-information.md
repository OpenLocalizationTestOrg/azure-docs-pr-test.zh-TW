---
title: "使用 linux 的 HDInsight 的 Azure 上的 Hadoop aaaTips |Microsoft 文件"
description: "取得實作的提示熟悉 hello Azure 雲端中執行的 Linux 環境上使用 linux 的 HDInsight (Hadoop) 叢集。"
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
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a><span data-ttu-id="e6240-103">在 Linux 上使用 HDInsight 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="e6240-103">Information about using HDInsight on Linux</span></span>

<span data-ttu-id="e6240-104">Azure HDInsight 叢集提供熟悉的 Linux 環境，在 hello Azure 雲端中執行的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="e6240-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in hello Azure cloud.</span></span> <span data-ttu-id="e6240-105">其操作大多與 Linux 安裝上的任何其他 Hadoop 相同。</span><span class="sxs-lookup"><span data-stu-id="e6240-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span></span> <span data-ttu-id="e6240-106">本文件會指出其中應注意的特殊不同之處。</span><span class="sxs-lookup"><span data-stu-id="e6240-106">This document calls out specific differences that you should be aware of.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6240-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e6240-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e6240-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e6240-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6240-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6240-109">Prerequisites</span></span>

<span data-ttu-id="e6240-110">許多 hello 本文件中的步驟會使用下列公用程式，可能需要安裝在您的系統上的 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="e6240-110">Many of hello steps in this document use hello following utilities, which may need toobe installed on your system.</span></span>

* <span data-ttu-id="e6240-111">[cURL](https://curl.haxx.se/) -toocommunicate 搭配 web 服務</span><span class="sxs-lookup"><span data-stu-id="e6240-111">[cURL](https://curl.haxx.se/) - used toocommunicate with web-based services</span></span>
* <span data-ttu-id="e6240-112">[jq](https://stedolan.github.io/jq/) -使用 tooparse JSON 文件</span><span class="sxs-lookup"><span data-stu-id="e6240-112">[jq](https://stedolan.github.io/jq/) - used tooparse JSON documents</span></span>
* <span data-ttu-id="e6240-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview)-使用的 tooremotely 管理 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="e6240-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used tooremotely manage Azure services</span></span>

## <a name="users"></a><span data-ttu-id="e6240-114">使用者</span><span class="sxs-lookup"><span data-stu-id="e6240-114">Users</span></span>

<span data-ttu-id="e6240-115">除非[已加入網域](hdinsight-domain-joined-introduction.md)，否則應將 HDInsight 視為**單一使用者**系統。</span><span class="sxs-lookup"><span data-stu-id="e6240-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span></span> <span data-ttu-id="e6240-116">單一的 SSH 使用者帳戶會建立與 hello 叢集，以系統管理員層級權限。</span><span class="sxs-lookup"><span data-stu-id="e6240-116">A single SSH user account is created with hello cluster, with administrator level permissions.</span></span> <span data-ttu-id="e6240-117">您可以建立額外的 SSH 帳戶，但還具有系統管理員存取 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-117">Additional SSH accounts can be created, but they also have administrator access toohello cluster.</span></span>

<span data-ttu-id="e6240-118">已加入網域的 HDInsight 可支援多個使用者和更細微的權限和角色設定。</span><span class="sxs-lookup"><span data-stu-id="e6240-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span></span> <span data-ttu-id="e6240-119">如需詳細資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="e6240-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="domain-names"></a><span data-ttu-id="e6240-120">網域名稱</span><span class="sxs-lookup"><span data-stu-id="e6240-120">Domain names</span></span>

<span data-ttu-id="e6240-121">hello 完整網域名稱 (FQDN) toouse hello 網際網路是從連接 toohello 叢集時 **&lt;clustername >。.azurehdinsight.net**或 （適用於僅 SSH)  **&lt;clustername-ssh>。.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="e6240-121">hello fully qualified domain name (FQDN) toouse when connecting toohello cluster from hello internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span></span>

<span data-ttu-id="e6240-122">就內部而言，hello 叢集中的每個節點都在叢集組態期間指派的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6240-122">Internally, each node in hello cluster has a name that is assigned during cluster configuration.</span></span> <span data-ttu-id="e6240-123">toofind hello 叢集名稱，請參閱 hello**主機**hello Ambari Web UI 上的頁面。</span><span class="sxs-lookup"><span data-stu-id="e6240-123">toofind hello cluster names, see hello **Hosts** page on hello Ambari Web UI.</span></span> <span data-ttu-id="e6240-124">您也可以使用下列 tooreturn 從 hello Ambari REST API 主機清單的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-124">You can also use hello following tooreturn a list of hosts from hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

<span data-ttu-id="e6240-125">取代**密碼**與 hello hello 系統管理員，帳戶的密碼和**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6240-125">Replace **PASSWORD** with hello password of hello admin account, and **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="e6240-126">此命令會傳回 JSON 文件包含一份 hello hello 叢集中的主機。</span><span class="sxs-lookup"><span data-stu-id="e6240-126">This command returns a JSON document that contains a list of hello hosts in hello cluster.</span></span> <span data-ttu-id="e6240-127">Jq 為使用的 tooextract hello`host_name`每個主控件的項目值。</span><span class="sxs-lookup"><span data-stu-id="e6240-127">Jq is used tooextract hello `host_name` element value for each host.</span></span>

<span data-ttu-id="e6240-128">如果您需要 toofind hello hello 節點名稱為特定服務時，您可以查詢 Ambari 該元件。</span><span class="sxs-lookup"><span data-stu-id="e6240-128">If you need toofind hello name of hello node for a specific service, you can query Ambari for that component.</span></span> <span data-ttu-id="e6240-129">比方說，toofind hello 主控件 hello HDFS 名稱節點，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-129">For example, toofind hello hosts for hello HDFS name node, use hello following command:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

<span data-ttu-id="e6240-130">此命令會傳回描述 hello 服務的 JSON 文件和 jq 然後提取出只 hello `host_name` hello 主機的值。</span><span class="sxs-lookup"><span data-stu-id="e6240-130">This command returns a JSON document describing hello service, and then jq pulls out only hello `host_name` value for hello hosts.</span></span>

## <a name="remote-access-tooservices"></a><span data-ttu-id="e6240-131">遠端存取 tooservices</span><span class="sxs-lookup"><span data-stu-id="e6240-131">Remote access tooservices</span></span>

* <span data-ttu-id="e6240-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="e6240-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span></span>

    <span data-ttu-id="e6240-133">驗證使用 hello 叢集系統管理員使用者和密碼，並再登入 tooAmbari。</span><span class="sxs-lookup"><span data-stu-id="e6240-133">Authenticate by using hello cluster administrator user and password, and then log in tooAmbari.</span></span>

    <span data-ttu-id="e6240-134">驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。</span><span class="sxs-lookup"><span data-stu-id="e6240-134">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e6240-135">一些 hello web Ui 可透過 Ambari 存取使用的內部網域名稱的節點。</span><span class="sxs-lookup"><span data-stu-id="e6240-135">Some of hello web UIs available through Ambari access nodes using an internal domain name.</span></span> <span data-ttu-id="e6240-136">內部網域名稱不是透過可公開存取 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="e6240-136">Internal domain names are not publicly accessible over hello internet.</span></span> <span data-ttu-id="e6240-137">嘗試 tooaccess hello 網際網路上的某些功能時，您可能會收到 「 找不到伺服器 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6240-137">You may receive "server not found" errors when trying tooaccess some features over hello Internet.</span></span>
    >
    > <span data-ttu-id="e6240-138">toouse hello 完整功能 hello Ambari web UI，使用 SSH 通道 tooproxy web 流量 toohello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="e6240-138">toouse hello full functionality of hello Ambari web UI, use an SSH tunnel tooproxy web traffic toohello cluster head node.</span></span> <span data-ttu-id="e6240-139">請參閱[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="e6240-139">See [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

* <span data-ttu-id="e6240-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span><span class="sxs-lookup"><span data-stu-id="e6240-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6240-141">使用 hello 叢集系統管理員使用者名稱和密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e6240-141">Authenticate by using hello cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="e6240-142">驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。</span><span class="sxs-lookup"><span data-stu-id="e6240-142">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

* <span data-ttu-id="e6240-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span><span class="sxs-lookup"><span data-stu-id="e6240-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6240-144">使用 hello 叢集系統管理員使用者名稱和密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e6240-144">Authenticate by using hello cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="e6240-145">驗證是純文字-一律使用 HTTPS toohelp 確保 hello 連線的安全。</span><span class="sxs-lookup"><span data-stu-id="e6240-145">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

* <span data-ttu-id="e6240-146">**SSH** - 連接埠 22 或 23 上的 &lt;clustername>-ssh.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="e6240-146">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span></span> <span data-ttu-id="e6240-147">連接埠 22。 使用的 tooconnect toohello 主要叢集前端節點，23 時使用的 tooconnect toohello 次要</span><span class="sxs-lookup"><span data-stu-id="e6240-147">Port 22 is used tooconnect toohello primary headnode, while 23 is used tooconnect toohello secondary.</span></span> <span data-ttu-id="e6240-148">如需有關 hello 前端節點的詳細資訊，請參閱[HDInsight 中的可用性和可靠性的 Hadoop 叢集](hdinsight-high-availability-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e6240-148">For more information on hello head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e6240-149">您只能從用戶端電腦透過 SSH 存取 hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="e6240-149">You can only access hello cluster head nodes through SSH from a client machine.</span></span> <span data-ttu-id="e6240-150">一旦連接之後，您就可以從前端節點使用 SSH，然後存取 hello 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="e6240-150">Once connected, you can then access hello worker nodes by using SSH from a headnode.</span></span>

## <a name="file-locations"></a><span data-ttu-id="e6240-151">檔案位置</span><span class="sxs-lookup"><span data-stu-id="e6240-151">File locations</span></span>

<span data-ttu-id="e6240-152">Hadoop 相關的檔案可以在 hello 叢集節點上找到`/usr/hdp`。</span><span class="sxs-lookup"><span data-stu-id="e6240-152">Hadoop-related files can be found on hello cluster nodes at `/usr/hdp`.</span></span> <span data-ttu-id="e6240-153">此目錄包含下列子目錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-153">This directory contains hello following subdirectories:</span></span>

* <span data-ttu-id="e6240-154">**2.2.4.9-1**: hello 目錄名稱是 hello hello Hortonworks Data Platform 使用 HDInsight 版本。</span><span class="sxs-lookup"><span data-stu-id="e6240-154">**2.2.4.9-1**: hello directory name is hello version of hello Hortonworks Data Platform used by HDInsight.</span></span> <span data-ttu-id="e6240-155">在叢集上的 hello 數目可能不同於此處所列的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="e6240-155">hello number on your cluster may be different than hello one listed here.</span></span>
* <span data-ttu-id="e6240-156">**目前**： 此目錄包含 hello 底下的連結 toosubdirectories **2.2.4.9-1**目錄。</span><span class="sxs-lookup"><span data-stu-id="e6240-156">**current**: This directory contains links toosubdirectories under hello **2.2.4.9-1** directory.</span></span> <span data-ttu-id="e6240-157">此目錄存在，所以您不需要 tooremember hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="e6240-157">This directory exists so that you don't have tooremember hello version number.</span></span>

<span data-ttu-id="e6240-158">在 Hadoop 分散式檔案系統的 `/example` 和 `/HdiSamples` 可取得範例資料和 JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6240-158">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span></span>

## <a name="hdfs-azure-storage-and-data-lake-store"></a><span data-ttu-id="e6240-159">HDFS、Azure 儲存體和 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e6240-159">HDFS, Azure Storage, and Data Lake Store</span></span>

<span data-ttu-id="e6240-160">在大部分的 Hadoop 散發 HDFS hello hello 叢集中的電腦上本機儲存體所支援。</span><span class="sxs-lookup"><span data-stu-id="e6240-160">In most Hadoop distributions, HDFS is backed by local storage on hello machines in hello cluster.</span></span> <span data-ttu-id="e6240-161">針對雲端解決方案使用本機儲存體的成本可能相當高，因為計算資源是以每小時或每分鐘為單位來計費。</span><span class="sxs-lookup"><span data-stu-id="e6240-161">Using local storage can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span></span>

<span data-ttu-id="e6240-162">HDInsight 使用 Azure 儲存體中的 blob 或 Azure Data Lake Store 做 hello 預設存放區。</span><span class="sxs-lookup"><span data-stu-id="e6240-162">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as hello default store.</span></span> <span data-ttu-id="e6240-163">這些服務會提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-163">These services provide hello following benefits:</span></span>

* <span data-ttu-id="e6240-164">長期儲存成本低廉</span><span class="sxs-lookup"><span data-stu-id="e6240-164">Cheap long-term storage</span></span>
* <span data-ttu-id="e6240-165">可從各種外部服務進行存取，例如網站、檔案上傳/下載公用程式、各種語言的 SDK 和網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="e6240-165">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span></span>

> [!WARNING]
> <span data-ttu-id="e6240-166">HDInsight 僅支援__一般用途__的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6240-166">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="e6240-167">它目前不支援 hello __Blob 儲存體__帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="e6240-167">It does not currently support hello __Blob storage__ account type.</span></span>

<span data-ttu-id="e6240-168">Azure 儲存體帳戶可以阻擋 too4.75 TB，雖然個別的 blob （或從 HDInsight 觀點來看的檔案） 可以只向上 too195 GB。</span><span class="sxs-lookup"><span data-stu-id="e6240-168">An Azure Storage account can hold up too4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up too195 GB.</span></span> <span data-ttu-id="e6240-169">Azure 資料湖存放區可以動態地成長檔案，的 toohold trillions 大於 pb 的個別檔案。</span><span class="sxs-lookup"><span data-stu-id="e6240-169">Azure Data Lake Store can grow dynamically toohold trillions of files, with individual files greater than a petabyte.</span></span> <span data-ttu-id="e6240-170">如需詳細資訊，請參閱[了解 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 和[Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。</span><span class="sxs-lookup"><span data-stu-id="e6240-170">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span>

<span data-ttu-id="e6240-171">使用 Azure 儲存體或資料湖存放區時，您沒有 toodo 特殊從 HDInsight tooaccess hello 資料的任何項目。</span><span class="sxs-lookup"><span data-stu-id="e6240-171">When using either Azure Storage or Data Lake Store, you don't have toodo anything special from HDInsight tooaccess hello data.</span></span> <span data-ttu-id="e6240-172">例如，下列命令的 hello 列出限制清單中 hello`/example/data`不論其是否儲存在 Azure 儲存體或資料湖存放區的資料夾：</span><span class="sxs-lookup"><span data-stu-id="e6240-172">For example, hello following command lists files in hello `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span></span>

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a><span data-ttu-id="e6240-173">URI 和配置</span><span class="sxs-lookup"><span data-stu-id="e6240-173">URI and scheme</span></span>

<span data-ttu-id="e6240-174">有些命令時，可能需要您 toospecify hello 配置 hello URI 的一部分存取檔案。</span><span class="sxs-lookup"><span data-stu-id="e6240-174">Some commands may require you toospecify hello scheme as part of hello URI when accessing a file.</span></span> <span data-ttu-id="e6240-175">例如，hello Storm HDFS 元件需要您 toospecify hello 配置。</span><span class="sxs-lookup"><span data-stu-id="e6240-175">For example, hello Storm-HDFS component requires you toospecify hello scheme.</span></span> <span data-ttu-id="e6240-176">當使用非預設儲存體 （儲存體新增為 「 其他 」 的儲存體 toohello 叢集），您必須一律使用 hello 配置 hello URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e6240-176">When using non-default storage (storage added as "additional" storage toohello cluster), you must always use hello scheme as part of hello URI.</span></span>

<span data-ttu-id="e6240-177">當使用__Azure 儲存體__，使用其中一種 hello 下列 URI 配置：</span><span class="sxs-lookup"><span data-stu-id="e6240-177">When using __Azure Storage__, use one of hello following URI schemes:</span></span>

* <span data-ttu-id="e6240-178">`wasb:///`︰使用未加密通訊存取預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e6240-178">`wasb:///`: Access default storage using unencrypted communication.</span></span>

* <span data-ttu-id="e6240-179">`wasbs:///`︰使用加密通訊存取預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e6240-179">`wasbs:///`: Access default storage using encrypted communication.</span></span>  <span data-ttu-id="e6240-180">只能從 HDInsight 3.6 版及更新版本支援 hello wasbs 配置。</span><span class="sxs-lookup"><span data-stu-id="e6240-180">hello wasbs scheme is supported only from HDInsight version 3.6 onwards.</span></span>

* <span data-ttu-id="e6240-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`︰以非預設儲存體帳戶進行通訊時使用。</span><span class="sxs-lookup"><span data-stu-id="e6240-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span></span> <span data-ttu-id="e6240-182">例如，當您有其他儲存體帳戶，或在可公開存取的儲存體帳戶中存取儲存的資料時。</span><span class="sxs-lookup"><span data-stu-id="e6240-182">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span></span>

<span data-ttu-id="e6240-183">當使用__Data Lake Store__，使用其中一種 hello 下列 URI 配置：</span><span class="sxs-lookup"><span data-stu-id="e6240-183">When using __Data Lake Store__, use one of hello following URI schemes:</span></span>

* <span data-ttu-id="e6240-184">`adl:///`： 存取 hello 預設 Data Lake Store hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-184">`adl:///`: Access hello default Data Lake Store for hello cluster.</span></span>

* <span data-ttu-id="e6240-185">`adl://<storage-name>.azuredatalakestore.net/`：用來與非預設 Data Lake Store 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="e6240-185">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store.</span></span> <span data-ttu-id="e6240-186">也可以用您的 HDInsight 叢集的 hello 根目錄之外的 tooaccess 資料。</span><span class="sxs-lookup"><span data-stu-id="e6240-186">Also used tooaccess data outside hello root directory of your HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6240-187">當使用資料湖存放區做為 hello HDInsight 的預設存放區，您必須指定 hello 存放區 toouse 內的路徑為 hello HDInsight 儲存區根目錄。</span><span class="sxs-lookup"><span data-stu-id="e6240-187">When using Data Lake Store as hello default store for HDInsight, you must specify a path within hello store toouse as hello root of HDInsight storage.</span></span> <span data-ttu-id="e6240-188">hello 預設路徑是`/clusters/<cluster-name>/`。</span><span class="sxs-lookup"><span data-stu-id="e6240-188">hello default path is `/clusters/<cluster-name>/`.</span></span>
>
> <span data-ttu-id="e6240-189">使用時`/`或`adl:///`tooaccess 資料，您只能存取儲存在 hello 根目錄中的資料 (例如， `/clusters/<cluster-name>/`) 的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-189">When using `/` or `adl:///` tooaccess data, you can only access data stored in hello root (for example, `/clusters/<cluster-name>/`) of hello cluster.</span></span> <span data-ttu-id="e6240-190">tooaccess 資料 hello 存放區中的任何位置使用 hello`adl://<storage-name>.azuredatalakestore.net/`格式。</span><span class="sxs-lookup"><span data-stu-id="e6240-190">tooaccess data anywhere in hello store, use hello `adl://<storage-name>.azuredatalakestore.net/` format.</span></span>

### <a name="what-storage-is-hello-cluster-using"></a><span data-ttu-id="e6240-191">Hello 叢集正在使用何種儲存體</span><span class="sxs-lookup"><span data-stu-id="e6240-191">What storage is hello cluster using</span></span>

<span data-ttu-id="e6240-192">您可以使用 Ambari tooretrieve hello 預設儲存體設定 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-192">You can use Ambari tooretrieve hello default storage configuration for hello cluster.</span></span> <span data-ttu-id="e6240-193">使用 hello 下列命令使用 curl，tooretrieve HDFS 組態資訊，並使用[jq](https://stedolan.github.io/jq/):</span><span class="sxs-lookup"><span data-stu-id="e6240-193">Use hello following command tooretrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span></span>

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> <span data-ttu-id="e6240-194">這會傳回第一次套用設定 toohello 伺服器 hello (`service_config_version=1`)，其中包含這項資訊。</span><span class="sxs-lookup"><span data-stu-id="e6240-194">This returns hello first configuration applied toohello server (`service_config_version=1`), which contains this information.</span></span> <span data-ttu-id="e6240-195">您可能需要 toolist toofind hello 最新版本的所有組態版本。</span><span class="sxs-lookup"><span data-stu-id="e6240-195">You may need toolist all configuration versions toofind hello latest one.</span></span>

<span data-ttu-id="e6240-196">此命令會傳回值的類似 toohello，下列 Uri:</span><span class="sxs-lookup"><span data-stu-id="e6240-196">This command returns a value similar toohello following URIs:</span></span>

* <span data-ttu-id="e6240-197">`wasb://<container-name>@<account-name>.blob.core.windows.net`，若使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6240-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span></span>

    <span data-ttu-id="e6240-198">hello 帳戶名稱是 hello hello Azure 儲存體帳戶名稱、 hello blob 容器 hello 容器名稱時，會是 hello 根 hello 叢集存放區。</span><span class="sxs-lookup"><span data-stu-id="e6240-198">hello account name is hello name of hello Azure Storage account, while hello container name is hello blob container that is hello root of hello cluster storage.</span></span>

* <span data-ttu-id="e6240-199">`adl://home`，若使用 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="e6240-199">`adl://home` if using Azure Data Lake Store.</span></span> <span data-ttu-id="e6240-200">tooget hello 資料湖存放區名稱，使用下列 REST 呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-200">tooget hello Data Lake Store name, use hello following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    <span data-ttu-id="e6240-201">此命令會傳回下列主機名稱的 hello: `<data-lake-store-account-name>.azuredatalakestore.net`。</span><span class="sxs-lookup"><span data-stu-id="e6240-201">This command returns hello following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span></span>

    <span data-ttu-id="e6240-202">是使用下列 REST 呼叫的 hello HDInsight 的 hello 根 hello 存放區內 tooget hello 目錄：</span><span class="sxs-lookup"><span data-stu-id="e6240-202">tooget hello directory within hello store that is hello root for HDInsight, use hello following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    <span data-ttu-id="e6240-203">此命令會傳回下列路徑的路徑類似的 toohello: `/clusters/<hdinsight-cluster-name>/`。</span><span class="sxs-lookup"><span data-stu-id="e6240-203">This command returns a path similar toohello following path: `/clusters/<hdinsight-cluster-name>/`.</span></span>

<span data-ttu-id="e6240-204">您也可以找到使用 hello Azure 入口網站使用下列步驟的 hello hello 儲存體資訊：</span><span class="sxs-lookup"><span data-stu-id="e6240-204">You can also find hello storage information using hello Azure portal by using hello following steps:</span></span>

1. <span data-ttu-id="e6240-205">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-205">In hello [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="e6240-206">從 hello**屬性**區段中，選取**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e6240-206">From hello **Properties** section, select **Storage Accounts**.</span></span> <span data-ttu-id="e6240-207">會顯示 hello hello 叢集的儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="e6240-207">hello storage information for hello cluster is displayed.</span></span>

### <a name="how-do-i-access-files-from-outside-hdinsight"></a><span data-ttu-id="e6240-208">如何從 HDInsight 外部存取檔案</span><span class="sxs-lookup"><span data-stu-id="e6240-208">How do I access files from outside HDInsight</span></span>

<span data-ttu-id="e6240-209">有各種方式從外部 hello HDInsight 叢集 tooaccess 資料。</span><span class="sxs-lookup"><span data-stu-id="e6240-209">There are a various ways tooaccess data from outside hello HDInsight cluster.</span></span> <span data-ttu-id="e6240-210">hello 以下是一些連結 tooutilities 和 Sdk 可與您的資料使用的 toowork:</span><span class="sxs-lookup"><span data-stu-id="e6240-210">hello following are a few links tooutilities and SDKs that can be used toowork with your data:</span></span>

<span data-ttu-id="e6240-211">如果使用__Azure 儲存體__，請參閱下列連結查看的方式，您可以存取資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-211">If using __Azure Storage__, see hello following links for ways that you can access your data:</span></span>

* <span data-ttu-id="e6240-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)：適用於 Azure 的命令列介面命令。</span><span class="sxs-lookup"><span data-stu-id="e6240-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span></span> <span data-ttu-id="e6240-213">安裝之後，使用 hello`az storage`命令說明使用的存放裝置或`az storage blob`blob 特定的命令。</span><span class="sxs-lookup"><span data-stu-id="e6240-213">After installing, use hello `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span></span>
* <span data-ttu-id="e6240-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage)：python 指令碼，用於 Azure 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e6240-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span></span>
* <span data-ttu-id="e6240-215">各種 SDK：</span><span class="sxs-lookup"><span data-stu-id="e6240-215">Various SDKs:</span></span>

    * [<span data-ttu-id="e6240-216">Java</span><span class="sxs-lookup"><span data-stu-id="e6240-216">Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
    * [<span data-ttu-id="e6240-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="e6240-217">Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
    * [<span data-ttu-id="e6240-218">PHP</span><span class="sxs-lookup"><span data-stu-id="e6240-218">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
    * [<span data-ttu-id="e6240-219">Python</span><span class="sxs-lookup"><span data-stu-id="e6240-219">Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
    * [<span data-ttu-id="e6240-220">Ruby</span><span class="sxs-lookup"><span data-stu-id="e6240-220">Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)
    * [<span data-ttu-id="e6240-221">.NET</span><span class="sxs-lookup"><span data-stu-id="e6240-221">.NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
    * [<span data-ttu-id="e6240-222">儲存體 REST API</span><span class="sxs-lookup"><span data-stu-id="e6240-222">Storage REST API</span></span>](https://msdn.microsoft.com/library/azure/dd135733.aspx)

<span data-ttu-id="e6240-223">如果使用__Azure Data Lake Store__，請參閱下列連結查看的方式，您可以存取資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-223">If using __Azure Data Lake Store__, see hello following links for ways that you can access your data:</span></span>

* [<span data-ttu-id="e6240-224">Web 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="e6240-224">Web browser</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* [<span data-ttu-id="e6240-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6240-225">PowerShell</span></span>](../data-lake-store/data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="e6240-226">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e6240-226">Azure CLI 2.0</span></span>](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [<span data-ttu-id="e6240-227">WebHDFS REST API</span><span class="sxs-lookup"><span data-stu-id="e6240-227">WebHDFS REST API</span></span>](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="e6240-228">Visual Studio 適用的 Data Lake 工具</span><span class="sxs-lookup"><span data-stu-id="e6240-228">Data Lake Tools for Visual Studio</span></span>](https://www.microsoft.com/download/details.aspx?id=49504)
* [<span data-ttu-id="e6240-229">.NET</span><span class="sxs-lookup"><span data-stu-id="e6240-229">.NET</span></span>](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="e6240-230">Java</span><span class="sxs-lookup"><span data-stu-id="e6240-230">Java</span></span>](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="e6240-231">Python</span><span class="sxs-lookup"><span data-stu-id="e6240-231">Python</span></span>](../data-lake-store/data-lake-store-get-started-python.md)

## <span data-ttu-id="e6240-232"><a name="scaling"></a>調整您的叢集規模</span><span class="sxs-lookup"><span data-stu-id="e6240-232"><a name="scaling"></a>Scaling your cluster</span></span>

<span data-ttu-id="e6240-233">hello 叢集調整功能可讓您 toodynamically 變更 hello 叢集所用的資料節點數。</span><span class="sxs-lookup"><span data-stu-id="e6240-233">hello cluster scaling feature allows you toodynamically change hello number of data nodes used by a cluster.</span></span> <span data-ttu-id="e6240-234">正在叢集上執行其他工作或處理序時，您可以執行調整作業。</span><span class="sxs-lookup"><span data-stu-id="e6240-234">You can perform scaling operations while other jobs or processes are running on a cluster.</span></span>

<span data-ttu-id="e6240-235">hello 不同的叢集類型會受到縮放比例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e6240-235">hello different cluster types are affected by scaling as follows:</span></span>

* <span data-ttu-id="e6240-236">**Hadoop**： 當規模 hello 叢集中的節點數目，某些 hello 叢集中的 hello 服務會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e6240-236">**Hadoop**: When scaling down hello number of nodes in a cluster, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="e6240-237">調整作業可能導致工作執行或暫止 toofail hello hello 調整大小作業完成時。</span><span class="sxs-lookup"><span data-stu-id="e6240-237">Scaling operations can cause jobs running or pending toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="e6240-238">當 hello 操作完成之後，您可以重新提交 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e6240-238">You can resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="e6240-239">**對 HBase**: hello 調整大小作業完成之後的幾分鐘內自動平衡地區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6240-239">**HBase**: Regional servers are automatically balanced within a few minutes after completion of hello scaling operation.</span></span> <span data-ttu-id="e6240-240">toomanually 平衡地區伺服器，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-240">toomanually balance regional servers, use hello following steps:</span></span>

    1. <span data-ttu-id="e6240-241">Toohello HDInsight 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="e6240-241">Connect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="e6240-242">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e6240-242">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    2. <span data-ttu-id="e6240-243">使用下列 toostart hello HBase 殼層 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-243">Use hello following toostart hello HBase shell:</span></span>

            hbase shell

    3. <span data-ttu-id="e6240-244">Hello HBase 殼層已載入後，使用下列 toomanually 平衡 hello 地區伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-244">Once hello HBase shell has loaded, use hello following toomanually balance hello regional servers:</span></span>

            balancer

* <span data-ttu-id="e6240-245">**Storm**︰執行調整作業之後，您應該重新平衡任何執行中的 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="e6240-245">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span></span> <span data-ttu-id="e6240-246">重新平衡可讓 hello 新 hello 叢集中的節點數目為基礎的 hello 拓撲 tooreadjust 平行處理原則設定。</span><span class="sxs-lookup"><span data-stu-id="e6240-246">Rebalancing allows hello topology tooreadjust parallelism settings based on hello new number of nodes in hello cluster.</span></span> <span data-ttu-id="e6240-247">toorebalance 執行拓撲中，使用其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="e6240-247">toorebalance running topologies, use one of hello following options:</span></span>

    * <span data-ttu-id="e6240-248">**SSH**: toohello 伺服器連接，並使用 hello 下列命令 toorebalance 拓撲：</span><span class="sxs-lookup"><span data-stu-id="e6240-248">**SSH**: Connect toohello server and use hello following command toorebalance a topology:</span></span>

            storm rebalance TOPOLOGYNAME

        <span data-ttu-id="e6240-249">您也可以指定參數 toooverride hello 平行處理原則提示原本提供的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="e6240-249">You can also specify parameters toooverride hello parallelism hints originally provided by hello topology.</span></span> <span data-ttu-id="e6240-250">例如，`storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10`檔重新設定 hello 拓撲 too5 背景工作處理序、 3 hello 藍色 spout 元件，執行程式和 10 hello 黃色閃電元件執行程式。</span><span class="sxs-lookup"><span data-stu-id="e6240-250">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures hello topology too5 worker processes, 3 executors for hello blue-spout component, and 10 executors for hello yellow-bolt component.</span></span>

    * <span data-ttu-id="e6240-251">**Storm UI**： 使用 hello 下列步驟 toorebalance 使用 hello Storm UI 的拓撲。</span><span class="sxs-lookup"><span data-stu-id="e6240-251">**Storm UI**: Use hello following steps toorebalance a topology using hello Storm UI.</span></span>

        1. <span data-ttu-id="e6240-252">開啟**https://CLUSTERNAME.azurehdinsight.net/stormui**網頁瀏覽器，其中 CLUSTERNAME 是 hello Storm 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="e6240-252">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is hello name of your Storm cluster.</span></span> <span data-ttu-id="e6240-253">如果出現提示，請輸入 hello HDInsight 叢集系統管理員 （管理員） 的名稱和密碼建立 hello 叢集時，您所指定。</span><span class="sxs-lookup"><span data-stu-id="e6240-253">If prompted, enter hello HDInsight cluster administrator (admin) name and password you specified when creating hello cluster.</span></span>
        2. <span data-ttu-id="e6240-254">選取您想 toorebalance，然後選擇 hello hello 拓撲**重新平衡** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6240-254">Select hello topology you wish toorebalance, then select hello **Rebalance** button.</span></span> <span data-ttu-id="e6240-255">執行 hello 重新平衡作業之前，請輸入 hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="e6240-255">Enter hello delay before hello rebalance operation is performed.</span></span>

<span data-ttu-id="e6240-256">如需有關調整 HDInsight 叢集的特定資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e6240-256">For specific information on scaling your HDInsight cluster, see:</span></span>

* [<span data-ttu-id="e6240-257">透過 hello Azure 入口網站來管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e6240-257">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="e6240-258">使用 Azure PowerShell 管理 HDInsight 上的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e6240-258">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a><span data-ttu-id="e6240-259">如何安裝 Hue (或其他 Hadoop 元件)？</span><span class="sxs-lookup"><span data-stu-id="e6240-259">How do I install Hue (or other Hadoop component)?</span></span>

<span data-ttu-id="e6240-260">HDInsight 是受管理的服務。</span><span class="sxs-lookup"><span data-stu-id="e6240-260">HDInsight is a managed service.</span></span> <span data-ttu-id="e6240-261">如果 Azure 偵測到問題與 hello 叢集時，它可能會刪除 hello 失敗節點，並建立節點 tooreplace 它。</span><span class="sxs-lookup"><span data-stu-id="e6240-261">If Azure detects a problem with hello cluster, it may delete hello failing node and create a node tooreplace it.</span></span> <span data-ttu-id="e6240-262">如果您手動 hello 叢集上安裝項目，它們不會保存時就會發生這項作業。</span><span class="sxs-lookup"><span data-stu-id="e6240-262">If you manually install things on hello cluster, they are not persisted when this operation occurs.</span></span> <span data-ttu-id="e6240-263">請改用 [HDInsight 指令碼動作](hdinsight-hadoop-customize-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="e6240-263">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="e6240-264">指令碼動作可以是使用的 toomake hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="e6240-264">A script action can be used toomake hello following changes:</span></span>

* <span data-ttu-id="e6240-265">安裝及設定服務或網站，例如 Spark 或 Hue。</span><span class="sxs-lookup"><span data-stu-id="e6240-265">Install and configure a service or web site such as Spark or Hue.</span></span>
* <span data-ttu-id="e6240-266">安裝和設定需要 hello 叢集中的多個節點上的組態變更的元件。</span><span class="sxs-lookup"><span data-stu-id="e6240-266">Install and configure a component that requires configuration changes on multiple nodes in hello cluster.</span></span> <span data-ttu-id="e6240-267">例如，必要的環境變數、建立記錄目錄或建立組態檔。</span><span class="sxs-lookup"><span data-stu-id="e6240-267">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span></span>

<span data-ttu-id="e6240-268">指令碼動作是 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e6240-268">Script Actions are Bash scripts.</span></span> <span data-ttu-id="e6240-269">hello 指令碼執行期間佈建叢集時，可使用的 tooinstall 及 hello 叢集上設定其他元件。</span><span class="sxs-lookup"><span data-stu-id="e6240-269">hello scripts run during cluster provisioning, and can be used tooinstall and configure additional components on hello cluster.</span></span> <span data-ttu-id="e6240-270">範例指令碼可供安裝下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6240-270">Example scripts are provided for installing hello following components:</span></span>

* [<span data-ttu-id="e6240-271">Hue</span><span class="sxs-lookup"><span data-stu-id="e6240-271">Hue</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="e6240-272">Giraph</span><span class="sxs-lookup"><span data-stu-id="e6240-272">Giraph</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="e6240-273">Solr</span><span class="sxs-lookup"><span data-stu-id="e6240-273">Solr</span></span>](hdinsight-hadoop-solr-install-linux.md)

<span data-ttu-id="e6240-274">如需開發您自己的指令碼動作相關資訊，請參閱 [使用 HDInsight 開發指令碼動作](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e6240-274">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

### <a name="jar-files"></a><span data-ttu-id="e6240-275">JAR 檔案</span><span class="sxs-lookup"><span data-stu-id="e6240-275">Jar files</span></span>

<span data-ttu-id="e6240-276">獨立的 jar 檔案中提供了一些 Hadoop 技術，其中包含可用來做為 MapReduce 工作一部分的函式，或者來自 Pig 或 Hive 內部的函式。</span><span class="sxs-lookup"><span data-stu-id="e6240-276">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span></span> <span data-ttu-id="e6240-277">雖然這些都可以使用安裝指令碼動作，它們通常不需要任何設定和佈建之後可以上傳的 toohello 叢集，直接使用。</span><span class="sxs-lookup"><span data-stu-id="e6240-277">While these can be installed using Script Actions, they often don't require any setup and can be uploaded toohello cluster after provisioning and used directly.</span></span> <span data-ttu-id="e6240-278">如果您想確定 hello 元件 toomake 未重新安裝映像的 hello 叢集，您可以為您的叢集 （WASB 或 ADL） hello jar 檔儲存在 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e6240-278">If you want toomake sure hello component survives reimaging of hello cluster, you can store hello jar file in hello default storage for your cluster (WASB or ADL).</span></span>

<span data-ttu-id="e6240-279">例如，如果您想要 toouse hello 最新版本的[DataFu](http://datafu.incubator.apache.org/)，您可以下載的 jar 包含 hello 專案，並將它上傳 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6240-279">For example, if you want toouse hello latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing hello project and upload it toohello HDInsight cluster.</span></span> <span data-ttu-id="e6240-280">如何依照 hello DataFu 文件 toouse 從 Pig 或登錄區。</span><span class="sxs-lookup"><span data-stu-id="e6240-280">Then follow hello DataFu documentation on how toouse it from Pig or Hive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6240-281">獨立 jar 檔案的某些元件所提供的 HDInsight，但是不在 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="e6240-281">Some components that are standalone jar files are provided with HDInsight, but are not in hello path.</span></span> <span data-ttu-id="e6240-282">如果您要尋找特定元件，您可以使用它的 hello 後續 toosearch 在叢集上：</span><span class="sxs-lookup"><span data-stu-id="e6240-282">If you are looking for a specific component, you can use hello follow toosearch for it on your cluster:</span></span>
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> <span data-ttu-id="e6240-283">此命令會傳回 hello 的任何相符的 jar 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="e6240-283">This command returns hello path of any matching jar files.</span></span>

<span data-ttu-id="e6240-284">toouse 不同版本的元件，請上傳 hello 版本，您需要並將它用於您的工作。</span><span class="sxs-lookup"><span data-stu-id="e6240-284">toouse a different version of a component, upload hello version you need and use it in your jobs.</span></span>

> [!WARNING]
> <span data-ttu-id="e6240-285">完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務可協助 tooisolate 並解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="e6240-285">Components provided with hello HDInsight cluster are fully supported and Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="e6240-286">自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="e6240-286">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="e6240-287">這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。</span><span class="sxs-lookup"><span data-stu-id="e6240-287">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="e6240-288">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="e6240-288">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6240-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6240-289">Next steps</span></span>

* [<span data-ttu-id="e6240-290">從 Windows 為基礎的 HDInsight tooLinux 式移轉</span><span class="sxs-lookup"><span data-stu-id="e6240-290">Migrate from Windows-based HDInsight tooLinux-based</span></span>](hdinsight-migrate-from-windows-to-linux.md)
* [<span data-ttu-id="e6240-291">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="e6240-291">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e6240-292">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="e6240-292">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e6240-293">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="e6240-293">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
