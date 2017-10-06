---
title: "aaaPublish Spring 開機應用程式以使用 Docker 容器 hello Azure Toolkit for Eclipse |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="814dd-103">Docker 容器發行 Spring 開機應用程式使用 hello Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="814dd-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="814dd-104">hello [Spring 架構]是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="814dd-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="814dd-105">其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，可提供簡單的方法建立獨立的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="814dd-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="814dd-106">[Docker]是開放原始碼解決方案，可協助開發人員自動化 hello 部署、 調整及管理其容器中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="814dd-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="814dd-107">本教學課程中引導您完成 hello 步驟 toodeploy Spring 開機應用程式，Azure Docker 容器 tooMicrosoft 為使用 hello Azure Toolkit for Eclipse。</span><span class="sxs-lookup"><span data-stu-id="814dd-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="814dd-108">複製 hello 預設 Spring 開機 Docker 儲存機制</span><span class="sxs-lookup"><span data-stu-id="814dd-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="814dd-109">匯入 hello 公用儲存機制</span><span class="sxs-lookup"><span data-stu-id="814dd-109">Import hello public repository</span></span>

<span data-ttu-id="814dd-110">hello 下列步驟引導您完成使用 IntelliJ 複製 hello Spring 開機 Docker 儲存機制 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="814dd-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="814dd-111">如果您想 toouse 命令列，請參閱[部署 Spring 開機應用程式在 Azure 容器服務中的 Linux 上][Deploy Spring Boot on Linux in ACS]。</span><span class="sxs-lookup"><span data-stu-id="814dd-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="814dd-112">開啟 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="814dd-112">Open Eclipse.</span></span>

1. <span data-ttu-id="814dd-113">按一下 [檔案] > [匯入]。</span><span class="sxs-lookup"><span data-stu-id="814dd-113">Click **File** > **Import**.</span></span>

   ![檔案匯入功能表][CL01]

1. <span data-ttu-id="814dd-115">當 hello**匯入**對話方塊隨即開啟：</span><span class="sxs-lookup"><span data-stu-id="814dd-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="814dd-116">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-116">a.</span></span> <span data-ttu-id="814dd-117">展開 [Git]。</span><span class="sxs-lookup"><span data-stu-id="814dd-117">Expand **Git**.</span></span>

   <span data-ttu-id="814dd-118">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-118">b.</span></span> <span data-ttu-id="814dd-119">選取 [Projects from Git] (Git 中的專案)。</span><span class="sxs-lookup"><span data-stu-id="814dd-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="814dd-120">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-120">c.</span></span> <span data-ttu-id="814dd-121">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-121">Click **Next**.</span></span>

   ![匯入對話方塊][CL02]

1. <span data-ttu-id="814dd-123">在 hello**選取儲存機制來源**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="814dd-124">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-124">a.</span></span> <span data-ttu-id="814dd-125">選取 [Clone URI] (複製 URI)。</span><span class="sxs-lookup"><span data-stu-id="814dd-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="814dd-126">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-126">b.</span></span> <span data-ttu-id="814dd-127">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-127">Click **Next**.</span></span>

   ![[選取存放庫來源] 頁面][CL03]

1. <span data-ttu-id="814dd-129">在 hello**來源 Git 儲存機制**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="814dd-130">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-130">a.</span></span> <span data-ttu-id="814dd-131">針對 [URI]，輸入 `https://github.com/spring-guides/gs-spring-boot-docker.git`。</span><span class="sxs-lookup"><span data-stu-id="814dd-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="814dd-132">此步驟應該自動填入 hello**主機**和**儲存機制路徑**hello 欄位更正的值。</span><span class="sxs-lookup"><span data-stu-id="814dd-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="814dd-133">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-133">b.</span></span> <span data-ttu-id="814dd-134">讓您的 Git 使用者名稱和密碼，您應該不需要 tooenter，是公用的 hello Spring 開機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="814dd-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="814dd-135">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-135">c.</span></span> <span data-ttu-id="814dd-136">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-136">Click **Next**.</span></span>

   ![[來源 Git 存放庫] 頁面][CL04]

1. <span data-ttu-id="814dd-138">在 hello**分支選取**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="814dd-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![[分支選擇] 頁面][CL05]

1. <span data-ttu-id="814dd-140">在 hello**本機目的地**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="814dd-141">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-141">a.</span></span> <span data-ttu-id="814dd-142">指定您想要您的本機儲存機制的 hello 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="814dd-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="814dd-143">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-143">b.</span></span> <span data-ttu-id="814dd-144">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-144">Click **Next**.</span></span>

   ![[本機目的地] 頁面][CL06]

