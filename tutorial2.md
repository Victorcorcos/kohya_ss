# 🍑🔥 Ultimate LoRA Training Guide with NSFW Body Shader (Eros Noir Workflow)

## 🚶 Steps

---

### 0. 📂 Dataset Preparation (Character + NSFW Body Shader)

1. 🏗️ Setup Folder structure:
```
/Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/
├── 5_charactername_character → Face, hair, identity (with repeat 5x)
└── 1_charactername_nsfw      → Body shader, poses, penis, butt (with repeat 1x)
```
```bash
# For the character images:
cd /Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/character_5
rename_all "YOUR_CHARACTER_NAME"
caption_all "YOUR_CHARACTER_NAME"

# For the NSFW body shader images (generic, no character name):
cd /Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/nsfw_1
rename_all "nsfw"
caption_all
```

---

### 1. 🏁 Run Kohya_ss

```bash
j kohya
./setup.sh
./gui.sh
```

→ Open the GUI in the browser:
**127.0.0.1:7860**

→ ⚠️ Switch to the `LoRA` tab. (It starts in Dreambooth by default.)

---

### 2. 🔄 Load Full Training Configuration

- At the very top in **Configuration → Load Config File**, click 📂 Load File.
- Select your config file:

```bash
/Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/configs/train/ultimate_lora.json
# Change values with your new character
```

✔️ This loads:
- Pretrained model path (e.g., Hemorrhoids)
- Dataset folder
- Output folder
- Network Dim/Alpha
- Learning rate, batch size, scheduler, optimizer, epochs
- Precision, clip skip, SDPA, etc.

---

### 3. 🔧 Manual Check (Mandatory)

#### 🏗️ Check Dataset Folder Structure:
- ✔️ Should be:
```
character_5
nsfw_1
```
→ Kohya auto-detects repeats from folder names.

#### ℹ️ (Optional) Instance Prompt & Class Prompt:
→ Located in **Dataset Preparation.**
→ These are cosmetic, do not affect LoRA training.

|   Instance Prompt   |   Class Prompt   |
|---------------------|------------------|
| your_character_name | 1boy, male, solo |

---

### 4. 🔥 Final Parameters Checklist (Auto-loaded by JSON)

| Setting             | Value                       |
|---------------------|-----------------------------|
| Pretrained Model    | hemorrhoids_v10.safetensors |
| SDXL                | ❌ (Do NOT check)           |
| Network Rank (Dim)  | 64                          |
| Network Alpha       | 32                          |
| Learning Rate       | 0.0001                      |
| Scheduler           | Cosine                      |
| Epochs              | 10                          |
| Batch Size          | 4                           |
| Clip Skip           | 2 (Anime Style)             |
| Precision           | bf16 (Apple Silicon)        |
| Enable Buckets      | ✅                          |
| Keep N Tokens       | 0                           |
| Optimizer           | AdamW                       |
| Cross Attention     | sdpa (for Mac)              |
| Xformers            | ❌ (NVIDIA only)            |

---

### 5. 🚀 Start Training

- Hit **Start Training.**
- Check the logs to confirm:
→ **character_5** is repeating correctly.
→ **nsfw_1** is loaded for body, penis, muscles, butt, shading, and sex poses.

---

## 🧪 Prompt Example for Testing LoRA

* ➕ Prompt
```rb
score_9, score_8_up, score_7_up, score_6_up, score_5_up, score_4_up, year2023, uncensored, game cg, official art, official style, anime screencap, 1boy, male focus, solo focus, INSERT_HERE_YOUR_LORA, slim athlete, twink, completely nude, testicles, male focus, precum, penis, veiny penis, uncensored, pubic hair, male pubic hair, foreskin, solo, nipples, cloud, sky, abs, outdoors, erection, looking at viewer, precum drip, smile, crotch, blush, from below, teeth, phimosis, thighs, cloudy sky, thick thighs, grin, <lora:Expressive_H:1> expressiveh, best quality, amazing quality, best aesthetic, absurdres, <lora:pony_good_hands:1> good_hands <lora:Detailer_NoobAI_Incrs_v1:1.0> detailed <lora:TCV_illusXL_Incrs_v2:0.3> anime
```

⤷ INSERT_HERE_YOUR_LORA = <lora:yumoto_hakone-000001:1> yumoto_hakone, male focus, 1boy, blonde hair, solo, anime coloring, red eyes, brown eyes, official style

* ➖ Prompt
```rb
1girl, feminine, pantyhose, female, girl, woman, breast, breasts, boobs, tits, lowres, bad, bad anatomy, bad proportions, bad perspective, text, error, missing, extra, fewer, cropped, jpeg artifacts, worst quality, bad quality, watermark, bad aesthetic, unfinished, chromatic aberration, scan, scan artifacts, twisted neck, twisted waist, twisted pelvis, intertwined limbs, intertwined fingers, missing limb, extra limb, extra legs, extra arms, extra hands, extra fingers, mutant limb, mutant arms, censored, POV, artist name, copyright name, crossed arms, crossed legs, severed limb, disembodied limb, crossed ankles, same face, twins, closed eyes, x-ray
```

---

## ⚠️ Important Reminders

| Item                      | Must Do?        |
|---------------------------|-----------------|
| Folder repeats (`[5]`)    | ✅ Manually set |
| Keep N Tokens = 0         | ✅ Critical     |
| Instance/Class Prompt     | ✅ Optional     |
| SDXL Checkbox             | ❌ Never check  |
| Config File JSON          | ✅ Load at top  |

---

## 🏆 File Naming Suggestion (Standard)

- Dataset folder:
`/Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/`

- Config file:
`/Users/victorcosta/Desktop/Ai/perfect_loras/YOUR_CHARACTER_NAME/YOUR_CHARACTER_NAME_config.json`

- Model output:
`yumoto_hakone.safetensors` (example)

---
