This exercise will use [Flowise hosted on Hugging Face](https://cheeweeng.github.io/Setup-Flowise-on-Hugging-Face/) to build a RAG (Retrieval-Augmented Generation) using LangChain.  
A RAG (Retrieval-Augmented Generation) pipeline in LangChain connects your data to a language model through a structured flow. Documents are loaded, split, converted into embeddings, and stored in a vector database, which is then accessed via a VectorDB QA Chain to retrieve relevant context for a user’s query. This retrieved information is passed to a chat model (e.g., OpenAI GPT) along with the question to generate a grounded answer. By combining retrieval with generation, RAG improves accuracy and allows the model to use up-to-date or private knowledge.  

### Load your data and text chunking  

<table>
  <tr>
    <td width="40%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/feb1c0f2-9dbb-44b4-92f8-56956e0d69f4" width="100%"/>
    </td>
    <td width="60%" valign="top">
      <ul>
        <li>LangChain has document loader nodes that read PDFs, text files, webpages, etc. into a usable format.</li>  <p></p>
        <li>Use the <b>Recursive Text Splitter</b> node to break large documents into smaller chunks. This makes searching faster and more accurate.</li>
      </ul>
    </td>
  </tr>
</table>

### Convert to embeddings  

<table>
  <tr>
    <td width="35%" valign="top" align="center">
      <img src="https://github.com/user-attachments/assets/eebfe822-a5b3-43fa-88e0-790e0422e9fd" width="100%"/>
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


<img width="600" height="520" alt="Image" src="https://github.com/user-attachments/assets/37ad3f09-5107-4704-9820-0d7bdde08880" />

<img width="1260" height="852" alt="Image" src="https://github.com/user-attachments/assets/797a2c50-ca21-48d8-a67f-6453978bc224" />
