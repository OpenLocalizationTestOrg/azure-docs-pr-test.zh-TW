---
title: "SAP S/4HANA 或 Azure VM 上的 BW/4HANA aaaDeploy |Microsoft 文件"
description: "在 Azure VM 上部署 SAP S/4HANA 或 BW/4HANA"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>在 Azure 上部署 SAP S/4HANA 或 BW/4HANA
本文說明如何使用 toodeploy 在 Azure 上的 S/4HANA hello SAP 雲端應用裝置程式庫 (SAP CAL) 3.0。 toodeploy 其他 SAP HANA 為基礎的解決方案，例如 BW/4HANA，遵循 hello 相同的步驟。

> [!NOTE]
如需 hello SAP CAL 的詳細資訊，請移至 toohello [SAP 雲端應用裝置程式庫](https://cal.sap.com/)網站。 SAP 也有關於 hello 部落格[SAP 雲端應用裝置程式庫 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)。

> [!NOTE]
2017 年 29，您可以使用 hello Azure Resource Manager 部署模型，因為除了 toohello 較偏好傳統部署模型 toodeploy hello SAP CAL。 我們建議您使用 hello 新的資源管理員部署模型，並忽略 hello 傳統部署模型。

## <a name="step-by-step-process-toodeploy-hello-solution"></a>逐步程序 toodeploy hello 解決方案

hello 下列螢幕擷取畫面的順序顯示如何使用 toodeploy 在 Azure 上的 S/4HANA hello SAP CAL。 hello 程序的運作 hello 其他解決方案，例如 BW/4HANA 相同的方式。

hello**解決方案**頁面會顯示某些 hello SAP CAL HANA 為基礎的解決方案可在 Azure 上。 **SAP S/4HANA 1610 FPS01，Fully-Activated 應用裝置**位於 hello 中間的資料列：

![SAP CAL 解決方案](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Hello SAP CAL 中建立帳戶
1. 中的 hello toohello SAP CAL toosign 第一次，使用 SAP S-使用者或其他使用者註冊與 SAP。 然後定義 hello Azure 上 SAP CAL toodeploy 應用裝置由 SAP CAL 帳戶。 在 hello 帳戶定義中，您需要：

    a. 選取 hello Azure （「 資源管理員 」 或 「 傳統 」） 上的部署模型。

    b. 輸入您的 Azure 訂用帳戶。 SAP CAL 帳戶可以指派只有 tooone 訂閱。 如果您需要多個訂用帳戶，您需要 toocreate SAP CAL 的其他帳戶。

    c. 提供 hello SAP CAL 權限 toodeploy 到您的 Azure 訂閱。

    > [!NOTE]
    hello 接下來的步驟顯示如何 toocreate SAP CAL 帳戶資源管理員部署。 如果您已經有 SAP CAL 帳戶是連結的 toohello 傳統部署模型，您*需要*toofollow 這些步驟 toocreate 新 SAP CAL 帳戶。 hello 新 SAP CAL 帳戶需要 toodeploy hello 資源管理員模型中。

2. 建立新的 SAP CAL 帳戶。 hello**帳戶**頁面會顯示 Azure 三個選項： 

    a. **Microsoft Azure （傳統）** hello 傳統部署模型，而不會再慣用。

    b. **Microsoft Azure**是 hello 新的資源管理員部署模型。

    c. **Windows Azure 由 21Vianet 運作**是中國使用 hello 傳統部署模型中的選項。

    toodeploy 在 hello 資源管理員模型中，選取**Microsoft Azure**。

    ![SAP CAL 帳戶詳細資料](./media/cal-s4h/s4h-pic-2a.png)

3. 輸入 hello Azure**訂用帳戶 ID**可以在 hello Azure 入口網站上找到的。

   ![SAP CAL 帳戶](./media/cal-s4h/s4h-pic3c.png)

4. 定義 tooauthorize hello SAP CAL toodeploy 到 hello Azure 訂用帳戶中，按一下**授權**。 hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：

   ![Internet Explorer 雲端服務登入](./media/cal-s4h/s4h-pic4c.png)

5. 如果列出多個使用者，請選擇屬於 hello 您選取的 Azure 訂用帳戶的連結的 toobe hello coadministrator hello Microsoft 帳戶。 hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：

   ![Internet Explorer 雲端服務確認](./media/cal-s4h/s4h-pic5a.png)

6. 按一下 [接受]。 Hello 授權是否成功，會再次顯示 hello SAP CAL 帳戶定義。 在一段時間之後, 會出現確認訊息 hello 授權程序成功。

7. tooassign hello 新建立的 SAP CAL 帳戶 tooyour 使用者中，輸入您**使用者識別碼**在 hello hello 右邊的文字方塊中，按一下 **新增**。

   ![帳戶 toouser 關聯](./media/cal-s4h/s4h-pic8a.png)

8. tooassociate toohello SAP CAL 用於 toosign 您帳戶的 hello 使用者按一下**檢閱**。 
 
9. toocreate hello 關聯使用者與 hello 新建立的 SAP CAL 帳戶，請按一下**建立**。

   ![使用者 tooSAP CAL 帳戶關聯](./media/cal-s4h/s4h-pic9b.png)

您已成功建立可執行下列作業的 SAP CAL 帳戶：

- 使用 hello Resource Manager 部署模型。
- 將 SAP 系統部署到您的 Azure 訂用帳戶。

現在您可以開始 toodeploy S/4HANA 到您在 Azure 中的使用者訂閱。

> [!NOTE]
在繼續之前，請先確定您是否有適用於 Azure H 系列 VM 的 Azure 核心配額。 在 hello 的時刻，hello SAP CAL 使用的 Azure Vm H 數列 toodeploy 某些 hello SAP HANA 為基礎的解決方案。 您的 Azure 訂用帳戶可能沒有 H 系列的核心配額。 如果是這樣，您可能需要 toocontact Azure 支援 tooget H 系列的最少 16 個核心的配額。

> [!NOTE]
當您部署在 Azure 中 SAP CAL hello 的解決方案時，您可能會發現，您可以選擇只有一個 Azure 區域。 其中一個 hello SAP CAL 所建議 toodeploy 成 hello 以外的 Azure 區域，，您需要 toopurchase 從 SAP CAL 訂用帳戶。 您也可能需要 tooopen SAP toohave 訊息您 CAL 帳戶啟用 toodeliver 成 hello 一開始建議的項目以外的 Azure 區域。

### <a name="deploy-a-solution"></a>部署解決方案

讓我們來部署解決方案從 hello**解決方案**hello SAP CAL 的頁面。 hello SAP CAL 有兩個序列 toodeploy:

- 都使用一個頁面 toodefine hello 系統 toobe 部署的基本順序
- 進階順序則會有某些 VM 大小可供您選擇 

我們將示範 hello 基本路徑 toodeployment。

1. 在 hello**帳戶詳細資料**頁面上，您需要：

    a. 選取 SAP CAL 帳戶  （使用 hello Resource Manager 部署模型與相關聯的 toodeploy 帳戶）。

    b. 輸入執行個體**名稱**。

    c. 選取 Azure **區域**。 hello SAP CAL 會建議一個區域。 如果您需要另一個 Azure 區域，而且您不需要在 SAP CAL 訂用帳戶，您需要與 SAP tooorder CAL 訂用帳戶。

    d. 輸入主要**密碼**8 或 9 個字元的 hello 解決方案。 hello hello 不同元件的系統管理員，使用 hello 密碼。

   ![SAP CAL 基本模式：建立執行個體](./media/cal-s4h/s4h-pic10a.png)

2. 按一下**建立**，在出現的 hello 訊息方塊中按一下**確定**。

   ![SAP CAL 支援的 VM 大小](./media/cal-s4h/s4h-pic10b.png)

3. 在 hello**私密金鑰**對話方塊中，按一下**存放區**toostore hello 私密金鑰 hello SAP CAL。 按一下 toouse hello 私用金鑰的密碼保護**下載**。 

   ![SAP CAL 私密金鑰](./media/cal-s4h/s4h-pic10c.png)

4. 讀取 hello SAP CAL**警告**訊息，然後按一下**確定**。

   ![SAP CAL 警告](./media/cal-s4h/s4h-pic10d.png)

    現在 hello 部署就會發生。 一段時間後 hello 大小和複雜度 hello 方案 (hello SAP CAL 提供的估計值)，根據 hello 顯示狀態為作用中且可供使用。

5. toofind hello 虛擬機器，以收集 hello 一個資源群組中其他相關聯的資源，請移 toohello Azure 入口網站： 

   ![Hello 新入口網站中部署的 SAP CAL 物件](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. 在 hello SAP CAL 入口網站，hello 狀態會顯示為**Active**。 tooconnect toohello 方案中，按一下 **連接**。 不同的選項 tooconnect toohello 不同元件部署這個方案中。

   ![SAP CAL 執行個體](./media/cal-s4h/active_solution.png)

7. 您可以使用其中一個 hello 選項 tooconnect toohello 部署系統之前，請按一下**入門指南**。 

   ![連接 toohello 執行個體](./media/cal-s4h/connect_to_solution.png)

    hello 文件名稱 hello 使用者針對每個 hello 連線方法。 hello 密碼，這些使用者會在 hello 開頭 hello 部署程序設定 toohello 您定義的主要密碼。 在 hello 文件，其他多運作的使用者會列出與他們的密碼，您可以使用在 toohello toosign 部署系統。 

    例如，如果您使用 hello 已預先安裝 SAP GUI hello Windows 遠端桌面的電腦上，hello S/4 系統看起來可能像這樣：

   ![在 hello SM50 預先安裝 SAP GUI](./media/cal-s4h/gui_sm50.png)

    或者，如果您使用 hello DBACockpit，hello 執行個體可能會看起來像這樣：

   ![在 hello DBACockpit SAP GUI SM50](./media/cal-s4h/dbacockpit.png)

在幾個小時內，狀況良好的 SAP S/4 應用裝置便會部署在 Azure 中。

如果您購買的 SAP CAL 訂用帳戶時，SAP 完全支援透過 hello SAP CAL 部署在 Azure 上。 hello 支援佇列是 BC-VCM-CAL。







