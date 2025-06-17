# 🍑🔥 Ultimate LoRA Training Guide with NSFW Body Shader (Eros Noir Workflow)

1. 🏗️ Setup Folder structure:
```
/Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/
├── 5_charactername_character → Face, hair, identity (with repeat 5x)
└── 1_charactername_nsfw      → Body shader, poses, penis, butt (with repeat 1x)
```

2. Add training data
```bash
# For the character images:
cd /Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/5_charactername_character
rename_all "YOUR_CHARACTER_NAME"
caption_all "YOUR_CHARACTER_NAME"

# For the NSFW body shader images (generic, no character name):
cd /Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/1_charactername_nsfw
rename_all "nsfw"
caption_all
```

3. Update `ultimate_lora.toml` file
```sh
/Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/configs/train/ultimate_lora.toml
```

4. Run `kohya_ss` terminal version
```sh
accelerate launch ./sd-scripts/sdxl_train_network.py --config_file /Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/configs/train/ultimate_lora.toml
```

* In case epochs are overrided
```sh
accelerate launch ./sd-scripts/sdxl_train_network.py \
   --config_file /Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/configs/train/ultimate_lora.toml \
   --max_train_epochs=1 \
   --save_every_n_epochs=1
````
