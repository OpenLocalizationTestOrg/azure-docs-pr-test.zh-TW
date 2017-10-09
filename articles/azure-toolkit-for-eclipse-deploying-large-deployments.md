---
title: "aaaDeploying 大型部署"
description: "了解如何使用 toodeploy 大型部署 hello Azure Toolkit for Eclipse。"
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
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>部署大型部署
如果您的部署太大 toobe hello 預設的 approot 資料夾中所包含，可用於本機儲存體資源 hello 部署根資料夾為 JDK 和應用程式伺服器。

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse 做為大型部署的 hello 部署根資料夾的本機儲存體資源
1. 建立新的本機儲存資源。 hello hello 資源名稱並不重要。 Hello 角色層級定義的存放裝置資源。 hello 最快方式 tooaccess hello 本機儲存體組態對話方塊中，您可以從中建立新的本機儲存體資源，是使用下列步驟的 hello: hello 中的以滑鼠右鍵按一下 hello 角色**Project Explorer**檢視 (依序展開您Azure 專案節點如果您沒有看見 hello 角色），按一下  **Azure**，然後按一下**本機儲存體**。 在 [hello**本機儲存體**] 對話方塊中，按一下**新增**toocreate 新的本機儲存體資源。

2. 設定 hello 預期大小 tooat （任何較不可能會造成 hello 相同的檔案大小問題一樣遇到 hello approot） 至少 2048 MB。

3. 請確認**hello 角色執行個體回收時清除 hello 內容**選取的; 這將有助於避免 hello 部署的啟動邏輯與 hello 資源中已存在的檔案發生衝突時 hello 角色執行個體就會回收。

4. 請確定該 hello**環境變數儲存部署後 hello 資源的目錄路徑**設 toohello 字串**DEPLOYROOT**。 您的本機儲存體資源對話方塊看起來類似 toohello 下列。

   ![][ic667943]

或者，如果您使用**DEPLOYROOT**為 hello*名稱*的本機資源，您不變更 hello 自動產生的環境變數名稱 (會太設**DEPLOYROOT_PATH**在此情況下)，也將適用於您應用程式。

如需有關建立本機儲存資源的其他資訊，請參閱[本機儲存體屬性][Local storage properties]。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
