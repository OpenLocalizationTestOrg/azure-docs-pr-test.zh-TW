---
title: "Azure AD Connect 同步：技術概念 | Microsoft Docs"
description: "說明 Azure AD Connect 同步處理的 hello 技術的概念。"
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
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a><span data-ttu-id="a372f-103">Azure AD Connect 同步處理：技術概念</span><span class="sxs-lookup"><span data-stu-id="a372f-103">Azure AD Connect sync: Technical Concepts</span></span>
<span data-ttu-id="a372f-104">這篇文章是 hello 主題的摘要[了解架構](active-directory-aadconnectsync-technical-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="a372f-104">This article is a summary of hello topic [Understanding architecture](active-directory-aadconnectsync-technical-concepts.md).</span></span>

<span data-ttu-id="a372f-105">Azure AD Connect 同步建置在一個穩固的中繼目錄同步處理平台上。</span><span class="sxs-lookup"><span data-stu-id="a372f-105">Azure AD Connect sync builds upon a solid metadirectory synchronization platform.</span></span>
<span data-ttu-id="a372f-106">hello 下列各節介紹中繼目錄同步處理的 hello 概念。</span><span class="sxs-lookup"><span data-stu-id="a372f-106">hello following sections introduce hello concepts for metadirectory synchronization.</span></span>
<span data-ttu-id="a372f-107">建置 MIIS、 ILM，和 FIM，hello Azure Active Directory 同步處理服務提供 hello 下一個平台連線 toodata 來源，資料來源，以及佈建和解除佈建身分識別的 hello 之間同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="a372f-107">Building upon MIIS, ILM, and FIM, hello Azure Active Directory Sync Services provides hello next platform for connecting toodata sources, synchronizing data between data sources, as well as hello provisioning and deprovisioning of identities.</span></span>

![技術概念](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

<span data-ttu-id="a372f-109">hello 下列各節會提供更多詳細 hello 遵循 hello FIM 同步處理服務的層面：</span><span class="sxs-lookup"><span data-stu-id="a372f-109">hello following sections provide more details about hello following aspects of hello FIM Synchronization Service:</span></span>

* <span data-ttu-id="a372f-110">連接器</span><span class="sxs-lookup"><span data-stu-id="a372f-110">Connector</span></span>
* <span data-ttu-id="a372f-111">屬性流程</span><span class="sxs-lookup"><span data-stu-id="a372f-111">Attribute flow</span></span>
* <span data-ttu-id="a372f-112">連接器空間</span><span class="sxs-lookup"><span data-stu-id="a372f-112">Connector space</span></span>
* <span data-ttu-id="a372f-113">Metaverse</span><span class="sxs-lookup"><span data-stu-id="a372f-113">Metaverse</span></span>
* <span data-ttu-id="a372f-114">佈建</span><span class="sxs-lookup"><span data-stu-id="a372f-114">Provisioning</span></span>

## <a name="connector"></a><span data-ttu-id="a372f-115">連接器</span><span class="sxs-lookup"><span data-stu-id="a372f-115">Connector</span></span>
<span data-ttu-id="a372f-116">連接器 （之前稱為管理代理程式 (Ma)） 時，會呼叫 hello 程式碼模組所使用的 toocommunicate 與連接的目錄。</span><span class="sxs-lookup"><span data-stu-id="a372f-116">hello code modules that are used toocommunicate with a connected directory are called connectors (formerly known as  management agents (MAs)).</span></span>

<span data-ttu-id="a372f-117">這些是執行 Azure AD Connect 同步處理的 hello 電腦上進行安裝。hello 連接器提供 hello 無代理程式的能力 tooconverse 使用遠端系統通訊協定，而不是依賴 hello 部署專用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="a372f-117">These are installed on hello computer running Azure AD Connect sync. hello connectors provide hello agentless ability tooconverse by using remote system protocols instead of relying on hello deployment of specialized agents.</span></span> <span data-ttu-id="a372f-118">這表示降低了風險與部署時間，特別是在處理重要的應用程式與系統時。</span><span class="sxs-lookup"><span data-stu-id="a372f-118">This means decreased risk and deployment times, especially when dealing with critical applications and systems.</span></span>

<span data-ttu-id="a372f-119">在上述的 hello 圖片，hello 連接器 hello 連接器空間同義，但包含所有與 hello 外部系統通訊。</span><span class="sxs-lookup"><span data-stu-id="a372f-119">In hello picture above, hello connector is synonymous with hello connector space but encompasses all communication with hello external system.</span></span>

<span data-ttu-id="a372f-120">hello 連接器負責所有匯入和匯出功能 toohello 系統，以及開發人員不需要 toounderstand 如何使用宣告式佈建 toocustomize 資料轉換時，原生 tooconnect tooeach 系統。</span><span class="sxs-lookup"><span data-stu-id="a372f-120">hello connector is responsible for all import and export functionality toohello system and frees developers from needing toounderstand how tooconnect tooeach system natively when using declarative provisioning toocustomize data transformations.</span></span>

<span data-ttu-id="a372f-121">匯入和匯出只發生排程時，允許進一步隔離 hello 系統內發生，因為變更不會自動傳播 toohello 連接的資料來源的變更。</span><span class="sxs-lookup"><span data-stu-id="a372f-121">Imports and exports only occur when scheduled, allowing for further insulation from changes occurring within hello system, since changes do not automatically propagate toohello connected data source.</span></span> <span data-ttu-id="a372f-122">此外，開發人員也可以建立自己的連接器，以連接 toovirtually 任何資料來源。</span><span class="sxs-lookup"><span data-stu-id="a372f-122">In addition, developers may also create their own connectors for connecting toovirtually any data source.</span></span>

## <a name="attribute-flow"></a><span data-ttu-id="a372f-123">屬性流程</span><span class="sxs-lookup"><span data-stu-id="a372f-123">Attribute flow</span></span>
<span data-ttu-id="a372f-124">hello metaverse 是來自相鄰連接器空間所有聯結的身分識別的 hello 合併檢視。</span><span class="sxs-lookup"><span data-stu-id="a372f-124">hello metaverse is hello consolidated view of all joined identities from neighboring connector spaces.</span></span> <span data-ttu-id="a372f-125">在 hello 圖中，屬性流程描繪以線條傳入和傳出流量的箭頭。</span><span class="sxs-lookup"><span data-stu-id="a372f-125">In hello figure above, attribute flow is depicted by lines with arrowheads for both inbound and outbound flow.</span></span> <span data-ttu-id="a372f-126">屬性流程是複製或將資料從一個系統 tooanother 轉換 hello 程序，所有屬性流程 （輸入或輸出）。</span><span class="sxs-lookup"><span data-stu-id="a372f-126">Attribute flow is hello process of copying or transforming data from one system tooanother and all attribute flows (inbound or outbound).</span></span>

<span data-ttu-id="a372f-127">屬性流程，就會發生 hello 連接器空間和 hello metaverse 之間雙向同步處理 （完整或差異） 的作業排程的 toorun 時。</span><span class="sxs-lookup"><span data-stu-id="a372f-127">Attribute flow occurs between hello connector space and hello metaverse bi-directionally when synchronization (full or delta) operations are scheduled toorun.</span></span>

<span data-ttu-id="a372f-128">屬性流程只會在執行這些同步處理時進行。</span><span class="sxs-lookup"><span data-stu-id="a372f-128">Attribute flow only occurs when these synchronizations are run.</span></span> <span data-ttu-id="a372f-129">屬性流動則是在同步化規則中定義。</span><span class="sxs-lookup"><span data-stu-id="a372f-129">Attribute flows are defined in Synchronization Rules.</span></span> <span data-ttu-id="a372f-130">這些可以是輸入 (ISR hello 如上圖) 或輸出 (OSR 在 hello 如上圖)。</span><span class="sxs-lookup"><span data-stu-id="a372f-130">These can be inbound (ISR in hello picture above) or outbound (OSR in hello picture above).</span></span>

## <a name="connected-system"></a><span data-ttu-id="a372f-131">連接的系統</span><span class="sxs-lookup"><span data-stu-id="a372f-131">Connected system</span></span>
<span data-ttu-id="a372f-132">連接的系統 （也稱為連接的目錄） 正在參照 toohello 遠端系統 Azure AD Connect 同步處理已連接 tooand 讀取和寫入從身分識別資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="a372f-132">Connected system (aka connected directory) is referring toohello remote system Azure AD Connect sync has connected tooand reading and writing identity data tooand from.</span></span>

## <a name="connector-space"></a><span data-ttu-id="a372f-133">連接器空間</span><span class="sxs-lookup"><span data-stu-id="a372f-133">Connector space</span></span>
<span data-ttu-id="a372f-134">每個連接的資料來源被以 hello 物件和屬性在 hello 連接器空間中的篩選子集。</span><span class="sxs-lookup"><span data-stu-id="a372f-134">Each connected data source is represented as a filtered subset of hello objects and attributes in hello connector space.</span></span>
<span data-ttu-id="a372f-135">這允許 hello 同步處理服務 toooperate 而 hello 需要 toocontact hello 遠端系統不在本機，hello 物件同步處理時，限制互動 tooimports 並只會匯出。</span><span class="sxs-lookup"><span data-stu-id="a372f-135">This allows hello sync service toooperate locally without hello need toocontact hello remote system when synchronizing hello objects and restricts interaction tooimports and exports only.</span></span>

<span data-ttu-id="a372f-136">當 hello 資料來源和 hello 連接器的 hello 能力 tooprovide 變更 （差異匯入） 的清單時，然後 hello 操作效率增加大幅如只能變更自 hello 上次輪詢循環會交換。</span><span class="sxs-lookup"><span data-stu-id="a372f-136">When hello data source and hello connector have hello ability tooprovide a list of changes (a delta import), then hello operational efficiency increases dramatically as only changes since hello last polling cycle are exchanged.</span></span> <span data-ttu-id="a372f-137">hello 連接器空間，以隔離 hello 連接的資料來源自動傳播的要求該 hello 連接器排程匯入和匯出的變更。</span><span class="sxs-lookup"><span data-stu-id="a372f-137">hello connector space insulates hello connected data source from changes propagating automatically by requiring that hello connector schedule imports and exports.</span></span> <span data-ttu-id="a372f-138">此層保障您安心測試、 預覽或確認 hello 下次更新時。</span><span class="sxs-lookup"><span data-stu-id="a372f-138">This added insurance grants you peace of mind while testing, previewing, or confirming hello next update.</span></span>

## <a name="metaverse"></a><span data-ttu-id="a372f-139">Metaverse</span><span class="sxs-lookup"><span data-stu-id="a372f-139">Metaverse</span></span>
<span data-ttu-id="a372f-140">hello metaverse 是來自相鄰連接器空間所有聯結的身分識別的 hello 合併檢視。</span><span class="sxs-lookup"><span data-stu-id="a372f-140">hello metaverse is hello consolidated view of all joined identities from neighboring connector spaces.</span></span>

<span data-ttu-id="a372f-141">識別連結在一起，並授權單位指派給各種屬性，透過匯入流程對應，hello 中央 metaverse 物件就會開始從多個系統 tooaggregate 資訊。</span><span class="sxs-lookup"><span data-stu-id="a372f-141">As identities are linked together and authority is assigned for various attributes through import flow mappings, hello central metaverse object begins tooaggregate information from multiple systems.</span></span> <span data-ttu-id="a372f-142">從這個物件的屬性流程對應，請執行資訊 toooutbound 系統。</span><span class="sxs-lookup"><span data-stu-id="a372f-142">From this object attribute flow, mappings carry information toooutbound systems.</span></span>

<span data-ttu-id="a372f-143">當授權系統投射至 hello metaverse 時，會建立物件。</span><span class="sxs-lookup"><span data-stu-id="a372f-143">Objects are created when an authoritative system projects them into hello metaverse.</span></span> <span data-ttu-id="a372f-144">一旦移除所有連線之後，會刪除 hello metaverse 物件。</span><span class="sxs-lookup"><span data-stu-id="a372f-144">As soon as all connections are removed, hello metaverse object is deleted.</span></span>

<span data-ttu-id="a372f-145">Hello metaverse 中的物件不能直接編輯。</span><span class="sxs-lookup"><span data-stu-id="a372f-145">Objects in hello metaverse cannot be edited directly.</span></span> <span data-ttu-id="a372f-146">透過屬性流程，就必須提供 hello 物件中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="a372f-146">All data in hello object must be contributed through attribute flow.</span></span> <span data-ttu-id="a372f-147">hello metaverse 會維護持續的連接器，與每個連接器空間。</span><span class="sxs-lookup"><span data-stu-id="a372f-147">hello metaverse maintains persistent connectors with each connector space.</span></span> <span data-ttu-id="a372f-148">這些連接器不需要在每次執行每次同步處理進行重新評估。</span><span class="sxs-lookup"><span data-stu-id="a372f-148">These connectors do not require reevaluation for each synchronization run.</span></span> <span data-ttu-id="a372f-149">這表示，Azure AD Connect 同步處理並沒有 toolocate hello 相符的遠端物件每一次。</span><span class="sxs-lookup"><span data-stu-id="a372f-149">This means that Azure AD Connect sync does not have toolocate hello matching remote object each time.</span></span> <span data-ttu-id="a372f-150">這可以避免成本高昂的代理程式，通常就是相互關聯的 hello 物件 tooprevent 變更 tooattributes hello 需要。</span><span class="sxs-lookup"><span data-stu-id="a372f-150">This avoids hello need for costly agents tooprevent changes tooattributes that would normally be responsible for correlating hello objects.</span></span>

<span data-ttu-id="a372f-151">當探索可能會有預先存在的物件需要 toobe 管理，Azure AD Connect 同步處理使用的程序的新資料來源稱為聯結規則 tooevaluate 潛在候選項目使用哪些 tooestablish 連結。</span><span class="sxs-lookup"><span data-stu-id="a372f-151">When discovering new data sources that may have preexisting objects that need toobe managed, Azure AD Connect sync uses a process called a join rule tooevaluate potential candidates with which tooestablish a link.</span></span>
<span data-ttu-id="a372f-152">當建立 hello 連結時，不會再次執行這項評估，而且可能是正常的屬性流程 hello 遠端連接的資料來源與 hello metaverse 之間。</span><span class="sxs-lookup"><span data-stu-id="a372f-152">Once hello link is established, this evaluation does not reoccur and normal attribute flow can occur between hello remote connected data source and hello metaverse.</span></span>

## <a name="provisioning"></a><span data-ttu-id="a372f-153">佈建</span><span class="sxs-lookup"><span data-stu-id="a372f-153">Provisioning</span></span>
<span data-ttu-id="a372f-154">當授權來源專案 hello metaverse 新的連接器空間物件至新的物件可由另一個連接器代表下游連接的資料來源中。</span><span class="sxs-lookup"><span data-stu-id="a372f-154">When an authoritative source projects a new object into hello metaverse a new connector space object can be created in another Connector representing a downstream connected data source.</span></span>

<span data-ttu-id="a372f-155">這本身就會建立連結，且屬性流程可以雙向進行。</span><span class="sxs-lookup"><span data-stu-id="a372f-155">This inherently establishes a link, and attribute flow can proceed bi-directionally.</span></span>

<span data-ttu-id="a372f-156">每當規則決定新的連接器空間物件需要 toobe 建立，就稱為佈建。</span><span class="sxs-lookup"><span data-stu-id="a372f-156">Whenever a rule determines that a new connector space object needs toobe created, it is called provisioning.</span></span> <span data-ttu-id="a372f-157">不過，這項作業只會發生在 hello 連接器空間內，因為它不會延續至 hello 連接的資料來源之前執行匯出。</span><span class="sxs-lookup"><span data-stu-id="a372f-157">However, because this operation only takes place within hello connector space, it does not carry over into hello connected data source until an export is performed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a372f-158">其他資源</span><span class="sxs-lookup"><span data-stu-id="a372f-158">Additional Resources</span></span>
* [<span data-ttu-id="a372f-159">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="a372f-159">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="a372f-160">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a372f-160">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
