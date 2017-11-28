---
title: "Service Fabric plug-in for Eclipse aaaAzure |Microsoft 文件"
description: "開始使用 Service Fabric 外掛程式 hello for Eclipse。"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="f5f0c-103">適用於 Eclipse Java 應用程式開發的 Service Fabric 外掛程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="f5f0c-104">Eclipse 是其中一個最常使用的 hello for Java 開發人員的整合式開發環境 (Ide)。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="f5f0c-105">在本文中，我們說明如何設定與 Azure Service Fabric 您 Eclipse 開發環境 toowork tooset。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="f5f0c-106">了解 tooinstall hello 外掛程式，Service Fabric 建立 Service Fabric 應用程式和部署 Service Fabric 應用程式 tooa 本機或遠端 Service Fabric 叢集在 Eclipse Neon 的方式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="f5f0c-107">安裝或更新 hello Service Fabric Eclipse Neon 外掛程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="f5f0c-108">您可以在 Eclipse 中安裝 Service Fabric 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="f5f0c-109">hello 外掛程式，可協助簡化建置和部署 Java 服務 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="f5f0c-110">請確定您擁有 hello 最新版本的 Eclipse Neon 和 hello 最新版 Buildship 安裝 （1.0.17 或更新版本）：</span><span class="sxs-lookup"><span data-stu-id="f5f0c-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="f5f0c-111">已安裝的元件，在 Eclipse Neon toocheck hello 版本太移**協助** > **安裝詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="f5f0c-112">tooupdate Buildship，請參閱[Eclipse Buildship: Eclipse 外掛程式 Gradle][buildship-update]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="f5f0c-113">如 toocheck 和安裝更新的 Eclipse Neon 移過**協助** > **檢查更新**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="f5f0c-114">tooinstall hello Service Fabric 外掛程式，請在 Eclipse Neon 跳過**協助** > **安裝新軟體**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="f5f0c-115">在 hello**搭配**方塊中，輸入**http://dl.microsoft.com/eclipse**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="f5f0c-116">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-116">Click **Add**.</span></span>

         ![適用於 Eclipse Neon 的 Service Fabric 外掛程式][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="f5f0c-118">選取 hello Service Fabric 外掛程式，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="f5f0c-119">完成 hello 安裝步驟，並接受 hello Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="f5f0c-120">如果您已經有 hello Service Fabric 外掛程式安裝，請確定您已擁有 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="f5f0c-121">可用的更新，toocheck 移過**協助** > **安裝詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="f5f0c-122">Hello 在清單中已安裝的外掛程式，請在選取 Service Fabric，，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="f5f0c-123">將安裝可用的更新。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="f5f0c-124">如果安裝或更新 hello Service Fabric 外掛程式緩慢時，它可能是因為 tooan Eclipse 設定。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="f5f0c-125">Eclipse 會收集的所有變更 tooupdate 站台會向您的 Eclipse 執行個體中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="f5f0c-126">toospeed hello 程序，檢查及安裝的 Service Fabric 外掛程式更新，跳過**可用軟體的站台**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="f5f0c-127">清除所有的站台，除了 hello 點 toohello Service Fabric 外掛程式的位置 (http://dl.microsoft.com/eclipse/azure/servicefabric) 的其中一個 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="f5f0c-128">在 Eclipse 中建立 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="f5f0c-129">在 Eclipse Neon 移過**檔案** > **新增** > **其他**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="f5f0c-130">選取 **Service Fabric 外掛程式**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric 新專案第 1 頁][create-application/p1]

2.  <span data-ttu-id="f5f0c-132">輸入專案的名稱，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric 新專案第 2 頁][create-application/p2]

3.  <span data-ttu-id="f5f0c-134">在 hello 範本清單中選取**服務範本**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="f5f0c-135">選取服務範本類型 (執行者、無狀態、容器或來賓二進位)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric 新專案第 3 頁][create-application/p3]

4.  <span data-ttu-id="f5f0c-137">輸入 hello 服務名稱和服務的詳細資訊，，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric 新專案第 4 頁][create-application/p4]

5. <span data-ttu-id="f5f0c-139">當您建立第一個 Service Fabric 專案，在 hello**開啟相關聯的檢視方塊**對話方塊中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric 新專案第 5 頁][create-application/p5]

