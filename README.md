# ===============================
# Required Packages (pip install)
# ===============================
# pip install streamlit
# pip install langchain
# pip install ollama

import streamlit as st
from langchain.llms import Ollama
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory

# Initialize LLM using Ollama local model
def get_llm():
    return Ollama(model="llama3")  # Make sure llama3 or any other model is available locally in Ollama

# Setup conversation memory and chain
def create_conversation_chain():
    llm = get_llm()
    memory = ConversationBufferMemory()
    return ConversationChain(llm=llm, memory=memory)

# Streamlit UI
def main():
    st.title("🧠 Local Chatbot with Ollama + Streamlit")
    st.markdown("This chatbot runs entirely locally using Ollama. No external API needed.")

    if "chain" not in st.session_state:
        st.session_state.chain = create_conversation_chain()
        st.session_state.chat_history = []

    user_input = st.text_input("You:", placeholder="Ask anything...", key="user_input")

    if user_input:
        response = st.session_state.chain.run(user_input)
        st.session_state.chat_history.append((user_input, response))

    if st.session_state.chat_history:
        for i, (q, a) in enumerate(reversed(st.session_state.chat_history)):
            st.markdown(f"**You:** {q}")
            st.markdown(f"**Bot:** {a}")

if __name__ == "__main__":
    main()

✅ Your **local chatbot** is ready using:

- 🧠 **Ollama** (e.g., LLaMA 3 or other local model)
- 🌐 **Streamlit UI**
- 🧩 **Langchain** for conversational memory
- 🔒 **No external API**

---

### 🚀 How to Run This Chatbot

1. **Start Ollama model** (e.g., LLaMA 3):
```bash
ollama run llama3
```

2. **Install requirements**:
```bash
pip install streamlit langchain ollama
```

3. **Run the app**:
```bash
streamlit run your_chatbot.py
```
