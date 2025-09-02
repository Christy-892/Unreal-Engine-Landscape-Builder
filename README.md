# Unreal Engine Landscape Generator
This tool enables procedural landscape creation within UE5, offering a flexible workflow that accommodates both rapid prototyping and advanced customization. Designed with scalability in mind, it supports streamlined setup for quick iterations as well as deeper parameter control for experienced users seeking precision.  
The concept was inspired by the Landscape Creation process on Project Pegasus (https://www.sidefx.com/tutorials/project-pegasus-landscape-creation/). Building on this foundation, the tool expands the approach into a modular pipeline tailored for varying skill levels, promoting accessibility without compromising depth.

## How To Guide
The intended use of this tool is to be used inside Unreal Engine with **Houdini Session Sync**. The idea is to use the Houdini Session to make changes and easily visualize any alterations made to the heightfield. Once ready, the user can then export into Unreal Engine. This allows for a smooth and seamless iteration process.
1. In Unreal Engine, browse to the HDA in your **Content Browser** and RMB>Instantiate at the origin
2. Run Houdini Session Sync (Houdini Engine>Open Houdini Session Sync...)
3. On the instance, enable "Do Not Generate Outputs" and then recook the HDA to see it appear inside Houdini Session
4. In Houdini, go inside the Geometry node and then RMB>Allow Editing of Contents
5. On the tab section where the Houdini Engine SessionSync display is, select the HDA tab to display the parameters
6. Now you can edit the parameters as desired and go inside the tool to make any further changes
7. To see changes in Unreal, disable "Do Not Generate Objects" (use this toggle to control Recooks in Unreal as constantly updating landscape data is time-consuming)

Note - The layout and colouring of the nodes inside the HDA has been carefully designed and structured for an easier understanding of where and how to make necessary changes

## Features
### Exposed "Basic" parameters
Exposed basic parameters to allow the user to make quick alterations for basic shape and noise:
![image](https://github.com/user-attachments/assets/e303e554-af28-467f-8f10-00a5c545ec9e)

### Generation Method
Tool has two generation methods; "Generate Heightfield" and "Import Heightfield". This allows the user to start from scratch or import an exisiting heightmap

### Parameter Presets
Presets that alter the parameters to give user suitable settings based on heightfield size:
![image](https://github.com/user-attachments/assets/bd5aff5a-1ae3-43ce-a5d4-e17d39037aa1)

Example of python snippet:
```python
##Generate Preset##
def generatePreset():
    node = hou.pwd()
    #1000x1000
    if(node.parm("presets").eval()==0):       
        #Set parameters
        node.parm("sizex").set(1000)
        node.parm("sizey").set(1000)
        node.parm("boundaryHeight").set(15)
        node.parm("shrinkRadius").set(25)
        node.parm("blurRadius").set(100)
        node.parm("macroNoiseAmplitude").set(50)
        node.parm("macroNoiseElementSize").set(225)
        node.parm("subtleNoiseAmplitude").set(22.5)
        node.parm("subtleNoiseElementSize").set(75)
        node.parm("distortNoiseAmplitude").set(35)
        node.parm("distortNoiseElementSize").set(200)
        node.parm("computeHeightRange").pressButton()
        node.parm("overrideMinHeight").set(0)
        node.parm("overrideMaxHeight").set(100)
```

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
>[!NOTE]
> - Unreal Engine version - 5.5.2
> - Houdini version - 20.5.487
1. Download otl file
2. Import into your Unreal Engine project's Content Browser

## Further Reading
- Artstation Post - https://www.artstation.com/artwork/y42ND8
- Tutorial Inspiration: https://www.sidefx.com/tutorials/project-pegasus-landscape-creation/
- SideFX Landscape Generation Guide: https://www.sidefx.com/docs/houdini/unreal/landscape/generate.html
  
## ToDo
- [x] Proof of Concept
- [x] Feature - Custom Heightmap Import
- [x] Improvement - Preview/Generation Speed
- [x] Feature - Presets
