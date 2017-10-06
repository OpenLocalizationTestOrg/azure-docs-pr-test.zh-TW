---
title: "啟動複寫的 Azure Vm tooanother 區域 aaaBefore |Microsoft 文件 '"
description: "摘要說明您之前使用 hello Azure Site Recovery 服務的 Azure 地區之間複寫 Azure Vm 需要 tootake hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>步驟 2：開始之前

您已檢閱過 hello 之後[架構](azure-to-azure-walkthrough-architecture.md)之間使用的 Azure 地區複寫 Azure 虛擬機器 (Vm) [Azure Site Recovery](site-recovery-overview.md)，使用此發行項 tooverify 必要條件。 

- 當您完成 hello 發行項時，您應該有明確的了解需要 toomake hello 部署什麼運作，而且已完成 hello 先決條件步驟。
- 張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

>[!NOTE]
>
> Azure VM 複寫目前為預覽狀態。



## <a name="support-recommendations"></a>支援建議

檢閱 hello 資料表下方。

**元件** | **需求**
--- | ---
**復原服務保存庫** | 我們建議您在 hello 目標的 toouse 災害的 Azure 區域中建立的復原服務保存庫。 例如，如果您想在美國東部 tooCentral 美國 tooreplicate 來源 Vm，美國中部建立 hello 保存庫。
**Azure 訂用帳戶** | 您的 Azure 訂用帳戶應啟用的 toocreate Vm，您想為 hello 災害復原區域 toouse hello 目標位置中。 請連絡客戶支援 tooenable hello 必要的配額。
**目標區域產能** | Hello 目標 Azure 地區，hello 訂用帳戶必須具備足夠的容量以 Vm、 儲存體帳戶和網路元件。
**儲存體** | 使用 hello[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)為您的 Azure Vm，tooavoid 效能問題的來源。<br/><br/> 儲存體帳戶必須在 hello 與 hello 保存庫相同的區域。<br/><br/> 您無法複寫在中部和印度南部及印度 toopremium 帳戶。<br/><br/> 如果您部署與 hello 預設設定進行複寫時，站台復原就會建立所需的 hello hello 來源設定為基礎的儲存體帳戶。 如果您自訂設定，請遵循 hello [VM 磁碟的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)。
**網路功能** | 您需要 tooallow 從 Azure Vm 的輸出連線的特定 Url/IP 範圍。<br/><br/> 網路帳戶必須在 hello 與 hello 保存庫相同的區域。 
**Azure VM** | 請確定所有最新的根憑證 hello hello Windows/Linux 的 Azure VM 上。 如果他們不這樣做，您必須能夠 tooregister hello Site Recovery 中的 VM 由於安全性限制。
**Azure 使用者帳戶** | 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。

取得支援需求的完整清單，在 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Hello 帳戶上設定權限

1. 閱讀有關 hello[權限](site-recovery-role-based-linked-access-control.md)您需要進行複寫。
2. 請遵循這些[指示](../active-directory/role-based-access-control-configure.md#add-access)tooadd 權限。


## <a name="verify-target-resources"></a>驗證目標資源

1. 啟用您的 Azure 訂用帳戶 tooallow toocreate Vm 在 hello 目標想要為 hello 災害復原區域 toouse 嚴重損壞修復 toouse 地區。 請連絡客戶支援 tooenable hello 必要的配額。
2. 請確定您的訂用帳戶有足夠的資源 tooenable Vm，以符合您的來源 Vm 的大小。 根據預設，當設定複寫、 站台復原來挑選 hello 相同大小的 hello 目標 VM，或 hello 最可能的大小。 深入了解針對目標資源進行[疑難排解](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097)。

## <a name="verify-azure-vm-certificates"></a>驗證 Azure VM 憑證

1. 檢查 hello Windows 或您想要 tooreplicate Linux Vm 上的所有 hello 最新的根憑證都存在。 如果 hello 最新的根憑證不存在，hello VM 不能註冊的 tooSite 復原，因為 toosecurity 條件約束。
2. 適用於 Windows Vm hello 遵循：

    - Hello VM 上安裝所有 hello 最新 Windows 更新，使所有 hello 受信任的根憑證都位於 hello 的電腦上。
    - 在中斷連線的環境，請遵循 hello 標準 Windows Update 處理程序/憑證更新程序中組織、 tooget hello 最新的根憑證和更新的 CRL，hello Vm 上。
3. 適用於 Linux Vm，請遵循您的 Linux 散發者 tooget hello 最受信任的根憑證與 hello 最新憑證撤銷清單 hello VM 上的所提供的 hello 指引。 深入了解針對受信任根發行進行[疑難排解](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066)。


## <a name="next-steps"></a>後續步驟

跳過[步驟 3： 規劃網路](azure-to-azure-walkthrough-network.md)tooset 上的傳出連線。
