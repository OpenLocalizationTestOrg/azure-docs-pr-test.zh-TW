---
title: "aaaDeploy SAP 的 Azure 上的 SAP ERP 6.0 IDE EHP7 SP3 |Microsoft 文件"
description: "在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3
本文說明如何 toodeploy SAP 與 SQL Server 和 Windows 作業系統 hello Azure 上執行 hello SAP 雲端應用裝置程式庫 (SAP CAL) 3.0 透過 IDE 系統。 hello 螢幕擷取畫面顯示 hello 逐步程序。 toodeploy 不同的解決方案，請遵循 hello 相同的步驟。

以 hello SAP CAL，請移 toohello toostart [SAP 雲端應用裝置程式庫](https://cal.sap.com/)網站。 SAP 也有關於 hello 部落格新[SAP 雲端應用裝置程式庫 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)。 

> [!NOTE]
2017 年 29，您可以使用 hello Azure Resource Manager 部署模型，因為除了 toohello 較偏好傳統部署模型 toodeploy hello SAP CAL。 我們建議您使用 hello 新的資源管理員部署模型，並忽略 hello 傳統部署模型。

如果您已經建立的 SAP CAL 帳戶使用 hello 傳統模式，*其他 SAP CAL 帳戶需要 toocreate*。 此帳戶需要 tooexclusively 使用 hello 資源管理員的模型部署至 Azure。

您登入 toohello SAP CAL 之後，第一頁的 hello 通常會引導您 toohello**解決方案**頁面。 hello hello SAP CAL 所提供的方案會持續穩定增加，因此您可能需要 tooscroll 稍微 toofind hello 您想的方案。 可在 Azure 的 hello 反白顯示 windows SAP IDE 解決方案示範 hello 部署程序：

![SAP CAL 解決方案](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>Hello SAP CAL 中建立帳戶
1. 中的 hello toohello SAP CAL toosign 第一次，使用 SAP S-使用者或其他使用者註冊與 SAP。 然後定義 hello Azure 上 SAP CAL toodeploy 應用裝置由 SAP CAL 帳戶。 在 hello 帳戶定義中，您需要：

    a. 選取 hello Azure （「 資源管理員 」 或 「 傳統 」） 上的部署模型。

    b. 輸入您的 Azure 訂用帳戶。 SAP CAL 帳戶可以指派只有 tooone 訂閱。 如果您需要多個訂用帳戶，您需要 toocreate SAP CAL 的其他帳戶。
    
    c. 提供 hello SAP CAL 權限 toodeploy 到您的 Azure 訂閱。

    > [!NOTE]
    hello 接下來的步驟顯示如何 toocreate SAP CAL 帳戶資源管理員部署。 如果您已經有 SAP CAL 帳戶是連結的 toohello 傳統部署模型，您*需要*toofollow 這些步驟 toocreate 新 SAP CAL 帳戶。 hello 新 SAP CAL 帳戶需要 toodeploy hello 資源管理員模型中。

2. 新的 SAP CAL toocreate 帳戶，hello**帳戶**頁面會顯示 Azure 兩個選擇： 

    a. **Microsoft Azure （傳統）** hello 傳統部署模型，而不會再慣用。

    b. **Microsoft Azure**是 hello 新的資源管理員部署模型。

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    toodeploy 在 hello 資源管理員模型中，選取**Microsoft Azure**。

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. 輸入 hello Azure**訂用帳戶 ID**可以在 hello Azure 入口網站上找到的。 

    ![SAP CAL 訂用帳戶識別碼](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. 定義 tooauthorize hello SAP CAL toodeploy 到 hello Azure 訂用帳戶中，按一下**授權**。 hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：

    ![Internet Explorer 雲端服務登入](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. 如果列出多個使用者，請選擇屬於 hello 您選取的 Azure 訂用帳戶的連結的 toobe hello coadministrator hello Microsoft 帳戶。 hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：

    ![Internet Explorer 雲端服務確認](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. 按一下 [接受]。 Hello 授權是否成功，會再次顯示 hello SAP CAL 帳戶定義。 在一段時間之後, 會出現確認訊息 hello 授權程序成功。

7. tooassign hello 新建立的 SAP CAL 帳戶 tooyour 使用者中，輸入您**使用者識別碼**在 hello hello 右邊的文字方塊中，按一下 **新增**。 

    ![帳戶 toouser 關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. tooassociate toohello SAP CAL 用於 toosign 您帳戶的 hello 使用者按一下**檢閱**。 

9. toocreate hello 關聯使用者與 hello 新建立的 SAP CAL 帳戶，請按一下**建立**。

    ![使用者 tooaccount 關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

您已成功建立可執行下列作業的 SAP CAL 帳戶：

- 使用 hello Resource Manager 部署模型。
- 將 SAP 系統部署到您的 Azure 訂用帳戶。

> [!NOTE]
您可以部署 Windows 和 SQL Server 為基礎的 hello SAP IDE 解決方案之前，您可能需要 toosign SAP CAL 訂用帳戶註冊。 否則，hello 方案可能會顯示為**鎖定**hello 概觀 頁面上。

### <a name="deploy-a-solution"></a>部署解決方案
1. 您將 SAP CAL 帳戶設定之後，請選取**hello Windows 和 SQL Server 上的 SAP IDE 解決方案**方案。 按一下**建立執行個體**，並確認 hello 使用量和詞彙的條件。 

2. 在 hello**基本模式： 建立執行個體**頁面上，您需要：

    a. 輸入執行個體**名稱**。

    b.這是另一個 C# 主控台應用程式。 選取 Azure **區域**。 您可能需要多個 Azure 區域提供 SAP CAL 訂用帳戶 tooget。

    c.  輸入 hello master**密碼**hello 方案，如所示：

    ![SAP CAL 基本模式：建立執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. 按一下 [建立] 。 一段時間後 hello 大小和複雜度 hello 方案 (hello SAP CAL 提供的估計值)，根據 hello 狀態會顯示為作用中且可供使用： 

    ![SAP CAL 執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. toofind hello 資源群組及其所建立的所有物件 hello SAP CAL 資訊，請 toohello Azure 入口網站。 開頭為相同執行個體名稱指定在 hello SAP CAL hello 可以找到 hello 虛擬機器。

    ![資源群組物件](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. 在 hello SAP CAL 入口網站中，移 toohello 部署執行個體，然後按一下**連接**。 此時會出現下列快顯視窗中的 hello: 

    ![連接 toohello 執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. 您可以使用其中一個 hello 選項 tooconnect toohello 部署系統之前，請按一下**入門指南**。 hello 文件名稱 hello 使用者針對每個 hello 連線方法。 hello 密碼，這些使用者會在 hello 開頭 hello 部署程序設定 toohello 您定義的主要密碼。 在 hello 文件，其他多運作的使用者會列出與他們的密碼，您可以使用在 toohello toosign 部署系統。

    ![SAP 歡迎使用文件](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

在幾個小時內，狀況良好的 SAP IDES 系統便會部署在 Azure 中。

如果您購買的 SAP CAL 訂用帳戶時，SAP 完全支援透過 hello SAP CAL 部署在 Azure 上。 hello 支援佇列是 BC-VCM-CAL。

