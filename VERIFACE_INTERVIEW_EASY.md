# VeriFace Interview Questions — Easy Set

This section contains basic questions that an interviewer can ask
to understand whether I know my project and its fundamentals.

---

## Q1. Tell me about your VeriFace project.

### Answer

VeriFace is a deep-learning based deepfake image detection system.

The main purpose of the project is to determine whether a given facial
image is real or fake.

I used Python, PyTorch, Torchvision and ResNet18 for the machine-learning
part and Streamlit to create the user interface.

I trained the model on approximately 5,000 real images and 5,000 fake
images. The model achieved around 97% training accuracy and approximately
93% testing accuracy.

The complete pipeline starts with the user uploading an image, followed
by preprocessing, model inference and finally displaying the prediction
as real or fake.

---

## Q2. Why did you build VeriFace?

### Answer

I built VeriFace because deepfake technology is becoming increasingly
realistic and can be used for misinformation, impersonation and identity
manipulation.

I wanted to build a practical computer-vision project that could analyze
a facial image and determine whether it was real or artificially
generated or manipulated.

---

## Q3. What is a deepfake?

### Answer

A deepfake is AI-generated or AI-manipulated media created using
deep-learning or generative-AI techniques.

In images, deepfakes can involve face swapping, facial manipulation,
identity replacement or completely synthetic faces.

---

## Q4. What exactly does VeriFace do?

### Answer

VeriFace performs binary image classification.

It takes a facial image as input and predicts one of two classes:

- REAL
- FAKE

The system does not generate deepfakes. It only attempts to detect them.

---

## Q5. What type of machine-learning problem is VeriFace?

### Answer

VeriFace is a supervised binary image-classification problem.

It is supervised because the training images have labels.

The two classes are:

REAL → 0
FAKE → 1

---

## Q6. Why did you use deep learning?

### Answer

I used deep learning because images contain complex visual patterns that
are difficult to manually define.

Deep-learning models can automatically learn useful features from images,
such as edges, textures, shapes and more complex visual patterns.

---

## Q7. Why did you use CNN?

### Answer

CNNs are well suited for image-related tasks because they preserve spatial
relationships between pixels.

They use convolutional filters to learn visual features automatically.

For example, early layers may learn edges and textures while deeper
layers learn more complex patterns.

---

## Q8. Which model did you use?

### Answer

I used ResNet18, which is a convolutional neural-network architecture
based on residual learning.

---

## Q9. Why did you choose ResNet18?

### Answer

I chose ResNet18 because it provides a good balance between model
performance and computational requirements.

Since I trained the model using CPU resources, ResNet18 was more practical
than using a much larger architecture.

It also provides residual connections that help with training deeper
networks.

---

## Q10. What is ResNet?

### Answer

ResNet stands for Residual Network.

Its main idea is to introduce shortcut connections that allow information
to bypass some layers of the network.

This helps improve gradient flow and makes deeper networks easier to
optimize.

---

## Q11. What is a CNN?

### Answer

CNN stands for Convolutional Neural Network.

It is a neural-network architecture commonly used for image processing.

CNNs use convolution operations to automatically learn spatial features
from images.

---

## Q12. What dataset did you use?

### Answer

I used a Kaggle deepfake image dataset containing approximately:

- 5,000 real images
- 5,000 fake images

So the total dataset was approximately 10,000 images.

---

## Q13. How many epochs did you train for?

### Answer

I trained the model for 5 epochs in my implementation.

---

## Q14. What accuracy did you achieve?

### Answer

The model achieved approximately:

Training accuracy: 97%

Testing accuracy: 93%

The difference between these values also indicated some degree of
overfitting.

---

## Q15. What is an epoch?

### Answer

An epoch means one complete pass through the entire training dataset.

For example, if the training dataset contains 10,000 images, one epoch
means the model has processed all 10,000 images once.

---

## Q16. What is overfitting?

### Answer

Overfitting occurs when a model performs very well on training data but
performs worse on unseen data.

In VeriFace, the training accuracy was around 97% while testing accuracy
was around 93%, which indicates a training-testing performance gap.

---

## Q17. How can you reduce overfitting?

### Answer

Some techniques I could use are:

- Data augmentation
- Dropout
- Weight decay
- Early stopping
- More diverse training data
- Better dataset splitting
- Cross-dataset evaluation

For deepfake detection, increasing dataset diversity is particularly
important because the model can otherwise learn dataset-specific artifacts.

---

## Q18. What framework did you use?

### Answer

I used PyTorch and Torchvision for the machine-learning implementation.

I used Streamlit for the user interface.

---

## Q19. Why did you use PyTorch?

### Answer

PyTorch provides tensors, automatic differentiation, neural-network
modules, pretrained models and GPU support.

It also provides flexibility for implementing custom training and
inference pipelines.

---

## Q20. Why did you use Streamlit?

### Answer

I used Streamlit because it allows a machine-learning model to be
quickly converted into an interactive web application.

It allowed me to create an interface where a user can upload an image
and receive the model's prediction.

---

## Q21. What happens when a user uploads an image?

### Answer

The basic flow is:

User uploads image
        ↓
Image preprocessing
        ↓
Image converted to tensor
        ↓
ResNet18
        ↓
Model prediction
        ↓
REAL / FAKE
        ↓
Result displayed in Streamlit

---

## Q22. What is a tensor?

### Answer

A tensor is a multidimensional numerical array used by deep-learning
frameworks.

For example, an RGB image can be represented using dimensions such as:

Channels × Height × Width

For example:

3 × 224 × 224

---

## Q23. What is a loss function?

### Answer

A loss function measures how different the model's prediction is from
the actual target.

During training, the model tries to minimize this loss.

---

## Q24. What is an optimizer?

### Answer

An optimizer updates the model's parameters using gradients calculated
during backpropagation.

Its goal is to reduce the loss and improve the model's predictions.

---

## Q25. What is your project's biggest limitation?

### Answer

The biggest limitation is generalization.

A model trained on one particular dataset may not perform equally well
on deepfakes generated using completely different techniques.

The model may also learn dataset-specific artifacts instead of learning
general deepfake characteristics.

---

## Q26. Can VeriFace detect every deepfake?

### Answer

No.

A deepfake detector cannot be assumed to detect every type of deepfake.

New generation techniques may produce different patterns from the ones
present in the training dataset.

Therefore, testing on unseen datasets and different generation methods
is very important.

---

## Q27. What would you improve in VeriFace?

### Answer

I would improve it by:

1. Increasing dataset size and diversity.
2. Including different deepfake generation techniques.
3. Testing on completely unseen datasets.
4. Evaluating precision, recall and F1-score.
5. Adding Grad-CAM for explainability.
6. Improving robustness against image compression.
7. Extending the system to video detection.
8. Creating a production-ready API.

---

## Q28. What was the biggest challenge you faced?

### Answer

One major challenge was computational cost because I trained the model
using CPU resources, which made training take several hours.

I also faced issues while loading the trained checkpoint into the
prediction pipeline because the model architecture and checkpoint
parameters had to be compatible.

Another challenge was understanding and handling the difference between
training and testing performance.