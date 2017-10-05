---
title: "部署大型部署"
description: "了解如何運用適用於 Eclipse 的 Azure 工具組部署大型部署。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a>部署大型部署
如果您的部署太大，預設的 approot 資料夾無法容納時，可以使用本機儲存資源，作為 JDK 和應用程式伺服器的部署根資料夾。

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>使用本機儲存資源作為大型部署的部署根資料夾
1. 建立新的本機儲存資源。 資源名稱不重要。 儲存資源以角色層級定義。 存取 [本機儲存組態] 對話方塊 (您可透過此對話方塊建立新的本機儲存資源) 最快速的方式是執行下列步驟：以滑鼠右鍵按一下 [專案總管] 檢視中的角色 (若未看見該角色，請展開 Azure 專案節點)，按一下 [Azure]，再按一下 [本機儲存體]。 在 [本機儲存體] 對話方塊中，按一下 [新增] 建立新的本機儲存資源。

2. 將所需的儲存容量設為至少 2048 MB (若小於此設定值，可能會發生 approot 中相同的容量問題)。

3. 請確定已勾選 [ **回收角色執行個體時清除內容** ]，這有助於回收角色執行個體時，避免部署的啟動邏輯與資源中既存的檔案發生衝突。

4. 請確定 [部署後儲存資源目錄路徑的環境變數] 值設為字串 **DEPLOYROOT**。 [本機儲存資源] 對話方塊如下所示。

   ![][ic667943]

或者，若您使用 **DEPLOYROOT** 作為您本機資源的「名稱」，且您未變更自動產生的環境變數名稱 (此例將該名稱設為 **DEPLOYROOT_PATH**)，這也適用於您的應用程式。

如需有關建立本機儲存資源的其他資訊，請參閱[本機儲存體屬性][Local storage properties]。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse] 

如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
