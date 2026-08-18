# VeriFace Interview Questions — Hard Set

This section contains deep technical, architecture, ML and
production-level questions.

The interviewer may use these questions to determine whether I
actually understand the project instead of simply knowing its name.

---

## Q1. What does your model actually learn when detecting a deepfake?

### Answer

The model learns statistical visual patterns that distinguish the real
and fake examples present in the training dataset.

These patterns may include:

- Texture inconsistencies
- Facial details
- Boundary artifacts
- Image-level patterns
- Other statistical differences

However, the model does not necessarily understand the concept of a
deepfake semantically.

It may also learn dataset-specific artifacts.

This is why generalization is one of the biggest challenges in
deepfake detection.

---

## Q2. Can your model detect every type of deepfake?

### Answer

No.

A model trained on a particular dataset cannot be assumed to detect
every future deepfake generation method.

Different generation techniques can produce different artifacts.

A model may perform very well on the dataset it was trained on but
perform worse on an unseen distribution.

---

## Q3. What is generalization?

### Answer

Generalization is the ability of a machine-learning model to perform
well on unseen data that is different from the exact examples used
during training.

For VeriFace, good generalization means the model should detect
different types of deepfakes rather than only recognizing the specific
artifacts present in the training dataset.

---

## Q4. Why is deepfake detection particularly difficult?

### Answer

Deepfake generation techniques continuously improve.

A detector may learn artifacts from older generation techniques, while
newer generators may produce images with different characteristics.

Other challenges include:

- Image compression
- Different resolutions
- Lighting conditions
- Dataset bias
- Face poses
- Unseen generation methods
- Adversarial manipulation

---

## Q5. What is dataset bias?

### Answer

Dataset bias occurs when the training dataset does not properly represent
the real-world distribution.

For example, if all fake images come from one generation method and all
real images come from a particular source, the model may learn the source
or generation artifacts instead of actual real-versus-fake differences.

---

## Q6. What is data leakage and why is it dangerous?

### Answer

Data leakage occurs when information from validation or test data
influences the training process.

For example, if nearly identical images or frames from the same original
source appear in both training and testing datasets, the model may
achieve artificially high accuracy.

This makes the evaluation unreliable.

---

## Q7. Is 93% testing accuracy enough to say VeriFace is reliable?

### Answer

No.

Accuracy alone is not enough to establish real-world reliability.

I would also need to know:

- How the dataset was created
- Whether the dataset is balanced
- Whether there is data leakage
- Precision
- Recall
- F1-score
- ROC-AUC
- Performance on unseen datasets
- Performance on different deepfake generation techniques
- Robustness against compression and transformations

Therefore, 93% testing accuracy is an evaluation result, not proof that
the system is production-grade forensic software.

---

## Q8. Your training accuracy is 97% and testing accuracy is 93%. What
does this tell you?

### Answer

It indicates a generalization gap.

The model performs better on training examples than on unseen testing
examples.

This could be caused by:

- Overfitting
- Dataset differences
- Limited dataset diversity
- Dataset-specific artifacts

The gap is not necessarily catastrophic, but it should be investigated.

---

## Q9. How would you reduce overfitting?

### Answer

I would consider:

1. More diverse training data
2. Data augmentation
3. Dropout
4. Weight decay
5. Early stopping
6. Appropriate fine-tuning
7. Cross-validation where applicable
8. Cross-dataset testing

For deepfake detection, improving dataset diversity is particularly
important.

---

## Q10. What if the dataset becomes highly imbalanced?

### Answer

Accuracy could become misleading.

For example:

9,500 real images
500 fake images

A model that predicts every image as real would achieve 95% accuracy,
but it would completely fail at detecting fake images.

I would therefore evaluate:

- Precision
- Recall
- F1-score
- Confusion matrix
- ROC-AUC
- PR-AUC

I could also use class weighting or resampling techniques.

---

## Q11. Which is more important: precision or recall?

### Answer

It depends on the application.

If missing a fake image is more dangerous, recall for the fake class
becomes particularly important.

If falsely accusing real images of being fake is more costly, precision
becomes more important.

In a practical system, I would analyze both rather than optimizing
only one metric.

---

## Q12. What happens if someone compresses a deepfake image?

### Answer

Compression can remove or modify visual artifacts that the model uses
for classification.

Therefore a detector trained primarily on high-quality images may
perform poorly on compressed images.

I would test the model at different compression levels and include
representative compressed images during training.

---

## Q13. What happens if a completely new deepfake generator is released?

### Answer

The existing model may not generalize to the new generation technique.

I would:

