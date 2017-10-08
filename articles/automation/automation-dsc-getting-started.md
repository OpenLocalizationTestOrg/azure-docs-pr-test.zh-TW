---
title: "開始使用 Azure Automation DSC 的 aaaGetting |Microsoft 文件"
description: "說明與 hello 最常見的工作在 Azure 自動化預期狀態設定 (DSC) 的範例"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>開始使用 Azure 自動化 DSC
本主題說明如何 toodo hello 與 Azure 自動化預期狀態設定 (DSC)，建立、 匯入，並編譯設定，登入機器太管理和檢視報表之類的常見工作。 如需何謂 Azure 自動化 DSC 的概觀，請參閱 [Azure 自動化 DSC 概觀](automation-dsc-overview.md)。 如需 DSC 文件，請參閱 [Windows PowerShell 預期狀態設定概觀](https://msdn.microsoft.com/PowerShell/dsc/overview)。

本主題提供逐步指南 toousing Azure Automation DSC。 如果您想未遵循本主題中所述的 hello 步驟已經設定好的範例環境，您可以使用[hello ARM 範本下列](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)。 此範本會設定完整的 Azure 自動化 DSC 環境，包括由 Azure 自動化 DSC 管理的 Azure VM。

## <a name="prerequisites"></a>必要條件
本主題中的 toocomplete hello 範例，hello 需要下列憑證：

* Azure 自動化帳戶。 如需建立 Azure 自動化執行身分帳戶的指示，請參閱 [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。
* 執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM (不是傳統)。 如需建立 VM 的指示，請參閱[hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>建立 DSC 組態
我們將建立簡單[DSC 設定](https://msdn.microsoft.com/powershell/dsc/configurations)這可確保 hello 存在或不存在的 hello **Web 伺服器**Windows 功能 (IIS)，根據您指定節點的方式。

1. 啟動 Windows PowerShell ISE hello （或任何文字編輯器）。
2. 輸入下列文字的 hello:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. 將 hello 檔案儲存為`TestConfig.ps1`。

這項設定會呼叫一項資源中每個節點區塊，hello [WindowsFeature 資源](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource)，這可確保 hello 存在或不存在的 hello **Web 伺服器**功能。

## <a name="importing-a-configuration-into-azure-automation"></a>將組態匯入 Azure 自動化
接下來，我們將會匯入 hello 組態 hello 自動化帳戶。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**。
4. 在 hello **DSC 設定**刀鋒視窗中，按一下 **加入組態**。
5. 在 hello**匯入組態**刀鋒視窗中，瀏覽 toohello`TestConfig.ps1`電腦上的檔案。
   
    ![螢幕擷取畫面的 hello * * 匯入設定 * * 刀鋒視窗](./media/automation-dsc-getting-started/AddConfig.png)
6. 按一下 [確定] 。

## <a name="viewing-a-configuration-in-azure-automation"></a>在 Azure 自動化中檢視組態
在匯入組態之後，您可以在 hello Azure 入口網站中檢視它。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**
4. 在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （這是您所匯入的 hello 組態的名稱，hello hello 前程序中）。
5. 在 hello **TestConfig 組態**刀鋒視窗中，按一下**檢視組態來源**。
   
    ![Hello TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **TestConfig 組態來源**刀鋒視窗隨即開啟，顯示 hello 組態 hello PowerShell 程式碼。

## <a name="compiling-a-configuration-in-azure-automation"></a>在 Azure 自動化中編譯組態
您可以套用所需的狀態 tooa 節點之前，必須編譯成一或多個節點組態 （MOF 文件），並放在 hello 自動化 DSC 提取伺服器上 DSC 設定定義該狀態。 如需在 Azure 自動化 DSC 中編譯設定的詳細說明，請參閱 [在 Azure 自動化 DSC 中編譯設定](automation-dsc-compile.md)。 如需編譯設定的詳細資訊，請參閱 [DSC 設定](https://msdn.microsoft.com/PowerShell/DSC/configurations)。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**
4. 在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （hello hello 名稱先前匯入組態）。
5. 在 hello **TestConfig 組態**刀鋒視窗中，按一下 **編譯**，然後按一下**是**。 這會啟動編譯作業。
   
    ![編譯按鈕反白顯示的 hello TestConfig 組態刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> 當您編譯 Azure 自動化中的組態時，自動將部署任何建立的節點設定 Mof toohello 提取伺服器。
> 
> 

## <a name="viewing-a-compilation-job"></a>檢視編譯作業
開始編譯之後，可以檢視在 hello**編譯工作**磚中 hello**組態**刀鋒視窗。 hello**編譯工作**磚顯示目前正在執行、 已完成，以及失敗的作業。 當您開啟編譯工作刀鋒視窗時，它會顯示該工作，包括任何錯誤或警告發生的相關資訊、 輸入的參數用於 hello 組態和編譯記錄檔。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 設定**。
4. 在 hello **DSC 設定**刀鋒視窗中，按一下  **TestConfig** （hello hello 名稱先前匯入組態）。
5. 在 hello**編譯工作**磚 hello **TestConfig 組態**刀鋒視窗中，按一下任何所列的 hello 作業。 A**編譯工作**啟動刀鋒視窗隨即開啟，加上 hello hello 編譯作業的日期。
   
    ![Hello 編譯工作刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/CompilationJob.png)
6. 按一下任何磚中 hello**編譯工作**進一步刀鋒視窗 toosee hello 作業的相關詳細資料。

## <a name="viewing-node-configurations"></a>檢視節點組態
成功完成編譯作業會建立一或多個新的節點組態。 節點設定為已部署的 toohello 提取伺服器與準備好 toobe 提取，且套用一個或多個節點的 MOF 文件。 您可以檢視您的自動化帳戶中 hello hello 節點設定**DSC 節點組態**刀鋒視窗。 節點組態都有名稱與 hello 表單*ConfigurationName*。*NodeName*。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點組態**。
   
    ![Hello DSC 節點組態 刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>將 Azure VM 上架以供 Azure 自動化 DSC 管理
您可以使用 Azure 自動化 DSC toomanage Azure Vm （傳統和資源管理員），在內部部署 Vm、 Linux 機器、 AWS Vm 和內部部署實體機器。 在本主題中，我們將討論如何 tooonboard Azure 資源管理員 Vm。 如需將其他類型的機器上架的詳細資訊，請參閱 [將機器上架以供 Azure 自動化 DSC 管理](automation-dsc-onboarding.md)。

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard 供 Azure Automation DSC 來管理 Azure 資源管理員 VM
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。
4. 在 hello **DSC 節點**刀鋒視窗中，按一下 **新增 Azure VM**。
   
    ![Hello DSC 節點刀鋒視窗中反白顯示 hello 新增 Azure VM 按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/OnboardVM.png)
5. 在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **選取虛擬機器 tooonboard**。
6. 在 hello**選取 Vm**刀鋒視窗中，選取 hello VM tooonboard，然後按一下**確定**。
   
   > [!IMPORTANT]
   > 這必須是執行 Windows Server 2008 R2 或更新版本的 Azure Resource Manager VM。
   > 
   > 
7. 在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **設定註冊資料**。
8. 在 hello**註冊**刀鋒視窗中，輸入 hello 名稱 hello 節點組態中，您想在 hello tooapply toohello VM**節點設定名稱**方塊。 這必須完全符合 hello hello 自動化帳戶中之節點組態的名稱。 在此時提供名稱是選擇性的。 您可以變更指派的 hello 節點組態上架 hello 節點之後。
   勾選 必要時重新啟動節點，然後按一下確定。
   
    ![Hello 註冊刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/RegisterVM.png)
   
    您指定的 hello 節點組態將會套用的 toohello VM hello 所指定的間隔**設定模式頻率**，和 hello VM 將會檢查在 hello所指定的間隔更新toohello節點組態**重新整理頻率**。 如需有關如何使用這些值的詳細資訊，請參閱[設定 hello 本機設定管理員](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)。
9. 在 hello**新增 Azure Vm**刀鋒視窗中，按一下 **建立**。

Azure 將啟動上架 hello VM 的 hello 程的序。 當完成時，hello VM 將會顯示在 hello **DSC 節點**hello 自動化帳戶中的刀鋒視窗。

## <a name="viewing-hello-list-of-dsc-nodes"></a>檢視 hello DSC 節點清單
您可以檢視已被 onboarded hello 自動化帳戶中管理的所有機器的 hello 清單**DSC 節點**刀鋒視窗。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。

## <a name="viewing-reports-for-dsc-nodes"></a>檢視 DSC 節點的報告
Azure 自動化 DSC 執行一致性檢查，受管理節點上，每次 hello 節點會傳送狀態報表後 toohello 提取伺服器。 您可以在該節點的 hello 刀鋒視窗上檢視這些報表。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。
4. 在 hello**報表**磚中，按一下任何 hello hello 清單中的報表。
   
    ![Hello 報表刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/NodeReport.png)

在 hello 刀鋒視窗中個別報表，您可以看到 hello 下列狀態資訊的 hello 對應一致性檢查：

* hello 報告狀態 — hello 節點是 「 符合標準 「 hello 設定 「 失敗 」，還是 hello 節點是 「 不相容 」 (當 hello 節點處於**applyandmonitor**模式和 hello 機器未處於預期的 hello 狀態)。
* hello hello 一致性檢查的開始時間。
* hello 總執行時間的 hello 一致性檢查。
* hello 的一致性檢查類型。
* 任何錯誤，包括 hello 錯誤程式碼和錯誤訊息。 
* Hello 組態和 hello 狀態，每個資源 （hello 節點是否在該資源的所需的 hello 狀態） 中使用任何 DSC 資源，您可以按一下每個資源 tooget 上更詳細的資源資訊。
* hello 名稱、 IP 位址和 hello 節點的組態模式。

您也可以按一下**檢視未經處理的報表**toosee hello 實際資料 hello 節點傳送 toohello 伺服器。 如需有關使用該資料的詳細資訊，請參閱 [使用 DSC 報告伺服器](https://msdn.microsoft.com/powershell/dsc/reportserver)。

它可能需要一些時間之後的節點時 onboarded hello 第一份報表之前。 您可能需要向上 too30 分鐘 toowait hello 第一個報表之後，您將產品上架節點。

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>重新指派節點 tooa 不同節點組態
Hello 一個一開始指派比您可以指派指定節點 toouse 的不同節點設定。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。
4. 在 hello **DSC 節點**刀鋒視窗中，按一下 hello 名稱要 tooreassign 的 hello 節點。
5. 在該節點的 hello 刀鋒視窗，按一下 **指派節點**。
   
    ![Hello 節點刀鋒視窗中反白顯示 hello 指派節點按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNode.png)
6. 在 hello**指派節點設定**刀鋒視窗中，選取 hello 節點組態 toowhich tooassign hello 節點，然後再按一下**確定**。
   
    ![Hello 指派節點設定刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>取消註冊節點
如果您不想再由 Azure Automation DSC 節點 toobe，您就可以將它移除註冊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **所有資源**，然後 hello 您的自動化帳戶名稱。
3. 在 hello**自動化帳戶**刀鋒視窗中，按一下  **DSC 節點**。
4. 在 hello **DSC 節點**刀鋒視窗中，按一下 hello 名稱要 toounregister 的 hello 節點。
5. 在該節點的 hello 刀鋒視窗，按一下 **取消註冊**。
   
    ![Hello 節點刀鋒視窗中反白顯示 hello 取消註冊按鈕的螢幕擷取畫面](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>相關文章
* [Azure 自動化 DSC 概觀](automation-dsc-overview.md)
* [上架由 Azure 自動化 DSC 管理的機器](automation-dsc-onboarding.md)
* [Windows PowerShell 預期狀態設定概觀](https://msdn.microsoft.com/powershell/dsc/overview)
* [Azure 自動化 DSC Cmdlet](/powershell/module/azurerm.automation/#automation)
* [Azure 自動化 DSC 價格](https://azure.microsoft.com/pricing/details/automation/)

