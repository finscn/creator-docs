# Dynamic Atlas

> Authors: Xunyi, youyou

## Introduction

Reducing DrawCall is a very straightforward and effective way to improve game rendering efficiency, and a very important factor in whether the two DrawCall can be combined into a DrawCall is whether the two DrawCall use the same texture.

Cocos Creator provides a static atlas packing when building a project -- **Auto Atlas**. But when the project grows bigger, the texture will become so much that it's hard to package the textures into a large texture. At this time, the static atlas packing is more difficult to meet the needs of reducing DrawCall. So Cocos Creator added the **Dynamic Atlas** feature to v2.0. It dynamically merges textures into a large texture while the project is running. When rendering to a texture, the Dynamic Atlas Manager will automatically detects if the texture has been added to the Dynamic Atlas Manager, if not, and the texture conforms to the Dynamic Atlas condition, then the texture will be merged into the large texture generated by the Dynamic Atlas Manager.

**Dynamic Atlas** is according to the rendering order to determine whether the texture is merged into a large texture. This ensures that adjacent DrawCall can be combined into a single DrawCall.

## Use details

Currently, the Dynamic Atlas Manager only supports the pack of the Sprite render component. If you want to add support for other types of render components, you can customize the rendering component yourself:

```js
cc.dynamicAtlasManager.insertSpriteFrame(spriteFrame);
```

When a Sprite Frame is added to a dynamic atlas, the texture of the Sprite Frame will be modify to **a larger image in the Dynamic Atlas Manager**. The uv in the Sprite Frame is also recalculated according to the coordinates in the large image.

**Note**: Before the scene is loaded, the Dynamic Atlas Manager will be reset, and the reference of the Sprite Frame texture and uv will be restored to their initial values.

## Texture restrictions

The Dynamic Atlas Manager limits the size of the texture that can be packed. By default, only textures with a width and height greater than **8** and less then **512** can enter the manager. Users can modify this restriction based on needs:

```js
cc.dynamicAtlasManager.minFrameSize = 8;
cc.dynamicAtlasManager.maxFrameSize = 512;
```

You can refer to the API docs [DynamicAtlasManager](../../../api/zh/classes/DynamicAtlasManager.html) for details.

## Debugging

If you want to see the effect of dynamic atlas packing, you can turn on debugging to see the resulting large texture, which will be added to a ScrollView to display.

```javascript
// Open debugging
cc.dynamicAtlasManager.showDebug(true);
// Close debugging
cc.dynamicAtlasManager.showDebug(false);
```
