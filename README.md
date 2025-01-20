# LuminaBrush

**Work in Progress (WIP): this page may be updated a lot recently.**

LuminaBrush is a project to build an interactive tool to draw illumination effects on images.

The framework is a two-stage method: one stage to convert an image to a "uniformly-lit" appearance, and another stage to generate the illumination effect with user scribbles.

# Demos

LuminaBrush is currently based on Flux.

HF Demo: https://huggingface.co/spaces/lllyasviel/LuminaBrush

Examples with seed 12345:

![image](https://github.com/user-attachments/assets/6c3cf816-4528-4ae0-8aba-dc0c50db0379)

![image](https://github.com/user-attachments/assets/0f642d13-2ecb-4b3f-8a23-cd9a4ff0e906)

![image](https://github.com/user-attachments/assets/e4f56516-f680-4cf0-b9d4-81f0644090da)

![image](https://github.com/user-attachments/assets/d5ed7f84-ee21-4e26-9b47-c3ec9642404f)

![image](https://github.com/user-attachments/assets/f127422a-8593-41a0-adda-3af271862af6)

(the above examples can be reproduced by clicking the HF demo page's examples)

(the HF demo page may have more examples)

# Framework

![image](https://github.com/user-attachments/assets/62511eb3-a785-4519-bc0c-054f9b277bca)

LuminaBrush is a two-stage framework. The first stage (on the left) convert images to "uniformly-lit" appearances (eg., those lit by uniformly distributed white ambient light sources); the second stage (on the right) generate illumination effects for those "uniformly-lit" appearances, guided by user scribbles.

Decomposing the illumination drawing problem into two stages makes the learning easier and more straightforward - otherwise (eg., if only use one stage) one may need to consider external constraints/regulations (like light transport consistency, etc) to stabilize model behaviors. 

We begin with collecting a relatively small set of images with relatively uniformly-lit appearances - for example like these:

![image](https://github.com/user-attachments/assets/67d056de-4076-417e-a0a9-cd0cce96bef7)

(and then we also expand this set with generated images from a Flux LoRA trained on this set)

Using these "uniformly-lit" images as an intermediate representation has some advantages, like avoiding overly sharp mesh boundaries or overly flat surfaces from 3D albedo. And those images are somewhat detailed enough to handle skin texture details, hair, fur, etc..

We then synthesize random normals to relight those "uniformly-lit" images randomly to train a model that can extract "uniformly-lit" appearances from any input images. 

After that, we extract "uniformly-lit" appearances from millions of high-quality in-the-wild images, to build paired data to train the final interactive illumination drawing model.

One obvious side-product of this method is an application to use the "uniformly-lit stage" independently to somewhat "delight" images - we also built an HF space for people who want to play with it:

https://huggingface.co/spaces/lllyasviel/lumina_brush_uniform_lit

![image](https://github.com/user-attachments/assets/f2bca6ae-5abe-4b5a-a9c0-cb6384c219b6)

![image](https://github.com/user-attachments/assets/ec29c0ec-5777-4c29-b60b-d194e6351f76)

![image](https://github.com/user-attachments/assets/3749e76b-7762-42ba-9589-d7335d6109c2)

![image](https://github.com/user-attachments/assets/8b29f3aa-dd64-4c2a-8917-3f8115b1d541)

![image](https://github.com/user-attachments/assets/fda5cfad-ea0a-43e5-ac5c-141bd45dd70f)

(the HF demo has more examples)

# bib

    @Misc{luminabrush2024,
      author = {LuminaBrush Team},
      title  = {LuminaBrush:. Illumination Drawing Tools for Text-to-Image Diffusion Models},
      year   = {2024},
    }

# Work in progress

more info will be added later ...
