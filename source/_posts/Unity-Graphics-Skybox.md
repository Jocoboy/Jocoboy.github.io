---
title: Unity自定义天空盒
date: 2020-01-06 21:02:25
categories:
- Unity
- C#
tags:
- Unity-Graphics
---

```
A Skybox is a six-sided cube that Unity draws behind all graphics in the Scene. 
```
一个天空盒是一个六面立方体，会将游戏场景中的所有图形包裹。

<!--more-->

## 自定义天空盒

### 创建步骤

1. 创建与天空盒六个面相对于的六个纹理，将它们放在项目的`Assets`文件夹中。
```
Make six Textures that correspond to each of the six sides of the skybox, and put them into your
Project’s Assets folder.
```
<img src="/images/skybox/skybox_textures.png" alt="skybox textures">

2. 对于每个纹理，需要将包裹模式从`Repeat`更改为`Clamp`。如果不这样做，边缘上的颜色将不匹配。
```
For each Texture, you need to change the wrap mode from Repeat to Clamp.
If you don’t do this, colors on the edges do not match up.
```
<img src="/images/skybox/wrap_mode.png" alt="wrap mode">

3. 从菜单栏中选择`Assets > Create > Material`以创建新材质。 
```
Create a new Material. To do this, choose Assets > Create > Material from the menu bar.
```

4. 在`Inspector`面板的顶部选择`Shader`下拉选单，然后选择`Skybox/6 Sided`。
```
Select the Shader drop-down and choose Skybox/6 Sided.
```

5. 将6个纹理分配给材质中的每个纹理字段。为此，可将每个纹理从`Project`面板拖放到相应的字段上。
```
Assign the six Textures to each Texture slot in the Material. 
To do this, you can drag each Texture from the Project View onto the corresponding slots.
```
<img src="/images/skybox/skybox_inspector.png" alt="skybox inspector">

6. 最后，将天空盒分配给当前场景，须执行以下操作：
    - 在菜单栏中选择`Window > Rendering > Lighting Settings`。
    - 在随后出现的窗口中选择Scene选项卡。
    - 将新的天空盒材质拖放到`Skybox`字段。
```
To assign the skybox to the Scene you’re working on:

- From the menu bar, choose Window > Rendering > Lighting Settings.
- In the window that appears, select the Scene tab.
- Drag the new Skybox Material to the Skybox slot.
```

<img src="/images/skybox/skybox_application.png" alt="skybox application">

## 官方文档

[How do I Make a Skybox?](https://docs.unity3d.com/Manual/HOWTO-UseSkybox.html)