# Conspiratorial Narratives At Scale

We release the annotation code book and dataset for the following paper.
If you use this dataset or refer to its results, please cite:
> Diab, Ahmad, Rr Nefriana, and Yu-Ru Lin. "Classifying Conspiratorial Narratives At Scale: False Alarms and Erroneous Connections.". *AAAI International Conference on Weblogs and Social Media (ICWSM)*, 2024. \[[paper](https://arxiv.org/abs/2404.00141)\]

## Code Book
File: _"CT coding guideline - ICWSM24.pdf"_.
We share the guidelines and instructions followed to obtain the golden label for the dataset.


## Dataset
We release the metadata of the Reddit posts used in this paper. To adhere to Reddit's terms of service, we only share the IDs and links to the collected posts without the actual content (i.e. title, text, etc).

### CT_labeled_dataset_ids.xlsx
Each line contains information regarding a single post from Reddit and its label (CT or Not) obtained via different methods. Attributes are:

* id: Unique identifier for the post on Reddit
* URL: Link to the post on the Reddit platform
* subreddit: Name of the subreddit from which the post was taken
* label: The golden label assigned to the original post by annotators
* Prediction (RoBERTa): Label assigned to the post by the RoBERTa model
* GPT (Simple Prompt) Label: Label assigned to the post by GPT when a simple prompt was used (yes/no answer only)
* GPT (Justification) Label: Label assigned to the post by GPT when a decision justification was requested
* GPT Justification: The justification provided by GPT for the selected label

### most_similar_10samples_ids.xlsx
In one of the experiments, we used context learning with GPT, a technique that augments the LLM prompt with helpful content to enhance the quality of the generative output. To engineer each prompt, we selected the most similar N samples labeled as positive (CT) and the most similar N samples labeled negative (non-CT) and concatenated them before asking GPT for the correct label of a post. The text similarity was calculated using the cosine-similarity metric on RoBERTa embeddings of all posts. The closest samples to each post are listed in this file. Attributes:

* index: Local sequential index assigned to each record, starting from 0
* id: Unique identifier for the post on Reddit
* label: The golden label assigned to the original post by annotators
* closest_pos_samples_indx: Indices of the 10 positive (labeled as "Yes") samples most similar to the current post
* closest_neg_samples_indx: Indices of the 10 negative (labeled as "No") samples most similar to the current post
* similarity_score_pos_samples: Similarity scores indicating the degree of similarity between the post and the 10 closest positive samples
* similarity_score_neg_samples: Similarity scores indicating the degree of similarity between the post and the 10 closest negative samples


## Model
We released the best-performing model trained on the labeled dataset. It is a RoBERTa-base variant, fine-tuned on an Nvidia GTX Titan X using a lr=1e-5, batch-size=24, and settings for the remaining parameters.
Google drive link to model: https://drive.google.com/file/d/1vvAaBEwkTEMDAMvg3Z85mCOYoqembSFL/view?usp=sharing
