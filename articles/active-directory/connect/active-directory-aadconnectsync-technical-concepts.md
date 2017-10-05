---
title: "Azure AD Connect 同步：技術概念 | Microsoft Docs"
description: "說明 Azure AD Connect 同步的技術概念。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 6cf8debc6443bb60fc5f601ea4aa392eb2f13a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a><span data-ttu-id="643ae-103">Azure AD Connect 同步處理：技術概念</span><span class="sxs-lookup"><span data-stu-id="643ae-103">Azure AD Connect sync: Technical Concepts</span></span>
<span data-ttu-id="643ae-104">本文是 [了解架構](active-directory-aadconnectsync-technical-concepts.md)主題的摘要。</span><span class="sxs-lookup"><span data-stu-id="643ae-104">This article is a summary of the topic [Understanding architecture](active-directory-aadconnectsync-technical-concepts.md).</span></span>

<span data-ttu-id="643ae-105">Azure AD Connect 同步建置在一個穩固的中繼目錄同步處理平台上。</span><span class="sxs-lookup"><span data-stu-id="643ae-105">Azure AD Connect sync builds upon a solid metadirectory synchronization platform.</span></span>
<span data-ttu-id="643ae-106">下列各節介紹中繼目錄同步處理的概念。</span><span class="sxs-lookup"><span data-stu-id="643ae-106">The following sections introduce the concepts for metadirectory synchronization.</span></span>
<span data-ttu-id="643ae-107">建置於 MIIS、ILM 以及 FIM 之上，Azure Active Directory 同步服務提供連接資料來源、在資料來源間同步處理資料，以及佈建和解除佈建身份識別的下一代平台。</span><span class="sxs-lookup"><span data-stu-id="643ae-107">Building upon MIIS, ILM, and FIM, the Azure Active Directory Sync Services provides the next platform for connecting to data sources, synchronizing data between data sources, as well as the provisioning and deprovisioning of identities.</span></span>

