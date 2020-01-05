---
title: Unity脚本生命周期
date: 2020-01-04 23:07:14
categories:
- Unity
- C#
tags:
- Unity-Scripting
---

```
Running a Unity script executes a number of event functions in a predetermined order.
```
一个Unity脚本中的事件函数将会以预先确定的顺序被执行。
<!--more-->

##  脚本生命周期

### 流程图

<img src="/images/monobehaviour_flowchart.svg" alt="monobehaviour flowchart">

### 说明

- **Awake**:
    ```
    This function is always called before any Start functions and also just after a prefab is instantiated.
    ```
    此方法将在预设物体被实例化时调用，优先于任何Start方法。

- **OnEnable**:
    ```
    This function is called just after the object is enabled. This happens when a MonoBehaviour instance is created, such as when a level is loaded or a GameObject with the script component is instantiated.
    ```
    此方法将在对象被激活时调用，例如关卡加载完成或一个携带脚本组件的游戏对象被实例化。

- **Start**:
    ```
    Start is called before the first frame update only if the script instance is enabled.
    ```
    此方法将紧跟Awake方法被调用，确切来说是在第一帧更新前并且此时脚本实例已被激活。

- **Reset**:
    ```
    Reset is called to initialize the script’s properties when it is first attached to the object and also when the Reset command is used.
    ```
    为物体添加一个脚本对象，或添加完成后点击Editor中的Reset按钮，此方法将被调用。

- **FixedUpdate**:
    ```
    FixedUpdate is often called more frequently than Update on a reliable timer, independent of the frame rate.
    ```
    此方法将会以固定时间间隔被调用，属于物理层。

- **Update**:
    ```
    Update is called once per frame. It is the main workhorse function for frame updates.
    ```
    此方法是更新游戏场景每一帧的主要方法，受当前渲染物体影响，被调用的时间间隔不固定。

- **LateUpdate**:
    ```
    LateUpdate is called once per frame, after Update has finished. 
    ```
    此方法将紧跟Update方法被调用，通常用于伴随逻辑的执行。

- **OnApplicationQuit**:
    ```
    This function is called on all game objects before the application is quit. In the editor it is called when the user stops playmode.
    ```
    此方法将在应用终止时被调用，例如在Editor中点击stop按钮关闭播放模式。

- **OnDisable**:
    ```
    This function is called when the behaviour becomes disabled or inactive.
    ```
    此方法将在对象激活状态关闭时被调用，例如OnApplicationQuit方法被执行之后。

- **OnDestroy**:
    ```
    This function is called after all frame updates for the last frame of the object’s existence (the object might be destroyed in response to Object.Destroy or at the closure of a scene).
    ```
    此方法将在完成对象最后一帧渲染后被调用，例如Object.Destory方法被调用或场景关闭之后。

## 方法调用时机

为一个Cube物体添加Lifecycle脚本组件。

### 测试代码

```csharp
using UnityEngine;

/// <summary>
/// Simple demo for script lifecycle .
/// <summary>

public class Lifecycle : MonoBehaviour
{
    private void Awake()
    {
        Debug.Log("Function : Awake() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void OnEnable()
    {
        Debug.Log("Function : OnEnable() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void Reset()
    {
        Debug.Log("Function : Reset() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void Start()
    {
        Debug.Log("Function : Start() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void FixedUpdate()
    {
        if (Time.time < 0.1)
        {
            Debug.Log("Function : FixedUpdate() " + "Time : " + Time.time + " Object.name : " + this.name);
        }
    }

    private void OnMouseDown()
    {
        Debug.Log("Function : OnMouseDown() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void Update()
    {
        if (Time.time < 0.1)
        {
            Debug.Log("Function : Update() " + "Time : " + Time.time + " Object.name : " + this.name);
        }
    }

    private void LateUpdate()
    {
        if (Time.time < 0.1)
        {
            Debug.Log("Function : LateUpdate() " + "Time : " + Time.time + " Object.name : " + this.name);
        }
    }

    private void OnGUI()
    {
        if (Time.time < 0.1)
        {
            Debug.Log("Function : OnGUI() " + "Time : " + Time.time + " Object.name : " + this.name);
        }
    }

    private void OnApplicationPause(bool pause)
    {
        if (pause)
        {
            Debug.Log("Function : OnApplicationPause() " + "Time : " + Time.time + " Object.name : " + this.name);
        }
        
    }

    private void OnApplicationQuit()
    {
        Debug.Log("Function : OnApplicationQuit() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    private void OnDisable()
    {
        Debug.Log("Function : OnDisable() " + "Time : " + Time.time + " Object.name : " + this.name);
    }

    public void OnDestroy()
    {
        Debug.Log("Function : OnDestroy() " + "Time : " + Time.time + " Object.name : " + this.name);
    }
}
```

### 测试结果


<img src="/images/lifecycle_demo.png" alt="lifecycle demo">

### 反馈

控制台输出结果表明，运行场景时点击pause按钮将不会触发OnApplicationPause方法，那么该方法的调用时机究竟是？？？

## 官方文档 

[Order of Execution for Event Functions](https://docs.unity3d.com/Manual/ExecutionOrder.html)
