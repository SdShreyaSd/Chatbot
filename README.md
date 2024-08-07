# Chatbot
This project focuses on developing a chatbot using an LSTM (Long Short-Term Memory) model to answer yes/no questions based on given stories. Here's a detailed description of the project:

### Project Overview

**Objective:**
The goal is to build a chatbot capable of understanding short stories and answering related yes/no questions with a high level of accuracy. The model is trained using a dataset of stories, questions, and answers.

### Data Preparation

1. **Loading Data:**
   - The training and test datasets (`train_qa.txt` and `test_qa.txt`) are loaded using the `pickle` module.
   - Data is structured in tuples of (story, question, answer).

2. **Vocabulary Creation:**
   - A vocabulary set is created by extracting unique words from both stories and questions.
   - Special tokens `yes` and `no` are added to the vocabulary.
   - The total vocabulary length and the maximum lengths of stories and questions are determined.

3. **Tokenization:**
   - Keras' `Tokenizer` is used to convert the vocabulary into a word index.
   - Stories and questions are converted into sequences of integers based on this index.

### Data Vectorization

- **Vectorization Function:**
  - A function `Vectorised_Data` is defined to convert stories, questions, and answers into numerical vectors suitable for model input.
  - The function pads sequences to ensure uniform input lengths and converts answers into one-hot encoded vectors.

### Model Architecture

1. **Embedding Layers:**
   - Separate embedding layers are used for encoding the input stories and questions.
   - These layers transform words into dense vectors of fixed size.

2. **Dropout Layers:**
   - Dropout is applied to the embeddings to prevent overfitting.

3. **Matching Layer:**
   - A dot product between the encoded stories and questions creates a match matrix, followed by a softmax activation to highlight relevant parts of the story.

4. **Response Layer:**
   - The response is generated by adding the match matrix to the encoded stories and permuting dimensions to align with the question encoding.
   - Concatenation of the response and the question encoding is performed.

5. **LSTM Layer:**
   - An LSTM layer processes the combined sequences to capture dependencies and context.

6. **Output Layer:**
   - A Dense layer with softmax activation generates the final prediction, providing probabilities for each word in the vocabulary.

### Model Training

- The model is compiled with `rmsprop` optimizer and `categorical_crossentropy` loss function.
- It is trained on the training data with validation on the test data for 35 epochs.
- Training progress is visualized using matplotlib to plot accuracy and validation accuracy.

### Model Evaluation and Usage

- After training, the model is saved and can be reloaded for making predictions.
- A sample prediction is demonstrated using a new story and question.
- The predicted answer is decoded from the word index, and the probability of certainty is printed.

### Example Usage

- A test story and question are provided, and the chatbot predicts the answer along with the probability of its certainty.
- An example demonstrates how to input new stories and questions and obtain predictions from the trained model.

This project showcases the application of deep learning techniques, specifically LSTM networks, to natural language processing tasks such as reading comprehension and question answering. It combines various stages of data preparation, model design, training, and evaluation to create a functional yes/no answering chatbot.
