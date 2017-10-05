---
title: "Unity Roll a Ball 教學課程"
description: "建立傳統 Unity Roll a Ball 遊戲的步驟，此遊戲是所有 Mobile Engagement Unity 教學課程的必要條件"
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
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="f1a9d-103"><a id="unity-roll-a-ball"></a>建立 Unity Roll a Ball 遊戲</span><span class="sxs-lookup"><span data-stu-id="f1a9d-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="f1a9d-104">本教學課程逐步引導您完成稍微修改過的 [Unity Roll a Ball 教學課程](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="f1a9d-105">此範例遊戲由 app 使用者控制的球面「玩家」物件所組成，遊戲的目標是使用這些可收集的物件碰撞玩家物件來「收集」可收集的物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="f1a9d-106">這是假設使用者對 Unity 編輯器環境有基本的熟悉度。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="f1a9d-107">如果您遇到任何問題，應該參閱完整的教學課程。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="f1a9d-108">設定遊戲</span><span class="sxs-lookup"><span data-stu-id="f1a9d-108">Setting up the game</span></span>
<span data-ttu-id="f1a9d-109">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f1a9d-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="f1a9d-110">開啟 **Unity 編輯器**，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="f1a9d-111">提供 [專案名稱]  &  [位置]、選取 [3D]，然後按一下 [建立專案]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="f1a9d-112">使用名稱 **MiniGame**，將剛建立的預設場景當做新專案的一部分，儲存在 **Assets**資料夾底下的新 **\_Scenes** 資料夾內︰</span><span class="sxs-lookup"><span data-stu-id="f1a9d-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="f1a9d-113">建立 **3D Object -> Plane** 做為遊戲場，然後將這個平面物件重新命名為 **Ground**</span><span class="sxs-lookup"><span data-stu-id="f1a9d-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="f1a9d-114">重設此 **Ground** 物件的轉換元件，使其位於原點。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="f1a9d-115">從 **Ground** 物件的 **Gizmos 功能表**取消核取 [顯示格線]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="f1a9d-116">將 **Ground** 物件的 **Scale** 元件更新為 [X = 2,Y = 1, Z = 2]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="f1a9d-117">將新的 **3D Object -> Sphere** 新增至專案，並將此球形物件重新命名為 **Player**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="f1a9d-118">選取 **Player** 物件，然後按一下類似於 Plane 物件的 [重設轉換]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="f1a9d-119">將玩家 Y 的 **Transform -> Position -> Y Coordinate** 元件更新為 0.5。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="f1a9d-120">在我們將建立材料以便為玩家著色所在的專案中，建立一個稱為 **Materials** 的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="f1a9d-121">在此資料夾中建立一個稱為 **Background** 的新 **Material**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="f1a9d-122">更新材料的 **Albedo** 屬性，以更新材料的色彩。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="f1a9d-123">您可以選取 RGB 值 [0,32,64]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="f1a9d-124">將此材料拖曳到場景檢視，以便將色彩套用至 **Ground** 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="f1a9d-125">最後，為清楚起見，將 Directional Light 物件的 **Transform -> Rotation -> Y** 更新為 60。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="f1a9d-126">移動玩家</span><span class="sxs-lookup"><span data-stu-id="f1a9d-126">Moving the player</span></span>
<span data-ttu-id="f1a9d-127">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f1a9d-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="f1a9d-128">將 **RigidBody** 元件新增至 **Player** 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="f1a9d-129">在專案中建立一個稱為 **Scripts** 的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="f1a9d-130">按一下 [新增元件 -> 新增指令碼 -> C# 指令碼]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="f1a9d-131">將其命名為 **PlayerController**，然後按一下 [建立及新增]。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="f1a9d-132">這將會建立一個指令碼，並將其附加至 Player 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="f1a9d-133">將此指令碼移到專案的 **Scripts** 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="f1a9d-134">開啟要在您最愛的指令碼編輯器中編輯的指令碼、將指令碼更新為下列程式碼並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
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
6. <span data-ttu-id="f1a9d-135">請注意，上述指令碼會使用 **Speed** 屬性。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="f1a9d-136">在 Unity Editor 中，將 speed 屬性更新為 10。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="f1a9d-137">按 Unity Editor 中的 **Play** 。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="f1a9d-138">現在您應該能夠使用鍵盤控制球，而且球應該會旋轉並四處移動。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="f1a9d-139">移動相機</span><span class="sxs-lookup"><span data-stu-id="f1a9d-139">Moving the camera</span></span>
<span data-ttu-id="f1a9d-140">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141)，而且會將 **Main Camera** 繫結至 **Player** 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="f1a9d-141">將 **Transform.Position** 更新為 X = 0、Y = 10.5、Z =-10。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="f1a9d-142">將 **Transform.Rotation** 更新為 X = 45、Y = 0、Z = 0。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="f1a9d-143">將稱為 **CameraController** 的新指令碼加入至 **MainCamera**，並將其移動到 Scripts 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="f1a9d-144">開啟指令碼進行編輯，並在其中加入下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="f1a9d-144">Open up the script for editing and add the following code in it:</span></span>
   
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
5. <span data-ttu-id="f1a9d-145">在 Unity 環境中，將 Player 變數拖曳到 Main Camera 物件的 Player 位置，使兩者相互關聯。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="f1a9d-146">現在如果您按 Unity Editor 中的 Play 並旋轉 Player Ball 物件，您將會看到 Camera 在該物件後面移動。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="f1a9d-147">設定遊戲區域</span><span class="sxs-lookup"><span data-stu-id="f1a9d-147">Setting up the Play area</span></span>
<span data-ttu-id="f1a9d-148">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="f1a9d-149">我們將在 Ground 周圍建立 Walls，讓 Player Ball 物件不會在移動時掉出遊戲區域。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="f1a9d-150">按一下 [建立 -> 建立空的 -> 遊戲物件]，並將它命名 **Walls**</span><span class="sxs-lookup"><span data-stu-id="f1a9d-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="f1a9d-151">在此 Walls 物件底下，建立新的 **3D 物件 -> Cube**，並將它命名為 "West wall"。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="f1a9d-152">更新此 West Wall 物件的 **轉換 -> 位置** 和 **轉換 -> 調整**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="f1a9d-153">複製 West wall，以更新的轉換位置和比例建立 **East wall** 。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="f1a9d-154">複製 East wall，以更新的轉換位置和比例建立 **North wall**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="f1a9d-155">複製 North wall，以更新的轉換位置和比例建立 **South wall**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="f1a9d-156">建立可收集的物件</span><span class="sxs-lookup"><span data-stu-id="f1a9d-156">Creating Collectible objects</span></span>
<span data-ttu-id="f1a9d-157">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="f1a9d-158">我們將會建立一些外觀吸引人的物件，這些物件會形成一組可收集的物件，Player Ball 物件必須透過碰撞這組可收集的物件來「收集」它們。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="f1a9d-159">建立新 **3D Cube** 物件，並將它命名為 Pickup。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="f1a9d-160">調整 Pickup 物件的 **轉換 -> 旋轉**  &  **轉換 -> 調整**。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="f1a9d-161">建立一個稱為 **Rotator** 的**新 C# 指令碼**，並將其附加至 Pickup 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="f1a9d-162">請務必將指令碼放在 Scripts 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="f1a9d-163">開啟此指令碼進行編輯，並將其更新如下：</span><span class="sxs-lookup"><span data-stu-id="f1a9d-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="f1a9d-164">現在按 Unity Editor 中的 Play 模式，您的 Pickup 物件應該就會在其軸上旋轉。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="f1a9d-165">在我們將建立材料以便為玩家著色所在的專案中，建立一個稱為 **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="f1a9d-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="f1a9d-166">拖曳 **Pickup** 物件，並將其放在 Prefabs 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="f1a9d-167">建立一個稱為 **Pickups** 的新 **Empty Game** 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="f1a9d-168">將其位置重設為原點，然後將 Pickup 物件拖曳到此遊戲物件底下。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="f1a9d-169">複製 **Pickup** 物件，並藉由適當地更新 **Transform.Position** 的 X 和 Z 值，將其散佈在 **Player** 物件周圍的 **Ground** 物件上。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="f1a9d-170">建立一個稱為 **Pickup** 的**新材料**，並藉由更新 **Albedo** 屬性 (類似我們更新 Ground 物件的方式)，將其更新為紅色。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="f1a9d-171">將材料套用至全部 4 個 Pickup 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="f1a9d-172">收集 Pickup 物件</span><span class="sxs-lookup"><span data-stu-id="f1a9d-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="f1a9d-173">下列步驟來自 [Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141)。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="f1a9d-174">我們將更新 Player，使其能夠透過碰撞的方式，「收集」Pickup 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="f1a9d-175">開啟已附加至 Player 物件的 **PlayerController** 指令碼進行編輯，並將其更新為：</span><span class="sxs-lookup"><span data-stu-id="f1a9d-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
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
2. <span data-ttu-id="f1a9d-176">建立一個稱為 **Pick Up** 的新 **Tag** (它必須符合指令碼中的內容)</span><span class="sxs-lookup"><span data-stu-id="f1a9d-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="f1a9d-177">將此 **Tag** 套用至 Prefab Pickup 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="f1a9d-178">為 Prefab 物件啟用 **IsTrigger** 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="f1a9d-179">將 Rigid body 新增至 Pickup Prefab 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="f1a9d-180">為將效能最佳化，我們將會更新我們用於 Dynamic Collider 的 Static Collider。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="f1a9d-181">最後，檢查 Prefab 物件的 **IsKinematic** 屬性。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="f1a9d-182">按 Unity 編輯器中的 [播放]，您就能夠透過使用鍵盤按鍵當做方向輸入移動 Player 物件來玩這個 **Roll a Ball** 遊戲。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="f1a9d-183">更新遊戲以便在行動裝置上玩遊戲</span><span class="sxs-lookup"><span data-stu-id="f1a9d-183">Updating the game for mobile play</span></span>
<span data-ttu-id="f1a9d-184">以上幾節就是 Unity 的基本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="f1a9d-185">現在，我們將修改遊戲，使其成為行動裝置上的遊戲。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="f1a9d-186">請注意，到目前為止我們使用鍵盤輸入來測試遊戲。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="f1a9d-187">現在，我們將修改遊戲，讓我們可以使用手機的動作控制玩家，亦即，</span><span class="sxs-lookup"><span data-stu-id="f1a9d-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="f1a9d-188">使用加速計做為輸入。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="f1a9d-189">開啟 **PlayerController** 指令碼進行編輯，並更新 **FixedUpdate** 方法，以使用加速計的動作移動 Player 物件。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="f1a9d-190">本教學課程使用 Unity 建立基本遊戲的部分到此結束，您可以在您選擇要玩遊戲的裝置上部署此遊戲。</span><span class="sxs-lookup"><span data-stu-id="f1a9d-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

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













