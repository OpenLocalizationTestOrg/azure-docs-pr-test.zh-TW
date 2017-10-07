---
title: "aaaHow tooconfigure 雲端服務 （入口網站） |Microsoft 文件"
description: "了解 tooconfigure 雲端服務在 Azure 中的方式。 了解 tooupdate hello 雲端服務組態和設定遠端存取 toorole 執行個體。 這些範例使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>如何 tooConfigure 雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-configure-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-configure.md)
>
>

您可以在 hello Azure 入口網站中設定雲端服務的 hello 最常使用的設定。 或者，如果您喜歡 tooupdate 組態檔直接下載服務組態檔 tooupdate 」，然後上傳與 hello 組態變更的 hello 更新檔案和更新 hello 雲端服務。 無論如何，hello 組態更新推入 tooall 角色執行個體。

您也可以管理您的雲端服務角色或遠端桌面的它們的 hello 執行個體。

Azure 才能確保服務 99.95%的可用性期間 hello 組態更新如果您有針對每個角色至少兩個角色執行個體。 可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。 如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

## <a name="change-a-cloud-service"></a>變更雲端服務
之後開啟 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 tooyour 雲端服務。 您可以從這裡管理許多層面。

![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)

hello**設定**或**所有設定**連結會開啟 hello**設定**刀鋒視窗，您可以在其中變更 hello**屬性**，變更 hello**組態**，管理 hello**憑證**，安裝程式**警示規則**，及管理 hello**使用者**誰可以存取toothis 雲端服務。

![Azure 雲端服務設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>管理客體作業系統版本

根據預設，Azure 會定期更新客體作業系統 toohello 最新支援映像，在您的服務組態 (.cscfg) 中所指定的作業系統系列 hello 例如 Windows Server 2016。

如果您需要 tootarget 特定的作業系統版本，可以設定在 hello**組態**刀鋒視窗。

![設定作業系統版本](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> 選擇特定的作業系統版本會停用作業系統自動更新，並使修補變成您的責任。 您必須確定您的角色執行個體可接收更新，或您可能會公開您的應用程式 toosecurity 弱點。

## <a name="monitoring"></a>監視
您可以加入警示 tooyour 雲端服務。 按一下 [設定] > [警示規則] > [新增警示]。

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

您可以從這裡設定警示。 以 hello**度量**下拉式清單方塊中，您可以設定警示來 hello 下列類型的資料。

* 磁碟讀取
* 磁碟寫入
* 網路輸入
* 網路輸出
* CPU 百分比

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>從計量圖格設定監視
而不是使用**設定** > **警示規則**，您可以按一下其中一個 hello 度量磚中 hello**監視**區段 hello**雲端服務**刀鋒視窗。

![雲端服務監視](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

從這裡您可以自訂 hello 圖表搭配 hello 磚，或加入警示規則。

## <a name="reboot-reimage-or-remote-desktop"></a>重新啟動、重新安裝映像或遠端桌面
在這個階段中，您無法設定遠端桌面使用 hello **Azure 入口網站**。 不過，您可以設定它透過 hello [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)， [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)，或透過[Visual Studio](../vs-azure-tools-remote-desktop-roles.md)。

首先，請按一下 hello 雲端服務執行個體上。

![雲端服務執行個體](./media/cloud-services-how-to-configure-portal/cs-instance.png)

從 hello 刀鋒視窗，開啟時，您可以起始遠端桌面連線中，從遠端重新啟動 hello 執行個體，或從遠端重新安裝映像 （開始使用新的映像） hello 執行個體。

![雲端服務執行個體按鈕](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>重新設定 .cscfg
您可能需要 tooreconfigure 您的雲端服務，透過 hello[服務組態 (cscfg)](cloud-services-model-and-package.md#cscfg)檔案。 首先，您必須 toodownload 您.cscfg 檔案，請修改它，然後將它上傳。

1. 按一下 hello**設定**圖示或 hello**所有設定**連結向上 hello tooopen**設定**刀鋒視窗。

    ![設定頁面](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. 按一下 hello**組態**項目。

    ![設定刀鋒視窗](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. 按一下 hello**下載** 按鈕。

    ![下載](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. 更新 hello 服務組態檔之後，請上傳，並套用 hello 組態更新：

    ![上傳](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. 選取 hello.cscfg 檔案，然後按一下**確定**。

## <a name="next-steps"></a>後續步驟
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。
* [管理您的雲端服務](cloud-services-how-to-manage-portal.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。
