# temporal-accumulation-shader-demo-bedrock
A tech demo of temporal accumulation for Minecraft: Bedrock Edition shaders
## General
This demo is a visualizer of chaos equations based on [this video](https://youtu.be/fDSIRXmnVvk "this video") that uses temporal accumulation to achieve trailing effect.
## Usage
Run `/particle demo:accumulation` command.
## How it works
Flipbook textures that are part of the terrain atlas are redrawn in the beginning of each frame, using `texture_blend.fragment` & `uv_blend_flipbook.vertex` shaders. The important part is that they're redrawn over their older versions on the same texture, which means we can use `GL_EXT_shader_framebuffer_fetch` in the fragment shader to sample fragment color from the previous frame - and that's the core principle behind this demo. Unfortunately, this method is highly limited, since we can't have any other inputs except time when the terrain atlas is getting re-drawn, which means applications of this tech are limited only to procedural textures or static/hardcoded path tracing.
