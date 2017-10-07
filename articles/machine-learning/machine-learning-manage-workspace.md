---
title: "aaaManage Machine Learning 工作區 |Microsoft 文件"
description: "管理存取 tooAzure 機器學習服務工作區，並將部署和管理 ML API web 服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>管理 Azure Machine Learning 工作區

> [!NOTE]
> 如需管理 hello 機器學習 Web 服務入口網站中的 Web 服務的資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。
> 
> 

您可以管理任一 hello Azure 入口網站中的機器學習服務工作區，或 hello Azure 傳統入口網站。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站

toomanage hello Azure 入口網站中的工作區：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)使用的 Azure 訂用帳戶系統管理員帳戶。
2. 在 hello 頁面頂端的 hello hello 搜尋方塊中輸入 「 機器學習服務工作區 」，然後選取**機器學習工作區**。
3. 按一下您想要 toomanage hello 工作區。

此外 toohello 標準資源管理資訊和可用的選項，您可以：

- 檢視**屬性**-此頁面會顯示 hello 工作區和資源資訊，而且您可以變更訂閱 hello 與此工作區會連接到資源群組。
- **重新同步處理儲存體金鑰**-hello 工作區會維護金鑰 toohello 儲存體帳戶。 如果 hello 儲存體帳戶變更索引鍵，則您可以按一下**重新同步處理金鑰**toosynchronize hello hello 工作區金鑰。

此工作區中，與相關聯的 toomanage hello web 服務使用 hello 機器學習 Web 服務入口網站。 請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)如需完整資訊。

> [!NOTE]
> toodeploy 或管理您的參與者必須被指派新的 web 服務或部署 hello 訂用帳戶 toowhich hello web 服務上的系統管理員角色。 您可以邀請其他使用者 tooa 機器學習服務工作區，您必須指派它們 tooa 參與者或系統管理員角色，hello 訂用帳戶才能部署或管理 web 服務。 
> 
>如需設定存取權限的詳細資訊，請參閱[hello Azure 入口網站-公開預覽中的使用者及群組的檢視存取工作分派](../active-directory/role-based-access-control-manage-assignments.md)。

## <a name="use-hello-azure-classic-portal"></a>使用 hello Azure 傳統入口網站

您可以使用 hello Azure 傳統入口網站，管理您的機器學習服務工作區，以：

* 監視 [hello] 工作區中的使用方式
* 設定 [hello] 工作區 tooallow 或拒絕存取
* 管理在 hello 工作區中建立的 Web 服務
* 刪除 hello 工作區

此外，hello 儀表板索引標籤會提供您工作區的使用方式的概觀，以及您的工作區資訊的快速概覽。  

> [!TIP]
> 在 hello，Azure Machine Learning Studio 中**WEB 服務**索引標籤上，您可以加入、 更新或刪除的機器學習 Web 服務。
> 
> 

toomanage hello Azure 傳統入口網站中的工作區：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。
2. 在 hello Microsoft Azure 服務面板中，按一下  **MACHINE LEARNING**。
3. 按一下您想要 toomanage hello 工作區。

hello 工作區頁面有三個索引標籤：

* **儀表板**-可讓您 tooview 工作區的使用方式和資訊
* **設定**-可讓您工作區中存取 toohello toomanage
* **WEB 服務**-可讓您 toomanage 從此工作區已發佈的 Web 服務

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor hello 工作區中的使用方式
按一下 hello**儀表板** 索引標籤。

從 hello 儀表板，您可以檢視工作區的整體使用狀況，並取得工作區資訊的快速概覽。

* hello**計算**圖表可顯示 hello hello 工作區正在使用的計算資源。 您可以變更 hello 檢視 toodisplay 相對或絕對值，而且您可以變更 hello hello 圖表中顯示的時間範圍內。
* **使用量概觀**顯示 hello 工作區正在使用的 Azure 儲存體。
* **快速概覽** 提供工作區資訊和實用連結的摘要。

> [!NOTE]
> hello**登入 tooML Studio**連結會開啟 Machine Learning Studio 使用 hello 目前登入的 Microsoft 帳戶。 hello toosign 用於 toohello Azure 傳統入口網站 toocreate 工作區的 Microsoft 帳戶不會自動具備權限 tooopen 該工作區。 tooopen 工作區中，您必須登入 toohello 已定義為 hello hello 工作區中，擁有者的 Microsoft 帳戶或您需要 tooreceive 從 hello 擁有者 toojoin hello 工作區的邀請。
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant 或暫止使用者的存取權
按一下 hello**設定** 索引標籤。

您可以從 hello 設定 索引標籤：

* 暫停存取 toohello Machine Learning 工作區，按一下 [拒絕]。 使用者將不再能夠 tooopen Machine Learning Studio 中的 hello 工作區。 toorestore 存取，請按一下 [允許]。

toomanage 其他帳戶擁有存取 toohello 工作區，在機器學習 Studio 中，按一下**登入 tooML Studio**在 hello**儀表板** 索引標籤 (請參閱 hello 前面附註有關**Sign-in tooML Studio**)。 這會開啟 Machine Learning Studio hello 工作區。 從這裡按一下 hello**設定** 索引標籤，然後**使用者**。 您可以按一下**更邀請使用者**toogive 使用者存取 toohello 工作區中，或選取的使用者，然後按一下**移除**。

### <a name="toomanage-web-services-in-this-workspace"></a>此工作區中的 toomanage web 服務
按一下 hello **WEB 服務** 索引標籤。

這會顯示從此工作區發佈的 Web 服務的清單。
toomanage web 服務，按一下 hello 清單 tooopen hello Web 服務頁面中的 hello 名稱。

Web 服務可能會有一個或多個定義的端點。

* 您可以新增 toohello"Default"端點中定義多個端點。 tooadd hello 端點，請按一下**管理端點**底部 hello hello 儀表板 tooopen hello Azure 機器學習 Web 服務入口網站。
* toodelete 端點 （您無法刪除 hello"Default"端點），按一下 [hello] 核取方塊，在 hello 開頭 hello 端點的資料列，然後按一下**刪除**。 這會移除 hello 端點從 hello Web 服務。
  
  > [!NOTE]
  > 如果刪除 hello 端點時，應用程式正在使用 hello web 服務端點，hello 應用程式會在下一次嘗試 tooaccess hello 服務時收到錯誤 hello。
  > 
  > 

按一下 Web 服務端點 tooopen hello 名稱它。 

從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。 您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。 hello 儀表板會顯示下列資訊的 hello:

* **要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。 它可以協助識別您所遇到的使用量尖峰。
* **要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。
* **平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。
* **平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。
* **服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。

從 hello 設定 頁面，您可以更新下列屬性的 hello:

* **描述**可讓您 tooenter hello Web 服務的描述。 [描述] 必要欄位。
* **記錄**可讓您登入 hello 端點 tooenable 或停用錯誤。 如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。
* **啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。 如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。 如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。

