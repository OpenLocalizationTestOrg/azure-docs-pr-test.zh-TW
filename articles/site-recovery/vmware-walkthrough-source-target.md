---
title: "hello 來源和目標與 Azure Site Recovery 的 VMware 複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset VMware Vm tooAzure 儲存體與 Azure Site Recovery 的複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>步驟 8: Hello 來源和目標 VMware 複寫 tooAzure 設定

本文說明如何 tooconfigure 來源和目標設定複寫時 VMware 虛擬機器 tooAzure，使用內部 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello 組態伺服器、 其註冊 hello 保存庫，以及探索 Vm。

1. 按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。
2. 如果您沒有設定伺服器，請按一下 [+設定伺服器]。
3. 在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。
4. 下載 hello Site Recovery 整合安裝程式安裝檔案。
5. 下載 hello 保存庫註冊金鑰。 您會在執行統一安裝時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

   ![設定來源](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Hello 保存庫中註冊伺服器 hello 組態

請勿 hello 下列之前啟動，然後執行整合安裝 tooinstall hello 組態伺服器、 hello 處理序伺服器，以及 hello 主要目標伺服器。
    - 透過影片快速建立概念

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - 在 hello 組態伺服器 VM，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。 應該相符。 如果快慢誤差 15 分鐘，安裝可能會失敗。
    - 以本機系統管理員身分 hello 組態伺服器 VM 上執行安裝程式。
    - 請確定 hello VM 上啟用 TLS 1.0。


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。



## <a name="connect-toovmware-servers"></a>TooVMware 伺服器連線

在內部部署環境中執行 tooallow Azure Site Recovery toodiscover 虛擬機器，您需要 tooconnect，您的 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery。 在開始之前，請注意下列 hello:

- 如果您新增 hello vCenter server 或不具有系統管理員權限的帳戶的 vSphere 主機 tooSite 復原 hello 伺服器上，hello 帳戶必須啟用這些權限：
    - 資料中心、資料存放區、資料夾、主機、網路、資源、虛擬機器、vSphere 分散式交換器。
    - hello vCenter server 必須儲存檢視的權限。
- 當您新增 VMware 伺服器 tooSite 復原時，可能需要 15 分鐘或更長，tooappear hello 入口網站中的。

### <a name="add-hello-account-for-automatic-discovery"></a>新增自動探索的 hello 帳戶

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>設定連線

連接 tooservers，如下所示：

1. 選取**+ vCenter** toostart VMware vCenter server 或 VMware vSphere ESXi 主機連接。
2. 在**新增 vCenter**指定 hello vSphere 主機或 vCenter 伺服器，好記名稱，然後指定 hello IP 位址或 hello 伺服器的 FQDN。
3. 除非您的 VMware 伺服器在不同的通訊埠上的要求設定的 toolisten 保留 hello 連接埠 443。 選取 tooconnect toohello VMware vCenter 或 vSphere ESXi 伺服器 hello 帳戶。 按一下 [確定] 。
4. 站台復原連接 tooVMware 伺服器使用 hello 指定設定，並探索 Vm。

> [!NOTE]
> 如果您要加入的伺服器或主控件以 hello vCenter 或主機伺服器沒有系統管理員權限的帳戶，請確定 hello 帳戶已啟用這些權限： 資料中心、 資料存放區、 資料夾、 主機、 網路、 虛擬機器的資源，並vSphere 分散式交換器。 此外，hello VMware vCenter server 必須啟用權限的 hello 儲存檢視表。


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

您設定 hello 目標環境之前，請確定您有 Azure 儲存體帳戶和虛擬網路設定。

1. 按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。
2. 指定目標部署模型是以 Resource Manager 為基礎或傳統。
3. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

   ![目標](./media/vmware-walkthrough-source-target/gs-target.png)
4. 如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**，toocreate 資源管理員帳戶或網路內嵌。

## <a name="next-steps"></a>後續步驟

跳過[步驟 9： 設定複寫原則](vmware-walkthrough-replication.md)