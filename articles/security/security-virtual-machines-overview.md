---
title: "使用 Azure 虛擬機器所用的 aaaAzure 安全性功能 |Microsoft 文件"
description: " 可以搭配 Azure 虛擬機器的 hello 核心 Azure 的安全性功能的概觀。 Azure Vm 提供您無須 toobuy hello 的虛擬化彈性和維護 hello 執行 hello VM 的實體硬體。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Azure 虛擬機器安全性概觀
您可利用 Azure 虛擬機器以敏捷的方式部署範圍廣泛的許多運算解決方案。 利用 Microsoft Windows、Linux、Microsoft SQL Server、Oracle、IBM、SAP 與 Azure BizTalk 服務的支援，就可以在近乎所有的作業系統上，使用任何語言部署所有工作負載。

Azure 虛擬機器可讓您無須 toobuy hello 的虛擬化彈性和維護 hello 實體硬體執行 hello 虛擬機器。  您可以建置和部署您的資料是受保護且安全，我們非常安全的資料中心中的 hello 保證的應用程式。

您可以使用 Azure 建置安全性已加強且相容的解決方案：

* 保護虛擬機器抵禦病毒和惡意程式碼
* 將敏感性資料加密
* 保護網路流量
* 識別和偵測威脅
* 符合規範需求

這篇文章的 hello 目標是 tooprovide hello 核心 Azure 的安全性功能，可以搭配虛擬機器的概觀。 我們也提供了提供給每項功能的詳細資料，因此，您可以深入的連結 tooarticles。  

hello 核心 Azure 虛擬機器的安全性功能 toobe 涵蓋在本文章：

* 反惡意程式碼
* 硬體安全性模型
* 虛擬機器磁碟加密
* 虛擬機器備份
* Azure Site Recovery
* 虛擬網路
* 安全性原則管理和報告
* 法規遵循

## <a name="antimalware"></a>反惡意程式碼
有了 Azure，您可以使用反惡意程式碼軟體，例如 Microsoft、 Symantec、 趨勢科技及 Kaspersky tooprotect 安全性廠商的虛擬機器從惡意檔案、 廣告軟體和其他威脅。 Hello toofind 如下一節文章了解，請參閱協力廠商解決方案。

適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware 是即時保護功能，有助於識別和移除病毒、間諜軟體和其他惡意軟體。  Microsoft 反惡意程式碼提供已知惡意或垃圾軟體嘗試 tooinstall 本身，或在您的 Azure 系統上執行時可設定的警示。

Microsoft 反惡意程式碼是單一代理程式解決方案的應用程式和租用戶環境中，設計 toorun hello 背景需要人為介入。 您可以部署根據您的應用程式工作負載，與其中一個基本安全依預設的 hello 需求或進階自訂組態，包括監視反惡意程式碼的保護。

當您部署並啟用 Microsoft 反惡意程式碼時，就可以使用 hello 下列核心功能：

* 即時保護-在雲端服務和虛擬機器 toodetect 和封鎖惡意程式碼執行的監視活動。
* 排定的掃描-會定期執行目標掃描 toodetect 惡意程式碼，包括正在執行的程式。
* 惡意程式碼補救 - 自動針對偵測到的惡意程式碼採取行動，例如刪除或隔離惡意檔案及清除惡意的登錄項目。
* 簽章更新-自動安裝 hello 最新保護 （防毒定義） 的簽章 tooensure 保護是最新的預先決定的頻率。
* 反惡意程式碼引擎更新-自動更新 hello Microsoft 反惡意程式碼引擎。
* 反惡意程式碼的平台更新-自動更新 hello Microsoft 反惡意程式碼的平台。
* 作用中保護-會報告有關偵測到的威脅和可疑資源 tooensure 快速回應，而且可讓您即時同步的簽章傳遞 hello Microsoft Active Protection 系統 (MAPS) 透過 tooAzure 遙測中繼資料。
* 範例 reporting： 提供和報告範例 toohello Microsoft 反惡意程式碼服務 toohelp 精簡 hello 服務和啟用疑難排解。
* 排除項目 – 可讓應用程式和服務系統管理員 tooconfigure 某些檔案時，處理程序，和磁碟機 tooexclude 其保護和效能，因為其他原因而進行掃描。
* 反惡意程式碼的事件集合-hello 反惡意程式碼服務健全狀況、 可疑活動，以及在 hello 作業系統事件記錄檔中所採取的修復動作記錄，並會加以收集到 hello 客戶的 Azure 儲存體帳戶。

進一步了解： 深入了解反惡意程式碼軟體 tooprotect toolearn 您的虛擬機器，請參閱：

