### **Structure**

- Input Layer → Hidden Layers → Output Layer.
- Each layer has **neurons**, connected with **weights**.

### **Forward Propagation**

- Input data moves through layers using **weights + bias**.
- Each neuron applies:
    output=activation(weights⋅inputs+bias)output = activation(weights \cdot inputs + bias)output=activation(weights⋅inputs+bias)

### **Backward Propagation**

- Compares predicted output to actual (loss).
- Adjusts weights to reduce error using **gradients**

![[Pasted image 20250729231020.png]]
## Activation Functions

Used to introduce **non-linearity** to models. Without them, neural networks are just linear regressions.

|Function|Formula|Used For|
|---|---|---|
|**ReLU**|max(0, x)|Fast and widely used in hidden layers|
|**Sigmoid**|1 / (1 + e^-x)|Outputs between 0 and 1 (e.g., binary classification)|
|**Tanh**|(e^x - e^-x)/(e^x + e^-x)|Zero-centered, better than sigmoid in some cases|

## Loss Functions

Measures **how wrong** the prediction is. Used during training to adjust weights.

| Task Type      | Loss Function            | Example                |
| -------------- | ------------------------ | ---------------------- |
| Regression     | Mean Squared Error (MSE) | House price prediction |
| Classification | Cross-Entropy Loss       | Spam detection         |

## Optimizers

Used to **update weights** based on gradients (from backpropagation).

- **SGD (Stochastic Gradient Descent):** Simple, but can be slow
- **Adam:** Faster and adaptive; most commonly used

## Overfitting vs Underfitting

| Concept          | What Happens                                     | Solution                       |
| ---------------- | ------------------------------------------------ | ------------------------------ |
| **Overfitting**  | Model memorizes training data, fails on new data | Regularization, Dropout        |
| **Underfitting** | Model too simple to capture pattern              | Use deeper model, train longer |
## Evaluation Metrics

| Task           | Metric              | Meaning                       |
| -------------- | ------------------- | ----------------------------- |
| Classification | Accuracy            | % correct predictions         |
| Classification | Precision/Recall/F1 | Important for imbalanced data |
| Regression     | MAE/MSE/RMSE        | Error distances               |