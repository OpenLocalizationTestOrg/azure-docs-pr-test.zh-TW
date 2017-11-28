---
title: "使用共用存取簽章-Azure HDInsight aaaRestrict 存取 |Microsoft 文件"
description: "了解如何 toouse 共用存取簽章 toorestrict HDInsight 存取 toodata 儲存在 Azure 儲存體 blob。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="42164-103">使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata HDInsight 中</span><span class="sxs-lookup"><span data-stu-id="42164-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="42164-104">HDInsight 具有完整存取 toodata hello 與 hello 叢集相關聯的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="42164-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="42164-105">您可以使用共用存取簽章 hello blob 容器 toorestrict 存取 toohello 資料上。</span><span class="sxs-lookup"><span data-stu-id="42164-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="42164-106">例如，tooprovide 唯讀存取 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="42164-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="42164-107">共用存取簽章 (SAS) 是 Azure 儲存體帳戶的功能，可讓您 toolimit 存取 toodata。</span><span class="sxs-lookup"><span data-stu-id="42164-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="42164-108">例如，提供唯讀存取 toodata。</span><span class="sxs-lookup"><span data-stu-id="42164-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42164-109">對於使用 Apache Ranger 的解決方案，請考慮使用已加入網域的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="42164-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="42164-110">如需詳細資訊，請參閱 hello[設定已加入網域的 HDInsight](hdinsight-domain-joined-configure.md)文件。</span><span class="sxs-lookup"><span data-stu-id="42164-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="42164-111">HDInsight 必須 hello 叢集的完整存取 toohello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="42164-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="42164-112">需求</span><span class="sxs-lookup"><span data-stu-id="42164-112">Requirements</span></span>

* <span data-ttu-id="42164-113">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42164-113">An Azure subscription</span></span>
* <span data-ttu-id="42164-114">C# 或 Python。</span><span class="sxs-lookup"><span data-stu-id="42164-114">C# or Python.</span></span> <span data-ttu-id="42164-115">提供 C# 範例程式碼做為 Visual Studio 解決方案。</span><span class="sxs-lookup"><span data-stu-id="42164-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="42164-116">Visual Studio 的版本必須是 2013、2015 或 2017</span><span class="sxs-lookup"><span data-stu-id="42164-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="42164-117">Python 的版本必須是 2.7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="42164-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="42164-118">以 Linux 為基礎的 HDInsight 叢集或者[Azure PowerShell] [ powershell] -如果您有現有以 Linux 為基礎的叢集，您可以使用 Ambari tooadd 共用存取簽章 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="42164-119">如果沒有，您可以使用 Azure PowerShell toocreate 叢集，並在叢集建立期間新增共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="42164-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="42164-120">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="42164-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42164-121">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="42164-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="42164-122">hello 範例檔案，從[https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature)。</span><span class="sxs-lookup"><span data-stu-id="42164-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="42164-123">這個儲存機制包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="42164-124">Visual Studio 專案，可以建立儲存體容器、預存原則，以及搭配 HDInsight 使用的 SAS</span><span class="sxs-lookup"><span data-stu-id="42164-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="42164-125">Python 指令碼，可以建立儲存體容器、預存原則，以及搭配 HDInsight 使用的 SAS</span><span class="sxs-lookup"><span data-stu-id="42164-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="42164-126">PowerShell 指令碼可建立 HDInsight 叢集，並將它設定 toouse hello SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="42164-127">共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="42164-127">Shared Access Signatures</span></span>

