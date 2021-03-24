
# Why This Script Was Created
#### This class allows you to resize an image on the GPU.
## Speeds

|Methods	|Speeds	  |Source	  |
|:--|--:|--:|
|`ResizeTool.Resize(..)`|**00:00:40.89**|This Tool **[FREE]**|
|`UnityEngine.Texture2D.Resize(..)`|**01:08:08.55**|[Unity Method](https://docs.unity3d.com/ScriptReference/Texture2D.Resize.html)|
|`ResizePro.Resize(..)`|  **00:00:40.28**|ResizePro [\[PAID ASSET\]](https://assetstore.unity.com/packages/tools/utilities/resize-pro-61344)|

![progress bars of ResizeTool vs Texture2D.Resize](img/example.gif)

### Here is the process:

1. `RenderTexture rt = RenderTexture.GetTemporary()` create a temporary render texture with the target size
2. `RenderTexture.active` set the active [RenderTexture](https://docs.unity3d.com/ScriptReference/RenderTexture.html) to the temporary texture so we can read from it
3.  `Graphics.Blit()` Copies source texture into destination render texture with a shader _(on the gpu)_ [more info](https://docs.unity3d.com/ScriptReference/Graphics.Blit.html)
4. `texture2D.Resize()` resize the texture to the target values _(this sets the pixel data as undefined)_ [more info](https://docs.unity3d.com/ScriptReference/Texture2D.Resize.html)
5. ` texture2D.ReadPixels()` reads the pixel values from the temporary [RenderTexture](https://docs.unity3d.com/ScriptReference/RenderTexture.html) onto the resized texture [more info](https://docs.unity3d.com/ScriptReference/Texture2D.ReadPixels.html)
6. ` texture2D.Apply()`  actually upload the changed pixels to the graphics card [more info](https://docs.unity3d.com/ScriptReference/Texture2D.Apply.html)
