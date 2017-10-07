---
title: " 在 Azure Site Recovery 中管理 VMware vCenter Server | Microsoft Doc"
description: "本文說明如何在 Azure Site Recovery 中新增並管理 VMware vCenter。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>在 Azure Site Recovery 中管理 VMware vCenter Server
這篇文章討論 hello 各種可對 VMware vCenter 的站台復原作業。

## <a name="prerequisites"></a>必要條件

**支援 VMware vCenter 和 VMware vSphere ESX 主機** | **詳細資料** |
|--- | --- |
|**內部部署 VMware 伺服器** | 一個或多個 VMware vSphere 伺服器 (執行具有最新更新的 6.0、5.5 或 5.1)。 伺服器應該位於相同網路 hello 組態伺服器 （或不同的處理序伺服器） 的 hello。<br/><br/> 我們建議 vCenter server toomanage 主機，執行 6.0 或 5.5 hello 最新的更新。 當您部署 6.0 版時，僅支援 5.5 中可用的功能。|

## <a name="prepare-an-account-for-automatic-discovery"></a>準備帳戶以進行自動探索
Site Recovery 需要存取 tooVMware hello 處理序伺服器 tooautomatically 探索虛擬機器，以及容錯移轉和容錯回復的虛擬機器。

* **移轉**： 如果您只想 toomigrate VMware 虛擬機器 tooAzure，而未曾經回失敗，您可以使用具有唯讀角色 VMware 帳戶。 這種角色可以執行容錯移轉，但不能關閉受保護的來源電腦。 這針對移轉並非必要。
* **Replicate/復原**： 如果您想 toodeploy 完整的複寫，複寫、 容錯移轉 （回復） hello 帳戶必須是能夠 toorun 作業，例如建立和移除磁碟，虛擬機器上的電源。
* **自動探索**︰需要至少一個唯讀帳戶。


|**工作** | **必要的帳戶/角色** | **權限** | **詳細資料**|
|--- | --- | --- | ---|
|**處理序伺服器自動探索 VMware 虛擬機器** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （vSphere 主機、 datastores、 虛擬機器和網路） 的物件。|
|**容錯移轉** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （vSphere 主機、 datastores、 虛擬機器和網路） 的物件。<br/><br/> 適用於移轉用途，而不是完整複寫、容錯移轉、容錯回復。|
|**容錯移轉和容錯回復** | 我們建議您建立含有 hello 所需的權限的角色 (AzureSiteRecoveryRole)，然後 hello 角色 tooa VMware 使用者或群組指派 | 資料中心物件 –> 傳播 tooChild 物件，角色 = AzureSiteRecoveryRole<br/><br/> 資料存放區 -> 配置空間、瀏覽資料存放區、底層檔案作業、移除檔案、更新虛擬機器檔案<br/><br/> 網路 -> 網路指派<br/><br/> 資源]-> [指派的 VM tooresource 集區、 移轉電源關閉的 VM、 移轉已開機的 VM<br/><br/> 工作 -> 建立工作、更新工作<br/><br/> 虛擬機器 -> 組態<br/><br/> 虛擬機器 -> 互動 -> 回答問題、裝置連線、設定 CD 媒體、設定磁碟片媒體、電源關閉、電源開啟、VMware 工具安裝<br/><br/> 虛擬機器 -> 清查 -> 建立、註冊、取消註冊<br/><br/> 虛擬機器 -> 佈建 -> 允許虛擬機器下載、允許虛擬機器檔案上傳<br/><br/> 虛擬機器 -> 快照 -> 移除快照 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （vSphere 主機、 datastores、 虛擬機器和網路） 的物件。|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>建立帳戶 tooconnect tooVMware vCenter Server / VMware vSphere EXSi 主機
1. 登入 hello 組態伺服器和啟動 hello cspsconfigtool.exe 使用 hello 捷徑放在 hello 桌面。
2. 按一下**新增帳戶**上 hello**管理帳戶** 索引標籤。

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. 提供 hello 帳戶詳細資料，然後按一下 [確定] tooadd hello 帳戶。 hello 帳戶應擁有 hello hello 中所列的權限[準備帳戶用來自動探索](#prepare-an-account-for-automatic-discovery)> 一節。

  >[!NOTE]
  它需要大約 15 分鐘的 hello 帳戶資訊 toobe 向上與 hello Site Recovery 服務進行同步處理。


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>關聯 VMware vCenter / VMware vSphere ESX 主機 (新增 vCenter)
* 在 hello Azure 入口網站中，瀏覽過*YourRecoveryServicesVault* > **Site Recovery 基礎結構** > **設定伺服器** > *ConfigurationServer*
* 在 hello 組態伺服器的詳細資料頁面中按一下 hello + vCenter 按鈕。

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>修改認證使用 tooconnect toohello vCenter server / vSphere ESXi 主機

1. 登入 hello 組態伺服器和啟動 hello cspsconfigtool.exe
2. 按一下**新增帳戶**上 hello**管理帳戶** 索引標籤。

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. 提供 hello 新帳戶詳細資料，然後按一下 [確定] tooadd hello 帳戶。 hello 帳戶應擁有 hello hello 中所列的權限[準備帳戶用來自動探索](#prepare-an-account-for-automatic-discovery)> 一節。
4. 在 hello Azure 入口網站中，瀏覽過*YourRecoveryServicesVault* > **Site Recovery 基礎結構** > **設定伺服器** > *ConfigurationServer*
5. 在 [hello 組態伺服器的詳細資料] 頁面上，按一下 [hello**重新整理伺服器**] 按鈕。
6. Hello 重新整理伺服器作業完成之後，請選取 hello vCenter Server tooopen hello vCenter 摘要頁面。
7. 選取 hello 新加入的帳戶在 hello **vCenter 伺服器 /vsphere 主機帳戶**欄位，然後按一下 hello**儲存** 按鈕。

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>在 Azure Site Recovery 中刪除 vCenter
1. 在 hello Azure 入口網站中，瀏覽過*YourRecoveryServicesVault* > **Site Recovery 基礎結構** > **設定伺服器** > *ConfigurationServer*
2. Hello 組態伺服器的詳細資料頁面中選取 hello vCenter Server tooopen hello vCenter 摘要頁面。
3. 按一下 hello**刪除**按鈕 toodelete hello vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
如果您需要 toomodify hello Vcenter IP 位址 /FQDN，連接埠詳細資料，則您需要 toodelete hello vCenter Server，然後重新加入。
