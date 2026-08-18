# VeriFace Interview Questions — Medium Set

This section contains questions that test whether I understand the
technical implementation behind VeriFace.

---

## Q1. Explain the complete architecture of VeriFace.

### Answer

The complete flow is:

User
  ↓
Streamlit Interface
  ↓
Image Upload
  ↓
Image Preprocessing
  ↓
Tensor Conversion
  ↓
ResNet18
  ↓
Classification Output
  ↓
REAL / FAKE
  ↓
Result Display

The training pipeline is separate:

Dataset
  ↓
Preprocessing
  ↓
Training Data
  ↓
ResNet18
  ↓
Loss Calculation
  ↓
Backpropagation
  ↓
Optimizer
  ↓
Updated Weights
  ↓
Best Checkpoint

---

## Q2. What is a residual connection?

### Answer

A residual connection is a shortcut connection that allows the original
input to bypass one or more layers.

Instead of learning the complete mapping H(x), the network learns a
residual function F(x).

The output becomes:

F(x) + x

This creates a direct path for information and gradients.

---

## Q3. Why are residual connections useful?

### Answer

As neural networks become deeper, optimization can become difficult.

Residual connections provide shortcut paths through the network, which
helps gradients flow backward more easily during backpropagation.

This makes deeper networks easier to optimize.

---

## Q4. Why ResNet18 instead of ResNet50?

### Answer

ResNet50 is deeper and computationally more expensive.

Because my training environment was CPU-based, ResNet18 was a more
practical choice.

It still provides the advantages of residual learning while keeping
the computational requirements relatively manageable.

---

## Q5. What is transfer learning?

### Answer

Transfer learning means using knowledge learned by a model on one task
and adapting that model to another related task.

For example:

Pretrained ResNet
      ↓
Learned visual features
      ↓
Adapt final layer
      ↓
REAL / FAKE classification

---

## Q6. Why is transfer learning useful?

### Answer

Training a deep network from scratch requires a large amount of data
and computational resources.

A pretrained model already contains useful visual representations.

Therefore, transfer learning can reduce training time and improve the
starting point of the model.

---

## Q7. What is fine-tuning?

### Answer

Fine-tuning means allowing some pretrained layers to continue learning
from the new dataset instead of keeping all pretrained layers frozen.

It allows the pretrained representation to adapt to the new task.

---

## Q8. What is the difference between feature extraction and fine-tuning?

### Answer

In feature extraction, most pretrained layers are frozen and only the
new classification layers are trained.

In fine-tuning, some pretrained layers are also updated using the new
dataset.

---

## Q9. What is convolution?

### Answer

Convolution is an operation where a small learnable filter or kernel
moves across an image or feature map.

The kernel performs mathematical operations with local regions of the
input and produces a feature map.

This allows the network to learn patterns such as edges and textures.

---

## Q10. What is a kernel?

### Answer

A kernel is a small matrix of learnable weights used during convolution.

Different kernels can learn to detect different visual patterns.

---

## Q11. What is stride?

### Answer

Stride determines how many pixels the kernel moves at each step.

Stride 1 means the kernel moves one pixel at a time.

Stride 2 means it moves two pixels at a time.

Increasing stride generally reduces the spatial dimensions of the output.

---

## Q12. What is padding?

### Answer

Padding adds extra pixels around the boundary of an input.

It can help preserve spatial dimensions and allow the network to process
information near image boundaries.

---

## Q13. What is ReLU?

### Answer

ReLU stands for Rectified Linear Unit.

Its formula is:

ReLU(x) = max(0, x)

It introduces non-linearity into the neural network.

---

## Q14. Why do neural networks need activation functions?

### Answer

Without nonlinear activation functions, multiple linear layers would
still behave like a single linear transformation.

Activation functions allow the network to learn complex nonlinear
patterns.

---

## Q15. What is backpropagation?

### Answer

Backpropagation is the process of calculating the gradients of the loss
with respect to the model parameters.

It uses the chain rule of calculus.

The optimizer then uses these gradients to update the parameters.

---

## Q16. Explain the training process.

### Answer

The training process is:

Input image
    ↓
Forward pass
    ↓
Prediction
    ↓
Calculate loss
    ↓
