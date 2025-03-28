# Developing a Neural Network Regression Model

## AIM
To develop a neural network regression model for the given dataset.

## THEORY
Regression problems involve predicting a continuous output variable based on input features. Traditional linear regression models often struggle with complex patterns in data. Neural networks, specifically feedforward neural networks, can capture these complex relationships by using multiple layers of neurons and activation functions. In this experiment, a neural network model is introduced with a single linear layer that learns the parameters weight and bias using gradient descent.

## Neural Network Model
Include the neural network model diagram.

## DESIGN STEPS
### STEP 1: Generate Dataset

Create input values  from 1 to 50 and add random noise to introduce variations in output values .

### STEP 2: Initialize the Neural Network Model

Define a simple linear regression model using torch.nn.Linear() and initialize weights and bias values randomly.

### STEP 3: Define Loss Function and Optimizer

Use Mean Squared Error (MSE) as the loss function and optimize using Stochastic Gradient Descent (SGD) with a learning rate of 0.001.

### STEP 4: Train the Model

Run the training process for 100 epochs, compute loss, update weights and bias using backpropagation.

### STEP 5: Plot the Loss Curve

Track the loss function values across epochs to visualize convergence.

### STEP 6: Visualize the Best-Fit Line

Plot the original dataset along with the learned linear model.

### STEP 7: Make Predictions

Use the trained model to predict  for a new input value .

## PROGRAM

### Name: YASHWINI M

### Register Number: 212223230249

```python
##YASHWINI M 212223230249

import torch
import torch.nn as nn
import torch.optim as optim
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
x = np.arange(1, 71, dtype=np.float32).reshape(-1, 1)
y = 3.5 * x + np.random.normal(0, 5, size=x.shape)

x = (x - x.mean()) / x.std()

x_train = torch.tensor(x, dtype=torch.float32)
y_train = torch.tensor(y, dtype=torch.float32)

class Model(nn.Module):
    def __init__(self, in_features, out_features):
        super().__init__()
        self.linear = nn.Linear(in_features, out_features)

    def forward(self, x):
        return self.linear(x)

model = Model(in_features=1, out_features=1)

##YASHWINI M 212223230249

criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.001)

epochs = 100
loss_values = []

for epoch in range(epochs):
    model.train()
    optimizer.zero_grad()
    predictions = model(x_train)
    loss = criterion(predictions, y_train)
    loss.backward()
    optimizer.step()

    loss_values.append(loss.item())

    if (epoch + 1) % 10 == 0:
        print(f'Epoch {epoch+1}/{epochs}, Loss: {loss.item():.4f}')

plt.figure(figsize=(8, 5))
plt.plot(range(epochs), loss_values, label="Training Loss", color='b')
plt.xlabel("Epochs")
plt.ylabel("Loss")
plt.title("Training Loss vs Epochs")
plt.legend()
plt.show()

##YASHWINI M 212223230249

model.eval()
with torch.no_grad():
    y_pred = model(x_train).numpy()
plt.figure(figsize=(8, 5))
plt.scatter(x, y, label="Data", color='')
plt.plot(x, y_pred, label="Best Fit Line", color='black')
plt.xlabel("Input (x)")
plt.ylabel("Output (y)")
plt.title("Best Fit Line for Regression")
plt.legend()
plt.show()

new_sample = torch.tensor([[55.0]])
predicted_output = model(new_sample).item()
print(f"Prediction for input 55: {predicted_output:.2f}")
```

### Dataset Information
![image](https://github.com/user-attachments/assets/d44f887b-9e08-428a-8509-d2b009c8180c)

### OUTPUT
Training Loss Vs Epochs

![image](https://github.com/user-attachments/assets/9e754e2d-6d8d-454b-aab5-4bdd223f5b0d)

Best Fit line plot

![image](https://github.com/user-attachments/assets/bea8af5d-75c0-45a0-b98a-dbe0349b9a8a)


### New Sample Data Prediction

![image](https://github.com/user-attachments/assets/33c55d4c-fd51-44e4-91eb-900ca2bdd08c)

## RESULT
Thus, a neural network regression model was successfully developed and trained using PyTorch.
