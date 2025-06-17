## Steps

0. Add character files to a folder and caption these images

```sh
/Users/victorcosta/Desktop/Ai/zLoRA/Turner
rename_all "yumoto_hakone"
caption_all "yumoto_hakone"
```

> [!NOTE]
> It will create the text captioning files (`.txt` files) and insert the metadata of them inside the associated pictures (`webp`, `jpg`, `jpeg`, `png`).
> The `caption_all` parameter will be used to insert the preffix on these files (the concept the AI is trying to learn)


1. Run `Kohya_ss`

```sh
j kohya
./setup.sh
./gui.sh
```

# 🚨 SELECT `LoRA` TAB 🚨
It will start with the wrong tab → `Dreambooth` 👎

2. LoRA → **Model**

Choose the model we are going to train the LoRA on.

2.1. `Pretrained model name or path` ↴

```sh
/Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/models/ponyDiffusionV6XL_v6StartWithThisOne.safetensors
/Users/victorcosta/Desktop/repositories/AI-generation/kohya_ss/models/hemorrhoids_v10.safetensors
```

2.2. `SDXL` → ✅

2.3. **Trained Model output name**: Which name should we call this LoRA? (e.g. **yumoto_hakone**)


3. LoRA → **Dataset Preparation**

3.1. **Instance Prompt**: The Instance Prompt ties your training images to the specific concept of "Takeru Higa"
```rb
yumoto_hakone, glasses, black-framed eyewear, black hair, brown hair, spiked hair, short hair, thick eyebrows, suit, formal, necktie, adjusting eyewear
````

3.2. **Class Prompt**: The Class Prompt isn’t actually used in LoRA (it’s a Dreambooth thing) but filling it won’t hurt. You can safely ignore it in LoRA. It tells the model what broad category your character belongs to, helping it differentiate your character from generic characters.

```rb
1boy, man, male focus, male, solo
```

3.3. **Training images** (directory containing the training images):

```rb
/Users/victorcosta/Desktop/Ai/zLoRA/Turner
```

3.4. **Repeats**: `7` (Represent the times AI will cycle though our dataset for each epoch)
> [!TIP]
> - **Check recommended configurations for LoRA training**
> https://gist.github.com/Victorcorcos/ab946d10f424e2e1b99e066c3f347027

3.5. **Destination training directory** (where formatted training and regularisation folders will be placed)

* Create and choose the folder:

```rb
/Users/victorcosta/Desktop/Ai/zLoRA/Yuya_Kazami_Train
```

* Click on **`Prepare training data`**
This will make the folders necessary to train the LoRA

* Click on **`Copy info to respective fields`**
Which will paste the info in `Folders`. If it miss something, put your own paths.


4. LoRA → **Parameters**

4.1. **Train batch size**: `4` (or `2` or `8`, depends mainly on what your GPU/NPU can handle) → More requires higher VRAM
> [!TIP]
> https://gist.github.com/Victorcorcos/ab946d10f424e2e1b99e066c3f347027

4.2. **Epoch**: `15` (The higher, the more AI will study the concept)
> [!TIP]
> https://gist.github.com/Victorcorcos/ab946d10f424e2e1b99e066c3f347027

4.3. **Max train epoch**: `15` (To avoid stopping with fewer epochs)

4.4. **Save every N epochs**: `1` (LoRAs generated per epoch)

4.5. **Caption file extension**: `.txt` (You generated `.txt` files previously)

4.6. **Learning rate**, **Unet learning rate**: `0,000025` (Controls how much the visual features of your training data (e.g., Takeru's appearance, color, and style) influence the generation process)

> [!TIP]
> **Unet learning rate**
>
> Higher → `0,0001` → AI focus on the details 🔍
>
> Lower → `0,00001` → AI focus on the big picture 🖼️
>
> (*Lower Learning Rate requires more steps*)

4.7. **Text Encoder learning rate**: `0,000025` (Controls how much the textual prompt's relationship to the visual features is adjusted during training)

> [!TIP]
> **Text Encoder learning rate**
>
> Higher → `0,00005` → More rigid on prompt association 🪨
>
> Lower → `0,00001` → More flexible on prompt association 💃

4.8. **LR Scheduler**: `constant` (This is the way AI learning rates will vary over time)

> [!TIP]
> If you feel your model overtrained, use `cosine`.

4.9. **Optimizer**: **`AdamW`** (`AdamW8bit`  only works with NVIDIA GPUs)

4.10. **LR warmup (% of total steps)**: `5%` ⚠️ If available ⚠️

4.11. **Resolution**: `512,512` / `768,768`

> [!TIP]
> * `512,512`
>
> ✔️ Faster training. Less VRAM use. Recommended for begginers and testing.
>
> ❌ Less quality (good enough tho), Harder to capture details.
>
> * `768,768` (or higher)
>
> ✔️ Higher Quality LoRA. Better details. Less likely to overtrain.
>
> ❌ A lot more time. Way more VRAM use.
>

4.12. **Enable buckets**: `✅` (Allows images with different resolutions in the datase. Otherwise they will be cropped at the center or random if you enabled the option `Random crop instead of center crop`)

4.13. **Network Rank (Dimension)**: `16` (`32`for higher fidelity, `8` if overfitting)
> [!TIP]
> https://gist.github.com/Victorcorcos/ab946d10f424e2e1b99e066c3f347027

4.14. **Network Alpha**: `8` (*Network Rank (Dimension) / 2*)
> [!TIP]
> https://gist.github.com/Victorcorcos/ab946d10f424e2e1b99e066c3f347027

- **Advanced**

4.15. **Clip skip**: `2` (`1` for realistic / `2` for anime-like)

4.16. **Shuffle caption**: `✅`

4.17. **Keep n tokens**: `4` (Leave it to `0` if you want to teach multiple keywords)

> [!IMPORTANT]
> Remember that some of these tokens are keywords though, for example: `takeru_higa, takeru higa, takeru, higa`
> **So you place `Keep n tokens` = `4` on this example** to skip the 4 first tokens.

4.18. **CrossAttention**: `sdpa` (`sdpa` or `xformers` keeps the generation faster and saves a lot of VRAM)

> [!IMPORTANT]
> Since you're using a MacBook Pro with an M3 chip, `xformers` is not compatible because it was designed for NVIDIA GPUs. Instead, you need to explicitly disable `xformers` in Kohya_ss.

4.19. **Enable horizontal flip augmentation**: `✅` Flip augmentation (To increase dataset variety)


5. LoRA → **Accelerate launch**

5.1. **Mixed precision**: **`no`** (`fp16` and etc only works with NVIDIA GPUs)

5.2. **Start Training**


6. LoRA → **Start Training**


7. Results

Let's test the generated LoRAs!

7.1. Go to Stable Diffusion WebUI (Forge)

+ Prompt
```rb
score_9, score_8_up, score_7_up, score_6_up, score_5_up, score_4_up, year2023, uncensored, game cg, official art, official style, anime screencap, 1boy, male focus, solo focus, INSERT_HERE_YOUR_LORA, slim athlete, twink, completely nude, testicles, male focus, precum, penis, veiny penis, uncensored, pubic hair, male pubic hair, foreskin, solo, nipples, cloud, sky, abs, outdoors, erection, looking at viewer, precum drip, smile, crotch, blush, from below, teeth, phimosis, thighs, cloudy sky, thick thighs, grin, <lora:Expressive_H:1> expressiveh, best quality, amazing quality, best aesthetic, absurdres, <lora:pony_good_hands:1> good_hands <lora:Detailer_NoobAI_Incrs_v1:1.0> detailed <lora:TCV_illusXL_Incrs_v2:0.3> anime
```
```rb
score_9, score_8_up, score_7_up, score_6_up, score_5_up, score_4_up, year2023, uncensored, game cg, official art, official style, anime screencap, 1boy, male focus, solo focus, INSERT_HERE_YOUR_LORA, slim athlete, twink, testicles, male focus, precum, penis, uncensored, pubic hair, male pubic hair, <lora:Foreskin_pony:0.5> uncircumcised, foreskin, foreskin, veiny penis, solo, nipples, cloud, sky, abs, outdoors, erection, looking at viewer, precum drip, smile, crotch, blush, from below, teeth, phimosis, thighs, cloudy sky, thick thighs, grin, <lora:Expressive_H:1> expressiveh, best quality, amazing quality, best aesthetic, absurdres, <lora:pony_good_hands:1> good_hands <lora:Detailer_NoobAI_Incrs_v1:1.0> detailed <lora:TCV_illusXL_Incrs_v2:0.3> anime
```
⤷ INSERT_HERE_YOUR_LORA = <lora:yumoto_hakone-000001:1> yumoto_hakone, male focus, 1boy, blonde hair, solo, anime coloring, red eyes, brown eyes, official style

- Prompt
```rb
1girl, feminine, pantyhose, female, girl, woman, breast, breasts, boobs, tits, lowres, bad, bad anatomy, bad proportions, bad perspective, text, error, missing, extra, fewer, cropped, jpeg artifacts, worst quality, bad quality, watermark, bad aesthetic, unfinished, chromatic aberration, scan, scan artifacts, twisted neck, twisted waist, twisted pelvis, intertwined limbs, intertwined fingers, missing limb, extra limb, extra legs, extra arms, extra hands, extra fingers, mutant limb, mutant arms, censored, POV, artist name, copyright name, crossed arms, crossed legs, severed limb, disembodied limb, crossed ankles, same face, twins, closed eyes, x-ray
```
```rb
muscles, toned body, defined anatomy, hyperrealism, sharp details, humanoid features, rough textures, bodybuilder, sinewy, wrinkles, shadows emphasizing muscle tone
```

7.2. Script → X/Y/Z plot

* `X type` → `Prompt S/R` → `yumoto_hakone-000001,yumoto_hakone-000002,yumoto_hakone-000003,yumoto_hakone-000004,yumoto_hakone-000005,yumoto_hakone-000006,yumoto_hakone-000007,yumoto_hakone-000008,yumoto_hakone-000009,yumoto_hakone-000010,yumoto_hakone-000011,yumoto_hakone-000012,yumoto_hakone-000013,yumoto_hakone-000014,yumoto_hakone-000015,yumoto_hakone`


> [!TIP]
> A code in ruby that will generate the `X type` above.

```rb
# loras('yumoto_hakone', 15)
def loras(name, quantity)
  (1..quantity).map { |number| "#{name}-#{number.to_s.rjust(6, '0')}" }.join(',') + ",#{name}"
end
```


## References

1. https://www.youtube.com/watch?v=xXNr9mrdV7s
 