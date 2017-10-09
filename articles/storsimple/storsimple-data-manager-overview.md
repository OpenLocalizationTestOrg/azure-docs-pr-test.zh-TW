---
title: "aaaMicrosoft Azure StorSimple Data Manager 概觀 |Microsoft 文件"
description: "提供 hello StorSimple Data Manager 服務 （私人預覽中） 的概觀"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="b6c03-103">StorSimple Data Manager 概觀 (私人預覽)</span><span class="sxs-lookup"><span data-stu-id="b6c03-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="b6c03-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b6c03-104">Overview</span></span>

<span data-ttu-id="b6c03-105">Microsoft Azure StorSimple 是混合式雲端儲存體解決方案位址 hello 通常與檔案共用相關聯的非結構化資料的複雜性。</span><span class="sxs-lookup"><span data-stu-id="b6c03-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="b6c03-106">StorSimple 會使用雲端儲存體，當做 hello 的延伸模組在內部部署解決方案和自動層 hello 在內部部署儲存體和雲端存放裝置之間的資料。</span><span class="sxs-lookup"><span data-stu-id="b6c03-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="b6c03-107">整合資料保護與本機和雲端快照集，可以降低對 hello 正在擴張的儲存體基礎結構需求。</span><span class="sxs-lookup"><span data-stu-id="b6c03-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="b6c03-108">封存和災害復原也是無縫式與 hello 做為異地位置的雲端中。</span><span class="sxs-lookup"><span data-stu-id="b6c03-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="b6c03-109">我們在本文中導入的 hello 資料轉換服務可讓您 tooseamlessly 存取 hello StorSimple hello 雲端中的資料。</span><span class="sxs-lookup"><span data-stu-id="b6c03-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="b6c03-110">此服務從 StorSimple 提供 Api tooextract 資料，並加以呈現 tooother Azure 服務，可以輕易地取用的格式。</span><span class="sxs-lookup"><span data-stu-id="b6c03-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="b6c03-111">支援在這個預覽中的 hello 格式是 Azure blob 和 Azure Media Services 資產。</span><span class="sxs-lookup"><span data-stu-id="b6c03-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="b6c03-112">此轉換可讓您 tooeasily 網路服務，例如 Azure Media Services、 Azure HDInsight、 Azure Machine Learning 中，與 Azure 搜尋 toooperate 資料 StorSimple 8000 系列的內部部署裝置上。</span><span class="sxs-lookup"><span data-stu-id="b6c03-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="b6c03-113">相關的高階區塊圖如下所示。</span><span class="sxs-lookup"><span data-stu-id="b6c03-113">A high-level block diagram illustrating this is shown below.</span></span>

![高階圖表](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="b6c03-115">本文說明如何註冊此服務的私人預覽。</span><span class="sxs-lookup"><span data-stu-id="b6c03-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="b6c03-116">它也會說明如何使用這個 hello 雲端中使用 StorSimple 資料和其他 Azure 服務的服務 toowrite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6c03-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="b6c03-117">註冊資料管理員預覽</span><span class="sxs-lookup"><span data-stu-id="b6c03-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="b6c03-118">註冊 hello 資料管理員服務之前，請檢閱下列先決條件的 hello。</span><span class="sxs-lookup"><span data-stu-id="b6c03-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b6c03-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6c03-119">Prerequisites</span></span>

<span data-ttu-id="b6c03-120">本練習假設您有</span><span class="sxs-lookup"><span data-stu-id="b6c03-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="b6c03-121">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6c03-121">an active Azure subscription.</span></span>
* <span data-ttu-id="b6c03-122">存取 tooa 註冊 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="b6c03-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="b6c03-123">所有 hello 與 hello StorSimple 8000 系列裝置相關聯的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b6c03-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="b6c03-124">註冊</span><span class="sxs-lookup"><span data-stu-id="b6c03-124">Sign up</span></span>

<span data-ttu-id="b6c03-125">hello StorSimple Data Manager 是在私人預覽。</span><span class="sxs-lookup"><span data-stu-id="b6c03-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="b6c03-126">執行下列步驟 toosign 註冊此服務的私人預覽中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6c03-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="b6c03-127">以登入 hello Azure 入口網站在 hello StorSimple Data Manager 擴充功能： [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)。</span><span class="sxs-lookup"><span data-stu-id="b6c03-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="b6c03-128">使用您的 Azure 認證 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="b6c03-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="b6c03-129">按一下 hello  **+** 圖示 toocreate 服務。</span><span class="sxs-lookup"><span data-stu-id="b6c03-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="b6c03-130">按一下**儲存體**，然後按一下**看到所有**在 hello 刀鋒視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="b6c03-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![搜尋 StorSimple Data Manager 圖示](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="b6c03-132">您會看到 hello StorSimple 資料管理員圖示。</span><span class="sxs-lookup"><span data-stu-id="b6c03-132">You see hello StorSimple Data Manager icon.</span></span>

    ![選取 StorSimple Data Manager 圖示](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="b6c03-134">按一下 StorSimple Data Manager 圖示，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="b6c03-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="b6c03-135">選取您想 tooenable hello private preview 中，然後按一下 hello 訂閱**我要註冊 ！**</span><span class="sxs-lookup"><span data-stu-id="b6c03-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![我要註冊](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="b6c03-137">這會將要求 tooonboard 您。</span><span class="sxs-lookup"><span data-stu-id="b6c03-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="b6c03-138">我們會儘速讓您加入。</span><span class="sxs-lookup"><span data-stu-id="b6c03-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="b6c03-139">在您的訂用帳戶啟用後，您就可以建立 StorSimple Data Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="b6c03-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="b6c03-140">tooeasily 存取 hello StorSimple Data Manager 服務，請按一下 hello 星狀圖示 toopin 它 tooyour 我的最愛。</span><span class="sxs-lookup"><span data-stu-id="b6c03-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![存取 StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="b6c03-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6c03-142">Next steps</span></span>

<span data-ttu-id="b6c03-143">[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c03-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
