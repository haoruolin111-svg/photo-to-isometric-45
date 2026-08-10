---
name: photo-to-isometric-45
description: Generate or refine image-generation prompts that convert one or more provided photos, especially architecture or place photos, into realistic 1:1 orthographic 45-degree isometric 3D renders, either as separate images or composed onto a specified paper size. Use when the user asks to turn photos into 等轴测图, 轴测45°, 45度轴测图, isometric render, 3D模型, building model style images, 多图拼接, A4拼版, or paper layout.
---

# Photo To Isometric 45

## Use When

Use this skill when the user provides or references a photo and asks to convert it into an isometric, 45-degree axonometric, realistic 3D render, architectural model, or similar style image.

If the user explicitly asks to generate an image, use the image-generation tool and include the supplied photo paths as reference images.

## Core Prompt

For building photos, use this wording as the core prompt:

```text
将这座建筑的照片转换为等轴测图的 3D 渲染样式，比例保持 1:1，以保留拍摄建筑的显著特征，渲染样式，45度轴测图
```

Always apply these added constraints unless the user explicitly says otherwise:

- 只保留画面中的主体建筑，删除独立附加建筑、背景楼体和无关建筑。
- 主体建筑自带的底座、裙房、入口大厅、台阶、雨棚、柱廊、连廊、首层附属体量属于主体建筑的一部分，必须保留；不要把这些部分当作附加建筑删除。
- 底座必须是完整的正方形地块，不是长方形、梯形或被裁切的底板；在轴测视角中应显示为四条边完整可见、两组边分别平行、四边等长的正方形轴测底板。如果主体建筑本身不足以填满正方形底座，必须用道路、广场、草地、铺装、少量树木等环境元素补齐到正方形。
- 风格必须是真实建筑 3D 渲染，不要插画风、卡通风、手绘风、低多边形风或过度微缩玩具感。
- 视角必须是标准正交投影的 45 度轴测图，不要透视相机、广角镜头或三点透视；所有建筑竖向边线必须在画面中保持垂直且互相平行，水平边线按等轴测方向平行展开，不要出现竖线倾斜、楼体上窄下宽、消失点或收敛。
- 所有生成图片的背景必须是纯白色 `#FFFFFF`；不要灰色渐变背景、摄影棚背景、阴影背景、天空背景、透明背景或带纹理背景。建筑底座可以有自然接触阴影，但画布背景必须保持纯白。

## Prompt Template

When generating the final image description, keep the request concise and include these constraints:

```text
将参考照片中的[主体]转换为等轴测图的真实 3D 建筑渲染样式，画面比例保持 1:1，采用标准正交投影的 45 度轴测视角。不要使用透视相机、广角镜头或三点透视；所有建筑竖向边线必须在画面中保持垂直且互相平行，水平边线按等轴测方向平行展开，不要出现竖线倾斜、楼体上窄下宽、消失点或透视收敛。只保留画面中的主体建筑，删除独立附加建筑、背景楼体和无关建筑。主体建筑自带的底座、裙房、入口大厅、台阶、雨棚、柱廊、连廊、首层附属体量属于主体建筑的一部分，必须保留，不要误删。保留主体建筑最显著的外观特征，包括整体轮廓、屋顶/立面结构、底座裙房、门窗位置、主要材质、颜色关系和标志性细节。主体建筑必须放置在完整正方形地块底座上，底座四条边完整可见、两组边分别平行、四边等长，不要生成长方形、梯形或被裁切的底板；如果主体建筑无法填满正方形底座，必须用道路、广场、草地、铺装、少量树木等环境元素补齐到正方形。渲染为真实建筑 3D 效果，材质真实，光照自然，边缘清晰，画布背景必须是纯白色 #FFFFFF，不要灰色渐变、摄影棚背景、天空背景、透明背景或纹理背景，避免插画风、卡通风、手绘风、低多边形风和夸张变形，不添加原图中不存在的核心建筑结构。
```

Use `[主体] = 这座建筑` by default. If the user names a specific object, place, storefront, room, street corner, or landmark, replace `[主体]` with that subject.

## Multiple Image Mode

When the user uploads multiple images, do not silently choose an output mode. First determine whether they want:

- `单张生成`: generate one separate isometric image for each uploaded photo.
- `多图拼接`: generate each isometric result, then compose the results onto one specified paper canvas.

If the user already says `逐一`, `分别`, `每张`, or `一张一张`, use `单张生成`.

If the user says `拼接`, `拼版`, `排版`, `放到一张纸`, `A4`, `A3`, `画幅`, or `海报`, use `多图拼接`. If the paper size is missing, ask for it before composing. Default recommendation: `A4 竖版`.

When asking, use this concise question:

```text
你上传了多张图片，请选择输出方式：
1. 单张生成：每张照片各生成一张等轴测图
2. 多图拼接：先生成每张等轴测图，再拼接到指定画幅纸张上（请说明 A4/A3/自定义、横版/竖版）
```

For `多图拼接`, keep each generated isometric image square and undistorted. Place them on a pure white `#FFFFFF` paper canvas with even margins and spacing. Use a simple grid layout unless the user gives a layout:

- 2 images: 1x2 or 2x1 depending on paper orientation.
- 3 images: 1x3 for landscape, 3x1 or balanced vertical stack for portrait.
- 4 images: 2x2.
- 5-6 images: 2x3 or 3x2.

