---
title: "使用 Visual Studio Online 連續傳遞雲端服務 | Microsoft Docs"
description: "了解如何設定連續傳遞 Azure 雲端應用程式，而不需將診斷儲存體金鑰儲存至服務組態檔"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="874ce-103">使用 Visual Studio Online 安全地儲存雲端服務診斷儲存體金鑰及設定連續整合和部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="874ce-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="874ce-104">這是現今開放原始碼專案的常見作法。</span><span class="sxs-lookup"><span data-stu-id="874ce-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="874ce-105">在組態檔中儲存應用程式密碼不再是安全的作法，因為從公用原始檔控制外洩的密碼會暴露安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="874ce-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="874ce-106">在連續整合管線的檔案中將密碼儲存為純文字並不安全，因為組建伺服器可能是雲端環境上的共用資源。</span><span class="sxs-lookup"><span data-stu-id="874ce-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="874ce-107">本文說明如何 Visual Studio 和 Visual Studio Online 降低開發和連續整合程序期間的安全性考量。</span><span class="sxs-lookup"><span data-stu-id="874ce-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="874ce-108">移除專案組態檔中的診斷儲存體金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="874ce-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="874ce-109">雲端服務診斷擴充功能需要 Azure 儲存體來儲存診斷結果。</span><span class="sxs-lookup"><span data-stu-id="874ce-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="874ce-110">儲存體連接字串先前指定於雲端服務組態 (.cscfg) 檔中，無法簽入原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="874ce-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="874ce-111">在最新的 Azure SDK 版本中，我們將行為變更為只以權杖所取代的金鑰來儲存部分連接字串。</span><span class="sxs-lookup"><span data-stu-id="874ce-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="874ce-112">下列步驟說明新雲端服務工具的運作方式︰</span><span class="sxs-lookup"><span data-stu-id="874ce-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="874ce-113">1.開啟角色設計工具</span><span class="sxs-lookup"><span data-stu-id="874ce-113">1. Open the Role designer</span></span>
* <span data-ttu-id="874ce-114">在雲端服務角色上連按兩下或按一下滑鼠右鍵，以開啟角色設計工具</span><span class="sxs-lookup"><span data-stu-id="874ce-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![開啟角色設計工具][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="874ce-116">2.[診斷] 區段下會新增 [不要從專案移除儲存體金鑰密碼] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="874ce-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="874ce-117">如果您使用本機儲存體模擬器，此核取方塊會停用，因為本機連接字串 (UseDevelopmentStorage = true) 沒有要管理的密碼。</span><span class="sxs-lookup"><span data-stu-id="874ce-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![本機儲存體模擬器連接字串並不是密碼][1]