1. <span data-ttu-id="814dd-146">在 hello**選取匯入專案精靈 toouse**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="814dd-147">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-147">a.</span></span> <span data-ttu-id="814dd-148">選取 [Import as a general project] (匯入為一般專案)。</span><span class="sxs-lookup"><span data-stu-id="814dd-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="814dd-149">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="814dd-149">b.</span></span> <span data-ttu-id="814dd-150">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-150">Click **Next**.</span></span>

   ![[選擇匯入專案精靈 toouse] 頁面][CL07]

1. <span data-ttu-id="814dd-152">在 hello**匯入專案**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="814dd-153">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-153">a.</span></span> <span data-ttu-id="814dd-154">指定專案名稱。</span><span class="sxs-lookup"><span data-stu-id="814dd-154">Specify your project name.</span></span>
   
   <span data-ttu-id="814dd-155">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-155">b.</span></span> <span data-ttu-id="814dd-156">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-156">Click **Finish**.</span></span>

   ![[匯入專案] 頁面][CL08]

1. <span data-ttu-id="814dd-158">當 hello 儲存機制成功複製時，您會看到在 Eclipse 中列出的所有 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="814dd-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Local repository (本機存放庫)][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="814dd-160">從本機存放庫建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="814dd-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="814dd-161">hello Spring 開機 Docker 儲存機制包含將用於此教學課程已完成的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="814dd-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="814dd-162">按一下 [檔案] > [匯入]。</span><span class="sxs-lookup"><span data-stu-id="814dd-162">Click **File** > **Import**.</span></span>

   ![匯入 hello 檔案 功能表上的命令][CL01]

1. <span data-ttu-id="814dd-164">當 hello**匯入**對話方塊隨即開啟：</span><span class="sxs-lookup"><span data-stu-id="814dd-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="814dd-165">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-165">a.</span></span> <span data-ttu-id="814dd-166">展開 [Maven]。</span><span class="sxs-lookup"><span data-stu-id="814dd-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="814dd-167">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-167">b.</span></span> <span data-ttu-id="814dd-168">選取 [Existing Maven Projects] (現有 Maven 專案)。</span><span class="sxs-lookup"><span data-stu-id="814dd-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="814dd-169">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-169">c.</span></span> <span data-ttu-id="814dd-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-170">Click **Next**.</span></span>

   ![匯入對話方塊][MV01]

1. <span data-ttu-id="814dd-172">在 hello **Maven 專案**頁面：</span><span class="sxs-lookup"><span data-stu-id="814dd-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="814dd-173">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-173">a.</span></span> <span data-ttu-id="814dd-174">如**根目錄**，指定 hello**完成**本機儲存機制中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="814dd-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="814dd-175">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-175">b.</span></span> <span data-ttu-id="814dd-176">展開 hello**進階**區段，然後輸入的自訂名稱**名稱範本**。</span><span class="sxs-lookup"><span data-stu-id="814dd-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="814dd-177">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-177">c.</span></span> <span data-ttu-id="814dd-178">選取 hello 方塊 hello **pom.xml** hello 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="814dd-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="814dd-179">d.</span><span class="sxs-lookup"><span data-stu-id="814dd-179">d.</span></span> <span data-ttu-id="814dd-180">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-180">Click **Finish**.</span></span>

   ![[Maven 專案] 頁面][MV02]

1. <span data-ttu-id="814dd-182">已成功開啟 hello Maven 專案時，您會看到在 Eclipse 中列出的第二個專案。</span><span class="sxs-lookup"><span data-stu-id="814dd-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Local Maven project (本機 Maven 專案)][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="814dd-184">使用 Maven 建置 Spring Boot 應用程式</span><span class="sxs-lookup"><span data-stu-id="814dd-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="814dd-185">在 [hello Eclipse 的專案總管] 中，選取 hello Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="814dd-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="814dd-186">按一下 [執行] > [執行身分] > [Maven 組建]。</span><span class="sxs-lookup"><span data-stu-id="814dd-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![命令 toorun 為 Maven 建置][BU01]

1. <span data-ttu-id="814dd-188">當您的應用程式建置成功時，hello 主控台視窗會顯示 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="814dd-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Successful Maven build (成功的 Maven 組建)][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="814dd-190">使用 Docker 容器發行您的 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="814dd-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="814dd-191">在 [hello Eclipse 的專案總管] 中，選取 hello Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="814dd-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="814dd-192">按一下 hello Azure**發行**功能表，然後再按一下**發佈為 Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="814dd-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![[發佈為 Docker 容器] 命令][PU01]

