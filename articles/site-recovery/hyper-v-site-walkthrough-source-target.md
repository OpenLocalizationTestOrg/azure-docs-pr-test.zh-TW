---
title: "aaaSet hello 來源和目標 HYPER-V 複寫 tooAzure （不含 System Center VMM) 與 Azure Site Recovery |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset HYPER-V Vm tooAzure 儲存體與 Azure Site Recovery 的複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>步驟 8: Hello 來源和目標 HYPER-V 複寫 tooAzure 設定

本文說明如何 tooconfigure 來源和目標設定複寫時內部部署 HYPER-V 虛擬機器 （不含 System Center VMM) tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello HYPER-V 站台、 HYPER-V 主機上安裝 Azure Site Recovery Provider hello 和 hello Azure 復原服務代理程式和 hello 保存庫中註冊 hello 站台。

1. 在 [準備基礎結構] 中，按一下 [來源]。 按一下 新的 HYPER-V 站台做為您的 HYPER-V 主機或叢集的容器 tooadd **+ HYPER-V 站台**。

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. 在**建立 HYPER-V 站台**，指定 hello 網站的名稱。 然後按一下 [確定] 。 現在，選取您建立，然後按一下 「 hello 」 站台**+ HYPER-V Server** tooadd 伺服器 toohello 站台。

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. 在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。

    - 請確定您想要 hello tooadd 符合該 hello HYPER-V 伺服器[必要條件](#on-premises-prerequisites)，和是無法 tooaccess hello 指定的 Url。
    - 下載 hello Azure Site Recovery Provider 安裝檔案。 執行此檔案 tooinstall hello 提供者並 hello 每個 HYPER-V 主機上的復原服務代理程式。

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>安裝 hello 提供者和代理程式

1. 您已新增 toohello HYPER-V 站台執行每個主機上的 hello 提供者安裝程式檔案。 如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。 安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。
2. 在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。
3. 在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。
4. 在**保存庫設定**，按一下 **瀏覽**tooselect hello 保存庫金鑰檔下載。 指定 hello Azure Site Recovery 訂用帳戶，hello 保存庫名稱，並所屬 hello HYPER-V 站台 toowhich hello HYPER-V 伺服器。

    ![伺服器註冊](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. 在**Proxy 設定**，指定 HYPER-V 主機上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路的方式。

    * 如果您想 hello 提供者 tooconnect 直接選取**直接連接不使用 proxy 的站台復原 tooAzure**。
    * 如果您現有的 proxy 需要驗證，或者您想 toouse 自訂 proxy hello 提供者連接，請選取**連線使用 proxy 伺服器的站台復原 tooAzure**。
    * 如果您使用 Proxy：
        - 指定 hello 位址、 連接埠和認證
        - 請確定 hello 中所述的 hello Url[必要條件](#prerequisites)允許透過 hello proxy。

    ![網際網路](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. 安裝完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![安裝位置](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. 註冊完成之後，Azure Site Recovery 中，擷取中繼資料從 hello HYPER-V 伺服器和中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **HYPER-V 主機**。


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

指定 hello Azure 儲存體帳戶來進行複寫，並容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。

1. 按一下 [準備基礎結構] > [目標]。
2. 選取 hello 訂用帳戶與您想 toocreate hello Azure Vm 容錯移轉之後的 hello 資源群組。 選擇 hello 部署模型的 toouse Azure （classic 或資源管理） 中的 hello Vm。

3. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

    - 如果您沒有儲存體帳戶，按一下**+ 儲存體**toocreate 資源管理員帳戶內嵌。 
    - 如果您沒有 Azure 網路，按一下**+ 網路**toocreate 資源管理員為基礎的網路內嵌。






## <a name="next-steps"></a>後續步驟

跳過[步驟 9： 設定複寫原則](hyper-v-site-walkthrough-replication.md)
