---
title: "aaaAutomating Amazon Web Services 中的 VM 部署 |Microsoft 文件"
description: "本文示範如何 toouse 將 tooautomate 建立 Azure 自動化的 Amazon Web 服務的 VM"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Azure 自動化案例 - 佈建 AWS 虛擬機器
在本文中，我們將示範如何利用 Azure 自動化 tooprovision Amazon Web 服務 (AWS) 訂用帳戶中的虛擬機器，並提供特定名稱 – 該 VM 的 AWS 指的是 「 標記 」 hello VM tooas。

## <a name="prerequisites"></a>必要條件
基於 hello 這篇文章，您會需要 toohave Azure 自動化帳戶和 AWS 訂用帳戶。 如需設定 Azure 自動化帳戶以及使用 AWS 訂用帳戶認證進行設定的詳細資訊，請檢閱[使用 Amazon Web Services 設定驗證](automation-configure-aws-account.md)。  此帳戶應該建立或更新以 AWS 訂用帳戶認證之前，我們會參考此帳戶在 hello 執行下列步驟。

## <a name="deploy-amazon-web-services-powershell-module"></a>部署 Amazon Web Services PowerShell 模組
我們 VM 佈建 runbook 將會利用 hello AWS PowerShell 模組 toodo 其工作。 執行下列步驟 tooadd hello 模組 tooyour 自動化帳戶已設有 AWS 訂用帳戶認證的 hello。  

1. 開啟網頁瀏覽器並瀏覽 toohello [PowerShell 資源庫](http://www.powershellgallery.com/packages/AWSPowerShell/)，然後按一下 hello**部署 tooAzure 自動化按鈕**。<br><br> ![AWS PS 模組匯入](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. 即會進入 toohello Azure 登入頁面，並驗證之後，將路由的 toohello Azure 入口網站，並顯示以 hello 遵循刀鋒視窗。<br><br> ![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. 選取 hello 資源群組從 hello**資源群組**下拉式清單，並在 hello 參數刀鋒視窗中，提供下列資訊的 hello:
   
   * 從 hello**新的或現有的自動化帳戶 （字串）**下拉式清單中，選取**現有**。  
   * 在 hello**自動化帳戶名稱 （字串）**方塊中，輸入 hello 完整名稱中的 hello 自動化帳戶，其中包含 hello AWS 訂用帳戶的認證。  例如，如果您建立名為的專用的帳戶**AWSAutomation**，則您在 [hello] 方塊中輸入的內容。
   * 選取 hello 適當區域從 hello**自動化帳戶位置**下拉式清單。
4. 當您完成輸入 hello 所需的資訊時，請按一下**建立**。
   
   > [!NOTE]
   > 雖然匯入至 Azure 自動化的 PowerShell 模組，它也擷取 hello cmdlet 且 hello 模組完全完成匯入和擷取 hello cmdlet 之前，不會出現這些活動。 此程序需要數分鐘的時間。  
   > <br>
   > 
   > 
5. 在 hello Azure 入口網站，開啟您在步驟 3 中所參考的自動化帳戶。
6. 按一下 hello**資產**磚和 hello**資產**刀鋒視窗中，選取 hello**模組**磚。
7. 在 hello**模組**刀鋒視窗，您會看到 hello **AWSPowerShell** hello 清單中的模組。

## <a name="create-aws-deploy-vm-runbook"></a>建立 AWS 部署 VM Runbook
一次 AWS PowerShell 模組已部署的 hello，我們現在可以製作 runbook tooautomate 佈建 AWS 使用 PowerShell 指令碼中的虛擬機器。 hello 執行下列步驟將示範如何 tooleverage 原生 PowerShell 指令碼在 Azure 自動化中。  

> [!NOTE]
> 如需進一步的選項和此指令碼的相關資訊，請造訪 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript)。
> 

