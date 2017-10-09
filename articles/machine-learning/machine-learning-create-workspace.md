---
title: "aaaCreate Machine Learning 工作區 |Microsoft 文件"
description: "如何 toocreate Azure Machine Learning Studio 中的工作區"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>建立和共用 Azure Machine Learning 工作區
這個功能表連結描述如何設定 hello tooset 各種資料科學環境使用 hello Cortana 分析程序 (CAP) 的 tootopics。

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse Azure Machine Learning Studio 中，您需要 toohave Machine Learning 工作區。 此工作區包含所需 toocreate hello 工具、 管理及發佈實驗。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate 工作區
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)

    > [!NOTE]
    > toosign 中的和建立工作區，您需要 toobe Azure 訂用帳戶系統管理員。 
    >
    > 

2. 按一下 [+ 新增]

3. 選取 [智慧 + 分析]按一下 [Machine Learning 工作區]，然後按一下 [建立]

4. 輸入您的工作區資訊

    - hello*工作區名稱*too260 字元、 空格結尾不存在。 hello 名稱不能包含下列字元：`< > * % & : \ ? + /`
    - hello *web 服務計劃*您選擇 （或建立），以及相關聯的 hello*定價層*您選取，如果您將部署此工作區的 web 服務使用。

    ![建立新的工作區](media/machine-learning-create-workspace/create-new-workspace.png)

5. 按一下 [建立] 

Hello 工作區部署之後，您可以在 Machine Learning Studio 中開啟它。

1. 瀏覽 tooMachine Learning Studio 在[https://studio.azureml.net/](https://studio.azureml.net/)。

2. 選取您的工作區在 hello 上限右手邊角。

    ![選取工作區](media/machine-learning-create-workspace/open-workspace.png)

3. 按一下 [我的實驗]。

    ![開啟實驗](media/machine-learning-create-workspace/my-experiments.png)

如需管理您的工作區的詳細資訊，請參閱 [管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。
如果您遇到問題，建立您的工作區，請參閱[疑難排解指南： 建立和連線 tooa Machine Learning 工作區](machine-learning-troubleshooting-creating-ml-workspace.md)。


## <a name="sharing-an-azure-machine-learning-workspace"></a>共用 Azure 機器學習服務工作區
一旦建立機器學習服務工作區，您可以邀請使用者 tooyour 工作區 tooshare 存取 tooyour 工作區和所有其實驗、 資料集、 筆記本等等。您可以將使用者新增至兩個角色之一︰

* **使用者**-工作區中使用者可以建立、 開啟、 修改及刪除實驗、 資料集等 hello 工作區中。
* **擁有者**-擁有者可以邀請，並移除 hello 工作區中增加 toowhat 使用者的使用者可以執行。

> [!NOTE]
> 建立 hello 工作區中的 hello 系統管理員帳戶會自動加入 toohello 工作區中，為工作區擁有者。 不過，其他的系統管理員或使用者，因為訂用帳戶不會自動授與存取權 toohello 工作區-您需要 tooinvite 它們明確。
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare 工作區

1. 登入 tooMachine 學習 Studio 在[https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. 在 hello 左面板中，按一下 **設定**

3. 按一下 hello**使用者** 索引標籤

4. 按一下**更邀請使用者**hello hello 頁底端

    ![Studio 設定](media/machine-learning-create-workspace/settings.png)

5. 輸入一或多個電子郵件地址。 hello 使用者需要有效的 Microsoft 帳戶或組織帳戶 （從 Azure Active Directory)。

6. 選取是否要 tooadd hello 使用者作為擁有者或使用者。

7. 按一下 hello**確定**核取記號按鈕。

您新增的每個使用者會收到一封電子郵件，說明如何在 toohello toosign 共用工作區。

> [!NOTE]
> 針對使用者 toobe 無法 toodeploy 或管理 web 服務，此工作區中的，它們必須參與者或 hello Azure 訂用帳戶中的系統管理員。 



