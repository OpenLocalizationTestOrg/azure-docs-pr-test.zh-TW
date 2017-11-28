---
title: "aaaProtect 您的 API，使用 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 tooprotect 配額和節流設定 （速率限制） 的原則與您的 API。"
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="a247c-103">使用 Azure API 管理以頻率限制保護 API</span><span class="sxs-lookup"><span data-stu-id="a247c-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="a247c-104">本指南也說明是多麼的輕鬆 tooadd 保護您的後端 API 藉由使用 Azure API 管理設定速率限制和配額原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="a247c-105">在此教學課程中，您將建立可讓開發人員 」 的免費試用 」 應用程式開發介面產品 toomake too10 呼叫每分鐘和向上 tooa 最大值為 200 的呼叫，每週 tooyour API 使用 hello[限制呼叫率，每個訂閱](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[每個訂閱設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a247c-106">然後，您將會發行 hello 應用程式開發介面，並測試 hello 速率限制原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="a247c-107">如需更進階節流使用 hello 案例[速率限制-由-索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey)和[配額的索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey)原則，請參閱[節流使用 Azure API 管理進階的要求](api-management-sample-flexible-throttling.md)。</span><span class="sxs-lookup"><span data-stu-id="a247c-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="a247c-108"><a name="create-product"></a>toocreate 產品</span><span class="sxs-lookup"><span data-stu-id="a247c-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="a247c-109">在本步驟中，您將建立不需核准訂用帳戶的免費試用產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="a247c-110">如果您已經有設定的產品，並想 toouse 它在此教學課程，您可以往前跳過[設定呼叫率限制和配額原則][ Configure call rate limit and quota policies]並從該處使用您的產品遵循 hello 教學課程取代 hello 免費試用版的產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="a247c-111">tooget 啟動，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a247c-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="a247c-113">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[管理您在 Azure API 管理中的第一個 API][ Manage your first API in Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a247c-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a247c-114">按一下**產品**在 hello **API 管理**功能表 hello 左的 toodisplay hello**產品**頁面。</span><span class="sxs-lookup"><span data-stu-id="a247c-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="a247c-116">按一下**新增產品**toodisplay hello**新增新的產品** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a247c-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Add new product][api-management-new-product-window]

<span data-ttu-id="a247c-118">在 hello**標題**方塊中，輸入**免費試用版**。</span><span class="sxs-lookup"><span data-stu-id="a247c-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="a247c-119">在 [hello**描述**] 方塊中，下列文字的型別 hello: **「 訂閱者 」 將會無法 toorun 10 呼叫/tooa 最大值 200 呼叫/週之後存取遭到拒絕的總分鐘。**</span><span class="sxs-lookup"><span data-stu-id="a247c-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="a247c-120">API 管理中的產品可以是受保護或開放的。</span><span class="sxs-lookup"><span data-stu-id="a247c-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="a247c-121">受保護的產品，必須是訂閱的 toobefore 可以使用。</span><span class="sxs-lookup"><span data-stu-id="a247c-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="a247c-122">開放產品不需要訂用帳戶即可使用。</span><span class="sxs-lookup"><span data-stu-id="a247c-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="a247c-123">請確認**需要訂用帳戶**是選取的 toocreate 一個受保護的產品，需要訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a247c-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="a247c-124">這是 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="a247c-124">This is hello default setting.</span></span>