1. Collect representative samples.
2. Evaluate the existing model.
3. Analyze failure cases.
4. Add diverse examples to the dataset.
5. Fine-tune or retrain the model.
6. Evaluate on a separate unseen test set.

---

## Q14. What is an adversarial example?

### Answer

An adversarial example is an input intentionally modified so that a
machine-learning model makes an incorrect prediction while the change
may be difficult for humans to notice.

For a deepfake detector, an attacker could potentially attempt to
modify an image specifically to fool the classifier.

---

## Q15. How would you test the robustness of VeriFace?

### Answer

I would create separate evaluation sets containing:

- Different deepfake generation methods
- Different image resolutions
- JPEG compression
- Noise
- Cropping
- Lighting variations
- Different face poses
- Images from unseen sources

Then I would compare performance across these conditions.

---

## Q16. How would you make VeriFace production-ready?

### Answer

I would separate the user interface from the machine-learning service.

A possible architecture would be:

Client
   ↓
API Gateway
   ↓
Backend
   ↓
ML Inference Service
   ↓
ResNet18
   ↓
Prediction

I would also add:

- Input validation
- Authentication
- Rate limiting
- Logging
- Monitoring
- Error handling
- Docker
- Scalable deployment
- Secure image handling

---

## Q17. Why shouldn't the model be loaded for every request?

### Answer

Loading the model for every request introduces unnecessary overhead.

In production, the model should normally be loaded when the inference
service starts and reused for multiple requests.

This significantly reduces inference latency.

---

## Q18. How would you scale VeriFace?

### Answer

For higher traffic, I could run multiple inference workers or containers
behind a load balancer.

If GPU acceleration is required, I could deploy the inference service
on GPU-enabled infrastructure.

I would also monitor:

- Request latency
- Throughput
- CPU usage
- GPU usage
- Memory
- Error rate

---

## Q19. How would you protect uploaded images?

### Answer

Because facial images can contain sensitive information, I would:

- Validate file types
- Limit file sizes
- Reject malformed files
- Avoid unnecessary storage
- Encrypt data where required
- Apply access controls
- Delete temporary files when they are no longer needed

Privacy should be considered when handling facial data.

---

## Q20. What is Grad-CAM?

### Answer

Grad-CAM stands for Gradient-weighted Class Activation Mapping.

It is an explainability technique that helps identify which regions of
an image contributed to the model's prediction.

For VeriFace, it could help visualize whether the model is focusing on
meaningful facial regions.

---

## Q21. Why is explainability important for VeriFace?

### Answer

If the model predicts that an image is fake, simply giving the label
doesn't tell us why.

An explainability technique such as Grad-CAM could help visualize which
areas influenced the prediction.

It can also help developers identify whether the model is relying on
meaningful features or unintended artifacts.

---

## Q22. What if Grad-CAM shows the model is focusing on the background?

### Answer

That would be a warning sign.

It could indicate that the model has learned a dataset-specific
correlation instead of actual facial manipulation features.

I would investigate the dataset, preprocessing and model behavior and
test whether the background correlation exists in other samples.

---

## Q23. CNN vs Vision Transformer?

### Answer

CNNs use convolution operations to learn local spatial patterns.

Vision Transformers divide an image into patches and use attention
mechanisms to model relationships between those patches.

CNNs can be efficient and work well with smaller datasets, while
Vision Transformers can model broader relationships and often benefit
from large-scale pretraining.

---

## Q24. GAN vs Deepfake Detector?

### Answer

A GAN is a generative architecture that can be used to create synthetic
data.

A deepfake detector is a discriminative system that attempts to
distinguish real data from manipulated or generated data.

Conceptually:

GAN:

Generate fake data

Detector:

Detect fake data

---

## Q25. What is a GAN?

### Answer

GAN stands for Generative Adversarial Network.

It contains two components:

Generator
Discriminator

The Generator attempts to create realistic synthetic data.

The Discriminator attempts to distinguish real data from generated data.

The two components compete during training.

---

## Q26. Why are GANs relevant to VeriFace?

### Answer

GANs can be used to generate realistic synthetic images and perform
certain types of image manipulation.

Therefore, understanding generative models helps us understand the
types of synthetic content a detector may need to identify.

---

# RAG / GENERATIVE AI

## Q27. What is RAG?

### Answer

RAG stands for Retrieval-Augmented Generation.

It combines information retrieval with a generative language model.

Basic flow:

User Question
     ↓
Embedding
     ↓
Vector Database
     ↓
Relevant Documents
     ↓
Prompt + Retrieved Context
     ↓
LLM
     ↓
Answer

---

## Q28. Why use RAG?

### Answer

RAG allows an LLM to use external information at inference time.

It is useful when information is:

