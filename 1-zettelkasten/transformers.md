Created on 2024-10-02_09-31-02

## 📔 Notes

### 2024-10-02

- transformers are a type of neural network architecture that is designed to handle sequential data
- they are based on the concept of self-attention
- self-attention is a mechanism that allows the model to focus on different parts of the input sequence when making predictions
- the transformer architecture consists of an encoder and a decoder
- the encoder processes the input sequence and produces a sequence of hidden states
- the decoder takes the hidden states produced by the encoder and generates the output sequence
- the transformer architecture has been shown to be highly effective for a wide range of natural language processing tasks, such as machine translation, text generation, and text classification
- the transformer architecture has also been adapted for other types of sequential data, such as images and audio
- the transformer architecture has been widely adopted in the field of natural language processing and has become the basis for many state-of-the-art models

- tokenizer is a tool that converts a sequence of characters into a sequence of tokens
- tensors are multi-dimensional arrays that can be used to represent data in a neural network

- bert-case-uncased is a pre-trained BERT model that has been trained on a large corpus of text data
- the model has been trained to predict the next word in a sentence, which allows it to learn the relationships between words in a sentence
- the model has been fine-tuned on a specific task, such as text classification or named entity recognition, to improve its performance on that task

- normal flow of process

1. human input --> tensors (facilitated by the `preprocess` method)
2. tensors -> tensor outputs (done by the `forward` method)
3. tensor outputs -> human intuitive outputs (done by `post_process` method)

Basic flow consists of two steps:
1. Tokenizers --> convert human language to model tokens (something on which the model is trained on)
2. model: converts input tensors to output tensors.

4 step process:

- convert strings to tokens
- convert tokens to input tensors/vectors
- process input tensors and generate output tensors
- convert output tensors to human strings.

#### getting deeper into tokenization and embedding

1. a text is converted into a form of `input_ids` which specify the sequence of tokens (could be words, punctuations, etc) for the model.
2. a token_type_ids specify the position of a token in a sentence (first, second) -> when multiple sentences are provided.
3. attention_mask regulates which token can attend to which token

these input_ids, token_type_ids are converted to embeddings
1. word_embeddings -> semantics of the word.
2. position_embeddings -> semantics related to positions of the words.
3. token type embeddings

- deep learning models require huge amount of memory for performing inferencing.

1. passage -> tokens -> vectors(aka embeddings) (captures semantics, positions). --> encoder (KQV formula) passed across multiple layers --> 

After this, it can be treated as a classification problem
1. token-level reasoning -> treating them in isolation, understand the context of other tokens in sequence.
2. sequence-level reasoning -> reason about the sequence as a whole --> create a network.

LLMs do something in the middle, reasoning on each token, allow for small opportunities in which network can consider sequence as a whole.

The attention mechanism states how tokens can communicate semantic information to other tokens in a sequence.

1. K(E), Q(E), V(E) -> 3 different embeddings derived from E.
2. sigma(A) -> how each embedding relates to other embeddings
3. sigma(A)V -> embdiggin which considers pre and post interface attention.

3 classes of models:

1. encoder-only models --> good at understanding semantics of human language. (It stops there)
2. encoder-decoder models --> understand semantics and generate sentences in other forms (machine translations)
3. decoder-only models --> generate new sentences (gpt style) --> predicting next word in a sequence.
    - process of training where we train the model to predict the next token based on the context in a sectence is called autoregression.


## 🔗 Links

- [[]]
