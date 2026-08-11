# photo-to-isometric-45

Cursor Skill for converting architecture or place photos into realistic orthographic 45-degree isometric renders.

## What It Does

- Converts one or more reference photos into 1:1 isometric building renders.
- Keeps only the main subject building and removes unrelated background buildings.
- Preserves subject podiums, bases, entrances, stairs, canopies, colonnades, and connected low-rise parts.
- Requires a complete square base, standard orthographic 45-degree axonometric view, vertical parallel building lines, and pure white `#FFFFFF` background.
- Supports multiple-image workflows: generate separately or compose results onto a paper canvas such as A4.

## Installation

Copy this folder into your Cursor personal skills directory:

```text
~/.cursor/skills/photo-to-isometric-45/
```

The folder must contain `SKILL.md`.

## Example Prompts

```text
照片转等轴测图（多图会提问是否需要拼接）
```

```text
生成轴测，拼接到 A4 竖版
```

```text
逐一照片转等轴测图
```

## Notes

This skill is intended for image-generation workflows where the user supplies reference photos. It emphasizes orthographic geometry, complete square bases, and realistic architectural rendering rather than illustration style.
