---
title: "aaaHow tooretain 常數 Azure 雲端服務的虛擬 IP 位址 |Microsoft 文件"
description: "了解如何 tooensure hello 虛擬 IP 位址 (VIP) 的 Azure 雲端服務，並不會變更。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>保持 Azure 雲端服務的固定虛擬 IP 位址
當您更新雲端服務裝載於 Azure 時，您可能需要 tooensure hello 虛擬 IP 位址 (VIP) hello 服務不會變更。 許多網域管理服務使用 hello 網域名稱系統 (DNS) 註冊網域名稱。 DNS 只有 hello VIP 會維持為 hello 相同。 您可以使用 hello**發行精靈**hello VIP 的雲端服務不會變更時的 Azure Tools tooensure 您更新它。 如需有關如何 toouse DNS 網域管理雲端服務，請參閱[設定 Azure 雲端服務的自訂網域名稱](cloud-services/cloud-services-custom-domain-name.md)。

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>發佈雲端服務而不變更其 VIP
當您第一次將它部署在特定的環境中，例如 hello 實際執行環境的 tooAzure 配置 hello VIP 的雲端服務。 只有明確刪除 hello 部署或隱含地刪除 hello 部署的 hello 部署的 hello VIP 變更的更新程序。 tooretain hello VIP，您必須刪除您的部署，您必須先確定 Visual Studio 並不會自動刪除您的部署。 

您可以指定部署設定中 hello**發行精靈**，可支援多種部署選項。 您可以指定全新部署或更新部署，後者可以是累加或同時的。 這兩種更新部署保留 hello VIP。 如需這些不同類型部署的定義，請參閱 [發佈 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)。 此外，您可以控制是否要在發生錯誤時，刪除 hello 先前部署的雲端服務。 如果您未正確設定該選項，hello VIP 可能會意外變更。

## <a name="update-a-cloud-service-without-changing-its-vip"></a>更新雲端服務而不變更其 VIP
1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。 

2. 在**方案總管 中**，以滑鼠右鍵按一下 hello 專案。 Hello 捷徑功能表上，選取**發行**。

    ![Publish menu](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. 在 hello**發行 Azure 應用程式**對話方塊中，選取 hello Azure 訂用帳戶 toowhich 想 toodeploy。 視需要登入，然後選取 [下一步]。

    ![發佈 Azure 應用程式登入頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. 在 hello**一般設定**索引標籤上，確認您要部署，hello hello 雲端服務 toowhich hello 名稱**環境**，hello**組建組態**，和 hello**服務組態**都正確。

    ![發佈 Azure 應用程式一般設定索引標籤](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. 在 hello**進階設定**索引標籤上，確認該 hello**部署標籤**和 hello**儲存體帳戶**正確無誤。 請確認該 hello**失敗時刪除部署**核取方塊已清除，並確認該 hello**部署更新**選取核取方塊。 透過清除 hello**失敗時刪除部署**您核取方塊，確保 VIP 部署期間發生錯誤時不會遺失。 藉由選取 hello**部署更新**核取方塊，確定您的部署不會遭到刪除，並重新發行應用程式時，無法遺失 VIP。 

    ![發佈 Azure 應用程式進階設定索引標籤](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. 指定要如何更新 hello 角色 toobe toofurther 中，選取**設定**下一步太**部署更新**。 選取 [累加式更新] 或 [同時更新]，然後選取 [確定]。 選擇**累加式更新**tooupdate 應用程式的每個執行個體，因此，hello 應用程式仍可使用。 選擇**同時更新**tooupdate hello 在應用程式的所有執行個體相同的時間。 同時更新較為快速，但您的服務可能無法使用 hello 更新程序期間。 完成後，選取 [下一步] 。

    ![發佈 Azure 應用程式部署設定頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. 在 [hello**發行 Azure 應用程式**對話方塊中，選取**下一步]**直到 hello**摘要**頁面隨即顯示。 確認您的設定，然後選取 [發佈]。
   
    ![發佈 Azure 應用程式摘要頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>後續步驟
- [使用 hello Visual Studio 發行 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)

