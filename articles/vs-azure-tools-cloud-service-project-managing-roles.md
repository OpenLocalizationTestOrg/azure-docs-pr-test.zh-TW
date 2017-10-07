---
title: "aaaManaging 角色在 Azure 中的雲端服務的 Visual Studio |Microsoft 文件"
description: "了解如何 tooadd] 和 [移除角色在 Azure 中的雲端服務的 Visual Studio。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>使用 Visual Studio 在 Azure 雲端服務中管理角色
建立 Azure 雲端服務之後，您可以新增新角色 tooit 或移除現有角色。 您也可以匯入現有的專案，並將它轉換 tooa 角色。 例如，您可以匯入 ASP.NET Web 應用程式，並將它指定為 Web 角色。

## <a name="adding-a-role-tooan-azure-cloud-service"></a>加入角色 tooan Azure 雲端服務
hello 步驟會引導您在 Visual Studio 中加入的 web 或背景工作角色 tooan Azure 雲端服務專案。

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點

1. 以滑鼠右鍵按一下 hello**角色**節點 toodisplay hello 操作功能表。 Hello 內容功能表中選取**新增**，然後從 hello 目前方案中，選取現有的 web 角色或背景工作角色或建立 web 或背景工作角色專案。 您可以選取適當的專案 (例如 ASP.NET Web 應用程式專案)，並將它與角色專案產生關聯。

    ![功能表選項 tooadd 角色 tooan Azure 雲端服務專案](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>從 Azure 雲端服務移除角色
hello 下列步驟會引導您從 Visual Studio 中的 Azure 雲端服務專案中移除的 web 或背景工作角色。

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**，展開 hello 專案節點

1. 展開 hello**角色**節點。

1. 以滑鼠右鍵按一下您想 tooremove，並從 hello 內容功能表中，選取 hello 節點**移除**。 

    ![功能表選項 tooadd 角色 tooan Azure 雲端服務](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>正在重新加入角色 tooan Azure 雲端服務專案
如果您從雲端服務專案中移除角色，但稍後決定回 tooadd hello 角色加入 toohello 專案中，只有 hello 角色宣告和基本屬性，例如端點和診斷資訊。 沒有其他資源或參考會加入 toohello`ServiceDefinition.csdef`檔案或 toohello`ServiceConfiguration.cscfg`檔案。 如果您想 tooadd 這項資訊，您需要 toomanually 將它加回到這些檔案。

例如，您可能移除 web 服務角色，您稍後決定此角色回的 tooadd 帶入方案中。 如果您這樣做，將會發生錯誤。 tooprevent 這個錯誤，您有 tooadd hello`<LocalResources>`示 hello 遵循 hello 送回 XML 項目`ServiceDefinition.csdef`檔案。 使用 hello 名稱 hello web 服務角色的一部分 hello hello 名稱屬性已加回到專案 hello  **<LocalStorage>** 項目。 在此範例中，是 hello hello web 服務角色名稱**WCFServiceWebRole1**。

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>後續步驟
- [使用 Visual Studio 設定 Azure 雲端服務的 hello 角色](vs-azure-tools-configure-roles-for-cloud-service.md)
