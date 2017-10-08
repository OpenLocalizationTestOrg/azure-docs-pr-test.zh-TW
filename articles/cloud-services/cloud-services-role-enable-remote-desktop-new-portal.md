---
title: "Azure 雲端服務中的角色的遠端桌面連線 aaaEnable |Microsoft 文件"
description: "如何 tooconfigure 您的 azure 雲端服務應用程式 tooallow 遠端桌面連線"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>啟用 Azure 雲端服務中角色的遠端桌面連線
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

遠端桌面可讓您在 Azure 中執行的角色 tooaccess hello 桌面。 您可以使用遠端桌面連線 tootroubleshoot 後診斷問題的應用程式，在執行時。

您可以啟用遠端桌面連線您的角色在開發期間包含在服務定義中的 hello 遠端桌面模組，或者您可以選擇透過遠端桌面延伸模組 hello tooenable 遠端桌面。 hello 慣用的方法為 toouse hello 遠端桌面延伸您可以在 hello 應用程式部署而不需要 tooredeploy 您的應用程式時，即使啟用遠端桌面。

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>從 hello Azure 入口網站中設定遠端桌面
hello Azure 入口網站會使用 hello 遠端桌面的擴充方法，因此即使在 hello 應用程式部署之後，您可以啟用遠端桌面。 hello**遠端桌面**刀鋒視窗中的為雲端服務可讓您 tooenable 遠端桌面變更 hello 本機系統管理員帳戶使用 tooconnect toohello 虛擬機器、 hello 憑證用於驗證和設定 hello到期日。

1. 按一下**雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**遠端桌面**。

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. 選擇是否 tooenable 遠端桌面針對個別的角色或所有的角色，然後變更 hello 切換器 hello 值太**啟用**。

3. 填寫使用者名稱、 密碼、 到期，以及憑證的 hello 必要欄位。

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > 當您首次啟用遠端桌面並按一下 [確定] \(打勾記號) 時，所有角色執行個體都會重新啟動。 tooprevent hello 憑證使用的 tooencrypt hello 密碼重新開機，必須安裝在 hello 角色。 重新啟動，tooprevent [hello 雲端服務將憑證上傳](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)，然後傳回 toothis 對話方塊。
   >
   >
3. 在**角色**，選取您想要 tooupdate 或選取 hello 角色**所有**所有角色。

4. 完成組態更新時，按一下 [儲存]。 它將需要一些時間才能在角色執行個體都是準備 tooreceive 連接。

## <a name="remote-into-role-instances"></a>角色執行個體的遠端存取
一旦 hello 角色上啟用遠端桌面，您可以起始直接從 hello Azure 入口網站的連接：

1. 按一下**執行個體**tooopen hello**執行個體**刀鋒視窗。
2. 選取已設定「遠端桌面」的角色執行個體。
3. 按一下**連接**toodownload RDP 檔，以取得 hello 角色執行個體。

    ![雲端服務的遠端桌面](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. 按一下**開啟**然後**連接**toostart hello 遠端桌面連線。

>[!NOTE]
> 如果您的雲端服務坐 NSG 後方，您可能需要 toocreate 規則以允許連接埠上的流量**3389**和**20000**。  遠端桌面使用者連接埠 **3389**。  雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000*** 開啟，如果您有 NSG 可能會封鎖連接。

## <a name="additional-resources"></a>其他資源

[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)
