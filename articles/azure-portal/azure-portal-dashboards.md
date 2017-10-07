---
title: "aaaCreate 和共用 Azure 入口網站的儀表板 |Microsoft 文件"
description: "本文說明如何 toocreate 和編輯的儀表板 hello Azure 入口網站。"
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>建立並共用 hello Azure 入口網站的儀表板
您可以建立多個儀表板並分享與其他人存取 tooyour Azure 訂用帳戶。  這篇文章探討 hello 的建立、 編輯、 發行及管理存取 toodashboards 的基本概念。

## <a name="create-a-dashboard"></a>建立儀表板
toocreate 儀表板中，選取 hello**新儀表板**按鈕下一步 toohello 目前儀表板的名稱。  

![建立儀表板](./media/azure-portal-dashboards/new-dashboard.png)

這個動作會建立全新的空白私人儀表板並讓您進入自訂模式，供您為儀表板命名並新增或重新排列圖格。  在此模式下，hello 可摺疊會並排組件庫會使用透過 hello 左的導覽功能表。  hello 並排組件庫可讓您尋找磚為您的 Azure 資源不同的方式： 您可以瀏覽[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)、 藉由資源類型，由[標記](../azure-resource-manager/resource-group-using-tags.md)，或依名稱搜尋您的資源。  

![自訂儀表板](./media/azure-portal-dashboards/customize-dashboard.png)

將磚加入拖曳和卸除它們拖曳至 hello 儀表板介面想要的位置。

未與特定資源相關聯的圖格有新的類別，其名稱為**一般**。  在此範例中，我們 hello Markdown 圖格釘選。  您使用此磚 tooadd 自訂內容 tooyour 儀表板。  hello 磚支援純文字[Markdown 語法](https://daringfireball.net/projects/markdown/syntax)，和一組有限的 HTML。  (基於安全考量，您無法執行一些作業，例如插入`<script>`標記，或使用特定的樣式項目，可能會干擾 hello 入口網站的 CSS。) 

![新增 Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>編輯儀表板
建立儀表板之後, 您可以釘選圖格來自 hello 並排組件庫或 hello 磚表示刀鋒視窗。 讓我們釘選 hello 表示我們的資源群組。 您也可以是固定項目，或從 hello 資源群組 刀鋒視窗，瀏覽 hello 時。 釘選磚表示法 hello hello 資源群組導致這兩種方法。

![Pin toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Hello 項目釘選，它就會出現在儀表板上。

![檢視儀表板](./media/azure-portal-dashboards/view-dashboard.png)

現在，我們已經 Markdown 磚和資源群組已釘選的 toohello 儀表板，我們可以調整大小及重新排列 hello 磚磚至適合的配置。

暫留並選取"..."或磚上按一下滑鼠右鍵，您可以看到該磚的 hello 內容命令。 預設會有兩個項目：

1. **從儀表板取消釘選**– 移除 hello hello 儀表板圖格
2. **自訂** – 進入自訂模式

![自訂圖格](./media/azure-portal-dashboards/customize-tile.png)

藉由選取自訂，您可以將圖格調整大小並重新排列。 hello 下列影像所示，tooresize 磚中，選取 hello hello 內容功能表上，從新的大小。

![對圖格調整大小](./media/azure-portal-dashboards/resize-tile.png)

或者，如果 hello 磚支援任何大小，您可以拖曳 hello 底端右下角 toohello 預期大小。

![對圖格調整大小](./media/azure-portal-dashboards/resize-corner.png)

之後調整磚的大小，檢視 hello 儀表板。

![檢視圖格](./media/azure-portal-dashboards/view-tile.png)

一旦您完成自訂儀表板時，只需選取 hello**完成自訂**tooexit 自訂模式或以滑鼠右鍵按一下並選取**完成自訂**hello 操作功能表中。

## <a name="publish-a-dashboard-and-manage-access-control"></a>發佈儀表板和管理存取控制
當您建立儀表板時，它是私用根據預設，這表示您可以看到它 hello 唯一人員項目。  toomake 它可見 tooothers，使用 hello**共用**顯示在旁邊的按鈕 hello 其他儀表板的命令。

![共用儀表板](./media/azure-portal-dashboards/share-dashboard.png)

系統會要求您發行至的訂用帳戶和資源群組的儀表板 toobe toochoose。 tooseamlessly 整合 hello 生態系統中的儀表板，我們已共用的儀表板實作做為 Azure 資源 （如此您就無法共用輸入電子郵件地址）。  大部分的 hello 入口網站中的 hello 磚所顯示的存取 toohello 資訊都受到[Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md)。 從存取控制觀點來看，共用儀表板與虛擬機器或儲存體帳戶並無不同。  

讓我們假設您有 Azure 訂用帳戶和您的小組成員已指派給 hello 角色**擁有者**，**參與者**，或**讀取器**hello 訂用帳戶。  使用者是擁有者或參與者都可以 toolist，檢視、 建立、 修改或刪除該訂用帳戶內的儀表板。  讀取器的使用者都能 toolist 和檢視儀表板，但無法修改或刪除它們。  讀取器存取的使用者可以 toomake 本機編輯 tooa 共用儀表板，但您不能 toopublish 這些變更後 toohello 伺服器。  不過，它們可讓 hello 儀表板供自己使用的私用複本。  一如往常，個別的圖格 hello 儀表板上強制執行自己根據它們對應於 hello 資源的存取控制規則。  

為了方便起見，hello 入口網站的發行您朝向您放置儀表板資源群組中的模式稱為體驗指南**儀表板**。  

![發佈儀表板](./media/azure-portal-dashboards/publish-dashboard.png)

您也可以選擇 toopublish 儀表板 tooa 特定資源群組。  hello 該儀表板的存取控制會比對 hello hello 資源群組的存取控制。  使用者可以管理該資源群組中的 hello 資源也會有存取 toohello 儀表板。

![發行儀表板 tooresource 群組](./media/azure-portal-dashboards/publish-to-resource-group.png)

發行您的儀表板之後，hello**共用 + 存取**控制項窗格將會重新整理並顯示 hello 發行儀表板，包括連結 toomanage 使用者存取 toohello 儀表板的相關資訊。  此連結會啟動 hello 標準 Role Based Access Control 刀鋒視窗中使用 toomanage 對於任何 Azure 資源存取。  您可以一律會回到 toothis 檢視選取**共用**。

![管理存取控制](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>後續步驟
* toomanage 資源，請參閱[透過入口網站管理 Azure 資源](../azure-resource-manager/resource-group-portal.md)。
* toodeploy 資源，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](../azure-resource-manager/resource-group-template-deploy-portal.md)。

