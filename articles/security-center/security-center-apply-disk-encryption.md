---
title: "在 Azure 資訊安全中心 aaaApply 磁碟加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 適用於磁碟加密 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>在 Azure 資訊安全中心中套用磁碟加密
如果您有未使用 Azure 磁碟加密進行加密的 Windows 或 Linux VM 磁碟，Azure 資訊安全中心會建議您套用磁碟加密。 磁碟加密可讓您替 Windows 和 Linux IaaS VM 磁碟加密。  加密是建議使用 hello OS 和 VM 上的資料磁碟區。

磁碟加密使用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux 的功能。 這些功能會提供作業系統，而且資料加密 toohelp 保護並保護您的資料符合您組織的安全性和相容性的承諾。 磁碟加密與整合[Azure 金鑰保存庫](https://azure.microsoft.com/documentation/services/key-vault/)toohelp 您控制，和管理您金鑰保存庫的訂用帳戶，同時確保 hello VM 磁碟中的所有資料會留在您都加密中的hello磁碟加密金鑰和密碼[Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)。

> [!NOTE]
> 支援下列 Windows 伺服器作業系統-Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2 的 hello azure 磁碟加密。 磁碟加密支援下列 Linux 伺服器作業系統-Ubuntu、 CentOS、 SUSE 和 SUSE Linux Enterprise Server (SLES) hello。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**套用磁碟加密**。
2. 在 hello**套用磁碟加密**刀鋒視窗中，您會看到一份磁碟加密建議您的 Vm。
3. 請遵循 hello 指示 tooapply 加密 toothese Vm。

![][1]

tooencrypt 已經由資訊安全中心識別為需要加密的 Azure 虛擬機器，我們建議 hello 下列步驟：

* 安裝並設定 Azure PowerShell。 這可讓您 toorun hello PowerShell 命令需要的 tooset hello 必要條件需要 tooencrypt Azure 虛擬機器上。
* 取得並執行 hello Azure 磁碟加密必要條件 Azure PowerShell 指令碼。
* 加密虛擬機器。

[加密 Azure 虛擬機器](security-center-disk-encryption.md)逐步引導您完成這些步驟。  本主題假設您使用 Windows 10 做 hello 用戶端電腦，您可以從此處設定磁碟加密。

有許多方法可以用於 Azure 虛擬機器。 如果您已精通 Azure PowerShell 或 Azure CLI 中，您可能偏好 toouse 替代方式。 toolearn 有關這些其他方法，請參閱[Azure 磁碟加密](../security/azure-security-disk-encryption.md)。

## <a name="see-also"></a>另請參閱
這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 」 套用磁碟加密 」。 toolearn 進一步了解磁碟加密，請參閱 hello 下列資訊：

* [使用 Azure 金鑰保存庫的加密和金鑰管理](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/)（視訊、 36 min 39 秒）-深入了解如何 toouse 磁碟加密管理的 IaaS Vm 和 Azure 金鑰保存庫 toohelp 保護，並保護您的資料。
* [加密 Azure 虛擬機器](security-center-disk-encryption.md)（文件）-深入了解如何 tooencrypt Azure 虛擬機器。
* [Azure 磁碟加密](../security/azure-security-disk-encryption.md)（文件）-深入了解如何 tooenable 磁碟適用於 Windows 和 Linux Vm 的加密。

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
