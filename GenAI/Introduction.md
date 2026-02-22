---

---
#agentic #genai 
# Generative AI
---
- **Discriminative AI**: Model distinguishes between different classes of data. Example: Email spam filter (spam vs. not spam). These are best suited for classification tasks, they cannot understand context and cannot generate new content.
- **Generative AI**: Generates new content based on the training data. It starts with a prompt (text, image, video etc.) and generates new content.

Creative skills of Generative AI comes from the following, which can be considered as the building blocks of Generative AI:
- GANs (Generative Adversarial Networks)
- VAEs (Variational Autoencoders)
- Transformers
- Diffusion Models

**Foundation Models** are AI models with *broad* capabilities, and can be used to build specialized or advanced models. These models have undergone unsupervised learning on huge amounts of data. Foundation Models are part of Generative AI models, as we are generating or predicting the next word or text. If we introduce small amount of labeled data, we can use Foundation Models to perform NLP tasks - this process is called *Tuning*. 

**LLMs (Large Language Models)** are a special category of Foundation Models that are trained to understand human language, and can *process and generate text*. OpenAIs GPT, Meta's Llama, Googles PaLM are some examples of LLMs.

**Natural Language Processing**: Natural language is unstructured to a computer: we convert it to a structured format that a computer can understand. NLP sits between structured and unstructured text and it's job is to translate between the two.
- Unstructured to Structured is called *Natural Language Understanding*
- Structured to Unstructured is called *Natural Language Generation*

Below are the steps involved in NLP:
1. *Tokenization*: Break unstructured text into tokens, we then work one token at a time
2. *Stemming*: Derive the word stem for a given token. For example, `Run,Runs, Ran ` the word stem is `Run` . Stemming doesn't work well for each token, for example, `Universal` and `University` do not stem down to `Universe`. For such situations, we have *Lemmatization*: takes a given token, learns it's meaning through a dictionary definition, and then derive it's root.
3. *Part of speech tagging*: Determine where the token is being used within the context of a sentence.
4. *Named Entity Recognition*:  For a given token, is there a NER associated with it? For example, for `Arizona` , is there an entity of `US State`

Once we have structured data after the above steps, we can apply it to various AI applications.

# In-Context Learning and Prompt Engineering
---
**In-Context Learning**: It's a method of *Prompt Engineering*, where demonstration of the task is provided to the LLM as part of the prompt in natural language. 
A new task is learned from a small set of examples presented within the context at inference time - no additional training is required.

**Prompt Engineering**: Prompts are instructions provided to the LLM as an input, guiding it to perform a specific task. A prompt has following components:
1. **Instructions**: Clear, direct commands that tell the LLM what to do. They need to be specific to ensure the LLM understands the task. Example: `Classify the following customer feedback into neutral, negative or positive sentiment` .
2. **Context**: Information that helps LLM make sense of the instructions. Example: `This review is part of feedback for a recently launched product`
3. **Input Data**: This is the actual data that the LLM will process. Example: this is where we would provide the customer feedback, `The product arrived late, but the quality exceeded my expectations`.
4. **Output Indicator** is the part of the prompt where LLMs response is expected.

> *Prompt Engineering* is the process of defining and refining the prompts to communicate with LLMs. Goal is to how to prompt in the best way possible: crafting prompts to elicit accurate, relevant and contextually appropriate responses. It directly influences the effectiveness and accuracy of LLMs.

# Prompt Engineering Methods
---
## Zero-Shot Prompt

It instructs an LLM to perform a task without giving any examples. It requires the LLM to understand the context without any previous tuning.
## One-Shot Prompt

It gives the LLM a single example to help it perform a *similar* task. Below is an example:

```text
Translating a sentence from English to French:
English: "How is the weather today?"
French: "Comment est le temps aujourd' hui?"

Now, translate the following sentence from English to French:
English: "Where is the nearest supermarket?"
```

## Few-Shot Prompt

Here, the LLM learns from a small set of examples before tacking a similar task to generalize from a few instances to new data.

```text
Here are a few examples of classifying emotions in statements:
Statement: "I just won my first marathon!"
Emotion: Joy

Statement: "I can't believe I lost my keys again."
Emotion: Frustration

Statement: "My friend is moving to another country."
Emotion: "Sadness"

Now, classify the emotion in the following statement:
Statement: "Thaht movie was so scary, I had to cover my eyes."
```

## Chain-of-Thought (CoT) Prompting


Here, we guide the LLM through complex reasoning in a *step-by-step* manner.

> This method is effective where solution requires multiple intermediate steps or reasoning that mimics human thought process.


```text
Consider the problem: A store has 22 apples. They sold 15 apples today and got a new delivery of 8 applies. How many apples are there now?

Break down each step of your calculation.
```

## Self-Consistency

It is used to enhance the reliability and accuracy of outputs. Here we generate multiple independent answers to the same question, and evaluate these to determine the most consistent result.

```text
When I was 6, my sister was half my age. Now I am 70, what age is my sister?
Provide three independent calculations and explanations, then determine the most consistent result.
```