<span data-ttu-id="42164-128">共用存取簽章有兩種格式：</span><span class="sxs-lookup"><span data-stu-id="42164-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="42164-129">臨機操作： hello 開始時間、 到期時間和 hello SAS 會指定在 hello SAS URI 的權限。</span><span class="sxs-lookup"><span data-stu-id="42164-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="42164-130">預存存取原則：預存存取原則會在資源容器中定義，例如 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="42164-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="42164-131">原則可以在一或多個共用的存取簽章使用的 toomanage 條件約束。</span><span class="sxs-lookup"><span data-stu-id="42164-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="42164-132">當您建立 SAS 關聯與預存的存取原則時，hello SAS 繼承 hello 的條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。</span><span class="sxs-lookup"><span data-stu-id="42164-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="42164-133">hello hello 兩個形式之間的差異是很重要的一個重要的案例： 撤銷。</span><span class="sxs-lookup"><span data-stu-id="42164-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="42164-134">SAS 是 URL，因此會取得 hello SAS 的任何人可以使用它，不論要求者 toobegin 與。</span><span class="sxs-lookup"><span data-stu-id="42164-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="42164-135">如果已公開發行 SAS，才能使用 hello 世界中的任何人。</span><span class="sxs-lookup"><span data-stu-id="42164-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="42164-136">散佈的 SAS 在發生以下四個情況其中之一之前都會持續有效：</span><span class="sxs-lookup"><span data-stu-id="42164-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="42164-137">hello 上 hello SAS 達到指定的到期時間。</span><span class="sxs-lookup"><span data-stu-id="42164-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="42164-138">hello hello 達到 SAS 所參考的 hello 預存存取原則中指定的到期時間。</span><span class="sxs-lookup"><span data-stu-id="42164-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="42164-139">hello 下列案例會造成 hello 到期時間達到 toobe:</span><span class="sxs-lookup"><span data-stu-id="42164-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="42164-140">hello 時間間隔已經耗盡時。</span><span class="sxs-lookup"><span data-stu-id="42164-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="42164-141">hello 預存存取原則是修改的 toohave hello 過去在到期時間。</span><span class="sxs-lookup"><span data-stu-id="42164-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="42164-142">變更 hello 到期時間是一種方式 toorevoke hello SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="42164-143">hello 預存存取原則參考的 hello SAS 遭到刪除，也就是另一個方式 toorevoke hello SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="42164-144">如果您重新建立 hello 預存存取原則，以名稱相同，為所有的 SAS 權杖的 hello hello 先前原則都有效 （如果尚未超過 SAS hello hello 上的到期時間）。</span><span class="sxs-lookup"><span data-stu-id="42164-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="42164-145">如果您想 toorevoke hello SAS，是確定 toouse 不同名稱，如果您重新建立與到期時間在未來的 hello hello 存取原則。</span><span class="sxs-lookup"><span data-stu-id="42164-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="42164-146">重新產生已使用的 toocreate hello SAS 的 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="42164-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="42164-147">重新產生 hello 金鑰會導致使用 hello 前一個索引鍵 toofail 驗證的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="42164-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="42164-148">更新所有元件 toohello 新機碼。</span><span class="sxs-lookup"><span data-stu-id="42164-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42164-149">共用的存取簽章 URI 都與 hello 帳戶金鑰的使用的 toocreate hello 簽章，與 hello 預存的存取原則 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="42164-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="42164-150">如果未不指定任何預存的存取原則，則 hello 只方式 toorevoke 共用的存取簽章是 toochange hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="42164-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="42164-151">建議您一律使用預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="42164-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="42164-152">使用預存的原則，您可以撤銷簽章，或視需要擴充 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="42164-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="42164-153">本文件中的 hello 步驟會使用預存的存取原則 toogenerate SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="42164-154">如需有關共用存取簽章的詳細資訊，請參閱[了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="42164-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="42164-155">使用 C\# 建立預存原則和 SAS</span><span class="sxs-lookup"><span data-stu-id="42164-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="42164-156">開啟 Visual Studio 中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="42164-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="42164-157">在 [方案總管] 中，以滑鼠右鍵按一下 hello **SASToken**專案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="42164-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="42164-158">選取**設定**並新增值 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="42164-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="42164-159">StorageConnectionString: hello 連接字串 hello 儲存體帳戶的 toocreate 儲存的原則和 SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="42164-160">hello 格式應該是`DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey`其中`myaccount`hello 儲存體帳戶名稱和`mykey`是 hello hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="42164-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="42164-161">ContainerName: hello hello 您想要 toorestrict 存取的儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="42164-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="42164-162">SASPolicyName: hello 的 hello 名稱 toouse 儲存原則 toocreate。</span><span class="sxs-lookup"><span data-stu-id="42164-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="42164-163">FileToUpload: hello 路徑 tooa 檔案上傳的 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="42164-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="42164-164">執行 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="42164-164">Run hello project.</span></span> <span data-ttu-id="42164-165">一旦產生 hello SAS，就會顯示下列文字的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="42164-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="42164-166">儲存 hello SAS 原則權杖、 儲存體帳戶名稱，以及容器名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="42164-167">建立 hello 儲存體帳戶與您的 HDInsight 叢集的關聯時，會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="42164-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="42164-168">使用 Python 建立預存原則和 SAS</span><span class="sxs-lookup"><span data-stu-id="42164-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="42164-169">開啟 hello SASToken.py 檔案並變更下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="42164-170">原則\_名稱： hello 的 hello 名稱 toouse 儲存原則 toocreate。</span><span class="sxs-lookup"><span data-stu-id="42164-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="42164-171">儲存體\_帳戶\_名稱： hello 您的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="42164-172">儲存體\_帳戶\_金鑰： hello hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="42164-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="42164-173">儲存體\_容器\_名稱： hello 您想要 toorestrict 存取的儲存體帳戶中的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="42164-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="42164-174">範例\_檔案\_路徑： hello 路徑 tooa 檔案上傳的 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="42164-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="42164-175">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="42164-175">Run hello script.</span></span> <span data-ttu-id="42164-176">它會顯示 hello SAS 權杖類似 toohello hello 指令碼完成時，下列文字：</span><span class="sxs-lookup"><span data-stu-id="42164-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="42164-177">儲存 hello SAS 原則權杖、 儲存體帳戶名稱，以及容器名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="42164-178">建立 hello 儲存體帳戶與您的 HDInsight 叢集的關聯時，會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="42164-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="42164-179">使用 hello SAS 與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="42164-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="42164-180">在建立 HDInsight 叢集時，您必須指定主要儲存體帳戶，您可以選擇性地指定其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42164-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="42164-181">這兩種方法的新增儲存體需要完整存取 toohello 儲存體帳戶和可用的容器。</span><span class="sxs-lookup"><span data-stu-id="42164-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="42164-182">toouse 共用存取簽章 toolimit 存取 tooa 容器，將自訂項目 toohello**核心站台**hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="42164-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="42164-183">如**windows**或**linux** HDInsight 叢集，您可以使用 PowerShell 的叢集建立期間新增 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="42164-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="42164-184">如**linux** HDInsight 叢集，變更後使用 Ambari 叢集建立的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="42164-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="42164-185">建立使用 hello SAS 的叢集</span><span class="sxs-lookup"><span data-stu-id="42164-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="42164-186">SAS 隨附於 hello 該使用 hello 建立 HDInsight 叢集的範例`CreateCluster`hello 儲存機制的目錄。</span><span class="sxs-lookup"><span data-stu-id="42164-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="42164-187">toouse 它使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42164-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="42164-188">開啟 hello`CreateCluster\HDInsightSAS.ps1`檔案文字編輯器中，並修改 hello hello hello 從文件開頭的值。</span><span class="sxs-lookup"><span data-stu-id="42164-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="42164-189">例如，變更`'mycluster'`toohello 名稱要 toocreate 的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="42164-190">建立儲存體帳戶和 SAS 權杖時，hello SAS 值應該符合 hello hello 先前步驟中的值。</span><span class="sxs-lookup"><span data-stu-id="42164-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="42164-191">一旦您已變更 hello 值，將儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="42164-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="42164-192">開啟新的 Azure PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="42164-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="42164-193">如果您不熟悉或尚未安裝 Azure PowerShell，請參閱[安裝和設定 Azure PowerShell][powershell]。</span><span class="sxs-lookup"><span data-stu-id="42164-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="42164-194">從 hello 提示字元中，使用下列命令 tooauthenticate tooyour Azure 訂用帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="42164-195">出現提示時，帳戶登入 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="42164-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="42164-196">如果您的帳戶與多個 Azure 訂用帳戶相關聯，您可能需要 toouse`Select-AzureRmSubscription`想 toouse tooselect hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="42164-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="42164-197">Hello 提示字元中，變更目錄 toohello `CreateCluster` hello HDInsightSAS.ps1 檔所在目錄。</span><span class="sxs-lookup"><span data-stu-id="42164-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="42164-198">然後使用下列命令 toorun hello 指令碼的 hello</span><span class="sxs-lookup"><span data-stu-id="42164-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="42164-199">Hello 指令碼執行，就會記錄輸出 toohello PowerShell 命令提示字元，會在建立 hello 資源群組和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42164-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="42164-200">您會提示的 tooenter hello HTTP 使用者 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="42164-201">此帳戶是使用的 toosecure HTTP/s 存取 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="42164-202">如果您是建立以 Linux 為基礎的叢集，系統會提示您輸入 SSH 使用者帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="42164-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="42164-203">此帳戶是使用的 tooremotely toohello 叢集中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="42164-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="42164-204">出現提示時輸入 hello HTTP/s 或 SSH 使用者名稱和密碼，您必須提供符合下列準則的 hello 的密碼：</span><span class="sxs-lookup"><span data-stu-id="42164-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="42164-205">長度必須小於 10 個字元</span><span class="sxs-lookup"><span data-stu-id="42164-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="42164-206">必須包含至少一個數字</span><span class="sxs-lookup"><span data-stu-id="42164-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="42164-207">必須包含至少一個非英數字元</span><span class="sxs-lookup"><span data-stu-id="42164-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="42164-208">必須包含至少一個大寫或小寫字元</span><span class="sxs-lookup"><span data-stu-id="42164-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="42164-209">它需要一些時間此指令碼 toocomplete，通常大約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="42164-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="42164-210">Hello 指令碼完成時沒有發生任何錯誤，已建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="42164-211">現有的叢集中使用 hello SAS</span><span class="sxs-lookup"><span data-stu-id="42164-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="42164-212">如果您有現有以 Linux 為基礎的叢集，您可以加入 hello SAS toohello**核心站台**組態使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42164-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="42164-213">開啟您的叢集，hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="42164-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="42164-214">此頁面的 hello 位址是 https://YOURCLUSTERNAME.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="42164-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="42164-215">出現提示時，驗證使用 hello 管理員名稱 （管理員） toohello 叢集和建立 hello 叢集時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="42164-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="42164-216">Hello hello Ambari web UI 的左方，從選取**HDFS** ，然後選取 hello **Configs** hello 中間的 hello 頁面 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42164-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="42164-217">選取 hello**進階**索引標籤，然後再向下捲動直到您找到 hello**自訂的核心站台**> 一節。</span><span class="sxs-lookup"><span data-stu-id="42164-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="42164-218">展開 hello**自訂的核心站台** 區段中，然後捲動 toohello 結束作業，並選取 hello**加入屬性...**連結。</span><span class="sxs-lookup"><span data-stu-id="42164-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="42164-219">使用 hello 下列值 hello**金鑰**和**值**欄位：</span><span class="sxs-lookup"><span data-stu-id="42164-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="42164-220">**金鑰**：fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="42164-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="42164-221">**值**: hello hello 先前執行的 C# 或 Python 應用程式所傳回的 SAS</span><span class="sxs-lookup"><span data-stu-id="42164-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="42164-222">取代**CONTAINERNAME** hello 容器名稱與您用於 hello C# 或 SAS 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="42164-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="42164-223">取代**STORAGEACCOUNTNAME** hello 您所使用的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="42164-224">按一下 hello**新增**按鈕 toosave 此索引鍵和值，然後按一下 hello**儲存**按鈕 toosave hello 組態變更。</span><span class="sxs-lookup"><span data-stu-id="42164-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="42164-225">出現提示時，新增 hello 變更 （「 新增 SAS 存放裝置存取 」，例如） 的描述，然後再按**儲存**。</span><span class="sxs-lookup"><span data-stu-id="42164-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="42164-226">按一下**確定**hello 變更都完成時。</span><span class="sxs-lookup"><span data-stu-id="42164-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="42164-227">Hello 變更生效之前，您必須重新啟動數個服務。</span><span class="sxs-lookup"><span data-stu-id="42164-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="42164-228">Hello Ambari web UI，在選取**HDFS** hello 清單 hello 左、，然後選取從**重新啟動所有**從 hello**服務動作**下拉式清單上 hello 右邊的清單。</span><span class="sxs-lookup"><span data-stu-id="42164-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="42164-229">出現提示時，選取 [開啟維護模式]，然後選取 [確認全部重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="42164-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="42164-230">對 MapReduce2 和 YARN 重複此程序。</span><span class="sxs-lookup"><span data-stu-id="42164-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="42164-231">Hello 服務已重新啟動後，選取每個和停用維護模式，從 hello**服務動作**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="42164-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="42164-232">測試限制的存取</span><span class="sxs-lookup"><span data-stu-id="42164-232">Test restricted access</span></span>

<span data-ttu-id="42164-233">您已限制的 tooverify 存取，請使用下列方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="42164-234">如**windows** HDInsight 叢集，使用遠端桌面 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="42164-235">如需詳細資訊，請參閱[連接使用 RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="42164-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="42164-236">一旦連接之後，使用 hello **Hadoop 命令列**hello 桌面 tooopen 命令提示字元上的圖示。</span><span class="sxs-lookup"><span data-stu-id="42164-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="42164-237">如**linux** HDInsight 叢集使用 SSH tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="42164-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="42164-238">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="42164-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="42164-239">一旦連接之後 toohello 叢集，使用下列步驟 tooverify，您可以在 hello SAS 儲存體帳戶只有讀取和清單的項目 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="42164-240">hello 容器 toolist hello 內容使用 hello hello 提示字元中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="42164-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="42164-241">取代**SASCONTAINER** hello hello 容器建立 hello SAS 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="42164-242">取代**SASACCOUNTNAME** hello hello hello SA 所使用的儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="42164-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="42164-243">hello 清單包含 hello 檔案上傳時已建立 hello 容器和 SAS。</span><span class="sxs-lookup"><span data-stu-id="42164-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="42164-244">使用下列命令，您可以讀取 hello hello 檔案內容的 tooverify hello。</span><span class="sxs-lookup"><span data-stu-id="42164-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="42164-245">取代 hello **SASCONTAINER**和**SASACCOUNTNAME**如同 hello 前一個步驟。</span><span class="sxs-lookup"><span data-stu-id="42164-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="42164-246">取代**FILENAME** hello 顯示 hello 先前命令中的 hello 檔名稱：</span><span class="sxs-lookup"><span data-stu-id="42164-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="42164-247">此命令會列出 hello hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="42164-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="42164-248">使用下列命令 toodownload hello 檔案 toohello 本機檔案系統的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="42164-249">此命令下載 hello tooa 本機檔案命名為**testfile.txt**。</span><span class="sxs-lookup"><span data-stu-id="42164-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="42164-250">使用 hello 下列命令 tooupload hello 本機檔案 tooa 名為新檔案**testupload.txt** hello SAS 存放裝置上：</span><span class="sxs-lookup"><span data-stu-id="42164-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="42164-251">您會收到訊息的類似 toohello，下列文字：</span><span class="sxs-lookup"><span data-stu-id="42164-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="42164-252">因為 hello 儲存位置讀取 + 清單只會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="42164-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="42164-253">使用下列命令 tooput hello 資料 hello hello 叢集中，這是可寫入的預設儲存體上的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="42164-254">這次 hello 作業應該順利完成。</span><span class="sxs-lookup"><span data-stu-id="42164-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="42164-255">疑難排解</span><span class="sxs-lookup"><span data-stu-id="42164-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="42164-256">已取消工作</span><span class="sxs-lookup"><span data-stu-id="42164-256">A task was canceled</span></span>

<span data-ttu-id="42164-257">**徵兆**： 建立使用 hello PowerShell 指令碼的叢集，您可能會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="42164-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="42164-258">**可能的原因**： 如果您使用的密碼 hello admin/HTTP 使用者 hello 叢集，或 （適用於以 Linux 為基礎的叢集），會發生此錯誤 hello SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="42164-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="42164-259">**解析**： 使用符合下列準則的 hello 的密碼：</span><span class="sxs-lookup"><span data-stu-id="42164-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="42164-260">長度必須小於 10 個字元</span><span class="sxs-lookup"><span data-stu-id="42164-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="42164-261">必須包含至少一個數字</span><span class="sxs-lookup"><span data-stu-id="42164-261">Must contain at least one digit</span></span>
* <span data-ttu-id="42164-262">必須包含至少一個非英數字元</span><span class="sxs-lookup"><span data-stu-id="42164-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="42164-263">必須包含至少一個大寫或小寫字元</span><span class="sxs-lookup"><span data-stu-id="42164-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="42164-264">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42164-264">Next steps</span></span>

<span data-ttu-id="42164-265">既然您已經學會如何 tooadd 限制存取儲存體 tooyour HDInsight 叢集，了解您的叢集上的資料與其他方式 toowork:</span><span class="sxs-lookup"><span data-stu-id="42164-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="42164-266">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="42164-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="42164-267">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="42164-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="42164-268">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="42164-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