* <span data-ttu-id="874ce-119">如果您要建立新專案，依預設不會選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="874ce-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="874ce-120">這會導致所選儲存體連接字串的儲存體金鑰部分被權杖取代。</span><span class="sxs-lookup"><span data-stu-id="874ce-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="874ce-121">在目前使用者的 AppData Roaming 資料夾下可找到權杖的值，例如︰C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="874ce-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="874ce-122">請注意，user\AppData 資料夾是依使用者登入控制存取權，被視為儲存開發機密的安全位置。</span><span class="sxs-lookup"><span data-stu-id="874ce-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![儲存體金鑰會儲存在使用者設定檔資料夾下][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="874ce-124">3.選取診斷儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="874ce-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="874ce-125">按一下 [...] 按鈕啟動的對話方塊，選取儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="874ce-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="874ce-126">帳戶。</span><span class="sxs-lookup"><span data-stu-id="874ce-126">button.</span></span> <span data-ttu-id="874ce-127">請注意，產生的儲存體連接字串不會有儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="874ce-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="874ce-128">例如︰DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="874ce-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="874ce-129">4.  進行專案偵錯</span><span class="sxs-lookup"><span data-stu-id="874ce-129">4.    Debugging the project</span></span>
* <span data-ttu-id="874ce-130">F5 可在 Visual Studio 中進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="874ce-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="874ce-131">所有項目的運作方式都應該如同以往。</span><span class="sxs-lookup"><span data-stu-id="874ce-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="874ce-132">![在本機開始偵錯][3]</span><span class="sxs-lookup"><span data-stu-id="874ce-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="874ce-133">5.從 Visual Studio 發佈專案</span><span class="sxs-lookup"><span data-stu-id="874ce-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="874ce-134">啟動 [發佈] 對話方塊並繼續執行登入指示，以將應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="874ce-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="874ce-135">6.其他資訊</span><span class="sxs-lookup"><span data-stu-id="874ce-135">6. Additional information</span></span>
> <span data-ttu-id="874ce-136">注意︰角色設計工具中的 [設定] 面板會保持原狀。</span><span class="sxs-lookup"><span data-stu-id="874ce-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="874ce-137">如果您想要使用密碼管理功能進行診斷，請移至 [組態] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="874ce-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![新增設定][4]

> <span data-ttu-id="874ce-139">附註︰若已啟用，Application Insights 金鑰會儲存為純文字。</span><span class="sxs-lookup"><span data-stu-id="874ce-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="874ce-140">此金鑰只用於上傳內容，所以沒有任何敏感性資料會有遭到入侵的風險。</span><span class="sxs-lookup"><span data-stu-id="874ce-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="874ce-141">使用 Visual Studio Online 工作範本來建置及發佈雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="874ce-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="874ce-142">下列步驟說明如何使用 Visual Studio Online 工作來設定雲端服務專案的持續整合︰</span><span class="sxs-lookup"><span data-stu-id="874ce-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="874ce-143">1.  取得 VSO 帳戶</span><span class="sxs-lookup"><span data-stu-id="874ce-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="874ce-144">[建立 Visual Studio Online 帳戶][ Create Visual Studio Online account]如果您還沒有任何</span><span class="sxs-lookup"><span data-stu-id="874ce-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="874ce-145">[建立 team 專案][ Create team project]在您的 Visual Studio online 帳戶</span><span class="sxs-lookup"><span data-stu-id="874ce-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="874ce-146">2.  在 Visual Studio 中設定原始檔控制</span><span class="sxs-lookup"><span data-stu-id="874ce-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="874ce-147">連接到 Team 專案</span><span class="sxs-lookup"><span data-stu-id="874ce-147">Connect to a team project</span></span>

![連接到 Team 專案][5]

![選取要連接的 Team 專案][6]

* <span data-ttu-id="874ce-150">將專案新增至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="874ce-150">Add your project to source control</span></span>

![將專案新增至原始檔控制][7]

![將專案對應至原始檔控制資料夾][8]

* <span data-ttu-id="874ce-153">從 Team Explorer 簽入您的專案</span><span class="sxs-lookup"><span data-stu-id="874ce-153">Check in your project from Team Explorer</span></span>

![將專案簽入原始檔控制][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="874ce-155">3.  設定建置流程</span><span class="sxs-lookup"><span data-stu-id="874ce-155">3.    Configure Build process</span></span>
* <span data-ttu-id="874ce-156">瀏覽至您的 Team 專案並新增建置流程範本</span><span class="sxs-lookup"><span data-stu-id="874ce-156">Browse to your team project and add a new build process Templates</span></span>

![新增組建][10]

* <span data-ttu-id="874ce-158">選取建置工作</span><span class="sxs-lookup"><span data-stu-id="874ce-158">Select build task</span></span>

![新增建置工作][11]

![選取 Visual Studio 建置工作範本][12]

* <span data-ttu-id="874ce-161">編輯建置工作輸入。</span><span class="sxs-lookup"><span data-stu-id="874ce-161">Edit build task input.</span></span> <span data-ttu-id="874ce-162">請根據您的需求自訂組建參數</span><span class="sxs-lookup"><span data-stu-id="874ce-162">Please customize the build parameters according to your need</span></span>

![設定建置工作][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="874ce-164">設定組建變數</span><span class="sxs-lookup"><span data-stu-id="874ce-164">Configure build variables</span></span>

![設定組建變數][14]

* <span data-ttu-id="874ce-166">新增工作以上傳組建置放</span><span class="sxs-lookup"><span data-stu-id="874ce-166">Add a task to upload build drop</span></span>

![選擇發佈組建置放工作][15]

![設定發佈組建置放工作][16]

* <span data-ttu-id="874ce-169">執行組建</span><span class="sxs-lookup"><span data-stu-id="874ce-169">Run the build</span></span>

![將新組建排入佇列][17]

![檢視組建摘要][18]

* <span data-ttu-id="874ce-172">如果建置成功，您會看到類似以下的結果</span><span class="sxs-lookup"><span data-stu-id="874ce-172">if the build is successful you will see a result similar to below</span></span>

![建置結果][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="874ce-174">4.  設定發行程序</span><span class="sxs-lookup"><span data-stu-id="874ce-174">4.    Configure Release process</span></span>
* <span data-ttu-id="874ce-175">建立新版本</span><span class="sxs-lookup"><span data-stu-id="874ce-175">Create a new release</span></span>

![建立新版本][20]

* <span data-ttu-id="874ce-177">選取 Azure 雲端服務部署工作</span><span class="sxs-lookup"><span data-stu-id="874ce-177">Select the Azure Cloud Services Deployment task</span></span>

![選取 Azure 雲端服務部署工作][21]

* <span data-ttu-id="874ce-179">因為儲存體帳戶金鑰並未簽入原始檔控制，所以我們需要指定秘密金鑰以便設定診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="874ce-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="874ce-180">展開 [建立新服務的進階選項] 區段，然後編輯 [診斷儲存體帳戶金鑰] 參數輸入。</span><span class="sxs-lookup"><span data-stu-id="874ce-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="874ce-181">此輸入接受多行的金鑰值組，其格式為 **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="874ce-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="874ce-182">注意︰如果您的診斷儲存體帳戶是在您要發佈雲端服務應用程式的相同訂用帳戶之下，您不必在部署工作中輸入金鑰；部署將以程式設計方式從您的訂用帳戶取得儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="874ce-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![設定雲端服務部署工作][22]

* <span data-ttu-id="874ce-184">使用密碼建置變數來儲存儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="874ce-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="874ce-185">若要變數遮掩為密碼，按一下變數輸入右邊的鎖定圖示</span><span class="sxs-lookup"><span data-stu-id="874ce-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![在密碼建置變數中儲存儲存體金鑰][23]

* <span data-ttu-id="874ce-187">建立版本並將專案部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="874ce-187">Create a release and deploy your project to Azure</span></span>

![建立新版本][24]

## <a name="next-steps"></a><span data-ttu-id="874ce-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="874ce-189">Next steps</span></span>
<span data-ttu-id="874ce-190">若要深入了解設定 Azure 雲端服務的診斷延伸模組，請參閱[使用 PowerShell 的 Azure 雲端服務中啟用診斷][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="874ce-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
