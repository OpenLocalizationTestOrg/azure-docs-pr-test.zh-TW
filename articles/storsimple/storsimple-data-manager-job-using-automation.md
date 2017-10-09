---
title: "aaaUse Azure 自動化 tootrigger 作業 |Microsoft 文件"
description: "深入了解如何 toouse Azure 自動化觸發 StorSimple Data Manager 作業 （私人預覽中）"
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="fd8d1-103">使用 Azure 自動化 tootrigger 作業 （私人預覽中）</span><span class="sxs-lookup"><span data-stu-id="fd8d1-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="fd8d1-104">此文章說明如何 toouse Azure 自動化 tootrigger StorSimple Data Manager 工作。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd8d1-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="fd8d1-105">Prerequisites</span></span>

<span data-ttu-id="fd8d1-106">開始之前，請確定您有︰</span><span class="sxs-lookup"><span data-stu-id="fd8d1-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="fd8d1-107">已安裝 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-107">Azure Powershell installed.</span></span> <span data-ttu-id="fd8d1-108">[下載 Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="fd8d1-109">組態設定 tooinitialize hello 資料轉換工作 （tooobtain 這些設定會包含在此處的指示）。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="fd8d1-110">已在資源群組內的混合式資料資源中正確設定的工作定義。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="fd8d1-111">下載`DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github 儲存機制中的檔案。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="fd8d1-112">下載`Get-ConfigurationParams.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1)hello github 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="fd8d1-113">下載`Trigger-DataTransformation-Job.ps1`[指令碼](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1)hello github 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="fd8d1-114">逐步說明</span><span class="sxs-lookup"><span data-stu-id="fd8d1-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="fd8d1-115">取得 Azure Active Directory hello 自動化工作 toorun hello 作業定義的權限</span><span class="sxs-lookup"><span data-stu-id="fd8d1-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="fd8d1-116">tooretrieve hello 組態參數，如 Active Directory 中，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="fd8d1-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="fd8d1-117">在本機電腦中開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="fd8d1-118">確認 [Azure PowerShell](https://azure.microsoft.com/downloads/) 已安裝。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="fd8d1-119">執行 hello `Get-ConfigurationParams.ps1` （在您下載上方 hello 資料夾） 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="fd8d1-120">輸入下列命令在 hello PowerShell 視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd8d1-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="fd8d1-121">hello ActiveDirectoryKey 是您稍後使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="fd8d1-122">輸入您選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-122">Enter a password of your choice.</span></span> <span data-ttu-id="fd8d1-123">AppName 可以是任何字串。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-123">AppName can be any string.</span></span>

2. <span data-ttu-id="fd8d1-124">此指令碼輸出 hello 觸發 hello 自動化 runbook 時，應該使用的值。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="fd8d1-125">記下這些值。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-125">Make a note of these values.</span></span>

    - <span data-ttu-id="fd8d1-126">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="fd8d1-126">Client ID</span></span>
    - <span data-ttu-id="fd8d1-127">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="fd8d1-127">Tenant ID</span></span>
    - <span data-ttu-id="fd8d1-128">Active Directory 金鑰 （相同 hello 上面輸入的其中一個）</span><span class="sxs-lookup"><span data-stu-id="fd8d1-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="fd8d1-129">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="fd8d1-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="fd8d1-130">設定 hello 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="fd8d1-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="fd8d1-131">登入 tooAzure，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="fd8d1-132">按一下**資產**磚 tooopen hello 列出的資產清單。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="fd8d1-133">按一下**模組**磚 tooopen hello 模組的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="fd8d1-134">按一下**+ 加入模組**啟動按鈕和 hello 新增模組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![自動化帳戶設定](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="fd8d1-136">選取 hello 之後`DataTransformationApp.zip`檔案從本機電腦，請按一下**確定**tooimport hello 模組。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="fd8d1-137">當 Azure 自動化匯入模組 tooyour 帳戶時，它會擷取 hello 模組的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="fd8d1-138">此作業可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-138">This operation may take a couple of minutes.</span></span>

   ![自動化帳戶設定](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="fd8d1-140">您會收到通知正在部署該 hello 模組和 hello 程序完成時的另一個通知。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="fd8d1-141">您也可以檢查 hello 狀態**模組**磚。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="fd8d1-142">tooimport hello runbook 觸發 hello 工作定義</span><span class="sxs-lookup"><span data-stu-id="fd8d1-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="fd8d1-143">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="fd8d1-144">按一下**Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="fd8d1-145">按一下 [+ 加入 Runbook]，然後按一下 [匯入現有 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![匯入現有 Runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="fd8d1-147">按一下**Runbook 檔案**和選取 hello 檔案 tooimport `Trigger-DataTransformation-Job.ps1`。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="fd8d1-148">按一下**建立**tooimport hello runbook。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="fd8d1-149">hello 新的 runbook 會出現在 hello 清單 hello 自動化帳戶的 runbook。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="fd8d1-150">按一下 Trigger-DataTransformation-Job Runbook，然後按一下編輯。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="fd8d1-151">按一下 [發行]，並在系統提示您確認時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="fd8d1-152">toorun hello runbook:</span><span class="sxs-lookup"><span data-stu-id="fd8d1-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="fd8d1-153">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="fd8d1-154">按一下 hello **Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="fd8d1-155">按一下 [Trigger-DataTransformation-Job]。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="fd8d1-156">按一下**啟動**toostart hello runbook。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-156">Click **Start** toostart hello runbook.</span></span>

   ![啟動 Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="fd8d1-158">在 hello**啟動 runbook**刀鋒視窗中，輸入所有 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="fd8d1-159">按一下**確定**toosubmit hello 資料轉換作業。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![啟動 Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="fd8d1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd8d1-161">Next steps</span></span>

<span data-ttu-id="fd8d1-162">[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="fd8d1-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
