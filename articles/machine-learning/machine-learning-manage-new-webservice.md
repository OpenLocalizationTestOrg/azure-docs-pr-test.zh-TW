---
title: "aaaUse hello Azure 機器學習 Web 服務入口網站 |Microsoft 文件"
description: "管理存取 tooAzure 機器學習服務工作區，並將部署和管理 ML API web 服務"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>管理 Web 服務使用 hello Azure 機器學習 Web 服務入口網站
您可以管理您使用 hello Microsoft Azure 機器學習 Web 服務入口網站的機器學習新的和傳統的 Web 服務。 因為傳統 Web 服務和新式 Web 服務是根據不同的基礎技術，所以各有稍微不同的管理功能。

在 hello 機器學習 Web 服務入口網站中，您可以：

* 監視 hello web 服務的使用方式。
* 設定 hello 描述，請更新 hello 金鑰 hello web 服務 （僅新）、 更新金鑰 （新增只），啟用記錄，您儲存體帳戶和啟用或停用的範例資料。
* 刪除 hello web 服務。
* 建立、刪除或更新計費方案 (僅限新式)。
* 新增和刪除端點 (僅限傳統)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>新的資源管理員的權限 toomanage 為基礎的 web 服務

新的 Web 服務會部署為 Azure 資源。 因此，您必須擁有 hello 正確的權限 toodeploy 和管理新的 web 服務。  toodeploy 或管理您的參與者必須被指派新的 web 服務或部署 hello 訂用帳戶 toowhich hello web 服務上的系統管理員角色。 您可以邀請其他使用者 tooa 機器學習服務工作區，您必須指派它們 tooa 參與者或系統管理員角色，hello 訂用帳戶才能部署或管理 web 服務。 

若 hello 使用者沒有正確權限 tooaccess 資源 hello Azure 機器學習 Web 服務入口網站中的 hello，就會收到下列錯誤，當嘗試 toodeploy web 服務的 hello:

*Web 服務部署工作失敗。此帳戶沒有足夠的存取 toohello 包含 hello 工作區的 Azure 訂用帳戶。順序 toodeploy Web 服務 tooAzure，hello 相同的帳戶必須是受邀 toohello 工作區，並可指定的存取 toohello Azure 訂用帳戶包含 hello 工作區。*

