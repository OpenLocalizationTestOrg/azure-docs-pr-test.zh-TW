---
title: "aaaAzure DevTest Labs 常見問題集 |Microsoft 文件"
description: "尋找答案 toocommon Azure DevTest Labs 問題"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Azure DevTest Labs 常見問題集
本文回答關於 Azure DevTest Labs hello 最常見問題的解答。

**一般**
## <a name="what-if-my-question-isnt-answered-here"></a>如果這裡沒有解答我的問題該怎麼辦？
如果這裡未列出您的問題，請告訴我們，好讓我們能協助您找到答案。

* 將問題張貼在 hello [Disqus 執行緒](#comments)結尾 hello 這個常見問題集和要與 hello Azure 快取小組和其他關於本文的社群成員交流。
* tooreach 更多觀眾，將問題張貼在 hello [Azure DevTest Labs MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)，和要與 hello Azure DevTest Labs 小組和其他 hello 社群成員交流。
* toomake 功能要求送出您的要求和意見 toohello [Azure DevTest 實驗室使用者語音](https://feedback.azure.com/forums/320373-azure-devtest-labs)。

## <a name="why-should-i-use-azure-devtest-labs"></a>為何應使用 Azure DevTest Labs？
Azure DevTest Labs 可讓您的小組節省時間和金錢。 開發人員可以建立他們自己使用數個不同的基底的環境，並使用 tooquickly 部署和設定應用程式的成品。 透過自訂映像和公式，就可以將虛擬機器儲存為範本並輕易予以重現。 此外，實驗室提供數個可設定原則，可讓實驗室系統管理員 tooreduce 浪費和管理小組的環境。 這些原則包括自動關機、成本臨界值、每一使用者的 VM 數上限和 VM 大小上限。 如需 Azure DevTest Labs 的更深入說明，讀取 hello[概觀](devtest-lab-overview.md)或監看式 hello[簡介影片](/documentation/videos/videos/what-is-azure-devtest-labs)。

## <a name="what-does-worry-free-self-service-mean"></a>「零煩惱的自助方式」是什麼意思？
"放心，自助 」 表示開發人員和測試人員視需要建立自己的環境，而且系統管理員擁有 hello 安全性得知 Azure DevTest Labs 有助於減少浪費並控制成本。 系統管理員可以指定的 VM 大小允許，hello 最大數目的 Vm，以及當 Vm 會啟動和關機。 Azure 的 DevTest Labs 可輕鬆 toomonitor 成本和設定警示 toostay 留意 hello 實驗室中的資源的使用方式。

## <a name="how-can-i-use-azure-devtest-labs"></a>如何使用 Azure DevTest Labs？
Azure 的 DevTest Labs 很有用，每當您需要開發人員或測試環境中，而且您想 tooreproduce 它們快速及/或儲存原則的成本管理它們。

以下是我們的客戶使用 Azure DevTest Labs 的一些案例︰

* 管理在同一個地方的開發和測試環境，利用原則 tooreduce 成本和自訂映像 tooshare hello 團隊建置。
* 開發應用程式使用自訂映像 toosave hello 磁碟狀態整個 hello 開發階段。
* 在追蹤關聯 tooprogress hello 成本。
* 建立大量測試環境以進行品質保證測試。
* 使用成品和公式 tooeasily 設定，並重現各種環境上的應用程式。
* Hackathons （共同開發或測試工作），如散發 Vm，然後輕鬆地解除佈建這些 hello 事件結束時。

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Azure DevTest Labs 如何收費？
Azure 的 DevTest Labs 是一個免費服務，表示建立實驗室和設定 hello 原則、 範本和成品免費。 您只針對付費 hello 實驗室，例如虛擬機器、 儲存體帳戶和虛擬網路內使用的 Azure 資源。 多個 hello 成本實驗室資源的詳細資訊，請參閱有關[Azure DevTest Labs 定價](https://azure.microsoft.com/pricing/details/devtest-lab/)。


**安全性**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>將不同的安全性等級 hello Azure DevTest Labs 中有哪些？
安全性存取權是由 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-built-in-roles.md)所決定。 toounderstand 存取的方式運作，這樣做，toounderstand hello 之間差異的權限、 角色，以及範圍所定義的 RBAC。

* **權限**-已定義的存取 tooa 特定動作的權限。 例如，權限可以讀取 tooall 虛擬機器。
* **角色**-角色是一組權限可以指派 tooa 使用者和群組。 例如，「 訂用帳戶擁有者 」 已訂用帳戶內存取 tooall 資源。
* **範圍**-領域是中的 Azure 資源的 hello 階層的層級。 例如，範圍可以是資源群組或單一實驗室或 hello 整個訂閱。

Hello Azure DevTest Labs 範圍內有兩種類型的角色 toodefine 使用者權限： 實驗室擁有者和實驗室使用者。

* **實驗室擁有者**-實驗室擁有者已在 hello 的實驗室中的 hello 存取 tooany 資源。 因此，它們可以修改原則、 讀取和寫入任何 Vm、 變更 hello 虛擬網路，並以此類推。
* **實驗室使用者** - 實驗室使用者可以檢視所有實驗室資源，例如 VM、原則和虛擬網路，但他們不能修改原則或任何由其他使用者所建立的 VM。 它也是可能 toocreate 自訂角色在 Azure 的 DevTest Labs，和您可以了解如何 hello 文章 toodo [toospecific 實驗室原則授與使用者權限](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)。

由於範圍是階層形式，當使用者擁有特定範圍的權限時，就會自動獲得該範圍所包含的每個較低層級範圍的權限。 比方說，如果使用者被指派 toohello 訂用帳戶擁有者的角色，則他們有存取 tooall 資源的訂用帳戶中。 這些資源包括所有虛擬機器、所有虛擬網路和所有實驗室。 因此，訂閱擁有者會自動繼承 hello 實驗室擁有者的角色。 但是，並非反之亦然 hello 相反。 實驗室擁有者具有存取 tooa 實驗室中，也就是比 hello 訂用帳戶層級較低的領域。 因此，實驗室擁有者不能 toosee 虛擬機器或虛擬網路或實驗室 hello 外的任何資源。

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>如何建立角色 tooallow 使用者 tooperform 特定的工作？
關於如何 toocreate 自訂角色和指派權限 toothat 角色可以在這裡找到的完整文件。 建立 hello 角色 「 DevTest Labs 進階使用者 」，其具有權限 toostart 和停止 hello 實驗室中的所有 Vm 的指令碼的範例如下：

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**CI/CD 整合與自動化**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs 是否會與我的 CI/CD 工具鏈整合？
如果您使用 VSTS，沒有[Azure DevTest Labs 工作擴充](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks)，可讓您的發行管線中 Azure DevTest Labs tooautomate。 Hello 使用這項擴充功能包括：

* 建立自動部署 VM 和設定與使用 Azure 檔案複製或 PowerShell VSTS 工作 hello 最新組建。
* 自動擷取 VM 的 hello 狀態之後測試 tooreproduce bug hello 做進一步調查相同的 VM。
* 不再需要時，刪除 hello 結尾 hello hello VM 發行管線。

hello 下列部落格文章提供指引和使用 hello VSTS 擴充功能的相關資訊：

* [Azure DevTest Labs – VSTS 擴充功能](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [從 VSTS 在現有 AzureDevTestLab 部署新的 VM](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [使用連續部署 tooAzureDevTestLabs VSTS Release Management](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

針對其他 CI/CD toolchains，所有的 hello 先前提到到 VSTS 工作延伸模組可以同樣地達成逐步部署的 hello 能達到之效果的案例[Azure 資源管理員範本](https://aka.ms/dtlquickstarttemplate)使用[Azure PowerShell cmdlet](../azure-resource-manager/resource-group-template-deploy.md)和[.NET Sdk](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/)。 您也可以使用[REST Api 的 DevTest Labs](http://aka.ms/dtlrestapis) toointegrate 您工具鏈使用。  


**虛擬機器**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>為什麼看不到在 hello Azure 虛擬機器刀鋒視窗中，我看到 Azure DevTest Labs 內特定 Vm？
在 Azure DevTest Labs 中建立 VM 時，權限是指定 tooaccess 該 VM。 是可以 tooview 它在 hello 實驗室刀鋒視窗和 hello**虛擬機器**刀鋒視窗。 Hello DevTest Labs 角色中的使用者可以看到在 hello 透過 hello 實驗室的實驗室中建立的所有虛擬機器**所有虛擬機器**刀鋒視窗。 不過，hello DevTest Labs 角色中的使用者不會自動授與其他人所建立的讀取權限 tooVM 資源。 因此，這些 Vm 中不會顯示 hello**虛擬機器**刀鋒視窗。

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>自訂映像和公式的 hello 差異為何？
自訂映像是 VHD (虛擬硬碟)，公式則是可額外進行設定之可儲存和重現的映像。 自訂影像可能較適合 tooquickly 如果您想建立數個環境，以 hello 相同基本的不可變的映像。 公式可能是較佳，如果您想要 tooreproduce hello 設定您的 VM 與 hello 最新的位元、 虛擬網路/子網路或特定的大小。 更深入的說明，請參閱 hello 文章[比較自訂映像和 DevTest Labs 中的公式](devtest-lab-comparing-vm-base-image-types.md)。

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>如何從 hello 建立多個 Vm 同時使用相同的範本？
您可以使用 hello [VSTS 工作擴充](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks)或[產生 Azure Resource Manager 範本](devtest-lab-add-vm.md#save-azure-resource-manager-template)建立 VM 時和[部署 hello Azure 資源管理員範本，從 Windows PowerShell](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>如何將現有 Azure VM 移到 Azure DevTest Labs 實驗室？
請遵循下列 toocopy hello 步驟是您現有的 Vm tooAzure DevTest Labs:

1. 複製 hello VHD 檔案，您使用這項功能的現有 VM 的[Windows PowerShell 指令碼](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [建立自訂映像 hello](devtest-lab-create-template.md) Azure DevTest Labs 實驗室內。
3. 從您的自訂映像的 hello 實驗室中建立 VM

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>可以將附加多個磁碟 toomy Vm？
附加多個磁碟 tooVMs 受到支援。  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>如果我想 toouse Windows OS 映像的我的測試時，有 toopurchase MSDN 訂閱？
如果您開發或測試在 Azure 中需要 toouse Windows 用戶端 OS 映像 (Windows 7 或更新版本)，然後是，您必須：

- [購買 MSDN 訂閱](https://www.visualstudio.com/products/how-to-buy-vs)。
- 如果您有 Enterprise 合約時，建立 Azure 訂用帳戶以 hello[企業開發/測試優惠](https://azure.microsoft.com/en-us/offers/ms-azr-0148p)。

如需有關 hello Azure 信用額度，對每個 MSDN 供應項目，請參閱[Visual Studio 訂閱者的每月 Azure 信用額度](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/)。

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>如何上傳 VHD 檔案 toocreate 自訂映像 hello 程序自動化？
有兩個選項：

* [Azure 的 AzCopy](../storage/common/storage-use-azcopy.md#blob-upload)可以使用的 toocopy 或上傳 VHD 檔案 toohello 儲存體帳戶與 hello 實驗室相關聯。
* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是在 Windows、OSX 和 Linux 上執行的獨立應用程式。   

toofind hello 目的地儲存體帳戶與您的實驗室，相關聯，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**資源群組**hello 左面板中。
3. 找出並選取您的實驗室相關聯的 hello 資源群組。
4. 在 hello**概觀**刀鋒視窗中，選取其中一個 hello 儲存體帳戶。
5. 選取 [Blob] 。
6. 尋找 hello 清單中上傳。 如果不存在，傳回 tooStep #4，然後再次嘗試另一個儲存體帳戶。
7. 使用 hello **URL**做為目的地的 AzCopy 命令。

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>如何刪除所有 hello Vm 我實驗室中的 hello 程序自動化？
此外 toodeleting Vm 從您的實驗室 hello Azure 入口網站中，您可以刪除所有 hello Vm 在您的實驗室使用的 PowerShell 指令碼。 在 hello 遵循範例中，修改 hello 參數值在 hello**值 toochange**註解。 您可以擷取 hello `subscriptionId`， `labResourceGroup`，和`labName`hello Azure 入口網站中的 hello 實驗室刀鋒視窗中的值。

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**構件**
## <a name="what-are-artifacts"></a>何謂構件？
成品是可以使用您最新的位元或您的開發人員工具拖曳至 VM 的 toodeploy 的可自訂項目。 它們是附加的 tooyour VM 建立簡單的按下滑鼠，期間和 hello 成品 hello VM 已佈建之後，部署和設定您的 VM。 我們的[公用 GitHub 存放庫](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)中有許多既存構件，但您也可以輕易地[撰寫自己的構件](devtest-lab-artifact-author.md)。


**實驗室組態**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>如何從 Azure Resource Manager 範本建立實驗室？
我們已提供[GitHub 儲存機制的實驗室 Azure Resource Manager 範本](https://aka.ms/dtlquickstarttemplate)，您可以部署為-修改您的實驗室 toocreate 自訂範本。 每個範本有一個連結，您可以按一下 toodeploy hello 實驗室做為-低於您的 Azure 訂用帳戶，或者您可以自訂 hello 範本和[部署使用 PowerShell 或 Azure CLI](../azure-resource-manager/resource-group-template-deploy.md)。

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>為何我的 VM 會建立在具有任意名稱的不同資源群組中？ 我是否可以重新命名或修改這些資源群組？
為了讓 Azure DevTest Labs toomanage hello 使用者權限和存取 toovirtual 機器會以這種方式建立資源群組。 雖然您可以移動 hello VM tooanother 資源群組，以您想要的名稱，不是建議您這麼做。 我們會努力改善這體驗 tooallow 更大的彈性。   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>多少實驗室我可以建立在 hello 相同訂用帳戶？
可以建立每個訂閱的實驗室的 hello 數目沒有特定限制。 不過，使用 hello 資源會限制每個訂閱。 您可以閱讀 hello[加諸於 Azure 訂用帳戶限制和配額](../azure-subscription-service-limits.md)和[如何 tooincrease 這些限制](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests)。

## <a name="how-many-vms-can-i-create-per-lab"></a>每個實驗室可以建立幾個 VM？
可建立每個實驗室 Vm 的 hello 數目沒有特定限制。 不過，使用 hello 資源會限制每個訂閱 (例如 VM 核心，公用 Ip 時，等。)。 您可以閱讀 hello[加諸於 Azure 訂用帳戶限制和配額](../azure-subscription-service-limits.md)和[如何 tooincrease 這些限制](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests)。

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>如何共用直接連結 toomy 實驗室？
tooshare 的直接連結 tooyour 實驗室使用者，您可以執行下列程序的 hello:

1. 瀏覽 toohello 實驗室 hello Azure 入口網站中。
2. 從您的瀏覽器複製 hello 實驗室 URL 並分享您的實驗室使用者。

> [!NOTE]
> 如果您的實驗室使用者與外部使用者[Microsoft 帳戶](#what-is-a-microsoft-account)和它們不屬於 tooyour 公司的 Active directory、 瀏覽 toohello 提供連結時，它們可能會收到錯誤。 如果收到錯誤，指示他們 tooclick 其名稱中的 hello 右上角 hello Azure 入口網站和從 hello hello 實驗室所在的選取 hello 目錄**目錄**hello 功能表區段。
>
>

## <a name="what-is-a-microsoft-account"></a>什麼是 Microsoft 帳戶？
Microsoft 帳戶是您使用 Microsoft 裝置和服務來執行幾乎所有作業時所使用的帳戶。 它是電子郵件地址和密碼使用 toosign tooSkype、 Outlook.com、 OneDrive、 Windows Phone 和 Xbox LIVE – 中的，這表示您的檔案、 相片、 連絡人、 並設定可以遵照您 tooany 裝置。

> [!NOTE]
> Toobe 稱為 「 Windows Live ID 」 使用 Microsoft 帳戶。
>
>


**疑難排解**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>在建立 VM 時，我的構件失敗了。 我該如何進行疑難排解？
請參閱太[如何 DevTest Labs toodiagnose 成品失敗](devtest-lab-troubleshoot-artifact-failure.md)toolearn tooobtain 有關失敗的成品記錄的方式。

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>為何我現有的虛擬網路未能正確儲存？
其中一個可能原因是您的虛擬網路名稱包含句點。 如果因此再試一次移除 hello 句號，或將其取代為連字號，然後再次嘗試儲存一次 hello 虛擬網路。

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>為何我從 PowerShell 佈建 VM 時遇到「找不到父資源」錯誤？
父 tooanother 資源一個資源時，必須存在 hello 父資源，才能建立 hello 子資源。 如果不存在，您會收到 **ParentResourceNotFound** 錯誤。 如果您未在 hello 父資源上指定相依性，可能 hello 父系之前部署 hello 子資源。

VM 是資源群組中實驗室下的子資源。 當您使用透過 PowerShell 的 Azure Resource Manager 範本 toodeploy 時，hello hello PowerShell 指令碼中提供的資源群組名稱應該是 hello 實驗室 hello 資源群組名稱。 如需詳細資訊，請參閱[對常見的 Azure 部署錯誤進行疑難排解](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound)。

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>當 VM 部署失敗時，我可以在哪裡找到更多錯誤資訊？
Hello 活動記錄中所擷取 VM 部署錯誤。 您可以找到實驗室 Vm 活動記錄檔，透過 hello**稽核記錄檔**或**虛擬機器診斷**hello 實驗室 VM 刀鋒視窗中的 hello 資源功能表上 (hello 刀鋒視窗會顯示您選取從helloVM之後**我的虛擬機器**清單)。

有時候，hello VM 部署的開始-例如當 hello 訂用帳戶以 hello VM 建立的資源超過限制之前，就會發生 hello 部署錯誤。 Hello 實驗室層級中的 hello 錯誤詳細資料會在此情況下，擷取**活動記錄**可以尋找在 hello 底部 hello**組態和原則**設定。 使用活動的詳細資訊記錄在 Azure 中，請參閱[檢視活動記錄在資源上的 tooaudit 動作](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit)。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
