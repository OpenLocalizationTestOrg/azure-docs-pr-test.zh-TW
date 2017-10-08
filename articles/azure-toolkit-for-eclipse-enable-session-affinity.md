---
title: "aaaEnable 工作階段親和性使用 hello Azure Toolkit for Eclipse"
description: "了解如何 tooenable 工作階段親和性使用 hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>啟用工作階段同質
在 hello Azure Toolkit for Eclipse，您可以啟用 HTTP 工作階段親和性或 「 自黏工作階段 」，您的角色。 hello 下列影像顯示 hello**負載平衡**屬性 對話方塊使用 tooenable hello 工作階段親和性功能：

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>tooenable 工作階段親和性，您的角色
1. 以滑鼠右鍵按一下 Eclipse 的專案總管 中的 hello 角色中，按一下**Azure**，然後按一下**負載平衡**。

2. 在 hello **WorkerRole1 負載平衡屬性**對話方塊：

   a. 核取 [為這個角色啟用 HTTP 工作階段同質 (黏性工作階段)] 

   b. 如**輸入端點 toouse**，例如，選取的輸入的端點 toouse， **http （public: 80，private: 8080）**。 您的應用程式必須使用這個端點作為其 HTTP 端點。 您可以啟用多個端點，您的角色，但您可以選取其中一個 toosupport 黏性工作階段。

   c. 重建您的應用程式

啟用之後，如果您有多個角色執行個體，來自特定用戶端的 HTTP 要求會繼續處理 hello 相同角色執行個體。

hello Eclipse 工具組支援此功能安裝到每個角色執行個體稱為 Application Request Routing (ARR) 的特殊 IIS 模組。 ARR 排列 HTTP 要求 toohello 適當的角色執行個體。 hello 工具組會自動重新設定 hello 選取端點，以便 hello 傳入的 HTTP 流量會第一個路由的 toohello ARR 軟體。 hello 工具組也會建立您的 Java 伺服器是設定的 toolisten 至的新內部端點。 這是 hello ARR tooreroute hello HTTP 流量 toohello 適當的角色執行個體所使用的端點。 如此一來，多個執行個體部署中的每個角色執行個體是做為所有的反向 proxy hello 其他情況下，啟用自黏工作階段。

## <a name="notes-about-session-affinity"></a>工作階段同質的相關注意事項
* 工作階段親和性在 hello 計算模擬器中無法運作。 hello 設定可以套用 hello 計算模擬器中，而不會干擾您的建置程序或計算模擬器執行，但 hello 功能本身 hello 計算模擬器中無法運作。

* 啟用工作階段親和性會佔用您的部署在 Azure 中，因為其他軟體會下載並安裝到您的角色執行個體，以 hello Azure 雲端服務啟動時的磁碟空間的 hello 數量的增加。

* hello 時間 tooinitialize 需要較久的每個角色。

* 內部端點，toofunction 流量重新路由傳送器，上面所述為將會加入。


## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
