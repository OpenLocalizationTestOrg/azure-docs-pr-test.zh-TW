---
title: "aaaHow toodelete 的 HDInsight 叢集的 Azure |Microsoft 文件"
description: "Hello，您可以刪除 HDInsight 叢集的各種方式的資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="54ab0-103">刪除您的瀏覽器、 PowerShell 或 hello Azure CLI 所使用的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="54ab0-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="54ab0-104">一旦建立叢集，並停止刪除 hello 叢集時，就會開始 HDInsight 叢集計費。</span><span class="sxs-lookup"><span data-stu-id="54ab0-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="54ab0-105">計費是以每分鐘按比例計算，因此不再使用時，請一律刪除您的叢集。</span><span class="sxs-lookup"><span data-stu-id="54ab0-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="54ab0-106">在本文件中，您學會如何叢集使用 toodelete hello Azure 入口網站、 Azure PowerShell 和 hello Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="54ab0-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54ab0-107">刪除 HDInsight 叢集不會刪除 hello Azure 儲存體帳戶，或與 hello 叢集相關聯的資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="54ab0-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="54ab0-108">您可以重複使用這些服務，在未來的 hello 中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="54ab0-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="54ab0-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="54ab0-109">Azure portal</span></span>

1. <span data-ttu-id="54ab0-110">登入 toohello [Azure 入口網站](https://portal.azure.com)並選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="54ab0-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="54ab0-111">如果您的 HDInsight 叢集不是已釘選的 toohello 儀表板，您可以使用 hello 搜尋欄位來依據名稱搜尋它。</span><span class="sxs-lookup"><span data-stu-id="54ab0-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![入口網站搜尋](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="54ab0-113">一旦 hello 刀鋒視窗中開啟 hello 叢集時，請選取 hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="54ab0-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="54ab0-114">出現提示時，選取**是**toodelete hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="54ab0-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![刪除圖示](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="54ab0-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54ab0-116">Azure PowerShell</span></span>

<span data-ttu-id="54ab0-117">從 PowerShell 提示中，使用下列命令 toodelete hello 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="54ab0-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="54ab0-118">取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="54ab0-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="54ab0-119">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="54ab0-119">Azure CLI 1.0</span></span>

<span data-ttu-id="54ab0-120">在提示字元中使用下列 toodelete hello 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="54ab0-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="54ab0-121">取代**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="54ab0-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="54ab0-122">Azure CLI 2.0 目前不支援刪除 HDInsight 叢集 (2017 年 7 月 31 日)。</span><span class="sxs-lookup"><span data-stu-id="54ab0-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>