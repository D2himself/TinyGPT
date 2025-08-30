# 🌍 Achebe Transformer: Teaching AI to Write Like Chinua Achebe

[![Python](https://img.shields.io/badge/Python-3.12%2B-blue)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-red)](https://pytorch.org/)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)

> "A man who does not know where the rain began to beat him cannot say where he dried his body." — Chinua Achebe

A character-level transformer trained from scratch on the complete works of Chinua Achebe, one of Africa's most celebrated authors. This project demystifies transformer architecture while exploring whether AI can capture the voice of African literature.

## 🎯 Why This Project Matters

1. **Educational**: Understand transformers by building one from scratch — no black boxes
2. **Cultural**: Preserve and explore African literary voices through AI
3. **Technical**: Learn why small, focused models can outperform larger, generic ones
4. **Practical**: Debugging and reasoning about transformer behavior becomes possible when you built it yourself



## 📊 Results

After training for ~10000 iterations on a single GPU:

| Metric | Value |
|--------|-------|
| Final Loss | 1.1598 |
| Parameters | 14.4M |
| Training Time | ~3 hours (T4 GPU) |
| Context Length | 512 characters |
| Vocabulary Size | 111 (unique characters) |

### Sample Generation

**Input Prompt**: "Biafra"

**Generated Text**:
* ```Ezeulu walked him at home detail home that war of the editorial gified Ikemefuna programming to this dead of British the commercial principal; na dismissed roading providence heard the position missed with the 1966. ```
  * This sentence is notable for its use of the character names **Ezeulu** (*Arrow of God*) and **Ikemefuna** (*Things Fall Apart*).

* ```In Umuachala had sent really to dispute the P-Importance was an engineal.```
  *  The village name **Umuachala** is a fictional setting from *Arrow of God*.

* ```Many of these people of their sister, who among the Biafrans had attempted meas to take out officers with it reasons the brethdibigue of Biafras and all overwhelment of the Nigerians local fastors of African action, of certainly the Biafran purely undertly unpapeared by suffering molligivene.```
  *  This output directly references the **Biafran** and **Nigerian** conflict, a key historical event that deeply influenced Achebe's later works and political commentary.

* ```the British Ahmaduka, no one of the drivers of many friendship senset out of these three morals and consequences by my hamsical chuncrits.```
  *  This sentence touches on themes of the **British** influence and the "morals and consequences" of cultural collision, a central idea in Achebe's writing.



## 🏗️ Architecture

```
Character Input
    ↓
Embedding (384 dims)
    ↓
Positional Encoding
    ↓
6x Transformer Blocks:
  - Multi-Head Attention (8 heads)
  - Layer Norm
  - Feed Forward (4x expansion)
  - Layer Norm
  - Dropout (0.2)
    ↓
Final Layer Norm
    ↓
Output Projection
    ↓
Next Character Prediction
```

### Key Design Choices

- **Character-level tokenization**: With only 2M training characters, subword tokenization was too sparse
- **512 context length**: Captures Achebe's flowing, proverb-rich narrative style
- **8 layers, 8 heads**: Optimal depth for this data size without overfitting
- **Dropout 0.1**: Critical for generalization with limited data


## 📚 Dataset

The model is trained on seven Chinua Achebe novels:
- *Things Fall Apart* (1958)
- *No Longer at Ease* (1960)  
- *Arrow of God* (1964)
- *A Man of the People* (1966)
- *Anthills of the Savannah* (1987)
- *There was a country a personal history of biafra* (2012)
- *Achebe stories* (1991)

Total: ~2.1M characters of Nigerian literature spanning pre-colonial to post-independence narratives.


### Hyperparameter Tuning

```yaml
model:
  n_embd: 384       # Embedding dimension
  n_head: 8        # Number of attention heads
  n_layer: 8        # Number of transformer blocks
  dropout: 0.1      # Dropout probability
  
training:
  batch_size: 32
  block_size: 512   # Context length
  learning_rate: 3e-4
  warmup_iters: 1000
  max_iters: 10000
```

## 🎓 Learning Resources

This project was built using insights from:

1. **[Andrej Karpathy's "Let's build GPT"](https://www.youtube.com/watch?v=kCc8FmEb1nY&list=PPSV)** — The foundational tutorial
2. **[Attention Is All You Need](https://arxiv.org/abs/1706.03762)** — Original transformer paper
3. **[Jay Alammar's Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)** — Visual understanding
4. **[The Transformer Family Version 2.0](https://lilianweng.github.io/posts/2023-01-27-the-transformer-family-v2/)** — Comprehensive survey

## 🤝 Contributing

Contributions are welcome! Especially interested in:

- Training on other African languages/literature
- Optimizing for smaller model sizes
- Adding reasoning capabilities
- Creating a web demo
- Documentation improvements


## 🐛 Known Issues

- Generation sometimes switches between past/present tense
- Igbo names occasionally get phonetically corrupted
- Memory usage spikes with batch_size > 64 on consumer GPUs

## 🗺️ Roadmap

- [ ] Web interface for interactive generation
- [ ] Fine-tuning on specific Achebe novels
- [ ] Swahili literature version
- [ ] Reasoning capability injection
- [ ] Distillation to even smaller models
- [ ] ONNX export for deployment


## 🙏 Acknowledgments

- Chinua Achebe's estate for preserving his literary works
- The PyTorch team for the incredible framework
- Andrej Karpathy for democratizing transformer knowledge
- The African AI community for inspiration and support



## 💬 Contact

- **Discussions**: [LinkedIn](https://www.linkedin.com/in/omokemi-ayodimeji/)
- **Medium**: [Medium](https://medium.com/@omokemiayodimeji/building-a-tiny-transformer-from-scratch-learning-from-achebe-c8075b4958fa)

---

*"Until the lions have their own historians, the history of the hunt will always glorify the hunter."* — Chinua Achebe

**Let's teach the lions to write.** 🦁✍️
