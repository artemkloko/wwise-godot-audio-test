# Testcase for wwise-godot-integration

### About

This is the testcase project on which [this PR](https://github.com/alessandrofama/wwise-godot-integration/pull/102) was tested and created.

The `main` branch contains `wwise-2023.1-for-godot-4.2-stable-2.0.4` from [https://github.com/alessandrofama/wwise-godot-integration/releases/tag/2.0.4-Wwise2023.1-Godot4.2](https://github.com/alessandrofama/wwise-godot-integration/releases/tag/2.0.4-Wwise2023.1-Godot4.2).

The `fixed` branch has updated version of `addons/Wwise/native/lib/macos` compiled from [https://github.com/artemkloko/wwise-godot-integration/tree/fix-geometry-transform](https://github.com/artemkloko/wwise-godot-integration/tree/fix-geometry-transform).

This repo also contains the `audio-test-wwise-project` that generated the included SoundBanks. It can be used to inspect the correctness of the spatial audio, but might need to be re-configured according to [https://github.com/alessandrofama/wwise-godot-integration/wiki/Getting-Started-(4.0)](https://github.com/alessandrofama/wwise-godot-integration/wiki/Getting-Started-(4.0)).

This project might still include some of my local paths in the settings of the Godot project or `audio-test-wwise-project`. Although it was created on macOS, it may need to be reconfigured slightly to work on other machines. Even more adjustments will likely be needed to run on a different OS.

--- 

### Testcase setup

Just a scene with 
- Pink room (AkRoom + AkGeometry) containing
    - Aura emitter (AkEvent)
    - Red wall (AkGeometry)
    - Blue wall (AkGeometry)
    - Pink portal (AkPortal) having Pink room as Front Room
- Yellow room (AkRoom + AkGeometry) containing
    - Robot emitter (AkEvent)
    - Yellow portal (AkPortal) having Yello room as Front Room
- Outside
    - Shake emitter (AkEvent)
    - Cyan wall (AkGeometry) (having an extra parent Node3D just for transform test)
    - The player (AkListener with isSpatial enabled)
        - Can be moved with WASD and rotated with the mouse after enabling capture with Esc

Some of the Ak components were setup in a very specific way, according to the source code of `wwise-2023.1-for-godot-4.2-stable-2.0.4`
- Event AkEvent and AkListener needs an Area3D child according to [https://github.com/alessandrofama/wwise-godot-integration/blob/2.0.4-Wwise2023.1-Godot4.2/addons/Wwise/native/src/scene/ak_room.cpp#L81](https://github.com/alessandrofama/wwise-godot-integration/blob/2.0.4-Wwise2023.1-Godot4.2/addons/Wwise/native/src/scene/ak_room.cpp#L81) so that AkRooms can detect their entrance / exit
- Every AkGeometry needs to be child of MeshInstance3D according to [https://github.com/alessandrofama/wwise-godot-integration/blob/2.0.4-Wwise2023.1-Godot4.2/addons/Wwise/native/src/scene/ak_geometry.cpp#L73](https://github.com/alessandrofama/wwise-godot-integration/blob/2.0.4-Wwise2023.1-Godot4.2/addons/Wwise/native/src/scene/ak_geometry.cpp#L73) so that AkGeometry's vertices, triangles and transform can be computed

| Project tree | Scene |
|---|---|
| <img src="readme-images/03-project-tree.png" height="100%" /> | <img src="readme-images/01-project-top-down.png" /><img src="readme-images/02-project-perspective.png" /> |

---

### Testcase comparison

| `wwise-2023.1-for-godot-4.2-stable-2.0.4` | `fix-geometry-transform` |
|---|---|
| ![](readme-images/11-position-1-og.png) | ![](readme-images/21-position-1-fixed.png)  |
| ![](readme-images/12-position-2-og.png) | ![](readme-images/22-position-2-fixed.png)  |
| ![](readme-images/13-position-3-og.png) | ![](readme-images/23-position-3-fixed.png)  |
| ![](readme-images/14-position-4-og.png) | ![](readme-images/24-position-4-fixed.png)  |
| ![](readme-images/15-position-5-og.png) | ![](readme-images/25-position-5-fixed.png)  |
| ![](readme-images/16-position-6-og.png) | ![](readme-images/26-position-6-fixed.png)  |
| ![](readme-images/17-position-7-og.png) | ![](readme-images/27-position-7-fixed.png)  |
