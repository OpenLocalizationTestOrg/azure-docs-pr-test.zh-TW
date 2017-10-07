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
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="f1669-103">使用 Visual Studio 在 Azure 雲端服務中管理角色</span><span class="sxs-lookup"><span data-stu-id="f1669-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="f1669-104">建立 Azure 雲端服務之後，您可以新增新角色 tooit 或移除現有角色。</span><span class="sxs-lookup"><span data-stu-id="f1669-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="f1669-105">您也可以匯入現有的專案，並將它轉換 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="f1669-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="f1669-106">例如，您可以匯入 ASP.NET Web 應用程式，並將它指定為 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="f1669-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="f1669-107">加入角色 tooan Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="f1669-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="f1669-108">hello 步驟會引導您在 Visual Studio 中加入的 web 或背景工作角色 tooan Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="f1669-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f1669-109">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="f1669-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f1669-110">在**方案總管 中**，展開 hello 專案節點</span><span class="sxs-lookup"><span data-stu-id="f1669-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="f1669-111">以滑鼠右鍵按一下 hello**角色**節點 toodisplay hello 操作功能表。</span><span class="sxs-lookup"><span data-stu-id="f1669-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="f1669-112">Hello 內容功能表中選取**新增**，然後從 hello 目前方案中，選取現有的 web 角色或背景工作角色或建立 web 或背景工作角色專案。</span><span class="sxs-lookup"><span data-stu-id="f1669-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="f1669-113">您可以選取適當的專案 (例如 ASP.NET Web 應用程式專案)，並將它與角色專案產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f1669-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![功能表選項 tooadd 角色 tooan Azure 雲端服務專案](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="f1669-115">從 Azure 雲端服務移除角色</span><span class="sxs-lookup"><span data-stu-id="f1669-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="f1669-116">hello 下列步驟會引導您從 Visual Studio 中的 Azure 雲端服務專案中移除的 web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="f1669-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f1669-117">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="f1669-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f1669-118">在**方案總管 中**，展開 hello 專案節點</span><span class="sxs-lookup"><span data-stu-id="f1669-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="f1669-119">展開 hello**角色**節點。</span><span class="sxs-lookup"><span data-stu-id="f1669-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="f1669-120">以滑鼠右鍵按一下您想 tooremove，並從 hello 內容功能表中，選取 hello 節點**移除**。</span><span class="sxs-lookup"><span data-stu-id="f1669-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![功能表選項 tooadd 角色 tooan Azure 雲端服務](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="f1669-122">正在重新加入角色 tooan Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="f1669-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="f1669-123">如果您從雲端服務專案中移除角色，但稍後決定回 tooadd hello 角色加入 toohello 專案中，只有 hello 角色宣告和基本屬性，例如端點和診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="f1669-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="f1669-124">沒有其他資源或參考會加入 toohello`ServiceDefinition.csdef`檔案或 toohello`ServiceConfiguration.cscfg`檔案。</span><span class="sxs-lookup"><span data-stu-id="f1669-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="f1669-125">如果您想 tooadd 這項資訊，您需要 toomanually 將它加回到這些檔案。</span><span class="sxs-lookup"><span data-stu-id="f1669-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="f1669-126">例如，您可能移除 web 服務角色，您稍後決定此角色回的 tooadd 帶入方案中。</span><span class="sxs-lookup"><span data-stu-id="f1669-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="f1669-127">如果您這樣做，將會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f1669-127">If you do this, an error occurs.</span></span> <span data-ttu-id="f1669-128">tooprevent 這個錯誤，您有 tooadd hello`<LocalResources>`示 hello 遵循 hello 送回 XML 項目`ServiceDefinition.csdef`檔案。</span><span class="sxs-lookup"><span data-stu-id="f1669-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="f1669-129">使用 hello 名稱 hello web 服務角色的一部分 hello hello 名稱屬性已加回到專案 hello  **<LocalStorage>** 項目。</span><span class="sxs-lookup"><span data-stu-id="f1669-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="f1669-130">在此範例中，是 hello hello web 服務角色名稱**WCFServiceWebRole1**。</span><span class="sxs-lookup"><span data-stu-id="f1669-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f1669-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1669-131">Next steps</span></span>
- [<span data-ttu-id="f1669-132">使用 Visual Studio 設定 Azure 雲端服務的 hello 角色</span><span class="sxs-lookup"><span data-stu-id="f1669-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
