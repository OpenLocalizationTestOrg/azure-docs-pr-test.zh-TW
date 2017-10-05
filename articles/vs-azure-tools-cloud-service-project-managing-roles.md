---
title: "使用 Visual Studio 在 Azure 雲端服務中管理角色 | Microsoft Docs"
description: "了解如何使用 Visual Studio，在 Azure 雲端服務中新增及移除角色。"
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
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="5bfe8-103">使用 Visual Studio 在 Azure 雲端服務中管理角色</span><span class="sxs-lookup"><span data-stu-id="5bfe8-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="5bfe8-104">當您建立 Azure 雲端服務之後，您可以在該服務中加入角色或從中移除現有角色。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="5bfe8-105">您也可以匯入現有的專案，並將它轉換成角色。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="5bfe8-106">例如，您可以匯入 ASP.NET Web 應用程式，並將它指定為 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="5bfe8-107">將角色加入至 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bfe8-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="5bfe8-108">下列步驟會逐步引導您完成將 Web 或背景工作角色加入至 Visual Studio 中的 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5bfe8-109">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5bfe8-110">在 [方案總管] 中，展開專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="5bfe8-111">以滑鼠右鍵按一下 [角色] 節點，以顯示操作功能表。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="5bfe8-112">從操作功能表中，選取 [新增]，然後選取現有的 Web 角色或背景工作角色，或是建立 Web 或背景工作角色專案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="5bfe8-113">您可以選取適當的專案 (例如 ASP.NET Web 應用程式專案)，並將它與角色專案產生關聯。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![將角色加入至 Azure 雲端服務專案的功能表選項](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="5bfe8-115">從 Azure 雲端服務移除角色</span><span class="sxs-lookup"><span data-stu-id="5bfe8-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="5bfe8-116">下列步驟會逐步引導您完成從 Visual Studio 中的 Azure 雲端服務專案移除 Web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5bfe8-117">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5bfe8-118">在 [方案總管] 中，展開專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="5bfe8-119">展開 [角色] 節點。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="5bfe8-120">以滑鼠右鍵按一下您要移除的節點，然後從操作功能表中選取 [移除]。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![將角色加入至 Azure 雲端服務的功能表選項](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="5bfe8-122">將角色重新加入至 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="5bfe8-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="5bfe8-123">如果您從雲端服務專案中移除角色，但稍後決定將該角色重新加入至專案，則只有角色宣告和基本屬性 (例如端點和診斷資訊) 會被加入專案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="5bfe8-124">不會將任何其他資源或參考加入至 `ServiceDefinition.csdef` 檔案或 `ServiceConfiguration.cscfg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="5bfe8-125">如果您想要加入此資訊，就必須手動將它重新加回這些檔案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="5bfe8-126">例如，您可能移除了 Web 服務角色，但稍後決定將這個角色重新加回方案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="5bfe8-127">如果您這樣做，將會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-127">If you do this, an error occurs.</span></span> <span data-ttu-id="5bfe8-128">為了避免這個錯誤，您必須將下列 XML 顯示的 `<LocalResources>` 元素重新加回 `ServiceDefinition.csdef` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="5bfe8-129">使用您重新加回專案的 Web 服務角色名稱作為 **<LocalStorage>** 項目的部分名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="5bfe8-130">在此範例中，此 Web 服務角色的名稱是 **WCFServiceWebRole1**。</span><span class="sxs-lookup"><span data-stu-id="5bfe8-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5bfe8-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bfe8-131">Next steps</span></span>
- [<span data-ttu-id="5bfe8-132">使用 Visual Studio 設定 Azure 雲端服務的角色</span><span class="sxs-lookup"><span data-stu-id="5bfe8-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