* [適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware](azure-security-antimalware.md)
* [在 Azure 虛擬機器上部署反惡意程式碼解決方案](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [如何 tooinstall 和設定 Trend Micro Deep Security 作為 Windows VM 上的服務](../virtual-machines/windows/classic/install-trend.md)
* [如何 tooinstall 及 Windows VM 上設定 Symantec Endpoint Protection](../virtual-machines/windows/classic/install-symantec.md)
* [在 hello Azure Marketplace 中的安全性解決方案](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>硬體安全性模型
您可以藉由改善金鑰安全性來增強加密和驗證保護。 您可以將它們儲存在 Azure 金鑰保存庫，來簡化 hello 管理和安全性關鍵的密碼和金鑰。 金鑰保存庫提供 hello 選項 toostore 您的硬體安全性模組 (Hsm) 認證的 tooFIPS 140-2 Level 2 標準中的索引鍵。 備份或 [透明資料加密](https://msdn.microsoft.com/library/bb934049.aspx) 的 SQL Server 加密金鑰都能與應用程式的任何金鑰或密碼一起存放在金鑰保存庫中。 權限和存取 toothese 受保護的項目透過[Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)。

深入了解：

* [什麼是 Azure 金鑰保存庫？](../key-vault/key-vault-whatis.md)
* [開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)
* [Azure 金鑰保存庫部落格](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>虛擬機器磁碟加密
Azure 磁碟加密是可讓您加密您的 Windows 和 Linux Azure 虛擬機器磁碟的新功能。 Azure 磁碟加密使用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooprovide 磁碟區加密 hello OS 與 hello 資料磁碟的功能。

您控制和管理 hello 磁碟加密金鑰和秘密中您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會留在您 Azure 儲存體都加密的 Azure 金鑰保存庫 toohelp 整合 hello 方案。

深入了解：

* [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [適用於 Linux 和 Windows 虛擬機器的 Azure 磁碟加密](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [加密虛擬機器](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>虛擬機器備份
Azure 備份是可調式解決方案，可以不需成本地保護您的應用程式資料，以及將操作成本降到最低。 應用程式錯誤可能導致資料損毀，而人為錯誤可能會將 Bug 導入應用程式中。 使用 Azure 備份，您執行 Windows 與 Linux 的虛擬機器會受到保護。

深入了解：

* [何謂 Azure 備份？](../backup/backup-introduction-to-azure-backup.md)
* [Azure 備份學習路徑](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Azure 備份服務 - 常見問題集](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
您的組織 BCDR 策略的重要部分找出如何 tookeep 企業工作負載和應用程式設定和執行計畫時和未規劃的中斷發生。 Azure Site Recovery 有助於協調工作負載和應用程式的複寫、容錯移轉及復原，因此能夠在主要位置發生故障時透過次要位置來提供工作負載和應用程式。

網站復原：

* **簡化 BCDR 策略**— Site Recovery 可輕鬆 toohandle 複寫、 容錯移轉和復原的多個商業工作負載和應用程式從單一位置。 Site Recovery 會協調複寫和容錯移轉，但不會攔截應用程式資料或擁有任何相關資訊。
* **提供彈性的複寫** - 使用 Site Recovery，您就可以複寫 Hyper-V 虛擬機器、VMware 虛擬機器和 Windows/Linux 實體伺服器上執行的工作負載。
* **支援容錯移轉和復原**-站台復原提供測試容錯移轉 toosupport 災害復原演練而不會影響實際執行環境。 您也可以執行計劃性容錯移轉，因為是預期中的中斷，所以不會遺失任何資料；或是執行非計劃性容錯移轉，以在發生非未預期的災害時將資料損失減到最少 (取決於複寫頻率)。 容錯移轉之後，您可以容錯回復 tooyour 主要站台。 Site Recovery 提供了包含指令碼和 Azure 自動化作業手冊的復原計畫，以供您自訂多層式應用程式的容錯移轉和復原。
* **排除次要資料中心**— 您可以 tooa 內部次要站台或 tooAzure 複寫。 使用 Azure 做為目的地，嚴重損壞修復排除 hello 成本和複雜度維護次要站台。 複寫的資料會儲存在 Azure 儲存體。
* **與現有 BCDR 技術整合** - Site Recovery 能夠與其他應用程式的 BCDR 功能搭配使用。 例如，您可以使用站台復原 tooprotect hello SQL Server 後端的企業工作負載。 這包括原生支援的 SQL Server AlwaysOn 可用性群組的 toomanage hello 容錯移轉。

深入了解：

* [什麼是 Azure Site Recovery？](../site-recovery/site-recovery-overview.md)
* [Azure Site Recovery 如何運作？](../site-recovery/site-recovery-components.md)
* [Azure Site Recovery 保護哪些工作負載？](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>虛擬網路
虛擬機器需要遠端連線。 toosupport 該需求，Azure 需要連接的虛擬機器 toobe tooan Azure 虛擬網路。 Azure 虛擬網路是建立在 hello Azure 的實體網路網狀架構之上一個邏輯結構。 每個邏輯 Azure 虛擬網路都會與其他所有 Azure 虛擬網路隔離。 此隔離有助於確保您的部署中的網路流量不是可存取 tooother Microsoft Azure 客戶。

深入了解：

* [Azure 網路安全性概觀](security-network-overview.md)
* [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)
* [網路功能與企業合作夥伴關係的案例](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>安全性原則管理和報告
Azure 資訊安全中心可協助您防止、 偵測，並回應 toothreats，，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

Azure 資訊安全中心藉由下列方式來協助您最佳化和監視虛擬機器︰

* 提供虛擬機器 [安全性建議](../security-center/security-center-recommendations.md) ，例如套用系統更新、設定 ACL 端點、啟用反惡意程式碼、啟用網路安全性群組，以及套用磁碟加密。
* 監視虛擬機器的 hello 狀態

深入了解：

* [簡介 tooAzure 資訊安全中心](../security-center/security-center-intro.md)
* [Azure 資訊安全中心常見問題集](../security-center/security-center-faq.md)
* [Azure 資訊安全中心規劃和操作](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>法規遵循
Azure 虛擬機器經過 FISMA、FedRAMP、HIPAA、PCI DSS Level 1 及其他重要規範計劃認證。 此憑證就容易為您自己的 Azure 應用程式 toomeet 相容性需求和商務 tooaddress 各種本國及國際法規需求。

深入了解：

* [Microsoft 信任中心：法規遵循](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [受信任的雲端：Microsoft Azure 安全性、隱私權及法規遵循](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
