## Notes

**Course**: [Efficiently Serving LLMs](https://www.deeplearning.ai/short-courses/efficiently-serving-llms/)

- Decoder Models -> Autoregressive Models
  - All past tokens are used to predict next token which is why it is called autoregressive language model
  - [x0, x1, ... xk] -> Embedding -> Attention -> MLP -> LM Head -> x(k+1)