<span data-ttu-id="a247c-125">如果您想要系統管理員 tooreview 並接受或拒絕的訂閱嘗試 toothis 產品，選取**需要訂閱核准**。</span><span class="sxs-lookup"><span data-stu-id="a247c-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="a247c-126">如果未選取 hello 核取方塊，訂閱嘗試將會自動核准。</span><span class="sxs-lookup"><span data-stu-id="a247c-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="a247c-127">在此範例中，訂用帳戶都會自動核准，因此不會選取 hello 方塊。</span><span class="sxs-lookup"><span data-stu-id="a247c-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="a247c-128">tooallow 開發人員帳戶 toosubscribe 多次 toohello 新產品，選取 hello**允許多個同時訂閱**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a247c-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="a247c-129">本教學課程不會使用多項同時訂閱，所以維持未核取即可。</span><span class="sxs-lookup"><span data-stu-id="a247c-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="a247c-130">輸入的所有值之後，請按一下**儲存**toocreate hello 產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="a247c-132">根據預設，新產品會顯示在 hello toousers**管理員**群組。</span><span class="sxs-lookup"><span data-stu-id="a247c-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="a247c-133">我們 tooadd hello**開發人員**群組。</span><span class="sxs-lookup"><span data-stu-id="a247c-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="a247c-134">按一下**免費試用版**，然後按一下hello**可視性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a247c-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="a247c-135">在 API 管理中，群組是產品 toodevelopers 使用的 toomanage hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="a247c-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="a247c-136">產品授與的可見性 toogroups 和開發人員可以檢視和訂閱 toohello 產品可見 toohello 所隸屬的群組。</span><span class="sxs-lookup"><span data-stu-id="a247c-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="a247c-137">如需詳細資訊，請參閱[toocreate 和使用在 Azure API 管理群組的方式][How toocreate and use groups in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="a247c-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="a247c-139">選取 hello**開發人員**核取方塊，然後**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a247c-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="a247c-140"><a name="add-api"></a>tooadd API toohello 產品</span><span class="sxs-lookup"><span data-stu-id="a247c-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="a247c-141">在此步驟 hello 教學課程中，我們將加入 hello 回應 API toohello 新免費試用版的產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="a247c-142">每個 API 管理服務執行個體隨附預先設定的一種回應的 API，可以與使用的 tooexperiment 和了解 API 管理。</span><span class="sxs-lookup"><span data-stu-id="a247c-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="a247c-143">如需詳細資訊，請參閱[在 Azure API 管理中管理您的第一個 API][Manage your first API in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="a247c-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="a247c-144">按一下**產品**從 hello **API 管理**hello 左、，然後按一下功能表**免費試用版**tooconfigure hello 產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="a247c-146">按一下**新增應用程式開發介面 tooproduct**。</span><span class="sxs-lookup"><span data-stu-id="a247c-146">Click **Add API tooproduct**.</span></span>

![新增應用程式開發介面 tooproduct][api-management-add-api]

<span data-ttu-id="a247c-148">請選取 Echo API，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="a247c-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="a247c-150"><a name="policies"></a>tooconfigure 呼叫率限制和配額的原則</span><span class="sxs-lookup"><span data-stu-id="a247c-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="a247c-151">速率限制和配額會設定在 hello 原則編輯器。</span><span class="sxs-lookup"><span data-stu-id="a247c-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="a247c-152">我們將加入本教學課程中的 hello 兩個原則是 hello[限制呼叫率，每個訂閱](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[每個訂閱設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a247c-153">在 hello 產品的範圍，就必須套用這些原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="a247c-154">按一下**原則**下 hello **API 管理**hello 左邊功能表上的。</span><span class="sxs-lookup"><span data-stu-id="a247c-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="a247c-155">在 hello**產品**清單中，按一下**免費試用版**。</span><span class="sxs-lookup"><span data-stu-id="a247c-155">In hello **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="a247c-157">按一下**新增原則**tooimport hello 原則範本，並開始建立 hello 速率限制和配額原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Add policy][api-management-add-policy]

<span data-ttu-id="a247c-159">速率限制和配額原則是輸入的原則，因此 hello 輸入項目中的位置 hello 資料指標。</span><span class="sxs-lookup"><span data-stu-id="a247c-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="a247c-161">捲動 hello 原則清單且找出 hello**限制呼叫率，每個訂閱**原則項目。</span><span class="sxs-lookup"><span data-stu-id="a247c-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="a247c-163">資料指標定位在 hello 之後 hello**輸入**原則項目，按一下旁邊的箭號 hello**限制呼叫率，每個訂閱**tooinsert 其原則範本。</span><span class="sxs-lookup"><span data-stu-id="a247c-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="a247c-164">您可以看到從 hello 片段，hello 原則允許設定限制 hello 產品的 Api 和操作。</span><span class="sxs-lookup"><span data-stu-id="a247c-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="a247c-165">本教學課程中我們將不使用這項功能，因此刪除 hello **api**和**作業**項目從 hello**速率限制**項目，例如只 hello 外部**速率限制**項目維持 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a247c-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="a247c-166">在 hello 免費試用版的產品，hello 最大可允許呼叫率是每分鐘 10 個呼叫，因此請輸入**10**為 hello hello 值**呼叫**屬性，和**60** hello **更新間隔**屬性。</span><span class="sxs-lookup"><span data-stu-id="a247c-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="a247c-167">tooconfigure hello**每個訂閱設定使用量配額**原則時，位置緊鄰下 hello 游標新增**速率限制**hello 內的項目**輸入**項目，然後找出並按一下 hello 箭號 toohello 左邊**每個訂閱設定使用量配額**。</span><span class="sxs-lookup"><span data-stu-id="a247c-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="a247c-168">同樣地 toohello**每個訂閱設定使用量配額**原則，**每個訂閱設定使用量配額**原則允許 hello 產品的 Api 和操作上設定的端點。</span><span class="sxs-lookup"><span data-stu-id="a247c-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="a247c-169">本教學課程中我們將不使用這項功能，因此刪除 hello **api**和**作業**項目從 hello**配額**項目，如下列範例中的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="a247c-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a247c-170">配額可以根據每個間隔、 頻寬或兩者的呼叫 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="a247c-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="a247c-171">在本教學課程中，我們不會節流根據的頻寬，請刪除 hello**頻寬**屬性。</span><span class="sxs-lookup"><span data-stu-id="a247c-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a247c-172">Hello 免費試用版的產品，在 hello 配額會是 200 每週的呼叫。</span><span class="sxs-lookup"><span data-stu-id="a247c-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="a247c-173">指定**200**為 hello hello 值**呼叫**屬性，然後再指定**604800**為 hello hello 值**更新間隔**屬性。</span><span class="sxs-lookup"><span data-stu-id="a247c-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="a247c-174">原則間隔是依秒來指定。</span><span class="sxs-lookup"><span data-stu-id="a247c-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="a247c-175">toocalculate hello 一週的間隔，您可以將 hello 天數 (7) 依 hello 以 hello 分鐘中的每分鐘 (60) 秒的 hello 數小時 (60) 的一天 （24 小時） 的小時數： 7 * 24 * 60 * 60 = 604800。</span><span class="sxs-lookup"><span data-stu-id="a247c-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="a247c-176">當您完成設定 hello 原則時，其值必須符合下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a247c-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="a247c-177">Hello 預期的原則設定之後，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a247c-177">After hello desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="a247c-179"><a name="publish-product"></a> toopublish hello 產品</span><span class="sxs-lookup"><span data-stu-id="a247c-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="a247c-180">既然 hello hello 應用程式開發介面，且 hello 原則設定，請使其可以用於開發人員必須發行 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="a247c-181">按一下**產品**從 hello **API 管理**hello 左、，然後按一下功能表**免費試用版**tooconfigure hello 產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="a247c-183">按一下**發行**，然後按一下 **是，將它發行**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="a247c-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="a247c-185"><a name="subscribe-account"></a>toosubscribe 開發人員帳戶 toohello 產品</span><span class="sxs-lookup"><span data-stu-id="a247c-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="a247c-186">現在該 hello 產品發行時，它就是可用訂閱的 toobe tooand 由開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="a247c-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="a247c-187">API 管理執行個體的系統管理員會自動訂閱的 tooevery 產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="a247c-188">在此教學課程步驟中，我們會訂閱 hello 非系統管理員的開發人員帳戶 toohello 免費試用版產品的其中一個。</span><span class="sxs-lookup"><span data-stu-id="a247c-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="a247c-189">如果您的開發人員帳戶屬於 hello 系統管理員角色，然後您可以依照此步驟中，即使您已經訂閱。</span><span class="sxs-lookup"><span data-stu-id="a247c-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="a247c-190">按一下**使用者**上 hello **API 管理**hello 功能表左、，然後按一下hello 您的開發人員帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a247c-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="a247c-191">在此範例中，我們會使用 hello **Clayton Gragg**開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a247c-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="a247c-193">按一下 [ **加入訂閱**]。</span><span class="sxs-lookup"><span data-stu-id="a247c-193">Click **Add Subscription**.</span></span>

![加入訂閱][api-management-add-subscription-menu]

<span data-ttu-id="a247c-195">選取 免費試用，然後按一下訂閱。</span><span class="sxs-lookup"><span data-stu-id="a247c-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![加入訂閱][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="a247c-197">在本教學課程中，不會啟用多個同時訂閱 hello 免費試用版產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="a247c-198">如果是，您將提示的 tooname hello 訂用帳戶 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a247c-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![加入訂閱][api-management-add-subscription-multiple]

<span data-ttu-id="a247c-200">按一下後**訂閱**，hello 產品會出現在 hello**訂用帳戶**hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="a247c-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![已新增訂用帳戶][api-management-subscription-added]

## <span data-ttu-id="a247c-202"><a name="test-rate-limit"></a>toocall 作業並測試 hello 速率限制</span><span class="sxs-lookup"><span data-stu-id="a247c-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="a247c-203">既然 hello 免費試用版產品設定和發佈，我們可以呼叫某些作業，並測試 hello 速率限制原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="a247c-204">交換器 toohello 開發人員入口網站，依序按一下**開發人員入口網站**hello 右上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="a247c-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="a247c-206">按一下**Api**在 hello 上方的功能表，然後按一下 **Echo API**。</span><span class="sxs-lookup"><span data-stu-id="a247c-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![開發人員入口網站][api-management-developer-portal-api-menu]

<span data-ttu-id="a247c-208">按一下 GET 資源，然後按一下嘗試。</span><span class="sxs-lookup"><span data-stu-id="a247c-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="a247c-210">保留 hello 預設參數值，然後選取 您的訂用帳戶金鑰 hello 免費試用版產品。</span><span class="sxs-lookup"><span data-stu-id="a247c-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![訂用帳戶金鑰][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="a247c-212">如果您有多個訂閱，是確定 tooselect hello 金鑰**免費試用版**，或其他 hello 先前步驟中設定的 hello 原則將不會生效。</span><span class="sxs-lookup"><span data-stu-id="a247c-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="a247c-213">按一下**傳送**，然後檢視 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="a247c-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="a247c-214">請注意 hello**回應狀態**的**200 確定**。</span><span class="sxs-lookup"><span data-stu-id="a247c-214">Note hello **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="a247c-216">按一下**傳送**的比率大於此數目的 10 每分鐘呼叫 hello 速率限制原則。</span><span class="sxs-lookup"><span data-stu-id="a247c-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="a247c-217">當超過 hello 速率限制原則之後，回應狀態**429 太多要求**傳回。</span><span class="sxs-lookup"><span data-stu-id="a247c-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="a247c-219">hello**回應內容**指出 hello 剩餘間隔之前重試將會成功。</span><span class="sxs-lookup"><span data-stu-id="a247c-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="a247c-220">後續呼叫時的每分鐘 10 呼叫 hello 速率限制原則生效時，將會失敗，直到從 hello 經過 60 秒 hello 10 成功呼叫 toohello 產品之前已超過 hello 速率限制的第一個。</span><span class="sxs-lookup"><span data-stu-id="a247c-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="a247c-221">在此範例中，hello 剩餘間隔會為 54 秒。</span><span class="sxs-lookup"><span data-stu-id="a247c-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="a247c-222"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="a247c-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a247c-223">監看下列影片 hello 設定速率限制和配額的示範。</span><span class="sxs-lookup"><span data-stu-id="a247c-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
