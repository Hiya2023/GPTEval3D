# GPTEval3D

A human-aligned evaluation metric for Text-to-3D Generative models.
This repository contains tournament data and results from running GPTEval3D for our study to evaluate six Text-to-3D Generative models. 

## Installation

Main dependencies : OpenAI library and PyTorch
For PyTorch installation, please refer to the official website as it highly depends on the environment.
Following contains code for installation other packages:

```bash
# Install OpenAI upgraded version
pip install --upgrade openai

# Other packages
pip install --upgrade tqdm numpy Pillow gdown
```

## Structure of the repository

Text prompts are in `prompts.json` file under the tournament folders (e.g. `data/tournament-color/prompts.json`).
For each prompt, 240 rendered images (120 RGB and corresponding 120 surface normal rendering), evenly spaced views using the camera angle chosen by the [Threestudio](https://github.com/threestudio-project/threestudio) codebase.
Each render is 512x512 resolution.
These renders were provided to the GPT model. (We have used the GPT-4 onmi model)

## Compute score for a Tournament

### Step 1: Organizing Data

A set of text-to-3D generative models organised in the following structure.

```bash
<root>
    config.json
    prompts.json
    methods/
        <method-name-1>
            <prompt-id-1>
                <seed-1>
                    rgb_0.png ...
                    normal_0.png ...   
                ...
                <seed-k>
            ...
            <prompt-id-m>
        ...
        <method-name-n>
```

For more information about what should be put into `config.json` and `prompts.json`,
please see [this link](assets/data_format.md).

### Step 2: Run Evaluation

```bash
python gpt_eval_alpha.py \
    --apikey <your_openai_api_key> \
    --eval tournament \               # Evaluating new method
    -t <path-to-tournament-data> \    # folder to tournament data
    -b 2000 \                          # budget (number of requests)
    -o results/<tournament-name>      # (optional) output directory
```
### Results from tournament

For our aspect(color, shape and style)-based tournament the resulting Elo scores obtained on running GPTEval3D metric are available in the following folder structure.

```bash
results
    <tournament-name>
        scores.json
    
```
## Citation

If you find our codebase useful for your research, please cite:

```bibtex
@inproceedings{wu2023gpteval3d,
   author = {Tong Wu and Guandao Yang and Zhibing Li and Kai Zhang and
             Ziwei Liu and Leonidas Guibas and Dahua Lin and Gordon Wetzstein},
   title = {GPT-4V(ision) is a Human-Aligned Evaluator for Text-to-3D Generation},
   booktitle = {CVPR},
   year = {2024},
}
}
```
## Acknowledgement
We sincerely thank the following projects including [GPT-4V](https://chat.openai.com/), [threestudio](https://github.com/threestudio-project/threestudio), [mvdream](https://github.com/MV-Dream/MVDream), [prolificdreamer](https://github.com/thu-ml/prolificdreamer), [shap-e](https://github.com/openai/shap-e) for providing their codebases!
