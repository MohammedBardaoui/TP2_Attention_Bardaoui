# TP Attention : Image Captioning avec RNN et Attention sur ResNet

## Overview
This section describes the training, evaluation, and analysis of the Image Captioning model based on a ResNet50 visual encoder and an LSTM decoder with an attention mechanism. The objective is to evaluate the model’s ability to generate meaningful textual descriptions for images from the Flickr30k dataset.

---

## Model Training

The model is trained using paired image–caption data in a supervised learning setting.

**Architecture**
- Encoder: ResNet50 pre-trained on ImageNet (frozen weights)
- Decoder: LSTM with attention
- Word embedding layer

**Training configuration**
- Embedding dimension: 256  
- LSTM hidden dimension: 256  
- Optimizer: Adam  
- Learning rate: 0.001  
- Learning rate scheduler: StepLR (step size = 10, gamma = 0.5)  
- Batch size: 32  
- Number of epochs: 30  
- Loss function: CrossEntropyLoss (padding token ignored)

During training, both training and validation losses are monitored at each epoch. Gradient clipping is applied to prevent exploding gradients and ensure stable optimization.

---

## Convergence Analysis

The loss curves show a gradual decrease in training loss across epochs, indicating effective learning. The validation loss follows a similar trend, suggesting good generalization and no significant overfitting.

These observations confirm that the model converges properly within 30 epochs and maintains stable performance throughout training.

---

## Model Evaluation

After training, the model is evaluated on a subset of the test dataset.

### Quantitative Evaluation
- Average test loss (on 512 samples): 3.4595

This value reflects a reasonable level of performance given the size of the vocabulary and the complexity of the Flickr30k dataset.

---

### Qualitative Evaluation

Generated captions are compared with ground-truth annotations to assess semantic quality.

Example 1  
- Ground truth: a shirtless man is sitting on the ground holding fruit.  
- Generated: a man in a blue shirt is sitting on a rock.

Example 2  
- Ground truth: a man races another man in the background.  
- Generated: a man in a black shirt is walking down a street.

Example 3  
- Ground truth: 2 worker men with white helmets and orange shirts.  
- Generated: a man in a white shirt and a white shirt and a white shirt and black pants.

The results show that the model captures global scene context effectively, although some repetitions and inaccuracies remain, which are common in sequence generation models.

---

## Attention Visualization

To better understand the model’s behavior, attention weights are visualized during caption generation.

- Each generated word is associated with 49 attention weights corresponding to a 7×7 spatial grid of image regions.
- The attention weights are normalized and sum to 1 for each time step.
- Visual inspection confirms that the model focuses on different image regions as it generates successive words.

This demonstrates that the attention mechanism operates correctly and contributes to interpretable caption generation.

---

## Summary

This phase validates the complete Image Captioning pipeline:
- Stable training over 30 epochs
- Proper convergence behavior
- Coherent caption generation
- Interpretable attention distributions

The results confirm that combining transfer learning, attention mechanisms, and LSTM-based sequence modeling provides an effective approach for automatic image captioning.
