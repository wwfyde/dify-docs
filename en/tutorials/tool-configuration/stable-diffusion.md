# Stable Diffusion
Stable Diffusion is a tool for generating images based on text prompts, MoLook has implemented the interface to access the Stable Diffusion WebUI API, so you can use it directly in MoLook. followings are steps to integrate Stable Diffusion in MoLook.

## 1. Make sure you have a machine with a GPU
Stable Diffusion requires a machine with a GPU to generate images. but it's not necessary, you can just use CPU to generate images, but it will be slow.

## 2. Launch Stable Diffusion WebUI
Launch the Stable Diffusion WebUI on your local machine or server.

### 2.1. Clone the Stable Diffusion WebUI repository
Clone the Stable Diffusion WebUI repository from the [official repository](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
    
```bash
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
```

### 2.2. Launch it locally
After cloning the repository, you should change directory to the cloned repository and run the following command to launch the Stable Diffusion WebUI.

#### Windows
```bash
cd stable-diffusion-webui
./webui.bat --api --listen
```

#### Linux
```bash
cd stable-diffusion-webui
./webui.sh --api --listen
```

### 2.3. Prepare Models
Now you can access the Stable Diffusion WebUI on your browser according to the address shown in the terminal, but the models are not available yet. You need to download the models HuggingFace or other sources and put them in the `models` directory of the Stable Diffusion WebUI.

For example, we use [pastel-mix](https://huggingface.co/JamesFlare/pastel-mix) as the model, use `git lfs` to download the model and put it in the `models` directory in `stable-diffusion-webui`.

```bash
git clone https://huggingface.co/JamesFlare/pastel-mix
```

### 2.4 Get Model Name
Now you can see `pastel-mix` in the model list, but we still need to get the model name, visit `http://your_id:port/sdapi/v1/sd-models`, you will see the model name like below.

```json
[
    {
        "title": "pastel-mix/pastelmix-better-vae-fp32.ckpt [943a810f75]",
        "model_name": "pastel-mix_pastelmix-better-vae-fp32",
        "hash": "943a810f75",
        "sha256": "943a810f7538b32f9d81dc5adea3792c07219964c8a8734565931fcec90d762d",
        "filename": "/home/takatost/stable-diffusion-webui/models/Stable-diffusion/pastel-mix/pastelmix-better-vae-fp32.ckpt",
        "config": null
    },
]
```

The `model_name` is what we need, in this case, it's `pastel-mix_pastelmix-better-vae-fp32`.

## 3. Integrate Stable Diffusion in MoLook
Fill in the Authentication and Model Configuration in `Tools > StableDiffusion > To Authorize` with the information you get from the previous steps.

## 4. Finish
Just try use it in MoLook!

