# Unreal Engine Landscape Builder (Proof of Concept)
This tool is inspired by the Landscape Creation process on Project Pegasus (https://www.sidefx.com/tutorials/project-pegasus-landscape-creation/). I wanted to take this concept further and build a tool/pipeline that is readable and adaptable for general users and could be used for various pipelines. This tool is to be used for initial Landscape Generation inside of Unreal Engine
## How To Guide
Intention of this tool, is to be used with Houdini Session Sync inside Unreal Engine. HDA layout/design has been setup to be user-friendly
## Features
### Exposed "Basic" parameters
Exposed basic parameters to allow the use to quick display Landscape with/without various features:
![image](https://github.com/user-attachments/assets/41770dc5-3d7c-430e-a3f1-565e8b83ea04)



### Reset all Simulations
Button callback script to trigger all simulations of HeightField Erode nodes:
```python
#Search all nodes for heightfield erode nodes and trigger "resimulate"
def triggerAllSims():
    for node in hou.node('/').allSubChildren():
        if node.type().name() == "heightfield_erode::2.0":
            node.parm("resimulate").pressButton()

```
## Setup
1. Download otl
2. Import into Unreal Engine Contents
3. Run Houdini Session Sync (Houdini Engine>Open Houdini Session Sync...)
## Further Reading
- Tutorial Inspiration: https://www.sidefx.com/tutorials/project-pegasus-landscape-creation/
- SideFX Landscape Generation Guide: https://www.sidefx.com/docs/houdini/unreal/landscape/generate.html
## ToDo
- [x] Proof of Concept
- [ ] Feature - Custom Heightmap Import
- [ ] Improvement - Preview/Generation Speed