![技術概念](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

<span data-ttu-id="643ae-109">下列章節提供有關 FIM 同步處理服務下列層面的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="643ae-109">The following sections provide more details about the following aspects of the FIM Synchronization Service:</span></span>

* <span data-ttu-id="643ae-110">連接器</span><span class="sxs-lookup"><span data-stu-id="643ae-110">Connector</span></span>
* <span data-ttu-id="643ae-111">屬性流程</span><span class="sxs-lookup"><span data-stu-id="643ae-111">Attribute flow</span></span>
* <span data-ttu-id="643ae-112">連接器空間</span><span class="sxs-lookup"><span data-stu-id="643ae-112">Connector space</span></span>
* <span data-ttu-id="643ae-113">Metaverse</span><span class="sxs-lookup"><span data-stu-id="643ae-113">Metaverse</span></span>
* <span data-ttu-id="643ae-114">佈建</span><span class="sxs-lookup"><span data-stu-id="643ae-114">Provisioning</span></span>

## <a name="connector"></a><span data-ttu-id="643ae-115">連接器</span><span class="sxs-lookup"><span data-stu-id="643ae-115">Connector</span></span>
<span data-ttu-id="643ae-116">用來與連接的目錄通訊之程式碼模組，稱為連接器 (之前稱為管理代理程式 (MA))。</span><span class="sxs-lookup"><span data-stu-id="643ae-116">The code modules that are used to communicate with a connected directory are called connectors (formerly known as  management agents (MAs)).</span></span>

<span data-ttu-id="643ae-117">這些模組是安裝在執行 Azure AD Connect 同步的電腦上。</span><span class="sxs-lookup"><span data-stu-id="643ae-117">These are installed on the computer running Azure AD Connect sync.</span></span>
<span data-ttu-id="643ae-118">連接器使用遠端系統通訊協定，替代依賴特定代理程式的部署，提供無代理程式能力的通訊。</span><span class="sxs-lookup"><span data-stu-id="643ae-118">The connectors provide the agentless ability to converse by using remote system protocols instead of relying on the deployment of specialized agents.</span></span> <span data-ttu-id="643ae-119">這表示降低了風險與部署時間，特別是在處理重要的應用程式與系統時。</span><span class="sxs-lookup"><span data-stu-id="643ae-119">This means decreased risk and deployment times, especially when dealing with critical applications and systems.</span></span>

<span data-ttu-id="643ae-120">在上圖中，連接器與連接器空間是同義詞，但包含了所有與外部系統的通訊。</span><span class="sxs-lookup"><span data-stu-id="643ae-120">In the picture above, the connector is synonymous with the connector space but encompasses all communication with the external system.</span></span>

<span data-ttu-id="643ae-121">連接器負責系統的所有匯入及匯出功能，並且讓開發人員不需要了解如何以原生方式連接到每個系統，即可使用宣告式佈建來自訂資料轉換。</span><span class="sxs-lookup"><span data-stu-id="643ae-121">The connector is responsible for all import and export functionality to the system and frees developers from needing to understand how to connect to each system natively when using declarative provisioning to customize data transformations.</span></span>

<span data-ttu-id="643ae-122">匯入與匯出作業只會在排程時進行，以進一步與系統中發生的變更隔絕，因為變更不會自動傳播至連接的資料來源。</span><span class="sxs-lookup"><span data-stu-id="643ae-122">Imports and exports only occur when scheduled, allowing for further insulation from changes occurring within the system, since changes do not automatically propagate to the connected data source.</span></span> <span data-ttu-id="643ae-123">此外，開發人員也可以建立自己的連接器，幾乎可連接至任何一個資料來源。</span><span class="sxs-lookup"><span data-stu-id="643ae-123">In addition, developers may also create their own connectors for connecting to virtually any data source.</span></span>

## <a name="attribute-flow"></a><span data-ttu-id="643ae-124">屬性流程</span><span class="sxs-lookup"><span data-stu-id="643ae-124">Attribute flow</span></span>
<span data-ttu-id="643ae-125">Metaverse 是鄰近連接器空間中所有聯結的身份識別的合併檢視。</span><span class="sxs-lookup"><span data-stu-id="643ae-125">The metaverse is the consolidated view of all joined identities from neighboring connector spaces.</span></span> <span data-ttu-id="643ae-126">在上圖中，屬性流程是利用具有箭頭的線條來繪製輸入和輸出流程。</span><span class="sxs-lookup"><span data-stu-id="643ae-126">In the figure above, attribute flow is depicted by lines with arrowheads for both inbound and outbound flow.</span></span> <span data-ttu-id="643ae-127">屬性流程是將資料從一個系統複製或轉換到另一個系統以及所有屬性流程 (輸入或輸出) 的程序。</span><span class="sxs-lookup"><span data-stu-id="643ae-127">Attribute flow is the process of copying or transforming data from one system to another and all attribute flows (inbound or outbound).</span></span>

<span data-ttu-id="643ae-128">當同步處理 (完整或差異) 作業已安排要執行時，屬性流程會在連接器空間與 Metaverse 的雙向通訊之間進行。</span><span class="sxs-lookup"><span data-stu-id="643ae-128">Attribute flow occurs between the connector space and the metaverse bi-directionally when synchronization (full or delta) operations are scheduled to run.</span></span>

<span data-ttu-id="643ae-129">屬性流程只會在執行這些同步處理時進行。</span><span class="sxs-lookup"><span data-stu-id="643ae-129">Attribute flow only occurs when these synchronizations are run.</span></span> <span data-ttu-id="643ae-130">屬性流動則是在同步化規則中定義。</span><span class="sxs-lookup"><span data-stu-id="643ae-130">Attribute flows are defined in Synchronization Rules.</span></span> <span data-ttu-id="643ae-131">這些可以是輸入 (如上圖之 ISR) 或輸出 (如上圖之 OSR)。</span><span class="sxs-lookup"><span data-stu-id="643ae-131">These can be inbound (ISR in the picture above) or outbound (OSR in the picture above).</span></span>

## <a name="connected-system"></a><span data-ttu-id="643ae-132">連接的系統</span><span class="sxs-lookup"><span data-stu-id="643ae-132">Connected system</span></span>
<span data-ttu-id="643ae-133">連接的系統 (也稱為連接的目錄) 是指 Azure AD Connect 同步處理已連接且來回讀取和寫入身分識別資料的遠端系統。</span><span class="sxs-lookup"><span data-stu-id="643ae-133">Connected system (aka connected directory) is referring to the remote system Azure AD Connect sync has connected to and reading and writing identity data to and from.</span></span>

## <a name="connector-space"></a><span data-ttu-id="643ae-134">連接器空間</span><span class="sxs-lookup"><span data-stu-id="643ae-134">Connector space</span></span>
<span data-ttu-id="643ae-135">每個已連接的資料來源都會以連接器空間中物件和屬性的已篩選子集的方式表示。</span><span class="sxs-lookup"><span data-stu-id="643ae-135">Each connected data source is represented as a filtered subset of the objects and attributes in the connector space.</span></span>
<span data-ttu-id="643ae-136">這可讓同步服務在本機作業，而不需要在同步處理物件時連接遠端系統並將互動限制為僅匯入及匯出。</span><span class="sxs-lookup"><span data-stu-id="643ae-136">This allows the sync service to operate locally without the need to contact the remote system when synchronizing the objects and restricts interaction to imports and exports only.</span></span>

<span data-ttu-id="643ae-137">當資料來源及連接器具有提供變更清單 (差異匯入) 的能力時，因為只在最後一次輪詢循環交換之後變更，作業效率會大幅提升。</span><span class="sxs-lookup"><span data-stu-id="643ae-137">When the data source and the connector have the ability to provide a list of changes (a delta import), then the operational efficiency increases dramatically as only changes since the last polling cycle are exchanged.</span></span> <span data-ttu-id="643ae-138">連接器空間可透過要求連接器排程匯入及匯出，讓已連接的資料來源不會受到自動傳播變更影響。</span><span class="sxs-lookup"><span data-stu-id="643ae-138">The connector space insulates the connected data source from changes propagating automatically by requiring that the connector schedule imports and exports.</span></span> <span data-ttu-id="643ae-139">這項新增的預防措施讓您在測試、預覽，或確認下次更新時可以更加放心。</span><span class="sxs-lookup"><span data-stu-id="643ae-139">This added insurance grants you peace of mind while testing, previewing, or confirming the next update.</span></span>

## <a name="metaverse"></a><span data-ttu-id="643ae-140">Metaverse</span><span class="sxs-lookup"><span data-stu-id="643ae-140">Metaverse</span></span>
<span data-ttu-id="643ae-141">Metaverse 是鄰近連接器空間中所有聯結的身份識別的合併檢視。</span><span class="sxs-lookup"><span data-stu-id="643ae-141">The metaverse is the consolidated view of all joined identities from neighboring connector spaces.</span></span>

<span data-ttu-id="643ae-142">由於身份識別連結在一起，且授權透過匯入流程對應指派給各種屬性，中心 Metaverse 物件要從多個系統開始彙總資訊。</span><span class="sxs-lookup"><span data-stu-id="643ae-142">As identities are linked together and authority is assigned for various attributes through import flow mappings, the central metaverse object begins to aggregate information from multiple systems.</span></span> <span data-ttu-id="643ae-143">從此物件屬性流程，對應包含輸出系統的資訊。</span><span class="sxs-lookup"><span data-stu-id="643ae-143">From this object attribute flow, mappings carry information to outbound systems.</span></span>

<span data-ttu-id="643ae-144">當授權系統投影物件到 Metaverse 時會建立物件。</span><span class="sxs-lookup"><span data-stu-id="643ae-144">Objects are created when an authoritative system projects them into the metaverse.</span></span> <span data-ttu-id="643ae-145">在所有的連接移除後，就會刪除 Metaverse 物件。</span><span class="sxs-lookup"><span data-stu-id="643ae-145">As soon as all connections are removed, the metaverse object is deleted.</span></span>

<span data-ttu-id="643ae-146">您無法直接編輯 Metaverse 中的物件。</span><span class="sxs-lookup"><span data-stu-id="643ae-146">Objects in the metaverse cannot be edited directly.</span></span> <span data-ttu-id="643ae-147">物件中的所有資料都必須透過屬性流程來提供。</span><span class="sxs-lookup"><span data-stu-id="643ae-147">All data in the object must be contributed through attribute flow.</span></span> <span data-ttu-id="643ae-148">Metaverse 會利用每個連接器空間來維護永續性連接器。</span><span class="sxs-lookup"><span data-stu-id="643ae-148">The metaverse maintains persistent connectors with each connector space.</span></span> <span data-ttu-id="643ae-149">這些連接器不需要在每次執行每次同步處理進行重新評估。</span><span class="sxs-lookup"><span data-stu-id="643ae-149">These connectors do not require reevaluation for each synchronization run.</span></span> <span data-ttu-id="643ae-150">這表示 Azure AD Connect 同步處理不需每次尋找相符的遠端物件。</span><span class="sxs-lookup"><span data-stu-id="643ae-150">This means that Azure AD Connect sync does not have to locate the matching remote object each time.</span></span> <span data-ttu-id="643ae-151">這樣就不需要使用昂貴的代理程式，來防止對通常負責建立物件之間關聯的屬性進行變更。</span><span class="sxs-lookup"><span data-stu-id="643ae-151">This avoids the need for costly agents to prevent changes to attributes that would normally be responsible for correlating the objects.</span></span>

<span data-ttu-id="643ae-152">探索可能具有既存需管理之物件的新資料來源 時，Azure AD Connect 同步會使用名為「聯結規則」的程序，評估建立連結的潛在候選項目。</span><span class="sxs-lookup"><span data-stu-id="643ae-152">When discovering new data sources that may have preexisting objects that need to be managed, Azure AD Connect sync uses a process called a join rule to evaluate potential candidates with which to establish a link.</span></span>
<span data-ttu-id="643ae-153">連結一旦建立，此評估就不會重新執行，而一般屬性流程則可在遠端連結的資料來源和 Metaverse 間進行。</span><span class="sxs-lookup"><span data-stu-id="643ae-153">Once the link is established, this evaluation does not reoccur and normal attribute flow can occur between the remote connected data source and the metaverse.</span></span>

## <a name="provisioning"></a><span data-ttu-id="643ae-154">佈建</span><span class="sxs-lookup"><span data-stu-id="643ae-154">Provisioning</span></span>
<span data-ttu-id="643ae-155">當授權來源投影一個新物件至 Metaverse　時，會在另一個連接器中建立新的連接器空間物件，代表一個下游的已連接資料來源。</span><span class="sxs-lookup"><span data-stu-id="643ae-155">When an authoritative source projects a new object into the metaverse a new connector space object can be created in another Connector representing a downstream connected data source.</span></span>

<span data-ttu-id="643ae-156">這本身就會建立連結，且屬性流程可以雙向進行。</span><span class="sxs-lookup"><span data-stu-id="643ae-156">This inherently establishes a link, and attribute flow can proceed bi-directionally.</span></span>

<span data-ttu-id="643ae-157">每當規則判斷需要建立新的連接器空間物件，此即稱為佈建。</span><span class="sxs-lookup"><span data-stu-id="643ae-157">Whenever a rule determines that a new connector space object needs to be created, it is called provisioning.</span></span> <span data-ttu-id="643ae-158">不過，因為此作業只會在連接器空間中進行，所以在執行匯出之前不會影響已連接的資料來源。</span><span class="sxs-lookup"><span data-stu-id="643ae-158">However, because this operation only takes place within the connector space, it does not carry over into the connected data source until an export is performed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="643ae-159">其他資源</span><span class="sxs-lookup"><span data-stu-id="643ae-159">Additional Resources</span></span>
* [<span data-ttu-id="643ae-160">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="643ae-160">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="643ae-161">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="643ae-161">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
