參考
https://www.youtube.com/watch?v=ylLP09RG_3g&list=LL&index=2



# 點螢幕新增物件
## 1.AR Session origin加入ARRaycastManager  
![](https://i.imgur.com/8B4DZKu.png)
## 新增ArTouchAddObj 自己撰寫的程式
![](https://i.imgur.com/6NSjb67.png)
1.這個程式點選螢幕之後會 Instantiate 一個物件，所以自己新增一個prefab物件拖曳到這裡來，就可以再點選螢幕之後，新增．  
2.拖入ARRaycastManager 


```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.XR.ARFoundation;

public class ArTouchAddObj : MonoBehaviour
{
    public GameObject Obj;
    public ARRaycastManager mARRaycastManager;
    private List<ARRaycastHit> m_hit = new List<ARRaycastHit>();
    void Start()
    {
        
    }


    void Update()
    {

        if (Input.touchCount > 0)
        {
            Touch t = Input.GetTouch(0);
            if (t.phase == TouchPhase.Began)
            {
                if (mARRaycastManager.Raycast(t.position, m_hit, UnityEngine.XR.ARSubsystems.TrackableType.PlaneWithinPolygon))
                {
                    Pose hitP = m_hit[0].pose;
                    Instantiate(Obj, hitP.position, hitP.rotation);
                }
            }
        }

    }
}
```


# people occulision
## 在 AR Camera下增加AR Occlusion manager 就可以啟動 人體遮罩

![](https://i.imgur.com/lwH3SHT.png)
![](https://i.imgur.com/HUlHRVt.png)
