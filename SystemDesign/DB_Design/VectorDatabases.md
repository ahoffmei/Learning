# Vector Databases 

Sources: 
- [pinecone article](https://www.pinecone.io/learn/vector-database/)
- [beginner friendly guide](https://www.dailydoseofds.com/a-beginner-friendly-and-comprehensive-deep-dive-on-vector-databases/)

# Overview
A vector database indexes and stores vector embeddings (typicall generated from unstructured data) for fast retrieval and similarity search, with capabilities like CRUD operations, metadata filtering, horizontal scaling, and serverless. Highly involved in large language models, generative AI, and semantic search. Also used in recommendation systems and search engines. 

Embedding Generation: 
<img src="https://www.dailydoseofds.com/content/images/size/w1600/2024/02/image-160.png" alt="Description of the image">

Architectural overview: 

<img src="https://www.pinecone.io/_next/image/?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Fvr8gru94%2Fproduction%2Fe88ebbacb848b09e477d11eedf4209d10ea4ac0a-1399x537.png&w=3840&q=75" alt="Description of the image">

# Embeddings 
This numerical vector is called an embedding, and the model is trained in such a way that these vectors capture the essential features and characteristics of the underlying data.

## Example Use Case 
Say we have a bunch of images (say landscapes), we can convert those images to embeddings. Then, when we search google images for "mountain ranges," what we're doing behind the scenes in converting that text input to a vector. We are then checking the vector database for landscapes that have similar characteristics. 

## Static Embeddings 
This is what we started with in a "pre-Transformers era". Use deep learning across a bjillion words and convert them into vectors. 

Good for operations like: 
(King - Man) + Woman = Queen 

But bad in cases like: 
1. "Format Excel <b>Table</b>"
2. "Dining Room <b>Table</b>"

Here "Table" is searched for in the same context for static embedding.
<img src="https://www.dailydoseofds.com/content/images/2024/02/image-174.png" alt="Description of the image"> 

### Transformers 
Two big transformers were invented for solving the problem discussed above. 

- **BERT** (Biridectional Encoder Representation from Transformers): Language Model 
  - Masked Language Modeling (**MLM**): Predict missing word in sentence given surrounding words 
  - Next Sentence Prediction (**NSP**): Given two sentences from a document, determine if they are randomly paired or sequential. 
  - Basically creates a contextualization model to group word usage. 
- **SentenceTransformer**: Creates embedding for sentences rather than individual words. 

## Freshness 
<img src="https://www.pinecone.io/_next/image/?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Fvr8gru94%2Fproduction%2F599081cb02fc876b4f0b52ba56520ca70f86531b-2164x1290.png&w=3840&q=75" alt="Description of the image">


# Algorithms 

## Aproximate Nearest Neighbor (ANN)
We could look for "exact" nearest neighbors (KNN or "K-Nearest Neighbors"), but that's computationally expensive. We sacrifice some percision for speed with ANN. 

### Flat Index 
Used for KNN I think? Idk this one sucks tho only good for smol dataset. 

### Inverted File Index (IVF): 
Idea is to organize vectors into partitions. Each partition designates a "centroid" that associates with the partition. We query by looking for a centroid. 

<img src="https://www.dailydoseofds.com/content/images/size/w1600/2024/02/image-191.png" alt="Description of the image">

## Vector Compression (Product Quantization)
So say we have a 256 dimension where each dimension is represented by a 32 bit integer. 

1. Split: Separate the 256 dimensions into say 8 segments. We get eight 32 dimensional sub-vectors. 
2. Train: Run k-Means, generating k centroids for each sub-vector/segment. 
3. Encode: TODO we somehow use the generated centroids to turn all 32 dimensional sub-vector into a 1-dimensional compressed version, containing centroid_ids that are based on the calculated centroids. 

# Using ANN with an Input Query Vector Post Compression 
Okay so question now is, now that we know how the vectors are compressed with PQ, how do we actually search using ANN. 
1. Break your 256 dim vector into the same number of sub-vectors (last example used 8 to make 32 dim vectors).
2. Perform the same K-Means step we did before. 
3. Create a distance matrix using the calculated "K-Means"

Generate `k` by `Dimensions` Sized Vector 
<img src="
https://www.dailydoseofds.com/content/images/size/w1600/2024/02/image-217.png" alt="Description of the image">

Distance Vector: 
<img src="
https://www.dailydoseofds.com/content/images/size/w1600/2024/02/image-218.png" alt="Description of the image">

1. Missing some details here so TODO, but basically we calculate the distance to the closest centroid given our current distance vector. This is an approximate calculation. 

## Random Projections (Pinecone Specific?)


<img src="https://www.pinecone.io/_next/image/?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Fvr8gru94%2Fproduction%2F22dffa542410c1b542fcaeafcafc088ad278add5-1303x534.png&w=3840&q=75" alt="Description of the image">

TLDR; Uses vector projections across a randomly generated matrix to determine the nearest neighbrors. Approximate method. 