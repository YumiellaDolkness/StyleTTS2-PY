# StyleTTS 2: The Python Package

This package makes StyleTTS2, an approach to human-level text-to-speech, accessible with an inference module that uses strictly MIT licensed libraries. See **Considerations** and **Notes** below.

## Quick Start
1. Ensure you are running Python >= 3.8
2. Ensure you have downloaded the StyleTTS2 LibriTTS checkpoint and corresponding config file. Both are available to download at https://huggingface.co/yl4579/StyleTTS2-LibriTTS.
3. Install the package using pip:
```bash
pip install styletts2
```
4. Try it out either in Python shell or in your code: 
```python
from styletts import tts

my_tts = tts.StyleTTS2(model_checkpoint_path='/PATH/TO/epochs_2nd_00020.pth', config_path='/PATH/TO/config.yml')

# optionally write to a WAV file
out = my_tts.inference("Hello there, I am now a python package.", output_wav_file="test.wav")

# specify target voice to clone
my_tts.inference("Hello there, I am now a python package.", target_voice_path="/PATH/TO/some_voice.wav", output_wav_file="another_test.wav")
```

Note: I'm not affiliated with the original authors. StyleTTS2 is a neat, open source, state-of-the-art approach to TTS. Pass your kudos and model-related questions to the authors at the model repo:

# [StyleTTS 2: Towards Human-Level Text-to-Speech through Style Diffusion and Adversarial Training with Large Speech Language Models](https://github.com/yl4579/StyleTTS2)

### Original authors: Yinghao Aaron Li, Cong Han, Vinay S. Raghavan, Gavin Mischler, Nima Mesgarani

> In this paper, we present StyleTTS 2, a text-to-speech (TTS) model that leverages style diffusion and adversarial training with large speech language models (SLMs) to achieve human-level TTS synthesis. StyleTTS 2 differs from its predecessor by modeling styles as a latent random variable through diffusion models to generate the most suitable style for the text without requiring reference speech, achieving efficient latent diffusion while benefiting from the diverse speech synthesis offered by diffusion models. Furthermore, we employ large pre-trained SLMs, such as WavLM, as discriminators with our novel differentiable duration modeling for end-to-end training, resulting in improved speech naturalness. StyleTTS 2 surpasses human recordings on the single-speaker LJSpeech dataset and matches it on the multispeaker VCTK dataset as judged by native English speakers. Moreover, when trained on the LibriTTS dataset, our model outperforms previous publicly available models for zero-shot speaker adaptation. This work achieves the first human-level TTS synthesis on both single and multispeaker datasets, showcasing the potential of style diffusion and adversarial training with large SLMs.

Paper: [https://arxiv.org/abs/2306.07691](https://arxiv.org/abs/2306.07691)

Audio samples: [https://styletts2.github.io/](https://styletts2.github.io/)

Online demo: [Hugging Face](https://huggingface.co/spaces/styletts2/styletts2) (thank [@fakerybakery](https://github.com/fakerybakery) for the wonderful online demo)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yl4579/StyleTTS2/blob/main/) [![Slack](https://img.shields.io/badge/Join%20Our%20Community-Slack-blue)](https://join.slack.com/t/styletts2/shared_invite/zt-2805io6cg-0ROMhjfW9Gd_ix_FJqjGmQ)

## Considerations
***Before using these pre-trained models, you agree to inform the listeners that the speech samples are synthesized by the pre-trained models, unless you have the permission to use the voice you synthesize. That is, you agree to only use voices whose speakers grant the permission to have their voice cloned, either directly or by license before making synthesized voices public, or you have to publicly announce that these voices are synthesized if you do not have the permission to use these voices.*** 

### Common Issues
- **High-pitched background noise**: This is caused by numerical float differences in older GPUs. For more details, please refer to issue [#13](https://github.com/yl4579/StyleTTS2/issues/13). Basically, you will need to use more modern GPUs or do inference on CPUs.
- **Pre-trained model license**: You only need to abide by the above rules if you use **the pre-trained models** and the voices are **NOT** in the training set, i.e., your reference speakers are not from any open access dataset. For more details of rules to use the pre-trained models, please see [#37](https://github.com/yl4579/StyleTTS2/issues/37).

## TODO
- [x] Inference support for LibriTTS (voice cloning) model inference
- [ ] Inference support for LJSpeech model

## Notes
- This package currently only supports (and has been tested for) inference capabilities.
- Currently using MIT-licensed [gruut](https://github.com/rhasspy/gruut) as the IPA phoneme converter. Found it to be the best alternative to phoneme converters based on [espeak](https://github.com/espeak-ng/espeak-ng)