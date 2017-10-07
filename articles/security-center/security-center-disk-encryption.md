---
title: "Azure 虛擬機器 aaaEncrypt |Microsoft 文件"
description: "這份文件可協助您 tooencrypt Azure 虛擬機器從 Azure 資訊安全中心收到警示之後。"
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>加密 Azure 虛擬機器
Azure 資訊安全中心會在您有未加密的虛擬機器時對您發出警示。 這些警示會顯示為高嚴重性和 hello 建議是 tooencrypt 這些虛擬機器。

![磁碟加密建議](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> 本文件中的 hello 資訊適用於 tooencrypting 虛擬機器，而不使用金鑰的加密金鑰 （這是必要的備份使用 Azure 備份的虛擬機器）。 請參閱 hello 文章[Azure 磁碟加密用於 Windows 及 Linux 的 Azure 虛擬機器](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)如需詳細資訊 toouse Key Encryption Key toosupport Azure 備份加密 Azure 虛擬機器。
>
>

tooencrypt 已由 Azure 資訊安全中心識別為需要加密的 Azure 虛擬機器，我們建議 hello 下列步驟：

* 安裝並設定 Azure PowerShell。 這可讓您 toorun hello PowerShell 命令需要的 tooset hello 必要條件需要 tooencrypt Azure 虛擬機器上。
* 取得並執行 hello Azure 磁碟加密必要條件 Azure PowerShell 指令碼
* 加密虛擬機器

這份文件 hello 目標是 tooenable 您 tooencrypt 您的虛擬機器，即使您在 Azure PowerShell 中有少量或沒有背景。
本文件假設您使用 Windows 10 做 hello 用戶端電腦，您將會從此處設定 Azure 磁碟加密。

有多種方法可以使用的 toosetup hello 必要條件和 tooconfigure 加密適用於 Azure 虛擬機器。 如果您已精通 Azure PowerShell 或 Azure CLI 中，您可能偏好 toouse 替代方式。

> [!NOTE]
> toolearn 進一步了解替代方案 tooconfiguring 加密為 Azure 虛擬機器，請參閱[Azure 磁碟加密用於 Windows 及 Linux 的 Azure 虛擬機器](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)。
>
>

## <a name="install-and-configure-azure-powershell"></a>安裝並設定 Azure PowerShell
您的電腦上需要安裝 Azure PowerShell 1.2.1 版或更新版本。 hello 文章[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)包含所有需要您使用 Azure PowerShell 的電腦 toowork tooprovision 的 hello 步驟。 hello 最直接的方法是在該文件中所述的 toouse hello Web PI 安裝方法。 即使您已經安裝 Azure PowerShell，請安裝一次使用 hello Web PI 方法，讓您擁有 hello 最新版本的 Azure PowerShell。

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>取得並設定指令碼執行 hello Azure 磁碟加密必要條件
hello Azure 磁碟加密必要條件設定指令碼會設定所有加密的 Azure 虛擬機器所需的 hello 必要條件。

1. 移 toohello GitHub 頁面，其中包含 hello [Azure 磁碟加密必要條件安裝程式指令碼](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)。
2. 在 hello GibHub 頁面上，按一下 [hello **Raw** ] 按鈕。
3. 使用**CTRL-A** tooselect 所有 hello hello 頁面上的文字，然後使用**CTRL-C** toocopy 所有 hello hello 頁面 toohello 剪貼簿上的文字。
4. 開啟**記事本**和複製的 hello 文字貼入 [記事本]。
5. 在 C: 磁碟機上建立名為 **AzureADEScript**的新資料夾。
6. 儲存 hello 記事本 檔案 – 按一下**檔案**，然後按一下 **存**。 在 [hello 檔案名稱] 文字方塊中，輸入**"ADEPrereqScript.ps1"**按一下**儲存**。 （請確定您將 hello 引號括住 hello 名稱，否則它會儲存 hello 檔案副檔名為.txt 的檔案）。

現在，儲存 hello 指令碼內容，請 hello PowerShell ISE 中開啟 hello 指令碼：

1. 在 hello 開始 功能表中，按一下  **Cortana**。 詢問**Cortana** "PowerShell"輸入**PowerShell** hello Cortana 搜尋文字方塊中。
2. 用滑鼠右鍵按一下 [Windows PowerShell ISE]，然後按一下 [以系統管理員身分執行]。
3. 在 hello**系統管理員： Windows PowerShell ISE**視窗中，按一下**檢視**，然後按一下**顯示指令碼窗格**。
4. 如果您看到 hello**命令**窗格右邊 hello hello 視窗中，按一下 hello **"x"** hello 右上角的 hello 窗格 tooclose 中它。 如果您 toosee 太小的 hello 文字，請使用**CTRL + 新增**（「 新增 」 為 hello"+"登入）。 如果 hello 文字而言太大，請使用**CTRL + 減號**(減去為 hello"-"號)。
5. 依序按一下 [檔案] 和 [開啟]。 瀏覽 toohello **C:\AzureADEScript**資料夾和 hello 按兩下 hello **ADEPrereqScript**。
6. hello **ADEPrereqScript**內容現在應該會出現在 hello PowerShell ISE 中，會以色彩標示的 toohelp 更容易看到各種元件，例如命令、 參數和變數。

您現在應該會看到 hello 下圖類似。

![PowerShell ISE 視窗](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

hello 上方窗格是參照的 tooas hello 「 指令碼窗格"而 hello 底部窗格是參照的 tooas hello 「 主控台 」。 本文稍後將會使用這些詞彙。

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>執行 hello Azure 磁碟加密必要條件 PowerShell 命令
hello Azure 磁碟加密必要條件指令碼會要求您提供 hello 開始 hello 指令碼之後，下列資訊：

* **資源群組名稱**-名稱的資源群組的 tooput hello hello 到金鑰保存庫。  如果還沒有建立該名稱，將建立新的資源群組與 hello 您所輸入的名稱。 如果您已經有您想要此訂用帳戶中的 toouse 資源群組，然後輸入 hello 該資源群組的名稱。
* **金鑰保存庫名稱**-在哪種加密金鑰是放置 toobe hello 金鑰保存庫的名稱。 如果您沒有此名稱的金鑰保存庫，則會以此名稱建立新的金鑰保存庫。 如果您已經有您想 toouse 金鑰保存庫，輸入 hello hello 現有金鑰保存庫名稱。
* **位置**-hello 金鑰保存庫的位置。 請確定在 hello hello 金鑰保存庫和 Vm toobe 加密相同的位置。 如果您不知道 hello 位置，將示範如何本文中稍後有步驟 toofind 出。
* **Azure Active Directory 應用程式名稱**-hello Azure Active Directory 應用程式將會使用的 toowrite 密碼 toohello 金鑰保存庫的名稱。 如果不存在此名稱的應用程式，將會以此名稱建立新的應用程式。 如果您已經有您想 toouse 的 Azure Active Directory 應用程式，輸入 hello 的 Azure Active Directory 應用程式名稱。

> [!NOTE]
> 如果您想為 toowhy 知道您需要 toocreate Azure Active Directory 應用程式，請參閱*與 Azure Active Directory 註冊應用程式*hello 文件中的區段[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md).
>
>

執行下列步驟 tooencrypt Azure 虛擬機器中的 hello:

1. 如果您關閉 hello PowerShell ISE，請開啟提升權限的 hello PowerShell ISE 的執行個體。 如果 hello PowerShell ISE 尚未開啟，請依照本文稍早的 hello 指示。 如果您關閉 hello 指令碼，然後開啟 hello **ADEPrereqScript.ps1**按一下**檔案**，然後**開啟**，然後選取 hello 指令碼從 hello **c:\AzureADEScript**資料夾。 如果您已依照本文從 hello 開始，然後只移 toohello 下一個步驟。
2. 在 hello 主控台中的 hello PowerShell ISE （hello hello PowerShell ISE 的下方窗格），請輸入，hello 焦點 toohello 本機 hello 指令碼的變更**cd c:\AzureADEScript**按**ENTER**。
3. 因此，您可以執行 hello 指令碼，請在電腦上設定 hello 執行原則。 型別**Set-executionpolicy Unrestricted**在 hello 主控台，然後按 ENTER。 如果您看到的對話方塊，告知 hello 的 hello 變更 tooexecution 原則的影響，請按一下 **是 tooall**或**是**(如果您看到**是 tooall**，如果選取該選項 –您不會看到**是 tooall**，然後按一下 **是**)。
4. 登入 Azure 帳戶。 在 [hello] 主控台中，輸入**登入 AzureRmAccount**按**ENTER**。 將會出現一個對話方塊，您可以在其中輸入您的認證 (請確定您有權限 toochange hello 虛擬機器 – 如果您沒有權限，就能 tooencrypt 它們。 如果不能確定，請詢問訂用帳戶擁有者或系統管理員)。 您應該會看到您 **Environment**、**Account**、**TenantId**、**SubscriptionId** 和 **CurrentStorageAccount** 的相關資訊。 複製 hello **SubscriptionId** tooNotepad。 您將需要 toouse 這步驟 #6 中。
5. 尋找您的虛擬機器什麼訂用帳戶所屬 tooand 其位置。 跳過[https://portal.azure.com](ttps://portal.azure.com)並登入。  在 hello hello 頁面的左側，按一下 **虛擬機器**。 您會看到一份您的虛擬機器和其所屬的 hello 訂用帳戶。

   ![虛擬機器](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. 傳回 toohello PowerShell ISE。 設定將在其中執行 hello 指令碼 hello 訂用帳戶的內容。 在 [hello] 主控台中，輸入**選取 AzureRmSubscription – 訂用帳戶 Id < your_subscription_Id >** (取代**< your_subscription_Id >**與實際的訂用帳戶 ID) 按**輸入**。 您會看到 hello 環境中，資訊**帳戶**， **TenantId**， **SubscriptionId**和**CurrentStorageAccount**。
7. 現在您已經準備就緒 toorun hello 指令碼。 按一下 hello**執行指令碼**按鈕或按**F5** hello 鍵盤上。

   ![執行 PowerShell 指令碼](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. hello 指令碼會要求**resourceGroupName:** -輸入 hello 名稱*資源群組*想 toouse，然後按下**ENTER**。 如果您沒有的話，請輸入您要 toouse 一個新名稱。 如果您已經有*資源群組*您想 toouse （例如 hello 其中所用虛擬機器)、 輸入 hello hello 現有的資源群組名稱。
9. hello 指令碼會要求**keyVaultName:** -輸入 hello hello 名稱*金鑰保存庫*toouse，然後按 ENTER 鍵。 如果您沒有的話，請輸入您要 toouse 一個新名稱。 如果您已經有您想 toouse 金鑰保存庫，輸入 hello 名稱 hello 現有*金鑰保存庫*。
10. hello 指令碼會要求**位置：** -輸入 hello 名稱 hello 位置中的 hello 想 tooencrypt VM 所在，然後按下**ENTER**。 如果您不記得 hello 位置，請回到 toostep #5。
11. hello 指令碼會要求**aadAppName:** -輸入 hello hello 名稱*Azure Active Directory*應用程式想 toouse，然後按下**ENTER**。 如果您沒有的話，請輸入您要 toouse 一個新名稱。 如果您已經有*Azure Active Directory 應用程式*您想 toouse、 輸入 hello 名稱 hello 現有*Azure Active Directory 應用程式*。
12. 此時會出現登入對話方塊。 提供您的認證 (是，您已登入一次，但現在您需要 toodo 再試一次)。
13. hello 指令碼執行和完成時它會要求您的 hello toocopy hello 值**aadClientID**， **aadClientSecret**， **diskEncryptionKeyVaultUrl**，和**keyVaultResourceId**。 每個這些值 toohello 剪貼簿複製並貼入 [記事本]。
14. 傳回 toohello PowerShell ISE，並將 hello 資料指標放在 hello 結尾 hello 最後一行，然後按**ENTER**。

hello hello 指令碼的輸出看起來應該像囉 」 畫面下方：

![PowerShell 輸出](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>加密 hello Azure 虛擬機器
您會 tooencrypt 現在準備好您的虛擬機器。 如果您的虛擬機器位於 hello 相同的資源群組，為您金鑰保存庫中，您可以移 toohello 加密步驟一節。 不過，如果您的虛擬機器不在 hello 相同資源群組為您金鑰保存庫，您必須在 hello PowerShell ISE 中的 hello 主控台 tooenter hello 下列：

**$resourceGroupName = <’Virtual_Machine_RG’>**

取代**< Virtual_Machine_RG >** hello hello 資源群組，其中會包含您的虛擬機器名稱，並以單引號括住。 然後按 **ENTER**鍵。
hello 正確輸入資源群組名稱中，輸入 hello PowerShell ISE 主控台 hello 下列 tooconfirm:

**$resourceGroupName**

按 **ENTER**鍵。 您應該會看到 hello 位於您的虛擬機器的資源群組名稱。 例如：

![PowerShell 輸出](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>加密步驟
首先，您需要 tootell PowerShell hello 名稱要 tooencrypt 的 hello 虛擬機器。 在 [hello] 主控台中，輸入：

**$vmName = <’your_vm_name’>**

取代**<'your_vm_name ' >** hello VM 名稱 （請確定 hello 名稱必須以括住的單引號），然後按**ENTER**。

tooconfirm hello 正確輸入 VM 名稱，請輸入：

**$vmName**

按 **ENTER**鍵。 您應該會看到 hello 名稱要 tooencrypt 的 hello 虛擬機器。 例如：

![PowerShell 輸出](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

有兩個方法 toorun hello 加密命令 tooencrypt 所有磁碟機 hello 虛擬機器上。 hello 第一種方法是下列命令在 PowerShell ISE 主控台 hello tootype hello:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

在輸入此命令後，按 **ENTER**鍵。

hello 第二種方法是 tooclick hello 指令碼窗格 （使用 hello PowerShell ISE 的 hello 上方窗格） 中，捲動 toohello hello 指令碼底部。 反白顯示 hello 上面所列的命令並再以滑鼠右鍵按一下它，然後按一下**執行選取項目**或按**F8** hello 鍵盤上。

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

不論 hello 方法使用，將會出現一個對話方塊通知您需要的 hello 作業 toocomplete 10-15 分鐘。 按一下 [是] 。

進行 hello 加密程序時，您可以傳回 toohello Azure 入口網站，並查看 hello hello 虛擬機器狀態。 在 hello hello 頁面的左側，按一下 **虛擬機器**，然後在 hello**虛擬機器**刀鋒視窗中，按一下您要加密的 hello 虛擬機器的 hello 名稱。 在出現的 hello 刀鋒視窗，您會發現該 hello**狀態**指出它是**更新**。 下圖展示進行中的加密。

![更多詳細 hello VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

傳回 toohello PowerShell ISE。 Hello 指令碼完成時，您會看到在 hello 圖中顯示的內容。

![PowerShell 輸出](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

hello 虛擬機器的 toodemonstrate 現在會加密，傳回 toohello Azure 入口網站，然後按一下**虛擬機器**上 hello hello 頁面的左側。 按一下 hello 加密 hello 虛擬機器名稱。 在 hello**設定**刀鋒視窗中，按一下 **磁碟**。

![設定選項](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

在 hello**磁碟**刀鋒視窗中，您會看到**加密**是**啟用**。

![磁碟屬性](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>後續步驟
在本文件中，您學到如何 tooencrypt Azure 虛擬機器。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)– 了解如何 toomonitor hello 您的 Azure 資源的健全狀況
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示
* [Azure 資訊安全中心常見問題集](security-center-faq.md)– 尋找使用 hello 服務相關的常見問題集
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) – 尋找有關 Azure 安全性與相容性的部落格文章
