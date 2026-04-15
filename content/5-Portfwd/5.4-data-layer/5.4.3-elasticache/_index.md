---
title: "Bedrock Knowledge Base"
weight: 3
chapter: false
pre: " <b> 4.4.3. </b> "
---
1. **Upload data (PDF)** to the `rag-data` bucket.
2. Open the **Amazon Bedrock console**.

![Networking Session](/AWS_Intern-Report/images/picture1.jpg)

3. **Choose Knowledge Base:** Click *Create Knowledge Base*.

![Networking Session](/AWS_Intern-Report/images/picture2.jpg)

4. **General Configuration:**

![Networking Session](/AWS_Intern-Report/images/picture3.jpg)

   - **Data source name:** Enter `RAG-data`.
   - **S3 URL:** Choose the file uploaded to the bucket in Step 1.
5. **Parsing strategy:** Choose *Amazon Bedrock default parser*.
6. **Chunking strategy:** Choose *Semantic chunking*.
7. **Choose embedding model:** Select your preferred model.

![Networking Session](/AWS_Intern-Report/images/picture4.jpg)

8. **Vector store:**
   - Choose *Quick create a new vector store*.
   - **Vector store type:** Choose *Amazon S3 vector*.
9. Click **'Create knowledge base'**.
10. Choose knowledge base created and click sync
![Networking Session](/AWS_Intern-Report/images/knowledgebase.png)
