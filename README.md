
# 🧠 Chatbot with LangChain & LangGraph

A minimal yet extendable chatbot built using **LangChain** and **LangGraph**, leveraging OpenAI’s GPT model for conversational interactions and memory persistence.

---

## 🔍 Features

- **Stateful Conversations** via `ConversationBufferMemory`
- **Graph-Based Flow** using LangGraph's `StateGraph`
- **LLM-Powered Responses** powered by `ChatOpenAI`
- **Modular and Extensible** architecture for easy future additions

---

## 🗂️ Project Structure

```

chatbot\_langchain\_langgraph/
├── basicChatBot/
│   └── basic1.py         # Core chatbot implementation with LangChain & LangGraph
├── requirements.txt      # Project dependencies
└── README.md             # This documentation

````

---

## 📦 Dependencies

Dependencies listed in `requirements.txt`:

```txt
langgraph==0.0.34
langchain==0.2.0
openai==1.30.1
````

Install them using:

```bash
pip install -r requirements.txt
```

Also, set your OpenAI credentials:

```bash
export OPENAI_API_KEY="your-api-key"
```

---

## 🧠 How It Works

1. **Define memory and graph schema**

   * Uses `ConversationBufferMemory` to track conversation history.
   * Creates a `StateGraph` with schema `MessagesState`.

2. **Define chat node**

   * `respond` — calls `ChatOpenAI` to generate a reply.
   * `final` — an optional placeholder node.

3. **Create graph flow**

   * Connects `START → respond → final → respond...` for a cyclic chat flow.

4. **Compile the graph**

   * `graph = StateGraph(...).compile(checkpointer=memory)` returns a runnable app.
   *  ![image](https://github.com/user-attachments/assets/51d26d2e-c5b6-480c-8bb6-873bafb5f450)



5. **Invoke chat**

   * Use `graph.invoke({"messages": [...]})` to send user messages and receive replies.

---

## 💻 Example Usage

```python
from basicchatbot.basic1 import graph

response=graph.invoke({"messages" : "Can you teach me about langChain ? "},config=config)

# `result["messages"][-1]` is the assistant's reply
print(result["messages"][-1].content)
```

---

## 🚀 Future Enhancements

* 🛠️ Add tools (e.g., calculators, search, APIs)
* 🌐 Integrate with a web or UI interface
* 📊 Implement branching logic in the graph
* 👥 Support multi-user conversations via thread IDs

---