1. 從 hello PowerShell 資源庫下載 hello PowerShell 指令碼新增 AwsVM，請開啟 PowerShell 工作階段，然後輸入 hello 下列：<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. 從 hello Azure 入口網站，開啟您的自動化帳戶，然後按一下 hello **Runbook**磚。  
3. 從 hello **Runbook**刀鋒視窗中，選取**新增 runbook**。
4. 在 hello**新增 runbook**刀鋒視窗中，選取**快速建立**（建立新的 runbook）。
5. 在 [hello **Runbook**屬性刀鋒視窗中，輸入 hello 名稱] 方塊中的名稱為您的 runbook 與 hello **Runbook 類型**下拉式清單中，選取**PowerShell**，然後按一下 **建立**。<br><br> ![匯入模組刀鋒視窗](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Hello 編輯 PowerShell Runbook 刀鋒視窗出現時，請複製並貼入 hello runbook 製作畫布中的 hello PowerShell 指令碼。<br><br> ![Runbook PowerShell 指令碼](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > 請使用 hello 範例 PowerShell 指令碼時，注意 hello 下列事項：
    > 
    > * hello runbook 包含預設參數值的數目。 請評估所有預設值，並且視需要更新。
    > * 如果您有儲存 AWS 認證認證資產名稱不同於**AWScred**，您必須在行 57 toomatch tooupdate hello 指令碼據此。  
    > * 當使用 hello AWS CLI 命令在 PowerShell 中，特別是此範例 runbook，您必須指定 hello AWS 區域。 否則，hello 指令程式將會失敗。  檢視 AWS 主題[指定 AWS 區域](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html)hello AWS 工具，以取得詳細資料的 PowerShell 文件中。  
    >

7. tooretrieve 一份您 AWS 訂用帳戶，從映像名稱啟動 PowerShell ISE，並匯入 hello AWS PowerShell 模組。  將 ISE 環境中的 **Get-AutomationPSCredential** 取代為 **AWScred = Get-Credential**，以驗證 AWS。  這會提示您輸入您的認證，而且您可以提供您**存取金鑰識別碼**hello 使用者名稱和**秘密便捷鍵**hello 密碼。  請參閱以下的 hello 範例：  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    hello 會傳回下列輸出：<br><br>
   ![取得 AWS 映像](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. 複製並貼上的其中一個 hello 映像名稱 hello hello runbook 中參考的自動化變數**$InstanceType**。 在此範例中我們使用 hello 可用 AWS 分層訂用帳戶，因為我們將使用**t2.micro** runbook 範例。  
9. 儲存 hello runbook，然後按一下 **發行**toopublish hello runbook，然後**是**出現提示時。

### <a name="testing-hello-aws-vm-runbook"></a>測試 hello AWS VM runbook
我們繼續測試 hello runbook 之前，我們需要 tooverify 幾件事。 具體而言：  

* 驗證 AWS 資產建立呼叫**AWScred**或 hello 指令碼已更新的 tooreference hello 認證資產名稱。    
* 已匯入 Azure 自動化中的 hello AWS PowerShell 模組  
* 已建立新的 Runbook，已驗證參數值並且視需要更新  
* **記錄詳細資訊記錄**並選擇性地**記錄進度記錄**hello runbook 設定下**記錄與追蹤**設定得**上**。<br><br> ![Runbook 記錄和追蹤](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. 我們想 toostart hello runbook，因此請按**啟動**，然後按一下**確定**hello 啟動 Runbook 刀鋒視窗開啟時。
2. 在 hello 啟動 Runbook 刀鋒視窗中，提供**VMname**。  您稍早預先 hello 指令碼中的其他參數接受 hello hello 的預設值。  按一下**確定**toostart hello runbook 工作。<br><br> ![啟動 New-AwsVM Runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. 工作窗格會開啟供 hello 剛才所建立的 runbook 工作。 關閉此窗格。
4. 我們可以檢視進度 hello 工作和檢視輸出**資料流**選取 hello**所有記錄檔**磚的 hello runbook 作業 刀鋒視窗。<br><br> ![串流輸出](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. 如果您目前未登入，tooconfirm hello 正在佈建 VM，登入 hello AWS 管理主控台。<br><br> ![AWS 主控台部署 VM](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>後續步驟
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
* tooknow 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)
* 如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

