# Rag_system
1.Setup Guide:
           Clone repo
           Run pip install -r requirements.txt
           Set GOOGLE_API_KEY environment variable with Gemini API key
           Upload HSC26_Bangla1stPaper.pdf to project folder
           Run python main.py
2. Tools / Libraries Used:
           PyMuPDF (fitz) --	PDF text extraction
           re	Basic -- text cleaning
           LangChain --	Text chunking (RecursiveCharacterTextSplitter)
           SentenceTransformers --	Embedding multilingual text for semantic search
           FAISS --	Efficient vector similarity search
           Google Gemini API --	Large language model for answer generation

3. Sample Queries & Outputs
Question (Bangla)	Expected Answer
অনুপমের ভাষায় সুপুরুষ কাকে বলা হয়েছে?	শুম্ভুনাথ
কাকে অনুপমের ভাগ্য দেবতা বলে উল্লেখ করা হয়েছে?	মামাকে
বিয়ের সময় কল্যাণীর প্রকৃত বয়স কত ছিল?	১৫ বছর

4. Must Answer Questions
Q: What method or library did you use to extract the text, and why? Did you face any formatting challenges with the PDF content?
A: Used PyMuPDF (fitz) for accurate, fast extraction of text from PDF pages. PDF formatting was sometimes inconsistent with line breaks and spacing, so cleaned text with regex (re.sub) to normalize newlines and spaces.

Q: What chunking strategy did you choose (e.g. paragraph-based, sentence-based, character limit)? Why do you think it works well for semantic retrieval?
A: Used LangChain’s RecursiveCharacterTextSplitter with 500 character chunks and 100 character overlap. This balances chunk size to capture meaningful semantic units without losing context, improving embedding quality and retrieval relevance.

Q: What embedding model did you use? Why did you choose it? How does it capture the meaning of the text?
A: Used paraphrase-multilingual-MiniLM-L12-v2 from SentenceTransformers. This model is optimized for multilingual semantic similarity tasks, effectively embedding Bengali and English text into a shared vector space capturing meaning.

Q: How are you comparing the query with your stored chunks? Why did you choose this similarity method and storage setup?
A: Used FAISS with L2 distance to compare dense vector embeddings of query and chunks. FAISS provides fast approximate nearest neighbor search, essential for scalable retrieval in large document collections.

Q: How do you ensure that the question and the document chunks are compared meaningfully? What would happen if the query is vague or missing context?
A: Semantic embeddings help match related concepts even if wording differs. However, vague or context-poor queries might retrieve less relevant chunks, reducing answer accuracy. Improving chunk size or adding query context can mitigate this.

Q: Do the results seem relevant? If not, what might improve them (e.g. better chunking, better embedding model, larger document)?
A: Results are generally relevant, but can improve by:
  Using larger or domain-specific embedding models
  Better chunking (e.g. semantic or sentence-based)
  Increasing document corpus size for richer knowledge
  Implementing feedback loops or relevance tuning

