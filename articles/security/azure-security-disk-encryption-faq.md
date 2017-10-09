---
title: "aaaAzure 磁碟加密常見問題集 |Microsoft 文件"
description: "本文提供的解答 toofrequently 常見問題的 Microsoft Azure 磁碟加密適用於 Windows 及 Linux IaaS Vm。"
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Azure 磁碟加密常見問題集 (FAQ)

此常見問題集中會解答 Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密的相關問題，如需這項服務的相關資訊，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)。

## <a name="general-questions"></a>一般問題
**問：** Azure 磁碟加密在 GA 中的哪一個區域？

**答：**Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密會在所有 Azure 公用區域的 GA 中提供。

**問：**Azure 磁碟加密有哪些使用者體驗？

**答：**Azure 磁碟加密 GA 支援 Azure Resource Manager 範本、Azure PowerShell、Azure CLI。 這為您提供很大的彈性，因為您會有三個不同選項可啟用您 IaaS VM 的磁碟加密。 Hello Azure 磁碟加密部署案例及體驗提供 hello 使用者體驗，以及逐步指引的更多詳細資料。

**問：**Azure 磁碟加密如何收費？

**答：**使用 Azure 磁碟加密來加密 VM 磁碟完全免費。

**問：**可以使用 Azure 磁碟加密搭配哪些虛擬機器層？

**答：**Azure 磁碟加密僅適用於標準層 VM，包括 [A、D、DS、G、GS、F](https://azure.microsoft.com/pricing/details/virtual-machines/) 等系列，IaaS VM 包括使用進階儲存體的 VM。 它並不適用於基本層 VM。

**問：**Azure 磁碟加密支援哪些 Linux 散發套件？

**答：** hello 下列 Linux 伺服器的發行版本和版本支援 Azure 磁碟加密：

| Linux 散發套件 | 版本 | 支援加密的磁碟區類型|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | 作業系統和資料磁碟 |
| Ubuntu | 14.04.5-DAILY-LTS | 作業系統和資料磁碟 |
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
| SLES | 優先順序：12-SP1 | 資料磁碟 |
| SLES | HPC 12 | 資料磁碟 |
| SLES | 優先順序：11-SP4 | 資料磁碟 |
| SLES | 11 SP4 | 資料磁碟 |

**問：**如何開始使用 Azure 磁碟加密？

**答：**客戶可以了解如何 tooget 啟動讀取 hello Azure 磁碟加密 （英文） 白皮書位於[這裡](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**問：**是否可以使用 Azure 磁碟加密來加密開機和資料磁碟區？

**答：**是，您可以加密 Windows 和 Linux IaaS VM 適用的開機和資料磁碟區。 適用於 Windows Vm，您無法加密 hello 資料，沒有第一個 encrpting hello OS 磁碟區。 適用於 Linux Vm，您可以先加密 hello 沒有 encryptinng hello OS 磁碟區的資料磁碟區。 一旦您已如 Liux 加密 hello OS 磁碟區，不支援停用作業系統磁碟區上的 Linux IaaS Vm 的加密

**問：**Azure 磁碟加密可讓您使用「自備金鑰」(BYOK) 功能嗎？

**答：**是，您可以提供自己的金鑰加密金鑰。 這些金鑰會受 Azure 金鑰保存庫，這是 hello Azure 磁碟加密金鑰存放區。 如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗

**問：**是否可以使用 Azure 建立的金鑰加密金鑰？

**答：**是，您可以使用 Azure 金鑰保存庫 toogenerate 金鑰的加密金鑰，Azure 磁碟加密使用。 這些金鑰會受 Azure 金鑰保存庫，這是 hello Azure 磁碟加密金鑰存放區。 如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗

**問：**我可以使用內部部署金鑰管理服務/HSM toosafeguard hello 加密金鑰？

**答：** hello 在內部部署金鑰管理服務/HSM toosafeguard hello 加密金鑰無法使用 Azure 磁碟加密。 您只能使用 hello Azure 金鑰保存庫服務 toosafeguard hello 加密金鑰。 如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗

**問：** hello 必要條件 tooconfigure Azure 磁碟加密為何？

**答：** hello Azure 磁碟加密必要條件 PowerShell 指令碼 toocreate AAD 應用程式，建立新的金鑰保存庫或設定現有磁碟加密存取 tooenable 加密和保護機密資料和金鑰的金鑰保存庫。  如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密先決條件和部署案例和體驗

**問：**哪裡取得更多有關如何設定 Azure 磁碟加密 toouse PowerShell？

**答：**我們有一些絕佳的文章，說明如何執行基本的 Azure 磁碟加密工作，以及更多進階的情節。 如 hello 基本的工作，請參閱瀏覽[Azure 磁碟加密使用 Azure PowerShell-第 1 部分](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/)。 如需更多進階的情節，請參閱探索[使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**問：**Azure 磁碟加密支援 Azure PowerShell 的什麼版本？

**答：**使用 hello 最新版本的 Azure PowerShell SDK 版本 tooconfigure Azure 磁碟加密。 下載 hello 最新版本[Azure PowerShell](https://github.com/Azure/azure-powershell/releases)。 Azure SDK version 1.1.0 版「不」支援 Azure 磁碟加密。

> [!NOTE]
> hello Linux 的 Azure 磁碟加密預覽功能延伸模組已被取代。 如需詳細資訊，請參閱 toodocumentation[這裡](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**問：**是否可以在我的自訂 Linux 映像上套用 Azure 磁碟加密？

**答：**無法在您的自訂 Linux 映像上套用 Azure 磁碟加密。 我們針對上述叫出 hello 支援散發版本支援只有 hello 圖庫 Linux 映像。 目前不支援自訂 Linux 映像

**問：**可以將套用更新 tooa Linux Red Hat VM 使用 Yum 更新嗎？

**答：**是，您可以執行更新和/或修補遵循[這裡](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)所述之指引的 Red Hat Linnux VM

**問：**其中可以移 tooask 問題或提供意見反應

**答：**詢問問題或意見反應 hello Azure 磁碟加密論壇，您可以提供[這裡](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>另請參閱
在本文件中，您學更 hello 最常見的問題相關的 tooAzure 磁碟加密，如需有關這項服務，並讀取其功能：

- [在 Azure 資訊安全中心套用磁碟加密](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [加密 Azure 虛擬機器](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure 資料靜態加密](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
