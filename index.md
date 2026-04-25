This exercise will use [Flowise hosted on Hugging Face](https://cheeweeng.github.io/Setup-Flowise-on-Hugging-Face/) to build a RAG (Retrieval-Augmented Generation) using LangChain.  
A RAG (Retrieval-Augmented Generation) pipeline in LangChain connects your data to a language model through a structured flow. Documents are loaded, split, converted into embeddings, and stored in a vector database, which is then accessed via a VectorDB QA Chain to retrieve relevant context for a user’s query. This retrieved information is passed to a chat model (e.g., OpenAI GPT) along with the question to generate a grounded answer. By combining retrieval with generation, RAG improves accuracy and allows the model to use up-to-date or private knowledge.  

### Load your data and text chunking  

<table>
  <tr>
    <td width="40%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/cdda123e-2864-4417-b661-1ad02ec3fe79" width="100%"/>
    </td>
    <td width="60%" valign="top">
      <ul>
        <li>LangChain has document loader nodes that read PDFs, text files, webpages, etc. into a usable format. In this setup, I have uploaded a LTA Sustainability Report 2024/2025 using a standard PDF loader. </li>  <p></p>
        <li>Caveat: A standard PDF loader may struggle with tables and ignore images.</li><p></p>
        <li>Use the <b>Recursive Text Splitter</b> node to break large documents into smaller chunks. This makes searching faster and more accurate.</li>
      </ul>
    </td>
  </tr>
</table>

### Convert to embeddings  

<table>
  <tr>
    <td width="35%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/eebfe822-a5b3-43fa-88e0-790e0422e9fd" width="90%"/>
    </td>
    <td width="65%" valign="top">
      <ul>
        <li>Each chunk is turned into a numerical representation using embedding models. There are many embedding models available (e.g., OpenAI embeddings). In this RAG, I am using <b>GoogleGenerativeAI Embedding</b>. Connect with a Google Gemini API key, choose the embedding model, and select <b>RETRIEVAL DOCUMENT</b> for task type.</li><p></p>
        <li>A point to take note: by default, newer Google models like <b>gemini-embedding-001</b> or <b>gemini-embedding-2</b> output <b>3072 dimensions</b>. Therefore, when creating the Pinecone index, the dimension must match accordingly.</li>
      </ul>
    </td>
  </tr>
</table>

### Store in a vector database 
<table>
  <tr>
    <td width="65%" valign="top">
      <p>
           <li>Store those embeddings in a vector database like <b>Pinecone</b>. This is where your “knowledge base” lives. For free tier accounts, Pinecone allows a maximum of <b>five indexes</b>.</li>
      </p>
      <p>
           <li>In this step, prepare your <b>Pinecone API key</b> and the <b>index name</b> created in your Pinecone account.</li>
      </p>
    </td>
    <td width="35%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/82535f9a-0eff-4841-b75b-e556da413c49" width="70%"/>
    </td>
  </tr>
</table>

### Retrieval and Generation  
<table>
  <tr>
    <td width="40%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/37ad3f09-5107-4704-9820-0d7bdde08880" width="100%"/>
    </td>
    <td width="60%" valign="top">
      <p>
         <li>The <b>VectorDB QA Chain</b> will access the vector store to retrieve relevant context for a user’s query.</li>
      </p>
      <p>
        <li>This retrieved information is passed to a chat model along with the question to generate a grounded answer. In this RAG setup, I utilized the <b>ChatOpenRouter API</b> endpoint via its dedicated node, allowing access to various free models without incurring API costs.</li>
      </p>
    </td>
  </tr>
</table>

### The complete RAG Chain
<img width="1000" height="750" alt="Image" src="https://github.com/user-attachments/assets/797a2c50-ca21-48d8-a67f-6453978bc224" />  

### Interface  
Once the RAG is completed, you can test the chatbot inside the flowise editor. After that, the final step is to move the chatbot out of the Flowise editor and into a real-world interface.  
There are several options available, you can embed the chatbot as a popup widget on any website or share the chatbot link with others.   
Share Chatbot creates a standalone, hosted webpage just for that specific bot.   
I will use the share chatbot link to make a quick [video demo of this RAG chatbot](https://youtu.be/ZaYb0DcJTag).
<p></p>
<img width="700" height="380" alt="image" src="https://github.com/user-attachments/assets/9e7d5ec5-ae77-4d70-9250-e42ed93a99c2" />

### Pro-Tips for a $0 RAG Build  
My goal is a totally free development environment, here is the "Golden Stack" for 2026 provided by Gemini 3:  
<img width="700" height="280" alt="image" src="https://github.com/user-attachments/assets/a624eb84-77b2-4f97-9d0e-eecbc7d0479e" />

This post is not sponsored and there are no affiliate links.  

Back to [Projects portfolio](https://cheeweeng.github.io/)
