---
title: "aaaPrepare 內部部署與 Azure Site Recovery 的複寫 tooAzure 的 VMware 資源 |Microsoft 文件"
description: "摘要說明 hello 複寫 VMware Vm tooAzure 存放裝置上執行的工作負載所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>步驟 6： 準備內部部署 VMware 複寫 tooAzure

使用此發行項 tooprepare 在內部部署 VMware 伺服器 toointeract 與 Azure Site Recovery，hello 指示，並準備 VMWare Vm hello 行動服務的安裝。 hello 行動服務代理程式必須安裝在所有內部部署 Vm 上的 tooreplicate tooAzure。

## <a name="prepare-for-automatic-discovery"></a>為自動探索做準備

Site Recovery 會自動探索在 vSphere ESXi 主機 (具有或不具有 vCenter 伺服器) 上執行的虛擬機器。 自動探索、 站台復原需求帳戶 tooaccess 主機和伺服器：

1. toouse 專用的帳戶，建立角色 （在 hello vCenter 層級，與 hello hello 表中所述的權限。 指定名稱，例如 **Azure_Site_Recovery**。
2. 然後，在 hello vSphere 主機/vCenter 伺服器上，建立使用者並指派 hello 角色 toohello 使用者。 您在 Site Recovery 部署期間指定此使用者帳戶。


### <a name="vmware-account-permissions"></a>VMware 帳戶權限

Site Recovery 需要存取 tooVMware hello 處理序伺服器 tooautomatically 探索的 Vm，以及容錯移轉和容錯回復的 Vm。

- **移轉**： 如果您只想 toomigrate VMware Vm tooAzure，而未曾經回失敗，您可以使用具有唯讀角色 VMware 帳戶。 這種角色可以執行容錯移轉，但不能關閉受保護的來源電腦。 移轉時不需要這樣。
- **Replicate/復原**： 如果您想 toodeploy 完整的複寫，複寫、 容錯移轉 （回復） hello 帳戶必須是能夠 toorun 作業，例如建立和移除磁碟，Vm 等上的電源。
- **自動探索**︰需要至少一個唯讀帳戶。


**Task** | **必要的帳戶/角色** | **權限** | **詳細資料**
--- | --- | --- | ---
**處理序伺服器自動探索 VMware VM** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild**物件、 toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路）。
**容錯移轉** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路） 的物件。<br/><br/> 適用於移轉用途，而不是完整複寫、容錯移轉、容錯回復。
**容錯移轉和容錯回復** | 我們建議您建立含有 hello 所需的權限的角色 (Azure_Site_Recovery)，然後 hello 角色 tooa VMware 使用者或群組指派 | 資料中心物件 –> 傳播 tooChild 物件，角色 = Azure_Site_Recovery<br/><br/> 資料存放區 -> 配置空間、瀏覽資料存放區、底層檔案作業、移除檔案、更新虛擬機器檔案<br/><br/> 網路 -> 網路指派<br/><br/> 資源]-> [指派的 VM tooresource 集區、 移轉電源關閉的 VM、 移轉已開機的 VM<br/><br/> 工作 -> 建立工作、更新工作<br/><br/> 虛擬機器 -> 組態<br/><br/> 虛擬機器 -> 互動 -> 回答問題、裝置連線、設定 CD 媒體、設定磁碟片媒體、電源關閉、電源開啟、VMware 工具安裝<br/><br/> 虛擬機器 -> 清查 -> 建立、註冊、取消註冊<br/><br/> 虛擬機器 -> 佈建 -> 允許虛擬機器下載、允許虛擬機器檔案上傳<br/><br/> 虛擬機器 -> 快照 -> 移除快照 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild**物件、 toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路）。


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>準備的 hello 行動服務推入安裝

hello 行動服務必須先安裝所有的 Vm 上您想 tooreplicate。 有多種方式 tooinstall hello 服務，包括手動安裝中，從 hello 站台復原處理序伺服器，推入安裝和使用方法如 System Center Configuration Manager 的安裝。

如果您想 toouse 推入安裝，您會需要 tooprepare tooaccess hello VM 之後，可以使用站台復原的帳戶。

- 您可以使用網域或本機帳戶
- 對於 Windows，如果您不使用網域帳戶，您需要 toodisable hello 本機電腦上的遠端使用者存取控制。 這樣一來，在 hello 註冊下 toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**，新增 hello DWORD 項目**LocalAccountTokenFilterPolicy**，值為 1。
- 如果您想要從 CLI Windows tooadd hello 登錄項目，輸入：``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- 適用於 Linux，hello 帳戶應為 hello 來源 Linux 伺服器上的根。



## <a name="next-steps"></a>後續步驟

跳過[步驟 7： 建立保存庫](vmware-walkthrough-create-vault.md)
