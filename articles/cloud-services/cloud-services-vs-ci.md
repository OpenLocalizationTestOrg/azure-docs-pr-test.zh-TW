---
title: "aaaContinuous 傳遞的雲端服務，無需使用 Visual Studio Online |Microsoft 文件"
description: "深入了解如何 tooset 總持續傳遞 azure 的雲端應用程式而不儲存診斷儲存體金鑰 toohello 服務組態檔"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="16cad-103">Securely 儲存雲端服務診斷儲存體金鑰和設定連續整合及部署使用 Visual Studio Online 的 tooAzure</span><span class="sxs-lookup"><span data-stu-id="16cad-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="16cad-104">Screen 鍵是常見的作法 tooopen 來源專案。</span><span class="sxs-lookup"><span data-stu-id="16cad-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="16cad-105">在組態檔中儲存應用程式密碼不再是安全的作法，因為從公用原始檔控制外洩的密碼會暴露安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="16cad-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="16cad-106">可能因為組建伺服器可能是因為不安全的檔案中的連續整合管線的純文字儲存密碼共用 hello 雲端環境上的資源。</span><span class="sxs-lookup"><span data-stu-id="16cad-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="16cad-107">本文說明 Visual Studio 和 Visual Studio Online 降低的方式 hello 安全性考量開發和持續整合程序期間。</span><span class="sxs-lookup"><span data-stu-id="16cad-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="16cad-108">移除專案組態檔中的診斷儲存體金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="16cad-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="16cad-109">雲端服務診斷擴充功能需要 Azure 儲存體來儲存診斷結果。</span><span class="sxs-lookup"><span data-stu-id="16cad-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="16cad-110">先前稱為 hello 儲存體連接字串 hello 雲端服務組態 (.cscfg) 檔中會指定，且無法檢查 toosource 控制項中。</span><span class="sxs-lookup"><span data-stu-id="16cad-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="16cad-111">Hello 最新的 Azure SDK 版本中，我們變更 hello 行為 tooonly 存放區部分連接字串 hello 金鑰語彙基元所取代。</span><span class="sxs-lookup"><span data-stu-id="16cad-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="16cad-112">hello 下列步驟說明 hello 新雲端服務工具的運作方式：</span><span class="sxs-lookup"><span data-stu-id="16cad-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="16cad-113">1.開啟 hello 角色設計工具</span><span class="sxs-lookup"><span data-stu-id="16cad-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="16cad-114">按兩下或在雲端服務角色 tooopen 角色設計工具上以滑鼠右鍵按一下</span><span class="sxs-lookup"><span data-stu-id="16cad-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![開啟角色設計工具][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="16cad-116">2.[診斷] 區段下會新增 [不要從專案移除儲存體金鑰密碼] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="16cad-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="16cad-117">如果您使用 hello 本機儲存體模擬器，這個核取方塊會停用，因為沒有任何密碼 toomanage hello 本機連接字串，也就是 UseDevelopmentStorage = true。</span><span class="sxs-lookup"><span data-stu-id="16cad-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![本機儲存體模擬器連接字串並不是密碼][1]

* <span data-ttu-id="16cad-119">如果您要建立新專案，依預設不會選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="16cad-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="16cad-120">這會導致 hello 儲存體金鑰 > 一節的 hello 選取儲存體連接字串語彙基元所取代。</span><span class="sxs-lookup"><span data-stu-id="16cad-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="16cad-121">hello hello 語彙基元的值將資料夾下找到 hello 目前使用者的 AppData 漫遊，例如： C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="16cad-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="16cad-122">請注意該 hello user\AppData 資料夾為存取控制的使用者登入，並且會被視為安全的地方 toostore 開發機密資料。</span><span class="sxs-lookup"><span data-stu-id="16cad-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![儲存體金鑰會儲存在使用者設定檔資料夾下][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="16cad-124">3.選取診斷儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="16cad-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="16cad-125">Hello 對話方塊啟動"…"hello，即可從選取的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="16cad-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="16cad-126">按鈕。</span><span class="sxs-lookup"><span data-stu-id="16cad-126">button.</span></span> <span data-ttu-id="16cad-127">請注意如何產生 hello 儲存體連接字串不會 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="16cad-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="16cad-128">例如︰DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="16cad-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="16cad-129">4.  Hello 專案進行偵錯</span><span class="sxs-lookup"><span data-stu-id="16cad-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="16cad-130">在 Visual Studio 中偵錯 F5 toostart。</span><span class="sxs-lookup"><span data-stu-id="16cad-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="16cad-131">所有項目應該使用相同 hello 與之前的方式。</span><span class="sxs-lookup"><span data-stu-id="16cad-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="16cad-132">![在本機開始偵錯][3]</span><span class="sxs-lookup"><span data-stu-id="16cad-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="16cad-133">5.從 Visual Studio 發佈專案</span><span class="sxs-lookup"><span data-stu-id="16cad-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="16cad-134">啟動 hello 發行對話方塊，並繼續進行登入指示 toopublish hello applicaion tooAzure。</span><span class="sxs-lookup"><span data-stu-id="16cad-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="16cad-135">6.其他資訊</span><span class="sxs-lookup"><span data-stu-id="16cad-135">6. Additional information</span></span>
> <span data-ttu-id="16cad-136">注意： hello 角色設計工具中的 hello 設定面板會保持原狀現在。</span><span class="sxs-lookup"><span data-stu-id="16cad-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="16cad-137">如果您想要診斷 toouse hello 密碼管理功能，請移 toohello 組態 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="16cad-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![新增設定][4]

> <span data-ttu-id="16cad-139">注意： 如果啟用，hello Application Insights 金鑰會儲存為純文字。</span><span class="sxs-lookup"><span data-stu-id="16cad-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="16cad-140">hello 金鑰只會使用上傳內容，因此任何機密資料將不會受到危害的風險。</span><span class="sxs-lookup"><span data-stu-id="16cad-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="16cad-141">使用 Visual Studio Online 工作範本來建置及發佈雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="16cad-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="16cad-142">hello 下列步驟說明如何 toosetup 連續整合的雲端服務專案使用 Visual Studio online 工作：</span><span class="sxs-lookup"><span data-stu-id="16cad-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="16cad-143">1.  取得 VSO 帳戶</span><span class="sxs-lookup"><span data-stu-id="16cad-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="16cad-144">[建立 Visual Studio Online 帳戶][ Create Visual Studio Online account]如果您還沒有任何</span><span class="sxs-lookup"><span data-stu-id="16cad-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="16cad-145">[建立 team 專案][ Create team project]在您的 Visual Studio online 帳戶</span><span class="sxs-lookup"><span data-stu-id="16cad-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="16cad-146">2.  在 Visual Studio 中設定原始檔控制</span><span class="sxs-lookup"><span data-stu-id="16cad-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="16cad-147">連接 tooa team 專案</span><span class="sxs-lookup"><span data-stu-id="16cad-147">Connect tooa team project</span></span>

![Tooteam 專案連接][5]

![若要選取的 team 專案 tooconnect][6]

* <span data-ttu-id="16cad-150">加入您專案的 toosource 控制項</span><span class="sxs-lookup"><span data-stu-id="16cad-150">Add your project toosource control</span></span>

![將專案 toosource 控制項][7]

![對應專案 tooa 原始檔控制資料夾][8]

* <span data-ttu-id="16cad-153">從 Team Explorer 簽入您的專案</span><span class="sxs-lookup"><span data-stu-id="16cad-153">Check in your project from Team Explorer</span></span>

![簽入 toosource 控制專案][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="16cad-155">3.  設定建置流程</span><span class="sxs-lookup"><span data-stu-id="16cad-155">3.    Configure Build process</span></span>
* <span data-ttu-id="16cad-156">瀏覽 tooyour team 專案並加入新的建置流程範本</span><span class="sxs-lookup"><span data-stu-id="16cad-156">Browse tooyour team project and add a new build process Templates</span></span>

![新增組建][10]

* <span data-ttu-id="16cad-158">選取建置工作</span><span class="sxs-lookup"><span data-stu-id="16cad-158">Select build task</span></span>

![新增建置工作][11]

![選取 Visual Studio 建置工作範本][12]

* <span data-ttu-id="16cad-161">編輯建置工作輸入。</span><span class="sxs-lookup"><span data-stu-id="16cad-161">Edit build task input.</span></span> <span data-ttu-id="16cad-162">請自訂 hello 組建必須根據 tooyour 參數</span><span class="sxs-lookup"><span data-stu-id="16cad-162">Please customize hello build parameters according tooyour need</span></span>

![設定建置工作][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="16cad-164">設定組建變數</span><span class="sxs-lookup"><span data-stu-id="16cad-164">Configure build variables</span></span>

![設定組建變數][14]

* <span data-ttu-id="16cad-166">新增工作 tooupload 組建置放</span><span class="sxs-lookup"><span data-stu-id="16cad-166">Add a task tooupload build drop</span></span>

![選擇發佈組建置放工作][15]

![設定發佈組建置放工作][16]

* <span data-ttu-id="16cad-169">執行 hello 組建</span><span class="sxs-lookup"><span data-stu-id="16cad-169">Run hello build</span></span>

![將新組建排入佇列][17]

![檢視組建摘要][18]

* <span data-ttu-id="16cad-172">hello 建置成功時，您會看到結果類似 toobelow</span><span class="sxs-lookup"><span data-stu-id="16cad-172">if hello build is successful you will see a result similar toobelow</span></span>

![建置結果][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="16cad-174">4.  設定發行程序</span><span class="sxs-lookup"><span data-stu-id="16cad-174">4.    Configure Release process</span></span>
* <span data-ttu-id="16cad-175">建立新版本</span><span class="sxs-lookup"><span data-stu-id="16cad-175">Create a new release</span></span>

![建立新版本][20]

* <span data-ttu-id="16cad-177">選取 hello Azure 雲端服務部署工作</span><span class="sxs-lookup"><span data-stu-id="16cad-177">Select hello Azure Cloud Services Deployment task</span></span>

![選取 Azure 雲端服務部署工作][21]

* <span data-ttu-id="16cad-179">Hello 儲存體帳戶金鑰不會檢查 toosource 控制項中，我們需要 toospecify hello 祕密金鑰設定診斷延伸。</span><span class="sxs-lookup"><span data-stu-id="16cad-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="16cad-180">展開 hello**建立新服務的進階選項**區段，並編輯 hello**診斷儲存體帳戶金鑰**參數的輸入。</span><span class="sxs-lookup"><span data-stu-id="16cad-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="16cad-181">在多行程式中的 hello 格式的機碼值組會採用此輸入**[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="16cad-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="16cad-182">附註： 如果您的診斷儲存體帳戶是在 hello 與您要在其中發行 hello 雲端服務應用程式相同的訂閱，您不需要 tooenter hello 金鑰 hello 部署工作輸入; 中hello 部署就會從您的訂用帳戶以程式設計方式取得 hello 儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="16cad-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![設定雲端服務部署工作][22]

* <span data-ttu-id="16cad-184">使用密碼建立變數 toosave 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="16cad-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="16cad-185">按一下右邊 hello hello hello 鎖定圖示的 做為密碼變數 toomask 變數輸入</span><span class="sxs-lookup"><span data-stu-id="16cad-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![在密碼建置變數中儲存儲存體金鑰][23]

* <span data-ttu-id="16cad-187">建立發行和部署專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="16cad-187">Create a release and deploy your project tooAzure</span></span>

![建立新版本][24]

## <a name="next-steps"></a><span data-ttu-id="16cad-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16cad-189">Next steps</span></span>
<span data-ttu-id="16cad-190">toolearn 進一步了解 Azure 雲端服務，設定診斷延伸模組，請參閱[使用 PowerShell 的 Azure 雲端服務中啟用診斷][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="16cad-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
