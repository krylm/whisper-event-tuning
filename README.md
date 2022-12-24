# Whisper fine tuning event 2022 - script modification

Last setup what was used for training best fine tuned model for Whisper 
in [HuggingFace Fine tuning event 2022](https://github.com/huggingface/community-events/tree/main/whisper-fine-tuning-event).

### DeepSpeed
First modification was to get access to bigger `batch_size` without `gradient_accumulation_steps` using [DeepSpeed](https://github.com/microsoft/DeepSpeed).

To make it run inside Docker, I've used guide from [Zihao's blogpost](https://zzhou.info/2022/11/22/deepspeed_docker/).

### Concatenation of input dataset
It was idea from [Bayar](https://github.com/bayartsogt-ya/whisper-multiple-hf-datasets). 
Whisper model uses 30 second batches, but Common Voice dataset is around 3-5 seconds of audio in each sample. 
We can concatenate audio and text together to fewer samples. To learn from more dense data. 
It should run faster and learn a lot more from each sample.

### Other ideas
According to some details of training Large v2 model in [Whisper paper](https://cdn.openai.com/papers/whisper.pdf)
I have some ideas to try in next steps.

- [SpecAugment: A New Data Augmentation Method for Automatic Speech Recognition](https://ai.googleblog.com/2019/04/specaugment-new-data-augmentation.html)
- More data collected from other datasets ([google/fleurs](https://huggingface.co/datasets/google/fleurs), [common voice 12/13](https://commonvoice.mozilla.org/en/datasets)) 
and combination with [Farsipal multistreaming](https://github.com/kamfonas/whisper-fine-tuning-event/blob/minor-mods-by-farsipal/run_speech_recognition_seq2seq_streaming.py) modification. 
- [PyTorch 2.0 optimization](https://pytorch.org/get-started/pytorch-2.0/)
- Collect custom dataset to get more training data 
   - creative commons filter on YouTube and videos with subtitles.
   - download videos without subtitles, use whisper to get some and manually fix them [ASR corpus creator](https://github.com/egorsmkv/asr-corpus-creator)

### Thanks for Whisper Fine tuning event 2022
- [HuggingFace](https://huggingface.co/) crew - for event itself and all support on discord 
  - [Sanchit Gandhi](https://github.com/sanchit-gandhi), 
  - [Vaibhav Srivastav - VB](https://github.com/Vaibhavs10)
- [LabmdaLabs](https://lambdalabs.com/) - for all GPU hours (insane 20k+ !!!)
- [OpenAI](https://github.com/openai/whisper) for Whisper model