如需建立工作區的詳細資訊，請參閱[建立和共用 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。

如需設定存取權限的詳細資訊，請參閱[hello Azure 入口網站-公開預覽中的使用者及群組的檢視存取工作分派](../active-directory/role-based-access-control-manage-assignments.md)。


## <a name="manage-new-web-services"></a>管理新式 Web 服務
toomanage 至新的 Web 服務：

1. 登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站使用您的 Microsoft Azure 帳戶-使用 hello 帳戶相關聯 hello Azure 訂用帳戶。
2. 在 [hello] 功能表上按一下**Web 服務**。

這會針對您的訂用帳戶顯示一份已部署的 Web 服務清單。 

toomanage Web 服務，按一下 Web 服務。 您可以從 hello Web 服務 頁面上：

* 按一下 hello web 服務 toomanage 它。
* 按一下 hello 計費計劃的 hello web 服務 tooupdate 它。
* 刪除 Web 服務。
* 複製 web 服務，並將它部署 tooanother 區域。

當您按一下 web 服務時，hello web 服務快速入門 頁面隨即開啟。 hello web 服務快速入門頁面有兩個功能表選項，可讓您 toomanage web 服務：

* **儀表板**-可讓您 tooview Web 服務使用。
* **設定**-允許您 tooadd 描述性文字，更新 hello 機碼 hello 儲存體帳戶與相關聯的 hello Web 服務和啟用或停用的範例資料。

### <a name="monitoring-how-hello-web-service-is-being-used"></a>監視 hello web 服務的使用方式
按一下 hello**儀表板** 索引標籤。

從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。 您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。 hello 儀表板會顯示下列資訊的 hello:

* **要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。 它可以協助識別您所遇到的使用量尖峰。
* **要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。
* **平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。
* **平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。
* **服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。

### <a name="configuring-hello-web-service"></a>設定 hello web 服務
按一下 hello**設定**功能表選項。

您可以更新下列屬性的 hello:

* **描述**可讓您 tooenter hello Web 服務的描述。
* **標題**可讓您 tooenter hello Web 服務的標題
* **索引鍵**可讓您 toorotate 您主要和次要的 API 金鑰。
* **儲存體帳戶金鑰**可讓您 tooupdate hello hello hello Web 服務的變更與相關聯的儲存體帳戶金鑰。 
* **啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。 如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。 如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。

### <a name="managing-billing-plans"></a>管理計費方案
按一下 hello**計劃**從 hello web 服務快速入門 頁面上的功能表選項。 您也可以按一下特定的 Web 服務 toomanage 計劃相關聯的 hello 計劃。

* **新**可讓您 toocreate 新計劃。
* **新增/移除計劃的執行個體**可讓您太 「 向外延展 」 的現有的計劃 tooadd 容量。
* **升級/降級**可讓您太 「 向上延展 」 的現有的計劃 tooadd 容量。
* **刪除**可讓您 toodelete 計劃。

按一下計劃 tooview 其儀表板。 hello 儀表板可讓您使用快照式或計劃在選取的一段時間。 tooselect hello 時間週期 tooview 中，按一下 hello**期間**在儀表板的 hello 右上方的下拉式清單。 

hello 方案儀表板提供下列資訊的 hello:

* **計劃描述**顯示 hello 成本和 hello 計劃相關聯的容量資訊。
* **規劃使用**顯示 hello 的交易和已付費 hello 計劃的計算時數的數字。
* **Web 服務**顯示使用此計劃的 Web 服務的 hello 數目。
* **排名最前面的 Web 服務所呼叫**顯示 hello 前四個 Web 服務，都需支付 hello 計劃的呼叫。
* **Web 服務前所計算的小時**顯示 hello 前四個 Web 服務使用 hello 計劃需支付的運算資源。

## <a name="manage-classic-web-services"></a>管理傳統 Web 服務
> [!NOTE]
> 本節中的 hello 程序是透過 hello Azure 機器學習 Web 服務入口網站的相關 toomanaging 傳統 web 服務。 如需管理傳統 Web 服務透過 hello Machine Learning Studio 和 hello Azure 傳統入口網站，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。
> 
> 

toomanage 傳統 Web 服務：

1. 登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站使用您的 Microsoft Azure 帳戶-使用 hello 帳戶相關聯 hello Azure 訂用帳戶。
2. 在 [hello] 功能表上按一下**傳統 Web 服務**。

toomanage 傳統的 Web 服務，按一下**傳統 Web 服務**。 您可以從 hello 傳統 Web 服務 頁面上：

* 按一下 hello web 服務 tooview 相關聯的 hello 端點。
* 刪除 Web 服務。

當您管理的傳統 Web 服務時，您每個 hello 端點分開管理。 當您按一下 hello Web 服務 頁面中的 web 服務時，會開啟 hello 與 hello 服務相關聯的端點清單。 

在 hello 傳統 Web 服務端點 頁面上，您可以加入及刪除 hello 服務上的端點。 如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。

按一下其中一個 hello 端點 tooopen hello web 服務快速入門頁面。 在 hello 快速入門 頁面上，有兩個功能表選項，可讓您 toomanage web 服務：

* **儀表板**-可讓您 tooview Web 服務使用。
* **設定**-tooadd 描述性文字，可讓您開啟錯誤記錄開啟或關閉更新 hello 機 hello 儲存體帳戶與相關聯的 hello Web 服務，以及啟用和停用的範例資料。

### <a name="monitoring-how-hello-web-service-is-being-used"></a>監視 hello web 服務的使用方式
按一下 hello**儀表板** 索引標籤。

從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。 您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。 hello 儀表板會顯示下列資訊的 hello:

* **要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。 它可以協助識別您所遇到的使用量尖峰。
* **要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。
* **平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。
* **平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。
* **錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。
* **服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。

### <a name="configuring-hello-web-service"></a>設定 hello web 服務
按一下 hello**設定**功能表選項。

您可以更新下列屬性的 hello:

* **描述**可讓您 tooenter hello Web 服務的描述。 [描述] 必要欄位。
* **記錄**可讓您登入 hello 端點 tooenable 或停用錯誤。 如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。
* **啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。 如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。 如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>授予或暫止 hello 入口網站中的使用者的存取 tooWeb 服務
您可以使用 hello Azure 傳統入口網站，允許或拒絕存取 toospecific 使用者。

### <a name="access-for-users-of-new-web-services"></a>新式 Web 服務的使用者存取
tooenable hello Azure 機器學習 Web 服務入口網站中的 Web 服務與其他使用者 toowork，就必須加入為共同管理員 Azure 訂用帳戶。

登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。

1. Hello 瀏覽窗格中，按一下**設定**，然後按一下 **管理員**。
2. 在 hello hello 視窗底部，按一下 **新增**。 
3. 在 hello 新增的共同管理員 對話方塊中，輸入您要 tooadd 做為共同管理員及您想 hello 共同管理員 tooaccess 然後選取 hello 訂閱 hello 人員 hello 電子郵件地址。
4. 按一下 [儲存] 。

### <a name="access-for-users-of-classic-web-services"></a>傳統 Web 服務的使用者存取
toomanage 工作區：

登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。

1. 在 hello Microsoft Azure 服務面板中，按一下  **MACHINE LEARNING**。
2. 按一下您想要 toomanage hello 工作區。
3. 按一下 hello**設定** 索引標籤。

Hello 組態 索引標籤，您可以暫停存取 toohello Machine Learning 工作區依序按一下**拒絕**。 使用者將不再能夠 tooopen Machine Learning Studio 中的 hello 工作區。 toorestore 存取按一下**允許**。

toospecific 使用者：

toomanage 其他帳戶擁有存取 toohello 工作區，在機器學習 Studio 中，按一下**登入 tooML Studio**在 hello**儀表板** 索引標籤。這會開啟 Machine Learning Studio hello 工作區。 從這裡按一下 hello**設定** 索引標籤，然後**使用者**。 您可以按一下**更邀請使用者**toogive 使用者存取 toohello 工作區中，或選取的使用者，然後按一下**移除**。

> [!NOTE]
> hello**登入 tooML Studio**連結會開啟 Machine Learning Studio 使用 hello 目前登入的 Microsoft 帳戶。 hello toosign 用於 toohello Azure 傳統入口網站 toocreate 工作區的 Microsoft 帳戶不會自動具備權限 tooopen 該工作區。 tooopen 工作區中，您必須登入 toohello 已定義為 hello hello 工作區中，擁有者的 Microsoft 帳戶或您需要 tooreceive 從 hello 擁有者 toojoin hello 工作區的邀請。
> 
> 