6.  <span data-ttu-id="f5f0c-141">新的專案看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="f5f0c-141">Your new project looks like this:</span></span>

    ![Service Fabric 新專案第 6 頁][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="f5f0c-143">在 Eclipse 中建置和部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="f5f0c-144">以滑鼠右鍵按一下新的 Service Fabric 應用程式，然後選取 [Service Fabric]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric 快顯功能表][publish/RightClick]

2. <span data-ttu-id="f5f0c-146">在 hello 子功能表中，選取您想要的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="f5f0c-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="f5f0c-147">按一下 toobuild hello 應用程式，而不清除，**建置的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="f5f0c-148">toodo 乾淨的組建的 hello 應用程式中，按一下**重建應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="f5f0c-149">按一下 tooclean hello 應用程式的內建的成品，**全新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="f5f0c-150">您也可以從這個功能表選擇部署、解除部署和發佈應用程式：</span><span class="sxs-lookup"><span data-stu-id="f5f0c-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="f5f0c-151">toodeploy tooyour 本機叢集，按一下 **部署應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="f5f0c-152">在 hello**發行應用程式**對話方塊方塊中，選取 發行設定檔：</span><span class="sxs-lookup"><span data-stu-id="f5f0c-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="f5f0c-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="f5f0c-153">**Local.json**</span></span>
        -  <span data-ttu-id="f5f0c-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="f5f0c-154">**Cloud.json**</span></span>

     <span data-ttu-id="f5f0c-155">這些 JavaScript Object Notation (JSON) 檔案會儲存必要的 tooconnect tooyour 本機或雲端 (Azure) 叢集的資訊 （例如連接端點和安全性資訊）。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Service Fabric 發佈功能表][publish/Publish]

<span data-ttu-id="f5f0c-157">替代方式 toodeploy Service Fabric 執行應用程式使用 Eclipse 組態。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="f5f0c-158">跳過**執行** > **回合組態**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="f5f0c-159">在下**Gradle 專案**，選取 hello **ServiceFabricDeployer**執行設定。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="f5f0c-160">Hello 右窗格中，在 hello**引數**索引標籤上，針對**publishProfile**，選取**本機**或**雲端**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="f5f0c-161">hello 預設值是**本機**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-161">hello default is **local**.</span></span> <span data-ttu-id="f5f0c-162">遠端 toodeploy tooa 或選取的雲端叢集**雲端**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="f5f0c-163">tooensure hello 適當的資訊會在 hello 填入發行設定檔，請編輯**Local.json**或**Cloud.json**視。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="f5f0c-164">您可以新增或更新端點詳細資料和安全性認證。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="f5f0c-165">請確認**工作目錄**點想 toodeploy toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="f5f0c-166">toochange hello 應用程式中，按一下 hello**工作區**按鈕，然後再選取您想要的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="f5f0c-167">按一下 套用，然後按一下執行。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="f5f0c-168">幾分鐘內即可建置和部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="f5f0c-169">您可以監視 Service Fabric 總管中的 hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="f5f0c-170">新增 Service Fabric 服務 tooyour Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="f5f0c-171">tooadd Service Fabric 服務 tooan 現有 Service Fabric 應用程式，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="f5f0c-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="f5f0c-172">以滑鼠右鍵按一下您想要 tooadd 的服務，然後再按一下 hello 專案**Service Fabric**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric 新增服務第 1 頁][add-service/p1]

2.  <span data-ttu-id="f5f0c-174">按一下**新增 Service Fabric 服務**，並完成 hello 的步驟 tooadd 服務 toohello 專案設定。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="f5f0c-175">選取 hello 服務想要的範本 tooadd tooyour 專案，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Service Fabric 新增服務第 2 頁][add-service/p2]

4.  <span data-ttu-id="f5f0c-177">輸入 hello 服務名稱 （和其他詳細資料，視需要），然後按一下hello**加入服務** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Service Fabric 新增服務第 3 頁][add-service/p3]