1. <span data-ttu-id="814dd-194">當 hello**在 Azure 上部署 Docker 容器** 對話方塊隨即出現：</span><span class="sxs-lookup"><span data-stu-id="814dd-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="814dd-195">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-195">a.</span></span> <span data-ttu-id="814dd-196">輸入自訂 Docker 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="814dd-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="814dd-197">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-197">b.</span></span> <span data-ttu-id="814dd-198">如**成品 toodeploy**，指定 hello 路徑 toohello **gs-spring-開機-docker-0.1.0.jar**您剛才建置的檔案。</span><span class="sxs-lookup"><span data-stu-id="814dd-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Specify Docker options (指定 Docker 選項)][PU02]

   <span data-ttu-id="814dd-200">顯示任何現有的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="814dd-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="814dd-201">如果您選擇 toodeploy tooan 現有主機，您可以略過 toostep 5。</span><span class="sxs-lookup"><span data-stu-id="814dd-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="814dd-202">否則，請使用下列步驟 toocreate 主機 hello:</span><span class="sxs-lookup"><span data-stu-id="814dd-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="814dd-203">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-203">a.</span></span> <span data-ttu-id="814dd-204">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="814dd-204">Click **Add**.</span></span>

      ![新增 Docker 主機][PU03]

   <span data-ttu-id="814dd-206">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-206">b.</span></span> <span data-ttu-id="814dd-207">當 hello**建立 Docker 主機** 對話方塊隨即出現，您可以選擇 tooaccept hello 預設值，或者您可以指定新的 Docker 主機的任何自訂設定。</span><span class="sxs-lookup"><span data-stu-id="814dd-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="814dd-208">(如需詳細說明 hello 的各種設定，請參閱[為 Docker 容器發行 web 應用程式，使用 IntelliJ hello Azure Toolkit][Publish Container with Azure Toolkit]。)按一下**下一步**當您指定哪些設定 toouse。</span><span class="sxs-lookup"><span data-stu-id="814dd-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![指定 Docker 主機選項][PU04]

   <span data-ttu-id="814dd-210">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-210">c.</span></span> <span data-ttu-id="814dd-211">您可以從 Azure 金鑰保存庫選擇 toouse 現有登入認證，或者您可以選擇 tooenter 新 Docker 登入認證。</span><span class="sxs-lookup"><span data-stu-id="814dd-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="814dd-212">當您已指定選項時，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="814dd-212">Click **Finish** when you have specified your options.</span></span>

      ![指定 Docker 主機認證][PU05]

1. <span data-ttu-id="814dd-214">選取您的 Docker 主機，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="814dd-214">Select your Docker host, and then click **Next**.</span></span>

   ![選取 Docker 主機 toouse][PU06]

1. <span data-ttu-id="814dd-216">Hello hello 最後一頁上**在 Azure 上部署 Docker 容器**對話方塊方塊中，指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="814dd-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="814dd-217">a.</span><span class="sxs-lookup"><span data-stu-id="814dd-217">a.</span></span> <span data-ttu-id="814dd-218">您可以選擇 toospecify hello 容器，將會裝載您的 Docker 容器的自訂名稱，或者您可以接受 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="814dd-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="814dd-219">b.</span><span class="sxs-lookup"><span data-stu-id="814dd-219">b.</span></span> <span data-ttu-id="814dd-220">使用下列語法的 hello docker 主機輸入 hello TCP 連接埠： *[外部連接埠]*:*[內部連接埠]*。</span><span class="sxs-lookup"><span data-stu-id="814dd-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="814dd-221">例如， **80:8080**指定外部連接埠 80 與 hello 預設 Spring 開機的內部連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="814dd-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="814dd-222">如果您已自訂您的內部連接埠 （例如，藉由編輯 hello application.yml 檔案），您需要 toospecify hello 連接埠號碼 hello 正確路由的 toooccur 在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="814dd-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="814dd-223">c.</span><span class="sxs-lookup"><span data-stu-id="814dd-223">c.</span></span> <span data-ttu-id="814dd-224">設定這些選項之後，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="814dd-224">After you configure these options, click **Finish**.</span></span>

   ![在 Azure 上部署 Docker 容器][PU07]

1. <span data-ttu-id="814dd-226">當 hello Azure Toolkit 完成發行時，hello Azure 活動記錄檔顯示**發佈**hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="814dd-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![已成功部署 Docker 主機][PU08]

## <a name="next-steps"></a><span data-ttu-id="814dd-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="814dd-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
