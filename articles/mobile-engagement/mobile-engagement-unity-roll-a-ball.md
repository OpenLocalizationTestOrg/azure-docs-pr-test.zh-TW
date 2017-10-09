---
title: "aaaUnity 回復球教學課程"
description: "步驟 toocreate hello 傳統 Unity 回復球遊戲也就是所有的 Mobile Engagement Unity 教學課程的必要條件"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="11e67-103"><a id="unity-roll-a-ball"></a>建立 Unity Roll a Ball 遊戲</span><span class="sxs-lookup"><span data-stu-id="11e67-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="11e67-104">本教學課程引導 hello 主要步驟稍微修改[Unity 回復球教學課程](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)。</span><span class="sxs-lookup"><span data-stu-id="11e67-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="11e67-105">此範例遊戲包含球面 'player' 物件所控制的 hello 應用程式的使用者與 hello hello 遊戲目標是 too'collect' 可回收物件衝突的 hello 播放程式物件，與這些可回收物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="11e67-106">這是假設使用者對 Unity 編輯器環境有基本的熟悉度。</span><span class="sxs-lookup"><span data-stu-id="11e67-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="11e67-107">如果您遇到任何問題，您應該參閱 toohello 完整的教學課程。</span><span class="sxs-lookup"><span data-stu-id="11e67-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="11e67-108">設定 hello 遊戲</span><span class="sxs-lookup"><span data-stu-id="11e67-108">Setting up hello game</span></span>
<span data-ttu-id="11e67-109">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="11e67-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="11e67-110">開啟 **Unity 編輯器**，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="11e67-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="11e67-111">提供 [專案名稱]  &  [位置]、選取 [3D]，然後按一下 [建立專案]。</span><span class="sxs-lookup"><span data-stu-id="11e67-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="11e67-112">儲存剛才建立 hello 新專案的一部分，如同 hello 名稱 hello 預設場景**MiniGame**內新**\_場景**下的資料夾**資產**資料夾：</span><span class="sxs-lookup"><span data-stu-id="11e67-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="11e67-113">建立**3D 物件]-> [平面**為 hello 播放欄位，然後重新命名這個平面物件做為**地面**</span><span class="sxs-lookup"><span data-stu-id="11e67-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="11e67-114">重設 hello 轉換元件，這個**地面**物件，讓它位於 hello 原點。</span><span class="sxs-lookup"><span data-stu-id="11e67-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="11e67-115">取消核取**顯示方格**從**Gizmos 功能表**hello**地面**物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="11e67-116">更新 hello**標尺**元件 hello**地面**物件 toobe [X = 2，Y = 1，Z = 2]。</span><span class="sxs-lookup"><span data-stu-id="11e67-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="11e67-117">加入新**3D 物件]-> [球體**toohello 專案和重新命名此球面物件當做**Player**。</span><span class="sxs-lookup"><span data-stu-id="11e67-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="11e67-118">選取 hello **Player**物件，並按一下**重設轉換**類似 toohello 平面物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="11e67-119">更新**轉換]-> [位置]-> [Y 座標**0.5 hello Player Y 元件。</span><span class="sxs-lookup"><span data-stu-id="11e67-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="11e67-120">建立新資料夾，稱為**材料**hello 我們將在其中建立 hello 材料 toocolor hello 播放程式的專案中。</span><span class="sxs-lookup"><span data-stu-id="11e67-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="11e67-121">在此資料夾中建立一個稱為 **Background** 的新 **Material**。</span><span class="sxs-lookup"><span data-stu-id="11e67-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="11e67-122">藉由更新 hello 更新 hello 色彩的 hello 材料**屑**它的屬性。</span><span class="sxs-lookup"><span data-stu-id="11e67-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="11e67-123">您可以選取 [0,32,64] hello RGB 值。</span><span class="sxs-lookup"><span data-stu-id="11e67-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="11e67-124">將這份資料拖曳到 hello 場景檢視 tooapply 色彩 toohello**地面**物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="11e67-125">最後更新 hello**轉換]-> [旋轉]-> [Y** too60 為了清楚起見 hello 方向燈物件上的。</span><span class="sxs-lookup"><span data-stu-id="11e67-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="11e67-126">移動 hello 播放程式</span><span class="sxs-lookup"><span data-stu-id="11e67-126">Moving hello player</span></span>
<span data-ttu-id="11e67-127">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="11e67-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="11e67-128">新增**RigidBody**元件 toohello **Player**物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="11e67-129">建立新資料夾，稱為**指令碼**hello 專案中。</span><span class="sxs-lookup"><span data-stu-id="11e67-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="11e67-130">按一下 [新增元件 -> 新增指令碼 -> C# 指令碼]。</span><span class="sxs-lookup"><span data-stu-id="11e67-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="11e67-131">將其命名為 **PlayerController**，然後按一下 [建立及新增]。</span><span class="sxs-lookup"><span data-stu-id="11e67-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="11e67-132">這將會建立並附加指令碼 toohello 播放程式物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="11e67-133">此指令碼在 hello 移**指令碼**hello 專案資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="11e67-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="11e67-134">開啟 hello 指令碼，以便在您最愛的指令碼編輯器中編輯，以下列程式碼的 hello 更新 hello 指令碼並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="11e67-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="11e67-135">請注意該 hello 上述指令碼會使用**速度**屬性。</span><span class="sxs-lookup"><span data-stu-id="11e67-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="11e67-136">在 hello Unity 編輯器中，更新 hello 速度屬性 too10。</span><span class="sxs-lookup"><span data-stu-id="11e67-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="11e67-137">叫用**播放**hello Unity 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="11e67-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="11e67-138">現在您應該使用 hello 鍵盤可以 toocontrol hello 球，它應該旋轉並四處移動。</span><span class="sxs-lookup"><span data-stu-id="11e67-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="11e67-139">移動 hello 相機</span><span class="sxs-lookup"><span data-stu-id="11e67-139">Moving hello camera</span></span>
<span data-ttu-id="11e67-140">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141)會結合 hello 和**Main 相機**toohello **Player**物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="11e67-141">更新 hello **Transform.Position** toobe X = Y，0 = 10.5，Z =-10。</span><span class="sxs-lookup"><span data-stu-id="11e67-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="11e67-142">更新 hello **Transform.Rotation** toobe X = 45，Y = 0，Z = 0。</span><span class="sxs-lookup"><span data-stu-id="11e67-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="11e67-143">加入新的指令碼呼叫**CameraController** toohello **MainCamera**並將其移 hello 指令碼 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="11e67-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="11e67-144">開啟供編輯的 hello 指令碼，並新增下列程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="11e67-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="11e67-145">在 Unity 環境-拖曳 hello 播放程式變數到 hello Player 位置 hello Main 相機物件，使 hello 兩個是與另一個相關聯。</span><span class="sxs-lookup"><span data-stu-id="11e67-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="11e67-146">現在如果您遇到播放 hello Unity editor 和旋轉 hello Player 球物件中您會看到 hello 依照 hello 移動的相機。</span><span class="sxs-lookup"><span data-stu-id="11e67-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="11e67-147">設定 hello 播放區域</span><span class="sxs-lookup"><span data-stu-id="11e67-147">Setting up hello Play area</span></span>
<span data-ttu-id="11e67-148">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="11e67-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="11e67-149">我們將建立 hello 牆以便 hello Player 球物件不會卸除關閉其移動中的 hello 播放區域周圍 hello 接地。</span><span class="sxs-lookup"><span data-stu-id="11e67-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="11e67-150">按一下 [建立 -> 建立空的 -> 遊戲物件]，並將它命名 **Walls**</span><span class="sxs-lookup"><span data-stu-id="11e67-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="11e67-151">在此 Walls 物件底下，建立新的 **3D 物件 -> Cube**，並將它命名為 "West wall"。</span><span class="sxs-lookup"><span data-stu-id="11e67-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="11e67-152">更新 hello**轉換]-> [位置**和**轉換]-> [標尺**這個西牆上的物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="11e67-153">重複的 hello 西牆 toocreate**東部牆**以更新的 hello 轉換位置和小數位數。</span><span class="sxs-lookup"><span data-stu-id="11e67-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="11e67-154">重複的 hello 東部牆 toocreate **North 牆**以更新的 hello 轉換位置和小數位數。</span><span class="sxs-lookup"><span data-stu-id="11e67-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="11e67-155">重複的 hello North 牆並建立**南牆**以更新的 hello 轉換位置和小數位數。</span><span class="sxs-lookup"><span data-stu-id="11e67-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="11e67-156">建立可收集的物件</span><span class="sxs-lookup"><span data-stu-id="11e67-156">Creating Collectible objects</span></span>
<span data-ttu-id="11e67-157">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="11e67-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="11e67-158">我們將會建立一些吸引人尋找物件形成 hello 一組可收集之物件的 hello Player 球物件需要 too'collect' 由它們互相衝突。</span><span class="sxs-lookup"><span data-stu-id="11e67-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="11e67-159">建立新 **3D Cube** 物件，並將它命名為 Pickup。</span><span class="sxs-lookup"><span data-stu-id="11e67-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="11e67-160">調整 hello**轉換]-> [旋轉** & **轉換]-> [標尺**的 hello 收取物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="11e67-161">建立並附加**新的 C# 指令碼**呼叫**Rotator** toohello 收取物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="11e67-162">請確定 tooput hello 指令碼 hello 指令碼 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="11e67-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="11e67-163">開啟供編輯這個指令碼，並更新其遵循 toobe hello:</span><span class="sxs-lookup"><span data-stu-id="11e67-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="11e67-164">現在點擊的 hello 播放模式中 hello Unity Editor 和收取物件顯示會旋轉的軸上。</span><span class="sxs-lookup"><span data-stu-id="11e67-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="11e67-165">在我們將建立材料以便為玩家著色所在的專案中，建立一個稱為 **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="11e67-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="11e67-166">拖曳 hello**收取**物件，並將它放在 hello Prefabs 資料夾。</span><span class="sxs-lookup"><span data-stu-id="11e67-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="11e67-167">建立一個稱為 **Pickups** 的新 **Empty Game** 物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="11e67-168">重設其位置 tooorigin，然後拖曳 hello 收取物件，在此遊戲的物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="11e67-169">重複的 hello**收取**物件，並散佈在 hello**地面**物件周圍 hello **Player**物件藉由更新 hello **Transform.Position 的 X & Z**適當值。</span><span class="sxs-lookup"><span data-stu-id="11e67-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="11e67-170">建立**新材料**呼叫**收取**並更新它 toobe 紅色色彩，以更新 hello**屑屬性**類似 toowhat 我們並未更新 hello 地面物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="11e67-171">適用於 hello 材料 tooall hello 4 收取物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="11e67-172">收集 hello 收取物件</span><span class="sxs-lookup"><span data-stu-id="11e67-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="11e67-173">從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="11e67-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="11e67-174">我們將會更新 hello 播放程式，使其能夠 too'collect' hello 正在與它們所收取的物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="11e67-175">開啟 hello **PlayerController**附加的 toohello Player 物件以供編輯的指令碼，並更新 toohello 遵循：</span><span class="sxs-lookup"><span data-stu-id="11e67-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="11e67-176">建立新**標記**呼叫**挑選向上**（它必須符合何謂 hello 指令碼中）</span><span class="sxs-lookup"><span data-stu-id="11e67-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="11e67-177">套用此**標記**toohello Prefab 收取物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="11e67-178">啟用**IsTrigger** hello Prefab 物件的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="11e67-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="11e67-179">將固定的主體 tooPickup Prefab 物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="11e67-180">效能最佳化，我們將會更新，我們使用 tooa 動態 collider hello 靜態 collider。</span><span class="sxs-lookup"><span data-stu-id="11e67-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="11e67-181">最後檢查 hello **IsKinematic** hello prefab 物件屬性。</span><span class="sxs-lookup"><span data-stu-id="11e67-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="11e67-182">叫用**播放**hello Unity editor，而且將會無法 tooplay 這**回復球**遊戲藉由移動 hello 方向輸入使用鍵盤按鍵的播放程式物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="11e67-183">更新行動裝置的播放遊戲 hello</span><span class="sxs-lookup"><span data-stu-id="11e67-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="11e67-184">上述從未的 hello Unity 從基本教學課程的 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="11e67-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="11e67-185">現在我們將會修改 hello 遊戲 toomake 它易記的行動裝置。</span><span class="sxs-lookup"><span data-stu-id="11e67-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="11e67-186">請注意，我們使用鍵盤輸入 hello 遊戲為止進行測試。</span><span class="sxs-lookup"><span data-stu-id="11e67-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="11e67-187">現在我們將會修改它，讓我們可以控制 hello 播放程式使用 hello 影片的 hello 電話也就使用加速計做為輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="11e67-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="11e67-188">開啟 hello **PlayerController**指令碼編輯和更新的 hello **FixedUpdate**方法 toouse hello 影片從 hello 加速計 toomove hello 播放程式物件。</span><span class="sxs-lookup"><span data-stu-id="11e67-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="11e67-189">本教學課程結束時，使用 Unity 的基本遊戲建立，您可以選擇 tooplay hello 遊戲的裝置上部署。</span><span class="sxs-lookup"><span data-stu-id="11e67-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













