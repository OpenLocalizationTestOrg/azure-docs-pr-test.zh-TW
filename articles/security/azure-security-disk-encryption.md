---
title: "aaaAzure 磁碟加密，適用於 Windows 和 Linux IaaS Vm |Microsoft 文件"
description: "本文提供 Windows 和 Linux IaaS VM 適用的 Microsoft Azure 磁碟加密概觀。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密
Microsoft Azure 是強式認可的 tooensuring 資料隱私權，資料 sovereignty 和 toocontrol 您的 Azure 託管可讓您透過的進階的技術 tooencrypt 範圍資料控制和管理加密金鑰控制和稽核資料的存取。 這會提供 Azure 客戶 hello 彈性 toochoose hello 解決方案以最符合其商務需求。 本文中，我們將介紹新技術解決方案 tooa 「 適用於 Windows 和 Linux IaaS VM 的 Azure 磁碟加密 」 toohelp 保護與防衛資料 toomeet 您組織的安全性與相容性承諾。 hello 紙張提供詳細的指引 toouse hello Azure 磁碟加密功能，包括 hello 如何支援案例和 hello 使用者經驗。

> [!NOTE]
> 某些建議可能會增加資料、網路或計算資源的使用量，導致額外的授權或訂用帳戶成本。

## <a name="overview"></a>概觀
Azure 磁碟加密是協助您加密 Windows 和 Linux IaaS 虛擬機器磁碟的新功能。 Azure 磁碟加密會利用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooprovide 磁碟區加密 hello OS 與 hello 資料磁碟的功能。 與整合 hello 方案[Azure 金鑰保存庫](https://azure.microsoft.com/documentation/services/key-vault/)toohelp 您控制和管理您金鑰保存庫的訂用帳戶中的 hello 磁碟加密金鑰和密碼。 hello 方案也能確保 hello 虛擬機器磁碟上的所有資料會留在您 Azure 儲存體都加密。

Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密現已在所有 Azure 公用區域和 AzureGov 區域**正式推出**，可供用於標準 VM 和具有高階儲存體的 VM。

### <a name="encryption-scenarios"></a>加密案例
hello Azure 磁碟加密解決方案支援下列客戶案例 hello:

* 對透過加密的 VHD 和加密金鑰建立的新 IaaS VM 啟用加密
* 在 從支援的 hello Azure 資源庫映像建立新的 IaaS Vm 上啟用加密
* 在 Azure 中執行的現有 IaaS VM 上啟用加密
* 在 Windows IaaS VM 上停用加密
* 在 Linux IaaS VM 的資料磁碟機上停用加密
* 允許加密受管理磁碟 VM
* 現有已加密非高階儲存體 VM 的更新加密設定
* 備份與還原以金鑰加密金鑰進行加密的已加密 VM

hello 解決方案支援 IaaS Vm 的下列案例，當啟用 Microsoft Azure 中的 hello:

* 與 Azure 金鑰保存庫整合
* 標準層 VM：[A、D、DS、G、GS、F 等系列 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)
* 在 Windows 和 Linux IaaS Vm 和 hello 從受管理的磁碟 Vm 上啟用加密支援 Azure 資源庫映像
* 在 Windows IaaS VM 與受管理磁碟 VM 的作業系統與資料磁碟機上停用加密
* 在 Linux IaaS VM 與受管理磁碟 VM 的資料磁碟機上停用加密
* 在執行 Windows Client OS 的 IaaS VM 上啟用加密
* 在具有掛接路徑的磁碟區上啟用加密
* 使用 mdadm 在設定了磁碟串接 (RAID) 的 Linux VM 上啟用加密
* 使用資料磁碟適用的 LVM 在 Linux VM 上啟用加密
* 在設定了儲存空間的 Windows VM 上啟用加密
* 現有已加密非高階儲存體 VM 的更新加密設定
* 支援所有 Azure 公用區域與 AzureGov 區域

hello 方案不支援下列案例、 功能和技術的 hello:

* 基本層 IaaS VM
* 在 Linux IaaS VM 的 OS 磁碟機上停用加密
* 停用加密資料磁碟機上的，如果 hello 作業系統磁碟機已加密適用於 Linux Iaas Vm
* 使用 hello 傳統 VM 建立方法所建立的 IaaS Vm
* 「不」支援透過 Windows 和 Linux IaaS VM 客戶自訂映像上啟用加密。 目前不支援在 Linux LVM OS 磁碟機上啟用加密。 此支援會立即出現。
* 與您的內部部署金鑰管理服務整合
* Azure 檔案 (共用檔案系統)、網路檔案系統 (NFS)、動態磁碟區和以軟體型 RAID 系統所設定的 Windows VM
* 備份與還原不以金鑰加密金鑰進行加密的已加密 VM。
* 現有已加密高階儲存體 VM 的更新加密設定。

> [!NOTE]
> 備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。 未使用 KEK 加密的 VM 則不支援。 KEK 是啟用 VM 加密的選擇性參數。 即將提供此支援。
> 不支援現有已加密高階儲存體 VM 的更新加密設定。 即將提供此支援。

### <a name="encryption-features"></a>加密功能
當您啟用並部署 Azure IaaS Vm 的 Azure 磁碟加密時，hello 下列功能已啟用，根據提供的 hello 組態：

* Hello OS 磁碟區 tooprotect hello 開機磁碟區的存放裝置中的靜止的加密
* 資料磁碟區 tooprotect hello 資料磁碟區的存放裝置中的靜止的加密
* 適用於 Windows 的 IaaS Vm 停用加密 hello OS 和資料磁碟機
* 停用加密 hello 的資料磁碟機適用於 Linux IaaS Vm （只有當作業系統不是加密磁碟機）
* 保護 hello 加密金鑰和金鑰保存庫訂用帳戶中的密碼
* 報告 hello hello 加密狀態加密 IaaS VM
* 磁碟加密組態設定從 hello IaaS 虛擬機器之移除
* 備份和還原的加密 Vm 使用 hello Azure 備份服務

> [!NOTE]
> 備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。 未使用 KEK 加密的 VM 則不支援。 KEK 是啟用 VM 加密的選擇性參數。

Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密解決方案包含：

* 適用於 Windows hello 磁碟加密延伸模組。
* 適用於 Linux hello 磁碟加密延伸模組。
* hello 磁碟加密 PowerShell 指令程式。
* hello 磁碟加密 Azure 命令列介面 (CLI) cmdlet。
* hello 磁碟加密 Azure Resource Manager 範本。

hello Azure 磁碟加密解決方案可支援執行 Windows 或 Linux 作業系統的 IaaS Vm。 如需支援的 hello 作業系統的詳細資訊，請參閱 hello < 先決條件 > 一節。

> [!NOTE]
> 使用 Azure 磁碟加密來加密 VM 磁碟完全免費。

### <a name="value-proposition"></a>價值主張
當您套用 hello Azure 磁碟加密管理解決方案時，可以滿足下列商務需求的 hello:

* IaaS Vm 保護待用，因為您可以使用業界標準加密技術 tooaddress 組織的安全性與相容性的需求。
* IaaS VM 會在客戶控制的金鑰和原則下開機，且您可以在金鑰保存庫中稽核其使用狀況。

### <a name="encryption-workflow"></a>加密工作流程
適用於 Windows 和 Linux Vm tooenable 磁碟加密 hello 遵循：

1. 選擇加密的情況下從 hello 之前加密案例。
2. 參加 tooenabling 磁碟加密透過 hello Azure 磁碟加密 Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令，並指定 hello 加密組態。

   * Hello 客戶加密 VHD 案例中上, 傳加密的 hello VHD tooyour 儲存體帳戶和 hello 加密金鑰材料 tooyour 金鑰保存庫。 然後，提供新的 IaaS VM 上的 hello 加密組態 tooenable 加密。
   * 針對新的 Vm 中建立的 hello Marketplace 並已在 Azure 中執行的現有 Vm，提供 hello 加密組態 tooenable 加密上 hello IaaS VM。

3. 授與存取 toohello Azure 平台 tooread hello 加密金鑰材料 （BitLocker 加密金鑰的 Windows 系統），適用於 Linux 的複雜密碼從您的金鑰保存庫 tooenable 加密 hello IaaS VM 上。

4. 提供 hello Azure Active Directory (Azure AD) 應用程式識別 toowrite hello 加密金鑰材料 tooyour 金鑰保存庫。 如此可讓上述步驟 2 中的 hello 案例 hello IaaS VM 上的加密。

5. Azure 會加密與 hello 金鑰保存庫設定，會更新 hello VM 服務模型，並設定加密 VM。

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>解密工作流程
對於 IaaS Vm，完成下列高層級步驟的 hello toodisable 磁碟加密：

1. 在 Azure 中執行的 IaaS VM 上選擇 toodisable 加密 （解密），透過 hello Azure 磁碟加密 Resource Manager 範本或 PowerShell 指令程式，並指定 hello 解密組態。

 此步驟會停用加密 hello OS 或 hello 資料磁碟區上或兩者都執行 Windows IaaS VM 的 hello。 不過，如 hello 前一節中所述，停用作業系統磁碟加密 for Linux 不支援。 hello 解密步驟只適用於 Linux Vm 上的資料磁碟機，只要 hello OS 磁碟不會加密。
2. 更新 azure hello VM 服務模型，且會標示解密 hello IaaS VM。 hello VM hello 內容已不再加密在靜止。

> [!NOTE]
> hello 停用加密作業不會刪除您金鑰保存庫和 hello 加密金鑰內容 （BitLocker 加密金鑰適用於 Windows 系統） 或適用於 Linux 的複雜密碼。
 > 不支援停用 Linux 適用的作業系統磁碟加密。 hello 解密步驟只適用於 Linux Vm 上的資料磁碟機。
不支援停用適用於 Linux 的資料磁碟加密，如果 hello 作業系統磁碟機已加密。

## <a name="prerequisites"></a>必要條件
您可以啟用 Azure IaaS Vm 上的 Azure 磁碟加密 hello < 概觀 > 一節中所討論的 hello 支援案例之前，請參閱 hello 下列必要條件：

* 您必須擁有有效的作用中 Azure 訂用 toocreate 資源 hello 支援地區的 Azure 中。
* 支援 azure 磁碟加密： hello 遵循 Windows Server 版本： Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2 和 Windows Server 2016。
* 支援 azure 磁碟加密： hello 遵循 Windows 用戶端版本： Windows 8 用戶端和 Windows 10 用戶端。

> [!NOTE]
> 針對 Windows Server 2008 R2，您必須先安裝 .NET Framework 4.5，才能在 Azure 中啟用加密。 安裝從 Windows Update 安裝 hello 選用更新適用於 Windows Server 2008 R2 x64 型系統的 Microsoft.NET Framework 4.5.2 ([KB2901983](https://support.microsoft.com/kb/2901983))。

* 支援 azure 磁碟加密 hello 下列 Azure 資源庫依據的 Linux 伺服器發行，版本：

| Linux 散發套件 | 版本 | 支援加密的磁碟區類型|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | 作業系統和資料磁碟 |
| Ubuntu | 14.04.5-DAILY-LTS | 作業系統和資料磁碟 |
| Ubuntu | 12.10 | 資料磁碟 |
| Ubuntu | 12.04 | 資料磁碟 |
| RHEL | 7.3 | 作業系統和資料磁碟 |
| RHEL | 7.2 | 作業系統和資料磁碟 |
| RHEL | 6.8 | 作業系統和資料磁碟 |
| RHEL | 6.7 | 資料磁碟 |
| CentOS | 7.3 | 作業系統和資料磁碟 |
| CentOS | 7.2n | 作業系統和資料磁碟 |
| CentOS | 6.8 | 作業系統和資料磁碟 |
| CentOS | 7.1 | 資料磁碟 |
| CentOS | 7.0 | 資料磁碟 |
| CentOS | 6.7 | 資料磁碟 |
| CentOS | 6.6 | 資料磁碟 |
| CentOS | 6.5 | 資料磁碟 |
| openSUSE | 13.2 | 資料磁碟 |
| SLES | 12 SP1 | 資料磁碟 |
| SLES | 12-SP1 (高階) | 資料磁碟 |
| SLES | HPC 12 | 資料磁碟 |
| SLES | 11-SP4 (高階) | 資料磁碟 |
| SLES | 11 SP4 | 資料磁碟 |

* Azure 磁碟加密需要，您的金鑰保存庫和 Vm 位於 hello 相同 Azure 地區和訂用帳戶。

> [!NOTE]
> 在不同的區域中設定 hello 資源會導致失敗啟用 hello Azure 磁碟加密 」 功能。

* tooset 和 Azure 磁碟加密設定金鑰保存庫，請參閱 > 一節**設定安裝及設定 Azure 磁碟加密金鑰保存庫**在 hello*必要條件*本文一節。
* tooset 和設定 Azure Active directory 中的 Azure AD 應用程式，Azure 磁碟加密，請參閱 > 一節**設定 Azure Active Directory 中的 hello Azure AD 應用程式**在 hello*必要條件*本文一節。
* tooset 和設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則，請參閱 > 一節**設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則**在 hello*必要條件*區段這篇文章。
* tooprepare 預先加密的 Windows VHD，請參閱 > 一節**準備預先加密的 Windows VHD**在 hello*附錄*。
* tooprepare 預先加密的 Linux VHD，請參閱 > 一節**準備預先加密的 Linux VHD**在 hello*附錄*。
* hello Azure 平台需要存取 toohello 加密金鑰或密碼中您金鑰保存庫 toomake 它們可用 toohello 虛擬機器開機和解密 hello 虛擬機器作業系統磁碟區時。 toogrant 權限 tooAzure 平台組 hello **EnabledForDiskEncryption** hello 金鑰保存庫中的屬性。 如需詳細資訊，請參閱**設定安裝及設定 Azure 磁碟加密金鑰保存庫**hello 附錄中。
* 您的金鑰保存庫密碼和 KEK URL 必須已設定版本。 Azure 會強制執行設定版本的這項限制。 有效的密碼及 KEK Url，請參閱下列範例中的 hello:

  * 有效祕密 URL 的範例︰https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  * 有效 KEK URL 的範例：https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

* Azure 磁碟加密不支援將連接埠號碼指定為金鑰保存庫密碼和 KEK URL 的一部分。 如需不支援和支援的金鑰保存庫 Url 的範例，請參閱 hello 下列：

  * 無法接受的金鑰保存庫 URL https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  * 可接受的金鑰保存庫 URL：https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

* tooenable hello Azure 磁碟加密 」 功能，hello IaaS Vm 必須符合下列網路端點的組態需求的 hello:
  * tooget 語彙基元 tooconnect tooyour 金鑰保存庫，hello IaaS VM 必須是 Azure Active Directory 無法 tooconnect tooan 的端點， \[login.microsoftonline.com\]。
  * toowrite hello 加密金鑰 tooyour 金鑰保存庫，hello IaaS VM 必須是能夠 tooconnect toohello 金鑰保存庫端點。
  * hello IaaS VM 必須能夠 tooconnect tooan Azure 儲存體端點主機 hello Azure 延伸模組儲存機制和主機 hello VHD 檔案的 Azure 儲存體帳戶。

  > [!NOTE]
  > 如果您的安全性原則會限制從 Azure Vm toohello 網際網路存取，您可以解決 hello 前面的 URI，並設定特定規則 tooallow 的傳出連線 toohello Ip。
  >
  >tooconfigure 和防火牆 (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) 存取 Azure 金鑰保存庫

* 使用 Azure PowerShell SDK 版本 tooconfigure Azure 磁碟加密 hello 最新版本。 下載 hello 最新版本[Azure PowerShell 版本](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > [Azure PowerShell SDK 1.1.0 版](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)不支援 Azure 磁碟加密。 如果您收到錯誤與相關 toousing Azure PowerShell 1.1.0，請參閱[Azure 磁碟加密相關錯誤 tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)。

* toorun 任何 Azure CLI 命令並將它與您 Azure 訂用帳戶產生關聯，您必須先安裝 Azure CLI:
  * tooinstall Azure CLI 和與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 及設定 Azure CLI](../cli-install-nodejs.md)。
  * toouse Azure CLI Mac、 Linux 和 Windows 使用 Azure 資源管理員中，請參閱[Resource Manager 模式中的 Azure CLI 命令](../virtual-machines/azure-cli-arm-commands.md)。

* 加密受管理的磁碟，時必要的先決條件 tootake hello 管理磁碟的快照集或 Azure 磁碟加密先前 tooenabling 加密之外的 hello 磁碟的備份。  若未備妥備份，任何未預期的失敗期間加密可能會讓 hello 磁碟和 VM 不含修復選項無法存取。  設定 AzureRmVMDiskEncryptionExtension 目前未不受管理的磁碟備份，然後會發生錯誤，如果使用針對受管理的磁碟，除非已指定 hello-skipVmBackup 參數。  這個參數是不安全的 toouse 除非之外 Azure 磁碟加密已進行過備份。   指定 hello-skipVmBackup 參數時，hello cmdlet 不會使受管理的 hello 磁碟先前 tooencryption 的備份。  基於這個理由，則會視為確定 hello 受管理磁碟 VM 處於位置先前 tooenabling Azure 磁碟加密修復是更新的備份所需的必要先決條件 toomake。  
> [!NOTE]
 > 除非快照集或備份已發出 Azure 磁碟加密外，應該永遠不會使用 hello-skipVmBackup 參數。 

* hello Azure 磁碟加密解決方案會使用適用於 Windows 的 IaaS Vm hello BitLocker 外部金鑰保護裝置。 對於加入網域的 VM，請勿推送任何會強制使用 TPM 保護裝置的群組原則。 在不含相容 TPM 的允許 BitLocker"hello 群組原則的相關資訊，請參閱[BitLocker 群組原則參考](https://technet.microsoft.com/library/ee706521)。
* 已加入網域的虛擬機器上的 Bitlocker 原則的自訂群組原則必須包含下列設定的 hello:`Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`當 Azure 磁碟加密 Bitlocker 的自訂群組原則設定不相容時，將會失敗。 在沒有 hello 的機器上可能需要正確的原則設定，套用 hello 新原則，強制新原則 tooupdate hello (gpupdate.exe /force) 並再重新啟動。  
* toocreate Azure AD 應用程式中，建立金鑰保存庫，或設定現有的金鑰保存庫並啟用加密，請參閱 hello[必要條件 PowerShell 指令碼的 Azure 磁碟加密](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)。
* 請參閱 < 使用 Azure CLI hello tooconfigure 磁碟加密必要條件[此 Bash 指令碼](https://github.com/ejarvi/ade-cli-getting-started)。
* toouse hello Azure 備份服務 tooback 向上及還原加密的 Vm，啟用加密時使用 Azure 磁碟加密，請使用 hello Azure 磁碟加密金鑰組態來加密您的 Vm。 hello 備份服務支援 KEK 設定只會使用加密的 Vm。 請參閱[tooback 向上及還原加密使用 Azure 備份加密的虛擬機器](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)。

* 加密的 Linux 作業系統磁碟區，請注意，在 VM 重新啟動目前需要在 hello hello 程序的結尾。 這可以透過 hello 入口網站、 powershell 或 CLI 來完成。   tootrack hello 進度的加密，會定期輪詢 hello Get AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus 所傳回的狀態訊息。  一旦完成加密，此命令傳回 hello hello 狀態訊息會指出這。  例如，"ProgressMessage： 成功地加密作業系統磁碟，請重新啟動 hello VM"在 VM 可重新啟動及使用此點 hello。  

* 適用於 Linux 的 azure 磁碟加密要求資料磁碟 toohave Linux 先前 tooencryption 掛接的檔案系統

* 以遞迴方式掛接的磁碟不會受到 hello Azure 磁碟加密適用於 Linux 的資料。 例如，如果 hello 目標系統已掛接的磁碟上 /foo/bar，然後另 /foo/bar/baz，/foo/bar/baz hello 加密將會成功，但加密/foo/列將會失敗。 

* Azure 磁碟加密才支援在符合 hello 上述必要條件的支援的 Azure 資源庫映像上。 由於 toocustom 資料分割配置和處理程序的行為可能存在於這些映像不支援客戶的自訂映像。 此外，即使以資源庫映像為基礎的 VM 一開始符合必要條件，但如果該 VM 在建立之後做過修改，則也可能會變得不相容。  ，因此，hello 建議加密 Linux VM 的程序是從全新的組件庫映像 toostart、 加密 hello VM，然後再將自訂軟體或資料 toohello 所需的 VM。  

> [!NOTE]
> 備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。 未使用 KEK 加密的 VM 則不支援。 KEK 是啟用 VM 的選擇性參數。

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Hello Azure AD 應用程式中設定 Azure Active Directory
當您需要在 Azure 中執行中的 VM 上啟用加密 toobe 時，會產生 Azure 磁碟加密，並寫入 hello 加密金鑰 tooyour 金鑰保存庫。 在金鑰保存庫中管理加密金鑰需要 Azure AD 驗證。

基於此目的，請建立 Azure AD 應用程式。 您可以找到詳細的步驟槲崞紵錭 hello 「 hello 應用程式取得身分識別 」 一節中 hello 部落格文章[Azure 金鑰保存庫-Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)。 這篇文章也包含一些有關安裝及設定金鑰保存庫的實用範例。 針對驗證目的，您可以使用用戶端密碼式驗證或用戶端憑證式 Azure AD 驗證。

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Azure AD 的用戶端密碼式驗證
hello 以下各節可協助您設定 Azure AD 的用戶端密碼型驗證。

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>使用 Azure PowerShell 來建立 Azure AD 應用程式
使用下列 PowerShell 指令程式 toocreate Azure AD 應用程式的 hello:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId hello Azure AD ClientID，而 $aadClientSecret hello 用戶端密碼，您應該使用更新版本 tooenable Azure 磁碟加密。 適當地保護 hello Azure AD 用戶端密碼。

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>從 hello Azure 傳統入口網站設定 hello Azure AD 用戶端識別碼和密碼
您也可以設定您的 Azure AD 用戶端識別碼和密碼使用 hello [Azure 傳統入口網站]( https://manage.windowsazure.com)。 tooperform 這項工作，請勿遵循 hello:

1. 按一下 hello **Active Directory**  索引標籤。

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. 按一下**新增應用程式**，然後類型 hello 應用程式的名稱。

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. 按一下 hello 箭號按鈕，然後設定 hello 應用程式屬性。

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. 按一下 hello 較低的左上的角 toofinish hello 核取記號。 hello 應用程式組態 頁面隨即出現，並在 hello hello 頁面底部會顯示 hello Azure AD 用戶端識別碼。

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. 按一下 hello 儲存 hello Azure AD 用戶端密碼**儲存** 按鈕。 請注意在 hello 索引鍵 文字方塊中的 hello Azure AD 用戶端密碼。 適當地保護該密碼。

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > hello Azure 傳統入口網站不支援 hello 上述流程。

##### <a name="use-an-existing-application"></a>使用現有的應用程式
tooexecute hello 下列命令，取得及使用 hello [Azure AD PowerShell 模組](https://technet.microsoft.com/library/jj151815.aspx)。

> [!NOTE]
> hello 下列命令必須從執行新的 PowerShell 視窗。 請勿使用 Azure PowerShell 或 hello Azure 資源管理員視窗 tooexecute hello 命令。 我們建議您使用這種方法，因為這些 cmdlet 在 hello MSOnline 模組或 Azure AD PowerShell。

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Azure AD 的憑證式驗證
> [!NOTE]
> Linux VM 目前不支援 Azure AD 憑證式驗證。

hello 以下各節顯示如何 tooconfigure Azure AD 的憑證式驗證。

##### <a name="create-an-azure-ad-application"></a>建立 Azure AD 應用程式
toocreate Azure AD 應用程式中，執行下列 PowerShell 指令程式的 hello:

> [!NOTE]
> 取代下列 hello`yourpassword`安全密碼，並保護 hello 密碼的字串。

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

在您完成此步驟之後上, 傳 PFX 檔案 tooyour 金鑰保存庫，並讓 hello 存取所需的原則 toodeploy 該憑證 tooa VM。

##### <a name="use-an-existing-azure-ad-application"></a>使用現有的 Azure AD 應用程式
如果您要設定現有的應用程式的憑證驗證，請使用如下所示的 hello PowerShell cmdlet。 要確定 tooexecute 其新的 PowerShell 視窗。

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

在您完成此步驟之後上, 傳 PFX 檔案 tooyour 金鑰保存庫，並啟用 hello toodeploy hello 憑證 tooa VM 所需的存取原則。

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>上傳 PFX 檔案 tooyour 金鑰保存庫
此程序的詳細說明，請參閱[hello 官方 Azure 金鑰保存庫團隊部落格](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)。 不過，hello 下列 PowerShell 指令程式是您只需要 hello 工作。 要確定 tooexecute 從 Azure PowerShell 主控台。

> [!NOTE]
> 取代下列 hello`yourpassword`安全密碼，並保護 hello 密碼的字串。

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>部署您的金鑰保存庫 tooan 現有的 VM 中的憑證
完成上傳 hello PFX 之後，部署 hello 金鑰保存庫 tooan hello 下列現有 VM 中的憑證：
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則
Azure AD 應用程式需要權限 tooaccess hello 金鑰或 hello 保存庫中的密碼。 使用 hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant toohello 應用程式權限，使用 hello 用戶端識別碼 （這產生 hello 應用程式註冊時） 為 hello _– ServicePrincipalName_參數值。 toolearn 詳細資訊，請參閱 hello 部落格文章[Azure 金鑰保存庫-Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)。 以下是範例如何 tooperform 這工作透過 PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Azure 磁碟加密會需要下列存取原則 tooyour Azure AD 用戶端應用程式的 tooconfigure hello: _WrapKey_和_設定_權限。

## <a name="terminology"></a>術語
toounderstand 某些 hello 的通用詞彙使用這項技術，使用 hello 下術語表：

| 術語 | 定義 |
| --- | --- |
| Azure AD | Azure AD 是 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)。 Azure AD 帳戶是從金鑰保存庫驗證、儲存和擷取密碼的必要條件。 |
| Azure 金鑰保存庫 | Key Vault 是密碼編譯金鑰管理服務，它是基於美國聯邦資訊處理標準 (FIPS) 驗證的硬體安全性模組，可協助您保護密碼編譯金鑰和敏感性密碼。 如需詳細資訊，請參閱 [Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。 |
| ARM | Azure Resource Manager |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx)是業界公認的 Windows 磁碟區加密技術，Windows IaaS Vm 上已使用 tooenable 磁碟加密。 |
| BEK | BitLocker 加密金鑰是使用的 tooencrypt hello OS 開機磁碟區和資料磁碟區。 hello BitLocker 金鑰會受金鑰保存庫中，為機密資料。 |
| CLI | 請參閱 [Azure 命令列介面](../cli-install-nodejs.md)。 |
| DM-Crypt |[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt)是 Linux IaaS Vm 已使用 tooenable 磁碟加密的 hello 以 Linux 為基礎、 透明磁碟加密子系統。 |
| KEK | Hello 非對稱金鑰 (RSA 2048)，您可以使用 tooprotect 或換行 hello 秘密金鑰加密金鑰。 您可以提供硬體安全性模組 (HSM) 保護的金鑰或軟體保護的金鑰。 如需詳細資訊，請參閱 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。 |
| PS Cmdlet | 請參閱 [Azure PowerShell Cmdlet](/powershell/azure/overview)。 |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>針對 Azure 磁碟加密安裝及設定您的金鑰保存庫
Azure 磁碟加密協助保護 hello 磁碟加密金鑰和金鑰保存庫中的密碼。 Azure 磁碟加密金鑰保存庫註冊 tooset，完成 hello 每 hello 下列各節中的步驟。

#### <a name="create-a-key-vault"></a>建立金鑰保存庫
toocreate 金鑰保存庫，可使用其中一種 hello 下列選項：

* ["101-Key-Vault-Create" Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Azure PowerShell 金鑰保存庫 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* 如何太[安全金鑰保存庫](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> 如果您已經有設定金鑰保存庫，您訂用帳戶，略過 toohello 下一節。

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>設定金鑰加密金鑰 (選擇性)
如果您想要 toouse KEK 額外的 hello BitLocker 加密金鑰的安全性，新增 KEK tooyour 金鑰保存庫。 使用 hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello 金鑰保存庫中的加密金鑰。 您也可以從內部部署金鑰管理 HSM 匯入 KEK。 如需詳細資訊，請參閱 [Key Vault 文件](https://azure.microsoft.com/documentation/services/key-vault/)。

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

您可以加入 hello KEK 移 tooAzure 資源管理員，或使用您金鑰保存庫的介面。

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>設定金鑰保存庫的權限
hello Azure 平台需要存取 toohello 加密金鑰或密碼中您金鑰保存庫 toomake 它們可用 toohello 開機和解密 hello 磁碟區的 VM。 toogrant 權限 toohello Azure 平台組 hello **EnabledForDiskEncryption** hello 機碼中的屬性保存庫使用 hello 金鑰保存庫 PowerShell cmdlet:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

您也可以設定 hello **EnabledForDiskEncryption**屬性，方法是瀏覽 hello [Azure 資源總管](https://resources.azure.com)。

如先前所述，您必須設定 hello **EnabledForDiskEncryption**金鑰保存庫上的屬性。 否則，hello 部署將會失敗。

您可以設定存取原則的 Azure AD 應用程式與 hello 金鑰保存庫的介面，如下所示：

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

在 hello**進階存取權原則**索引標籤上，請確定您的金鑰保存庫已啟用 Azure 磁碟加密：

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>磁碟加密部署案例和使用者體驗
您可以啟用多個磁碟加密案例，並 hello 步驟可能會相應 toohello 案例而有所不同。 hello 下列各節涵蓋 hello 更詳細的案例。

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>在新建立的 hello Marketplace IaaS Vm 上啟用加密
您可以啟用 hello Azure 中的服務商場中的新 IaaS Windows VM 上的磁碟加密使用 hello [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)。

1. Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。

2. Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密新的 IaaS VM 上。

> [!NOTE]
> 此範本會建立新的加密的 Windows VM 使用 Windows Server 2012 hello 資源庫映像。

您可以使用此 [Resource Manager 範本](https://aka.ms/fde-rhel)，在具有 200 GB RAID-0 陣列的新 IaaS RedHat Linux 7.2 VM 上啟用磁碟加密。 部署 hello 範本之後，請使用 hello 確認 hello VM 加密狀態`Get-AzureRmVmDiskEncryptionStatus`cmdlet，如中所述[加密作業系統磁碟機上執行的 Linux VM](#encrypting-os-drive-on-a-running-linux-vm)。 Hello 機器時傳回狀態_VMRestartPending_，重新啟動 hello VM。

hello 下表列出 hello 資源管理員範本參數的新 Vm 從 hello Marketplace 案例使用 Azure AD 用戶端識別碼：

| 參數 | 說明 |
| --- | --- |
| adminUserName | Hello 虛擬機器的系統管理員使用者名稱。 |
| adminPassword | Hello 虛擬機器的系統管理員使用者密碼。 |
| newStorageAccountName | Hello 儲存體帳戶 toostore OS 和資料 Vhd 的名稱。 |
| vmSize | Hello VM 的大小。 目前僅支援標準的 A、D 和 G 系列。 |
| virtualNetworkName | Hello VNet 該 hello VM NIC 的名稱都必須屬於。 |
| subnetName | Hello 在 hello VNet 該 hello VM NIC 的子網路名稱都必須屬於。 |
| AADClientID | Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端識別碼。 |
| AADClientSecret | Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端密碼。 |
| keyVaultURL | URL 的 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。 您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`。 |
| keyEncryptionKeyURL | URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰 （選擇性）。 |
| keyVaultResourceGroup | Hello 金鑰保存庫的資源群組。 |
| vmName | Hello hello 加密作業的 VM 名稱是 toobe 上執行。 |

> [!NOTE]
> _KeyEncryptionKeyURL_ 是選擇性參數。 您可以整合您自己 KEK toofurther 保護 hello 資料加密金鑰 （複雜密碼） 在金鑰保存庫中。

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>在透過客戶加密 VHD 和加密金鑰所建立的新 IaaS VM 上啟用加密
在此案例中，您可以啟用加密使用 hello Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令。 hello 下列各節說明在更詳細的 hello Resource Manager 範本和 CLI 命令。

從其中一個預先加密可以在 Azure 中使用的映像準備陳述式的這些章節，請遵循 hello 指示。 建立 hello 映像之後，您可以使用下一個區段 toocreate hello 加密的 Azure VM 中的 hello 步驟。

* [準備已預先加密的 Windows VHD](#preparing-a-pre-encrypted-windows-vhd)
* [準備已預先加密的 Linux VHD](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>使用 hello Resource Manager 範本
您也可以使用 hello 加密 VHD 上啟用磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)。

1. Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。

2. Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密 hello 新 IaaS VM。

hello 下表列出 hello 資源管理員範本參數的加密 VHD:

| 參數 | 說明 |
| --- | --- |
| newStorageAccountName | 名稱的 hello 儲存體帳戶 toostore hello 加密 OS VHD。 這個儲存體帳戶應該已經建立 hello 中相同的資源群組和 hello VM 相同的位置。 |
| osVhdUri | Hello OS VHD 從 hello 儲存體帳戶的 URI。 |
| osType | 作業系統產品類型 (Windows/Linux)。 |
| virtualNetworkName | Hello VNet 該 hello VM NIC 的名稱都必須屬於。 hello 名稱應該已經建立 hello 中相同的資源群組和 hello VM 相同的位置。 |
| subnetName | Hello hello VNet 該 hello VM NIC 上的子網路名稱都必須屬於。 |
| vmSize | Hello VM 的大小。 目前僅支援標準的 A、D 和 G 系列。 |
| keyVaultResourceID | hello ResourceID 識別 hello Azure 資源管理員中的金鑰保存庫資源。 您可以使用 hello PowerShell cmdlet 來取得`(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`。 |
| keyVaultSecretUrl | 設定 hello 金鑰保存庫中的 hello 磁碟加密金鑰的 URL。 |
| keyVaultKekUrl | Hello hello 產生磁碟加密金鑰加密的金鑰的加密金鑰的 URL。 |
| vmName | Hello IaaS VM 的名稱。 |

#### <a name="using-powershell-cmdlets"></a>使用 PowerShell Cmdlet
您也可以使用 hello PowerShell cmdlet 在您已加密的 VHD 上啟用磁碟加密[ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk)。  

#### <a name="using-cli-commands"></a>使用 CLI 命令
tooenable 磁碟加密，此案例中使用 CLI 命令，不要 hello 遵循：

1. 設定金鑰保存庫的存取原則：

   * 設定 hello **EnabledForDiskEncryption**旗標：

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * 設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. 在現有或未執行 VM，型別上 tooenable 加密：

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. 取得加密狀態：

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. 新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>在 Azure 中現有或執行中的 IaaS Windows VM 上啟用加密
在此案例中，您可以啟用加密使用 hello Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令。 hello 下列各節詳細說明如何 tooenable 它使用 hello Resource Manager 範本和 CLI 命令。

#### <a name="using-hello-resource-manager-template"></a>使用 hello Resource Manager 範本
您可以啟用現有的或使用 hello 在 Azure 中執行 IaaS Windows Vm 上的磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)。

1. Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。

2. Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable hello 現有或執行 IaaS VM 上的加密。

hello 下表列出針對現有的或執行 Vm 所使用的 Azure AD 用戶端識別碼 hello 資源管理員範本參數：

| 參數 | 說明 |
| --- | --- |
| AADClientID | Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端識別碼。 |
| AADClientSecret | Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端密碼。 |
| keyVaultName | 名稱 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。 您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`。 |
|  keyEncryptionKeyURL | URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰。 這個參數是選擇性，如果您選取**nokek** hello UseExistingKek 下拉式清單中。 如果您選取**kek**在 hello UseExistingKek 下拉式清單中，您必須輸入 hello _keyEncryptionKeyURL_值。 |
| volumeType | Hello 加密作業執行的磁碟區的類型。 有效值為 _OS_、_Data_ 和 _All_。 |
| sequenceVersion | 序列版的 hello BitLocker 作業。 每次磁碟加密作業不會對 hello 遞增此版本號碼相同的 VM。 |
| vmName | Hello hello 加密作業的 VM 名稱是 toobe 上執行。 |

> [!NOTE]
> _KeyEncryptionKeyURL_ 是選擇性參數。 您可以將自己 KEK toofurther 保護 hello 資料加密金鑰 （BitLocker 加密機密） 帶入 hello 金鑰保存庫中。

#### <a name="using-powershell-cmdlets"></a>使用 PowerShell Cmdlet
如需使用 PowerShell cmdlet 來啟用與 Azure 磁碟加密的加密資訊，請參閱 hello 部落格文章[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。

#### <a name="using-cli-commands"></a>使用 CLI 命令
在現有的或使用 CLI 命令，在 Azure 中執行 IaaS Windows VM 上 tooenable 加密 hello 遵循：

1. tooset hello 金鑰保存庫中的存取原則：
   * 設定 hello **EnabledForDiskEncryption**旗標：

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * 設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. 在現有或未執行 VM 上 tooenable 加密：

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. tooget 加密的狀態：

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. 新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>在 Azure 中現有或執行中的 IaaS Linux VM 上啟用加密
您可以啟用磁碟上現有的或執行 IaaS Linux VM 在 Azure 中的加密使用 hello [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)。

1. 按一下**部署 tooAzure** hello Azure 快速入門在範本上，輸入 hello 加密組態上 hello**參數**刀鋒視窗中，然後再按一下**確定**。

2. Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable hello 現有或執行 IaaS VM 上的加密。

hello 下表列出針對現有的或執行 Vm，使用 Azure AD 用戶端識別碼，資源管理員範本參數：

| 參數 | 說明 |
| --- | --- |
| AADClientID | Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端識別碼。 |
| AADClientSecret | Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端密碼。 |
| keyVaultName | 名稱 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。 您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`。 |
|  keyEncryptionKeyURL | URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰。 這個參數是選擇性，如果您選取**nokek** hello UseExistingKek 下拉式清單中。 如果您選取**kek**在 hello UseExistingKek 下拉式清單中，您必須輸入 hello _keyEncryptionKeyURL_值。 |
| volumeType | Hello 加密作業執行的磁碟區的類型。 支援的有效值為 _OS_ 或 _All_ (適用於 RHEL 7.2、CentOS 7.2 和 Ubuntu 16.04)，和 _Data_ (適用於所有其他的散發套件)。 |
| sequenceVersion | 序列版的 hello BitLocker 作業。 每次磁碟加密作業不會對 hello 遞增此版本號碼相同的 VM。 |
| vmName | Hello hello 加密作業的 VM 名稱是 toobe 上執行。 |
| passPhrase | 輸入強式複雜密碼做為 hello 資料加密金鑰。 |

> [!NOTE]
> _KeyEncryptionKeyURL_ 是選擇性參數。 您可以整合您自己 KEK toofurther 保護 hello 資料加密金鑰 （複雜密碼） 在金鑰保存庫中。

#### <a name="cli-commands"></a>CLI 命令
您可以啟用磁碟加密加密 VHD 上安裝和使用 hello [CLI 命令](../cli-install-nodejs.md)。 在現有的或使用 CLI 命令，在 Azure 中執行 IaaS Linux Vm 上 tooenable 加密 hello 遵循：

1. Hello 金鑰保存庫中設定存取原則：

 * 設定 hello **EnabledForDiskEncryption**旗標：

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * 設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. 在現有或未執行 VM 上 tooenable 加密：

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. 取得加密狀態：

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. 新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>取得加密的 IaaS VM hello 加密狀態
您可以使用 Azure 資源管理員，取得 hello 加密狀態[PowerShell cmdlet](/powershell/azure/overview)，或 CLI 命令。 hello 下列各節說明 toouse hello Azure 傳統入口網站和 CLI 命令 tooget hello 加密狀態。

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>使用 Azure 資源管理員取得加密的 Windows VM hello 加密狀態
您可以藉由 hello 下列取得 hello 加密的 hello IaaS VM 的狀態從 Azure 資源管理員：

1. 登入 toohello [Azure 傳統入口網站](https://portal.azure.com/)，然後按一下**虛擬機器**hello 左的窗格 toosee hello 您訂用帳戶中的虛擬機器的摘要檢視中。 您可以篩選 hello 虛擬機器 檢視中 hello 選取 hello 訂用帳戶名稱**訂用帳戶**下拉式清單。

2. 頂端的 hello hello**虛擬機器**頁面上，按一下**資料行**。

3. 在 hello**選擇資料行**刀鋒視窗中，選取**磁碟加密**，然後按一下**更新**。 您應該會看到 hello 磁碟加密資料行顯示 hello 加密狀態_啟用_或_未啟用_針對每個 VM，hello 遵循圖所示：

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>使用 hello 磁碟加密 PowerShell cmdlet 來取得 hello 加密的加密 (Windows/Linux) IaaS VM 的狀態
您可以從 hello 磁碟加密 PowerShell cmdlet 來取得 hello IaaS VM hello 加密狀態`Get-AzureRmVMDiskEncryptionStatus`。 tooget hello 加密設定，讓您的 VM，請輸入 hello 下列：

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

您可以檢查的 hello 輸出_Get AzureRmVMDiskEncryptionStatus_加密金鑰的 Url。

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

hello OSVolumeEncrypted 和 DataVolumesEncrypted 設定值會設定 too_Encrypted_，會顯示這兩個磁碟區使用 Azure 磁碟加密進行加密。 如需使用 PowerShell cmdlet 來啟用與 Azure 磁碟加密的加密資訊，請參閱 hello 部落格文章[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。

> [!NOTE]
> Linux Vm 上花費三 toofour 分鐘 hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello 加密狀態。

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>收到 hello 磁碟加密 CLI 命令的 hello IaaS VM 的 hello 加密狀態
您可以使用 hello 磁碟加密 CLI 命令，以取得 IaaS VM hello hello 加密狀態`azure vm show-disk-encryption-status`。 tooget hello 加密設定，讓您的 VM，請輸入您的 Azure CLI 工作階段：

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>在執行中 Windows IaaS VM 上停用加密
您可以停用加密透過 hello Azure 磁碟加密 Resource Manager 範本或 PowerShell cmdlet 執行的 Windows 或 Linux IaaS VM，並指定 hello 解密。

##### <a name="windows-vm"></a>Windows VM
hello 停用加密步驟會停用加密 hello OS、 hello 資料磁碟區，或兩者上執行 Windows IaaS VM 的 hello。 您無法停用 hello OS 磁碟區，並保留 hello 資料磁碟區加密。 Hello 停用加密步驟執行時，hello Azure 傳統部署模型更新 hello VM 的服務模型，且會標示解密 hello Windows IaaS VM。 hello VM hello 內容已不再加密在靜止。 hello 解密並不會刪除您金鑰保存庫和 hello 加密金鑰內容 （BitLocker 加密金鑰適用於 Windows 和 Linux 的複雜密碼）。

##### <a name="linux-vm"></a>Linux VM
hello 停用加密步驟會停用加密 hello hello 執行 Linux IaaS VM 上的資料量。 如果 hello OS 磁碟未加密，僅適用於此步驟。

> [!NOTE]
> 在 Linux Vm 上不允許停用加密 hello OS 磁碟上。

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>在現有或執行中 IaaS VM 上停用加密
您可以停用對於執行 Windows IaaS Vm 中使用 hello 磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)。

1. Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 解密組態**參數**刀鋒視窗中，然後再按一下**確定**。

2. Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密新的 IaaS VM 上。

適用於 Linux Vm，您可以使用停用加密 hello[停用執行中的 Linux VM 上的加密](https://aka.ms/decrypt-linuxvm)範本。

hello 下表列出用來停用加密，在執行中的 IaaS VM 上的資源管理員範本參數：

| 參數 | 說明 |
| --- | --- |
| vmName | Hello hello 加密作業的 VM 名稱是 toobe 上執行。
| volumeType | 執行解密作業所在磁碟區的類型。 有效值為 _OS_、_Data_ 和 _All_。 您無法停用加密不在執行上 Windows IaaS VM OS/開機磁碟區停用加密 hello_資料_磁碟區。 也請注意，停用加密 hello OS 磁碟上不允許在 Linux Vm 上。 |
| sequenceVersion | 序列版的 hello BitLocker 作業。 每次磁碟解密作業不會對 hello 遞增此版本號碼相同的 VM。 |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>在現有或執行中 IaaS VM 上停用加密
toodisable 加密上現有的或執行 IaaS VM 使用 hello PowerShell cmdlet，請參閱[ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)。 此 Cmdlet 同時支援 Windows 和 Linux VM。 toodisable 加密，它會在 hello 虛擬機器上安裝擴充功能。 如果 hello_名稱_未指定參數，hello 預設名稱的延伸模組_Windows Vm AzureDiskEncryption_建立。

在 Linux Vm 上使用 hello AzureDiskEncryptionForLinux 延伸模組。

> [!NOTE]
> 此 cmdlet 會重新啟動 hello 虛擬機器。

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>在具有 Azure 受管理磁碟且預先加密的 IaaS VM 上啟用加密
使用加密的 VM，從使用 hello ARM 範本預先加密的 VHD 位於 hello Azure 受管理磁碟臂範本 toocreate   
[從預先加密的 VHD/儲存體 blob 建立新的已加密受管理磁碟] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>在具有 Azure 受管理磁碟的新 Linux IaaS VM 上啟用加密
使用新的加密使用 hello ARM 範本位於 Linux IaaS VM 的 hello Azure 受管理磁碟臂範本 toocreate   
[使用完整磁碟加密部署 RHEL 7.2] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>在具有 Azure 受管理磁碟的新 Windows IaaS VM 上啟用加密
 使用新的加密使用 hello ARM 範本位於 Linux IaaS VM 的 hello Azure 受管理磁碟臂範本 toocreate   
 [從資源庫映像建立新的已加密 Windows IaaS 受管理磁碟 VM] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >它是強制性 toosnapshot 及/或備份的受管理的磁碟基礎的外部 VM 執行個體和先前 tooenabling Azure 磁碟加密。  Hello 受管理磁碟的快照集可以取自 hello 入口網站，或可以使用 Azure 備份。  備份確保復原選項可以在 hello 案例中的任何未預期的失敗期間加密。  建立備份之後，hello 組 AzureRmVMDiskEncryptionExtension 指令程式可以藉由指定 hello-skipVmBackup 參數是使用的 tooencrypt 管理磁碟。  在建立好備份並指定了這個參數之前，對以受控磁碟為基礎的 VM 執行這個命令都將會失敗。    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>現有已加密非高階 VM 的更新加密設定
  使用 hello 現有 Azure 磁碟加密支援的介面執行 VM [PS 指令程式，CLI 或 ARM 範本] tooupdate hello 加密設定喜歡 AAD 用戶端識別碼/密碼、 加密金鑰 [KEK]，Windows VM 或複雜密碼的 BitLocker 加密金鑰只有非 premium 儲存體所支援的 Vm 支援 Linux VM 等 hello 更新加密設定。 不支援高階儲存體所支援 VM 的。

## <a name="appendix"></a>附錄
### <a name="connect-tooyour-subscription"></a>連接 tooyour 訂用帳戶
在繼續之前，檢閱 hello*必要條件*〉 一節。 確定已符合所有必要條件之後，請進行 hello 下列連接 tooyour 訂用帳戶：

1. 啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：

    `Login-AzureRmAccount`

2. 如果您有多個訂用帳戶，而且想 toospecify 一個 toouse，輸入下列帳戶 toosee hello 訂閱 hello:

    `Get-AzureRmSubscription`

3. 您想 toouse，toospecify hello 訂用帳戶類型：

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify hello 訂用帳戶設定正確無誤，輸入：

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure 磁碟加密會安裝 cmdlet，類型：

    `Get-command *diskencryption*`

6. hello 下列輸出會確認 hello Azure 磁碟加密 PowerShell 安裝：

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>準備已預先加密的 Windows VHD
hello 以下各節是必要的 tooprepare 預先加密為加密的 VHD 在 Azure IaaS 中部署 Windows VHD。 使用 hello 資訊 tooprepare 和開機全新 Windows VM (VHD)，在 Azure Site Recovery 或 Azure。

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>更新群組原則 tooallow 非 TPM OS 保護
設定 hello BitLocker 群組原則設定**BitLocker 磁碟機加密**，這會在下看到**本機電腦原則** > **電腦設定**  > **系統管理範本** > **Windows 元件**。 變更此設定太**作業系統磁碟機** > **需要在啟動時的其他驗證** > **不含相容 TPM允許使用BitLocker**hello 遵循圖所示：

![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>安裝 BitLocker 功能元件
Windows Server 2012 和更新版本中，使用下列命令的 hello:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Windows Server 2008 R2，使用下列命令的 hello:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>使用 BitLocker 的準備 hello OS 磁碟區`bdehdcfg`
toocompress hello OS 磁碟分割和 BitLocker 的準備 hello 機器，執行下列命令的 hello:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>使用 BitLocker 來保護 hello OS 磁碟區
使用 hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx)命令 tooenable 加密使用外部的金鑰保護裝置 hello 開機磁碟區上。 此外 hello 外接式磁碟機或磁碟區上放置 hello 外部索引鍵 （.bek 檔案）。 Hello 下次重新開機後 hello 系統/開機磁碟區上啟用加密。

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> 做好使用 BitLocker 取得 hello 外部索引鍵與個別資料/資源 VHD hello VM。

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>在執行中的 Linux VM 上加密 OS 磁碟機
加密作業系統磁碟機上執行的 Linux VM 的支援下列散發 hello:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>OS 磁碟加密的必要條件

* 從 Marketplace 映像 hello Azure 資源管理員中，必須先建立 hello VM。
* 具有至少 4 GB RAM 的 Azure VM (建議大小為 7 GB)。
* (適用於 RHEL 和 CentOS) 停用 SELinux。 toodisable SELinux，請參閱 「 4.4.2。 以停用 SELinux"hello [SELinux 使用者和系統管理員指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux)hello VM 上。
* 停用 SELinux 之後，重新啟動 hello VM 至少一次。

##### <a name="steps"></a>步驟
1. 建立 VM 使用其中一種 hello 先前指定的分佈。

 若為 CentOS 7.2，支援透過特殊映像加密 OS 磁碟。 toouse 此映像，指定 「 7.2n"hello SKU，當您建立 hello VM 為：
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. 設定 hello VM 相應 tooyour 需求。 如果您正在 tooencrypt hello （OS + 資料） 的所有磁碟機，hello 資料磁碟機就會需要 toobe 指定和從 /etc/fstab 裝載。

 > [!NOTE]
 > 使用 UUID =...toospecify /etc/hosts fstab 而不是指定 hello 區塊裝置名稱 (例如，/dev/sdb1) 中的資料磁碟機。 在加密期間，hello hello VM 上的磁碟機變更的順序。 如果您的 VM 依賴封鎖裝置的特定順序，它將會失敗 toomount 它們加密之後。

3. 登出 hello SSH 工作階段。

4. tooencrypt hello 的作業系統上，指定做為 volumeType**所有**或**OS**時您[啟用加密](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure)。

 > [!NOTE]
 > 未以 `systemd` 服務的形式執行的所有使用者空間程序皆應使用 `SIGKILL` 來終止。 重新啟動 hello VM。 當您在執行中的 VM 上啟用 OS 磁碟加密時，請規劃 VM 停機時間。

5. 定期監視加密進度 hello 使用 hello hello 指示[下一節](#monitoring-os-encryption-progress)。

6. Get AzureRmVmDiskEncryptionStatus 顯示 「 VMRestartPending 」 之後，重新啟動您的 VM 在 tooit 登入或使用 hello 入口網站、 PowerShell 或 CLI。
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
您重新開機之前，我們建議您儲存[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)的 hello VM。

#### <a name="monitoring-os-encryption-progress"></a>監視 OS 加密進度
有三種方式可監視 OS 加密進度：

* 使用 hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet，並檢查 hello ProgressMessage 欄位：
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Hello VM 達到 「 作業系統磁碟加密已啟動 」 之後，它會有約 40 too50 分鐘高階儲存體的備份 VM。

 由於 WALinuxAgent 發生 [388 號問題](https://github.com/Azure/WALinuxAgent/issues/388)，某些散發套件的 `OsVolumeEncrypted` 和 `DataVolumesEncrypted` 會顯示為 `Unknown`。 若使用 WALinuxAgent 2.1.5 和更新版本，就會自動修正此問題。 如果您看到`Unknown`在 hello 輸出中，您可以使用 hello Azure 資源總管確認磁碟加密狀態。

 跳過[Azure 資源總管](https://resources.azure.com/)，然後展開左側 hello 選取面板中的此階層：

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 在 hello InstanceView，捲動 toosee hello 加密狀態，您的磁碟機。

 ![VM 執行個體檢視](./media/azure-security-disk-encryption/vm-instanceview.png)

* 查看[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)。 訊息從 hello ADE 延伸前面應該要有`[AzureDiskEncryption]`。

* 登入 toohello 透過 SSH 的 VM，並取得 hello 延伸模組中的記錄檔：

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 我們建議，您沒有登入 toohello VM OS 加密進行中時。 Hello 其他兩個方法都失敗時才複製 hello 記錄檔。

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>準備已預先加密的 Linux VHD
##### <a name="ubuntu-16"></a>Ubuntu 16
設定加密 hello 發佈安裝期間執行 hello 下列：

1. 選取**設定加密的磁碟區**當您分割 hello 磁碟。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. 另外建立一個不得加密的開機磁碟機。 加密根磁碟機。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. 提供複雜密碼。 這是您上傳 toohello 金鑰保存庫的 hello 複雜密碼。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. 完成分割。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. 當您啟動 hello VM，並會要求輸入複雜密碼時，使用您在步驟 3 中提供的 hello 複雜密碼。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. 將上傳至 Azure 中，使用準備 hello VM[這些指示](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)。 請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。

設定使用 Azure 加密 toowork 執行 hello 下列：

1. 建立 hello 下列指令碼中的 hello 內容 /usr/local/sbin/azure_crypt_key.sh 下的檔案。 因為它是供 Azure hello 複雜密碼的檔案名稱，請特別注意 toohello KeyFileName。

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. 變更中的 hello crypt config */etc/hosts crypttab*。 它看起來應該如下所示：
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. 如果您要編輯*azure_crypt_key.sh* Windows 和您在複製它 tooLinux，執行`dos2unix /usr/local/sbin/azure_crypt_key.sh`。

4. 加入可執行檔的權限 toohello 指令碼：
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. 以加上程式碼行的方式編輯 /etc/initramfs-tools/modules：
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. 執行`update-initramfs -u -k all`tooupdate hello initramfs toomake hello`keyscript`才會生效。

7. 現在您可以取消佈建 hello VM。

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. 繼續下一個步驟中 toohello 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。

##### <a name="opensuse-132"></a>openSUSE 13.2
tooconfigure 加密 hello 發佈在安裝期間，請勿 hello 遵循：
1. 當您分割 hello 磁碟時，請選取**加密磁碟區群組**，然後輸入密碼。 這是您要上傳 tooyour 金鑰保存庫的 hello 密碼。

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. 開機 hello VM 使用您的密碼。

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. 準備 hello VM 中的 hello 指示上載 tooAzure [SLES 或 openSUSE 虛擬機器做好 Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)。 請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。

有了 Azure，tooconfigure 加密 toowork hello 遵循：
1. 編輯 hello /etc/dracut.conf 並加入以下的 hello:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Hello hello 結束這行程式碼的註解檔案 /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. 附加在 hello 檔案 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 開頭的行下 hello:
 ```
    DRACUT_SYSTEMD=0
 ```
變更所有出現的：
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
至：
```
    if [ 1 ]; then
```
4. 編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh，並將其附加到太 「 # 開啟 LUKS 裝置 」:

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. 執行`/usr/sbin/dracut -f -v`tooupdate hello initrd。

6. 現在您可以取消佈建 hello VM 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。

##### <a name="centos-7"></a>CentOS 7
tooconfigure 加密 hello 發佈在安裝期間，請勿 hello 遵循：
1. 在分割磁碟時選取 [加密資料]。

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. 確定已為根分割選取 [加密]。

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. 提供複雜密碼。 這是您要上傳 tooyour 金鑰保存庫的 hello 複雜密碼。

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. 當您啟動 hello VM，並會要求輸入複雜密碼時，使用您在步驟 3 中提供的 hello 複雜密碼。

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. 上傳至 Azure，使用中的 hello"CentOS 7.0 + 」 指示準備 hello VM [CentOS 為基礎的虛擬機器做好 Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)。 請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。

6. 現在您可以取消佈建 hello VM 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。

有了 Azure，tooconfigure 加密 toowork hello 遵循：

1. 編輯 hello /etc/dracut.conf 並加入以下的 hello:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Hello hello 結束這行程式碼的註解檔案 /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. 附加在 hello 檔案 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 開頭的行下 hello:
```
    DRACUT_SYSTEMD=0
```
變更所有出現的：
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
to
```
    if [ 1 ]; then
```
4. 編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 並附加之後 hello 「 # 開啟 LUKS 裝置 」:
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. 執行 hello"/ usr/來啟動/dracut-f-v"tooupdate hello initrd。

![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>上傳加密的 VHD tooan Azure 儲存體帳戶
在啟用 BitLocker 加密或 DM Crypt 加密之後，hello 本機加密 VHD 需要上傳 toobe tooyour 儲存體帳戶。

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>上傳 hello 預先加密 VM tooyour 金鑰保存庫的 hello 磁碟加密密碼
您所取得的 hello 磁碟加密密碼之前必須上傳做為金鑰保存庫中的密碼。 hello 金鑰保存庫需要 toohave 磁碟加密，並啟用您的 Azure AD 用戶端權限。

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>未使用 KEK 加密的磁碟加密密碼
註冊您的金鑰保存庫，使用中的 hello 密碼 tooset[組 AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)。 如果您有 Windows 虛擬機器，hello bek 檔案編碼為 base64 字串，然後再上傳 tooyour 金鑰保存庫使用 hello `Set-AzureKeyVaultSecret` cmdlet。 適用於 Linux，hello 複雜密碼會編碼為 base64 字串，然後再上傳 toohello 金鑰保存庫。 此外，請確定下列標記該 hello 會設定當您建立 hello 金鑰保存庫中的 hello 密碼。

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

使用 hello `$secretUrl` hello 下一個步驟中[附加 hello OS 磁碟，而不使用 KEK](#without-using-a-kek)。

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>使用 KEK 加密的磁碟加密密碼
您上傳 hello toohello 秘密金鑰保存庫之前，您可以選擇性地加密它所使用的加密金鑰。 使用 hello 包裝[API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst 加密 hello 使用 hello 金鑰的加密金鑰的密碼。 hello 這個 wrap 作業的輸出是 base64 URL 編碼字串，如此您可以再使用上傳做為密碼 hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet。

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

使用`$KeyEncryptionKey`和`$secretUrl`hello 下一個步驟中[附加 hello OS 磁碟使用 KEK](#using-a-kek)。

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>連接 OS 磁碟時，指定密碼的 URL
#### <a name="without-using-a-kek"></a>不使用 KEK
雖然您正在附加 hello OS 磁碟，您需要 toopass `$secretUrl`。 產生 hello 「 未加密的 KEK 與磁碟加密密碼 」 一節中的 hello URL。

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>使用 KEK
當您附加 hello OS 磁碟時，傳遞`$KeyEncryptionKey`和`$secretUrl`。 產生 hello 「 未加密的 KEK 與磁碟加密密碼 」 一節中的 hello URL。

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>下載此指南
您可以下載本指南從 hello [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)。

## <a name="for-more-information"></a>取得詳細資訊
[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