- Private
- Frequently changing
- Domain-specific
- Too large to rely on model memory alone

It can also help reduce unsupported answers by grounding generation
in retrieved information.

---

## Q29. What is an embedding?

### Answer

An embedding is a numerical vector representation of information such
as text.

Semantically similar pieces of information tend to have similar vector
representations.

---

## Q30. What is a vector database?

### Answer

A vector database stores embeddings and allows similarity-based
retrieval.

Examples include:

- FAISS
- Pinecone
- Weaviate
- Milvus
- Chroma

---

## Q31. What is chunking?

### Answer

Chunking means dividing a large document into smaller pieces before
creating embeddings.

The purpose is to retrieve only the relevant portions of a document
instead of sending the entire document to the LLM.

---

## Q32. What is chunk overlap?

### Answer

Chunk overlap means neighboring chunks share some content.

This helps preserve context when an important sentence or concept lies
near the boundary between two chunks.

---

## Q33. What is cosine similarity?

### Answer

Cosine similarity measures the similarity between two vectors based on
the angle between them.

Formula:

cos(theta) = (A · B) / (||A|| ||B||)

It is commonly used when comparing embeddings.

---

## Q34. RAG vs Fine-Tuning?

### Answer

RAG retrieves external information at runtime.

Fine-tuning changes the model's parameters through additional training.

RAG is useful when knowledge changes frequently.

Fine-tuning is useful when we want to change or specialize model
behavior.

---

## Q35. Is RAG part of VeriFace?

### Answer

No.

The current VeriFace implementation is primarily a computer-vision
classification system using ResNet18.

RAG could be added as a separate explanation or knowledge layer, but it
is not the actual deepfake classifier.

---

## Q36. How could RAG be added to VeriFace?

### Answer

The architecture could be:

Image
  ↓
ResNet18
  ↓
REAL / FAKE
  ↓
Explanation System
  ↓
RAG
  ↓
Deepfake knowledge base
  ↓
Explanation

The ResNet model would remain responsible for classification.

RAG could retrieve information about:

- Deepfake techniques
- Known artifacts
- Detection methods
- Model limitations

---

# PROJECT OWNERSHIP QUESTIONS

## Q37. What exactly did YOU do?

### Answer

I worked on the machine-learning pipeline of VeriFace.

My work included dataset preparation, preprocessing, model training,
ResNet18 implementation, checkpoint handling, prediction and Streamlit
integration.

I should always describe only the work I personally performed.

---

## Q38. What was the hardest technical problem?

### Answer

One major challenge was the computational cost because I trained the
model using CPU resources.

Another challenge was checkpoint compatibility between the training and
prediction pipelines.

I also had to understand the difference between training and testing
performance and the resulting overfitting/generalization issue.

---

## Q39. If you had one more month, what would you do?

### Answer

I would focus primarily on generalization and robustness.

I would:

1. Expand the dataset.
2. Include multiple deepfake generation methods.
3. Test on completely unseen datasets.
4. Add better evaluation metrics.
5. Experiment with stronger architectures.
6. Add Grad-CAM.
7. Test compression robustness.
8. Extend the system to video.
9. Build a production API.
10. Improve privacy and security.

---

## Q40. What is the biggest weakness of your project?

### Answer

The biggest weakness is that the current evaluation does not guarantee
generalization to every real-world deepfake generation technique.

The model may learn characteristics specific to the training dataset.

Therefore, cross-dataset and cross-generation-method evaluation would
be important before considering it a production-grade forensic system.

---

# FINAL HARD QUESTION

## Q41. Why should we believe that you actually built this project?

### Answer

Because I can explain the project at multiple levels.

At the application level, I can explain the user flow and Streamlit
interface.

At the machine-learning level, I can explain the dataset, preprocessing,
training, evaluation and overfitting.

At the deep-learning level, I can explain CNNs, convolution, ResNet,
residual connections, backpropagation and optimization.

I can also explain the problems I personally encountered, such as CPU
training and checkpoint compatibility, and how I approached them.

---

# GOLDEN RULE

Never memorize only the final answer.

For every technical statement, be prepared for:

WHY?
HOW?
WHAT HAPPENS INSIDE?
WHAT IF IT FAILS?
HOW WOULD YOU IMPROVE IT?

Example:

"I used ResNet18."

Interviewer:

Why ResNet18?
    ↓
What is ResNet?
    ↓
What is residual learning?
    ↓
What is a residual connection?
    ↓
Why does it help?
    ↓
What is a gradient?
    ↓
What is backpropagation?
    ↓
What is gradient descent?
    ↓
What optimizer did you use?
    ↓
Why that optimizer?

This is how project interviews become deep technical interviews.