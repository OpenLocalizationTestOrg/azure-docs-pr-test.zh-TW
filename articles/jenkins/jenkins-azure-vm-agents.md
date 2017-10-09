---
title: "與 Jenkins 連續整合 aaaUse Azure VM 代理程式。"
description: "Azure VM 代理程式作為 Jenkins 從屬。"
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>使用 Azure VM 代理程式與 Jenkins 持續整合。

本快速入門示範如何 toouse 會 hello Jenkins Azure VM 代理程式外掛程式 toocreate 隨 Linux (Ubuntu) 代理程式在 Azure 中。

## <a name="prerequisites"></a>必要條件

toocomplete 本快速入門：

* 如果您還沒有 Jenkins master，就可以開始 hello[方案範本](install-jenkins-solution-template.md) 
* 請參閱太[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)如果您還沒有 Azure 服務主體。

## <a name="install-azure-vm-agents-plugin"></a>安裝 Azure VM 代理程式外掛程式

如果您從 hello 啟動[方案範本](install-jenkins-solution-template.md)，會安裝在 hello Jenkins master 中的 hello Azure VM 代理程式外掛程式。

否則，安裝 hello **Azure VM 代理程式**hello Jenkins 儀表板中的外掛程式。

## <a name="configure-hello-plugin"></a>設定 hello 外掛程式

* 在 hello Jenkins 儀表板內，按一下**管理 Jenkins-> 設定系統->** 。 捲動 toohello hello 頁面的底部，找出與 hello 下拉式清單中的 hello 區段**加入新的雲端**。 從 [hello] 功能表中，選取**Microsoft Azure VM 代理程式**
* 從 hello Azure 認證下拉式清單中選取現有的帳戶。  新的 tooadd **Microsoft Azure 服務主體，**輸入 hello 下列值： 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點。

![Azure 認證](./media/jenkins-azure-vm-agents/service-principal.png)

* 按一下**確認組態**toomake hello 設定檔設定是否正確。
* 儲存 hello 組態，並繼續 toohello 下一個步驟。

## <a name="template-configuration"></a>範本設定

### <a name="general-configuration"></a>一般設定
接著，設定使用 toodefine Azure VM 代理程式的範本。 

* 按一下**新增**tooadd 範本。 
* 提供新範本的名稱。 
* 為 hello 標籤，請輸入"ubuntu。 」 此標籤還可用於 hello 工作設定。
* 從 hello 下拉式方塊中選取 hello 所需的區域。
* 選取 hello 所需的 VM 大小。
* 指定 hello Azure 儲存體帳戶名稱，或保持空白 toouse hello 預設名稱 「 jenkinsarmst。 」
* 指定以分鐘為單位的 hello 保留時間。 此設定會定義 hello Jenkins 可以自動刪除閒置的代理程式之前等待的分鐘數。 如果您不想自動刪除閒置的代理程式 toobe，指定為 0。

![一般設定](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>映像設定

toocreate Linux (Ubuntu) 代理程式中，選取**映像參考**並使用 hello 遵循組態的範例。 請參閱太[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello 最新的 Azure 支援映像。

* 映像發佈者︰Canonical
* 映像提供：UbuntuServer
* 映像 Sku：14.04.5-LTS
* 映像版本：最新
* OS 類型：Linux
* 啟動方法：SSH
* 提供管理員認證
* 針對 VM 初始化指令碼，請輸入：
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![映像設定](./media/jenkins-azure-vm-agents/image-config.png)

* 按一下**驗證範本**tooverify hello 組態。
* 按一下 [儲存] 。

## <a name="create-a-job-in-jenkins"></a>在 Jenkins 中建立作業

* 在 hello Jenkins 儀表板內，按一下**新項目**。 
* 輸入名稱並選取 [Freestyle 專案]，然後按一下 [確定]。
* 在 hello**一般**索引標籤、 選取"限制可以執行專案"和"ubuntu"標籤運算式中的型別。 現在，您會看到 「 ubuntu"hello 下拉式清單中。
* 按一下 [儲存] 。

![設定作業](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>建置新專案

* 返回 toohello Jenkins 儀表板。
* Hello 新工作時，以滑鼠右鍵按一下您建立群組，然後按一下 **現在就建置**。 隨即開始建置。 
* Hello 建置完成之後，請跳過**主控台輸出**。 您會看到 hello 建置在 Azure 上已從遠端執行。

![主控台輸出](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>參考

* Azure 星期五視訊：[使用 Azure VM 代理程式與 Jenkins 持續整合](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* 支援資訊和設定選項：[Azure VM 代理程式 Jenkins 外掛程式 Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