Backpropagation
    ↓
Calculate gradients
    ↓
Optimizer updates weights
    ↓
Repeat

This process continues for multiple batches and epochs.

---

## Q17. What is gradient descent?

### Answer

Gradient descent is an optimization technique used to minimize the loss
function.

The model calculates the gradient and updates its parameters in the
direction that reduces the loss.

---

## Q18. What is learning rate?

### Answer

Learning rate controls the size of the parameter update during
optimization.

A very high learning rate can make training unstable.

A very low learning rate can make training extremely slow.

---

## Q19. What is batch size?

### Answer

Batch size is the number of training samples processed before one
parameter update.

For example, with a batch size of 32, the model processes 32 images,
calculates the gradients and then updates its parameters.

---

## Q20. What is data augmentation?

### Answer

Data augmentation creates different variations of training images using
transformations.

Examples include:

- Cropping
- Flipping
- Rotation
- Scaling
- Color transformations

It helps improve generalization.

---

## Q21. Why is data augmentation important for VeriFace?

### Answer

Deepfake images can appear in different orientations, resolutions,
lighting conditions and visual conditions.

Data augmentation can increase the diversity of the training data.

However, augmentations must be selected carefully because unrealistic
transformations could introduce artificial patterns that the model
learns instead of genuine deepfake characteristics.

---

## Q22. What is `model.train()`?

### Answer

`model.train()` puts a PyTorch model into training mode.

This is important for layers such as Dropout and Batch Normalization,
whose behavior differs between training and inference.

---

## Q23. What is `model.eval()`?

### Answer

`model.eval()` puts the model into evaluation mode.

It should be used during validation and inference so that layers such
as Dropout and Batch Normalization behave correctly.

---

## Q24. Why use `torch.no_grad()`?

### Answer

During inference, we don't need to calculate gradients because we are
not updating the model.

`torch.no_grad()` disables gradient tracking, which reduces unnecessary
computation and memory usage.

Example:

model.eval()

with torch.no_grad():
    output = model(image)

---

## Q25. What is a checkpoint?

### Answer

A checkpoint is a saved state of the trained model.

It allows us to save the best model and later use it for inference or
resume training.

---

## Q26. What is a PyTorch `state_dict`?

### Answer

A `state_dict` is a dictionary containing the model's learned parameters
and buffers mapped to their layer names.

---

## Q27. Why can a checkpoint fail to load?

### Answer

The architecture used during inference must be compatible with the
architecture used during training.

If the layer names or parameter shapes do not match, PyTorch can produce
errors such as:

- Missing keys
- Unexpected keys
- Size mismatch

---

## Q28. What is the difference between training and testing accuracy?

### Answer

Training accuracy measures performance on data used to train the model.

Testing accuracy measures performance on unseen data.

A large gap can indicate overfitting or a difference between the
training and testing distributions.

---

## Q29. Is accuracy enough to evaluate VeriFace?

### Answer

No.

I would also evaluate:

- Precision
- Recall
- F1-score
- Confusion matrix
- ROC-AUC

Accuracy can be misleading when the dataset is imbalanced.

---

## Q30. What is precision?

### Answer

Precision tells us:

"Out of everything predicted as positive, how much was actually positive?"

Formula:

Precision = TP / (TP + FP)

---

## Q31. What is recall?

### Answer

Recall tells us:

"Out of all actual positive samples, how many did the model correctly
identify?"

Formula:

Recall = TP / (TP + FN)

---

## Q32. What is F1-score?

### Answer

F1-score is the harmonic mean of precision and recall.

Formula:

F1 = 2 × Precision × Recall
          -----------------
          Precision + Recall

It is useful when we want a balance between precision and recall.

---

## Q33. What is a confusion matrix?

### Answer

A confusion matrix shows:

- True Positives
- True Negatives
- False Positives
- False Negatives

It helps us understand exactly what types of mistakes the classifier
is making.

---

## Q34. What is a false positive in VeriFace?

### Answer

A false positive would occur when a real image is predicted as fake,
assuming fake is the positive class.

---

## Q35. What is a false negative?

### Answer

A false negative would occur when a fake image is predicted as real.

This can be particularly concerning because a manipulated image would
incorrectly be accepted as authentic.