Supported paper sizes to mention: `A4`, `A3`, `A2`, `Letter`, or custom width x height. If exact print output is needed, use 300dpi dimensions, such as A4 = `2480 x 3508 px`.

## Image Settings

- Aspect ratio: `1:1`.
- View: orthographic 45-degree isometric / axonometric, not perspective.
- Geometry: vertical building edges must stay visually vertical and parallel; horizontal edges follow parallel isometric axes; no vanishing points, lens distortion, narrowing towers, or converging verticals.
- Subject: keep only the main subject building; remove separate secondary buildings, background towers, side buildings, and unrelated structures.
- Preserve as part of the subject: podium, base volume, entrance hall, stairs, canopy, colonnade, arcade, connector, and physically connected low-rise volumes.
- Base: complete square plot/base only; four visible edges, two pairs of parallel edges, equal side lengths in the axonometric footprint. Do not use rectangular, trapezoid, cropped, or partial bases. Complete empty areas with simple environment such as paving, road, plaza, lawn, small trees, or site edges.
- Style: realistic architectural 3D render, natural lighting, believable materials.
- Background: pure white `#FFFFFF` canvas only; no gray gradient, studio backdrop, sky, transparent background, or texture.
- Preservation priority: massing, silhouette, podium/base, entrance sequence, facade rhythm, roof shape, doors/windows, signs, color palette, material cues.
- Avoid: illustration style, cartoon style, hand-drawn style, low-poly style, toy-like miniature exaggeration.
- Simplification allowed: remove small clutter, people, cars, wires, background noise, and non-subject buildings unless the user asks to keep them.

## Workflow

1. Check whether the user supplied one or more reference images.
2. If multiple images are supplied, follow `Multiple Image Mode` before generating.
3. Identify the main subject building in each photo. If a photo contains multiple comparable buildings and the user did not specify which one is the subject, ask for clarification.
4. Separate independent background/side buildings from the subject building's own parts. When unsure whether a lower volume is a separate building or a podium/base of the subject, preserve it.
5. If an image is available and the user asks for an output image, call image generation with the reference image paths.
6. If the user selected `多图拼接`, generate the individual square isometric results first, then compose them onto the requested paper canvas.
7. If no image is available, ask the user to provide the photo instead of inventing the building.
8. If the user only asks for a prompt, return the prompt text without generating an image.
9. Preserve user constraints only when they do not conflict with the default requirements: subject-only building, square base, realistic 3D style.
10. After generation, visually inspect the result. If the base is not a complete square, if vertical building lines are tilted/converging, or if the view reads as perspective rather than orthographic 45-degree axonometric, regenerate with stronger wording instead of accepting the result.

## Quality Checklist

Before generating or returning the prompt, verify:

- It says `1:1`.
- It says `正交投影`, `45 度轴测`, and no perspective camera.
- It explicitly requires vertical edges to stay vertical and parallel.
- It asks to keep only the main subject building and remove separate other buildings.
- It explicitly preserves the subject building's podium/base, entrance, stairs, canopy, colonnade, and physically connected low-rise parts.
- It requires a complete square base with four visible equal-length edges, not a rectangle, trapezoid, cropped base, or partial base.
- It says to regenerate/reject outputs where the base is not square, verticals are not vertical, or the view is perspective.
- It requires realistic 3D architectural rendering, not illustration style.
- It requires a pure white `#FFFFFF` background for every generated image.
- It asks to preserve recognizable features from the subject building in the photo.
- For multiple uploaded images, it confirms `单张生成` or `多图拼接` unless the user already made the mode clear.
- For `多图拼接`, it includes paper size, orientation, margins, spacing, and square undistorted image placement.
- It avoids changing the building identity.
- It does not request added architectural elements unless the user explicitly asks.

## Examples

User: `把这张楼的照片转成45度轴测模型`

Use:

```text
将这座建筑的照片转换为等轴测图的真实 3D 建筑渲染样式，比例保持 1:1，以保留拍摄建筑的显著特征，渲染样式，正交投影的45度轴测图。不要使用透视相机、广角镜头或三点透视；所有竖向边线必须保持垂直且互相平行，不要出现竖线倾斜或透视收敛。只保留主体建筑，删除独立附加建筑、背景楼体和无关建筑。主体建筑自带的底座、裙房、入口大厅、台阶、雨棚、柱廊、连廊、首层附属体量必须保留。主体建筑放置在正方形底座上，可以用道路、广场、草地、铺装和少量树木补齐底座。保留建筑的整体轮廓、底座裙房、立面开窗、屋顶形态、材质颜色和标志性细节，真实材质，自然光照，画布背景必须是纯白色 #FFFFFF，避免插画风、卡通风和手绘风。
```

User: `生成一个小红书风格的店铺轴测图`

Use:

```text
将参考照片中的店铺主体转换为等轴测图的真实 3D 建筑渲染样式，画面比例保持 1:1，采用正交投影的 45 度轴测视角。不要使用透视相机、广角镜头或三点透视；所有竖向边线必须保持垂直且互相平行，不要出现竖线倾斜或透视收敛。只保留店铺主体，删除相邻独立店铺、背景建筑和无关结构。店铺自带的门头、入口台阶、雨棚、外摆平台、首层附属体量必须保留。店铺放置在正方形底座上，可以用人行道、铺装、少量绿植和街道边界补齐底座。保留招牌、门头、橱窗、外立面颜色和装饰元素，真实材质，自然光照，画布背景必须是纯白色 #FFFFFF，避免插画风、卡通风和手绘风。
```