5.  <span data-ttu-id="f5f0c-179">加入 hello 服務之後，您整體的專案結構看起來類似 toohello 下列專案：</span><span class="sxs-lookup"><span data-stu-id="f5f0c-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Service Fabric 新增服務第 4 頁][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="f5f0c-181">編輯 Service Fabric Java 應用程式的資訊清單版本</span><span class="sxs-lookup"><span data-stu-id="f5f0c-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="f5f0c-182">tooedit 資訊清單版本，hello 專案上按一下滑鼠右鍵，跳過**Service Fabric**選取**編輯資訊清單版本...**從 hello 功能表下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="f5f0c-183">在 hello 精靈中，您可以更新應用程式資訊清單，服務資訊清單的 hello 資訊清單版本和 hello 版本**程式碼**， **Config**和**資料**封裝。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="f5f0c-184">如果您核取 hello 選項**自動更新應用程式和服務版本**和更新版本，然後將會自動更新 hello 資訊清單版本。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="f5f0c-185">toogive 的範例，您先選取 hello 核取方塊，然後更新 hello 版本**程式碼**版本 0.0.0 too0.0.1 並按一下**完成**，然後服務資訊清單版本和應用程式資訊清單會自動更新的 too0.0.1 版本。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="f5f0c-186">升級 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="f5f0c-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="f5f0c-187">升級案例中，假設您建立 hello **App1** hello Service Fabric 外掛程式在 Eclipse 的專案。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="f5f0c-188">您使用部署 hello 外掛程式 toocreate 應用程式名為**fabric: / App1Application**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="f5f0c-189">hello 應用程式類型是**App1AppicationType**，和 hello 應用程式版本為 1.0。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="f5f0c-190">現在，您希望 tooupgrade 應用程式不會插斷可用性。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="f5f0c-191">首先，tooyour 應用程式中，進行任何變更，然後重新建立 hello 修改服務。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="f5f0c-192">更新 hello 修改服務的資訊清單檔案 (ServiceManifest.xml) 與 hello 服務 （和程式碼、 組態中，或為相關的資料） 的 hello 更新版本。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="f5f0c-193">此外，修改 hello 應用程式資訊清單 (ApplicationManifest.xml) 與更新的 hello hello 應用程式的版本號碼和 hello 已修改的服務。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="f5f0c-194">tooupgrade 使用 Eclipse Neon 應用程式，您可以建立重複的執行的組態設定檔。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="f5f0c-195">然後，使用 tooupgrade 視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="f5f0c-196">跳過**執行** > **回合組態**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="f5f0c-197">Hello 左窗格中，按一下 hello 的小箭號 toohello 左邊**Gradle 專案**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="f5f0c-198">以滑鼠右鍵按一下 **ServiceFabricDeployer**，然後選取 [重複]。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="f5f0c-199">輸入此設定的新名稱，例如，**ServiceFabricUpgrader**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="f5f0c-200">在 hello 右面板中，在 hello**引數**索引標籤上，變更**層 Pconfig = '部署'**太**層 Pconfig = '升級'**，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="f5f0c-201">此程序會建立並執行的組態設定檔會儲存您可以在任何時間 tooupgrade 使用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="f5f0c-202">它也會取得從 hello 應用程式資訊清單檔案的 hello 最新的更新的應用程式類型版本。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="f5f0c-203">hello 應用程式升級將會花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="f5f0c-204">您可以監視 Service Fabric 總管中的 hello 應用程式升級。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="f5f0c-205">移轉舊服務網狀架構 Java 應用程式 toobe 搭配 Maven 使用</span><span class="sxs-lookup"><span data-stu-id="f5f0c-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="f5f0c-206">我們最近已從 Service Fabric Java SDK tooMaven 儲存機制移服務網狀架構 Java 文件庫。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="f5f0c-207">雖然 hello 新應用程式，您可以產生使用 Eclipse 中，將會產生 （這會是可以與 Maven toowork） 最新版本更新的專案，您可以更新您現有的 Service Fabric 無狀態或執行者 Java 應用程式，而且已使用 hello Service Fabric Java SDK更早版本，toouse hello 服務網狀架構 Java 相依性從 Maven。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="f5f0c-208">請遵循所述的 hello 步驟[這裡](service-fabric-migrate-old-javaapp-to-use-maven.md)tooensure Maven 適用於較舊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5f0c-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
