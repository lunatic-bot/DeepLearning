# Model Exploration & Visualization Notes

### Workflow Reminder
* **Teachable Machine:** Used for rapid prototyping, instant data gathering via hardware devices, and spinning up quick baseline models. Export targets typically include Keras (`.h5`), TensorFlow Lite (`.tflite`), or TF.js.
* **Netron:** Used to inspect the static underlying graph architecture. Drag-and-drop your exported file here to read input/output shapes, specific tensor operators (`Conv2D`, `Dense`, `Dropout`), weight dimensions, biases, and layer connections.

---

### Other Advanced Tools for Exploring Deep Learning Models

To go beyond static structural graphs (Netron) and look into model training dynamics, feature map extractions, or explainability patterns, use these industry-standard frameworks:

#### 1. SHAP (SHapley Additive exPlanations)
* **What it does:** Measures feature importance based on cooperative game theory. 
* **Why use it:** It tells you exactly how much each individual input feature (or pixel region) pushed a prediction toward or away from a target class. Great for debugging model bias.

#### 2. TensorBoard
* **What it does:** TensorFlow/Keras's dynamic tracking dashboard.
* **Why use it:** Logs real-time metrics (loss, accuracy, learning rate curves), visualizes weight distributions across training iterations, and includes a **3D Embedding Projector** to map high-dimensional embeddings.

#### 3. Hidden Layer Activation Profiles (Feature Maps)
* **What it does:** Custom code hooks targeting mid-network layers.
* **Why use it:** Extracts intermediate outputs. For convolutional networks, plotting these slices allows you to literally see the features (edges, textures, shapes) individual layers are learning from your inputs.

#### 4. Grad-CAM (Gradient-weighted Class Activation Mapping)
* **What it does:** Visual explanation algorithms for computer vision.
* **Why use it:** Generates spatial heatmaps indicating exactly what part of an image a CNN focused on before making a classification (e.g., did it categorize a dog based on its ears or the background grass?).