# Yabble Theme Counting Test - Walmart Survey Analysis

This repository contains a thematic analysis solution for Yabble's coding assessment, focusing on identifying themes and patterns in Walmart customer feedback survey data using advanced NLP techniques.

##  Project Overview

### What is Thematic Analysis?
Thematic analysis is a qualitative research method that systematically identifies, analyzes, and reports patterns (themes) within data. In market research, it helps organizations understand customer opinions, sentiments, and experiences by:

- **Identifying recurring patterns** in customer feedback
- **Systematically coding responses** into meaningful categories  
- **Deriving actionable themes** that inform business decisions
- **Creating narratives** that explain customer behavior and preferences

### Business Problem
Given customer survey responses about Walmart vs Target, we need to:
1. Identify the main themes in customer complaints about Walmart
2. Understand what customers think Target does better than Walmart
3. Discover what customers love about Walmart
4. Provide actionable insights for business improvement

##  Dataset

**Source**: `Data/raw/walmart.csv`
- **Total Responses**: 253 survey participants
- **Geographic Scope**: Texas only
- **Demographics**: Mixed age groups (18-74), gender diverse
- **Preference Split**: 174 prefer Walmart, 79 prefer Target

### Survey Questions Analyzed:
1. **Walmart Complaints**: "What would you complain about regarding Walmart?"
2. **Target Advantages**: "What do you think Target does better than Walmart?"
3. **Walmart Positives**: "What do you love about Walmart?"

### Demographic Breakdown:
- **Gender**: Female (143), Male (109), Gender diverse (1)
- **Age Groups**: 45-54 (53), 25-34 (50), 35-44 (43), 18-24 (39), 55-64 (34), 65-74 (27)
- **State**: Texas (253)

##  Technical Approach

### Methodology: BERTopic for Theme Discovery

**Why BERTopic?**
- Uses state-of-the-art BERT embeddings to understand semantic meaning
- Automatically discovers optimal number of topics
- Handles small datasets better than traditional LDA
- Provides interpretable topic representations with keywords

### Analysis Pipeline:

>  **Workflow Diagram**: View the complete analysis pipeline in [Excalidraw format](./thematic-analysis-workflow.excalidraw)

**Detailed Steps:**

1. **Data Preprocessing**
   - Text normalization (lowercase, punctuation removal)
   - Tokenization using NLTK
   - Stop word removal
   - Lemmatization for word root extraction

2. **Embedding Generation**
   - Used `all-MiniLM-L6-v2` sentence transformer model
   - Converts text to high-dimensional semantic vectors
   - Captures contextual meaning beyond keyword matching

3. **Topic Clustering**
   - HDBSCAN clustering to group similar responses
   - Automatic outlier detection (Topic -1)
   - C-TF-IDF for meaningful topic representation

4. **Visualization & Interpretation**
   - Interactive topic maps and bar charts
   - Representative documents for each topic
   - Keyword extraction for easy interpretation



##  Key Findings

### Walmart Complaint Themes (6 Main Topics)

| Topic | Count | Theme | Key Issues |
|-------|--------|--------|------------|
| **0** | 46 | **Checkout & Staffing** | Long lines, insufficient cashiers, self-checkout problems |
| **1** | 39 | **Poor Customer Service** | Rude staff, poor treatment, unhelpful employees |
| **2** | 26 | **General Service Issues** | Broad customer service complaints |
| **3** | 26 | **Vague Complaints** | Uncertain or non-specific feedback |
| **4** | 18 | **Product Quality** | Fresh food quality, meat, produce pricing |
| **5** | 11 | **Store Cleanliness** | Dirty stores, poor maintenance, bathroom issues |

### Target's Competitive Advantages (3 Topics)

| Topic | Count | Theme | Advantages |
|-------|--------|--------|------------|
| **-1** | 55 | **Overall Quality** | Better products, quality, customer experience |
| **0** | 14 | **Store Experience** | Better store feel, atmosphere, real cashiers |
| **1** | 10 | **Organization & Cleanliness** | More organized, cleaner, helpful employees |

##  Setup Instructions

### Environment Setup

1. **Create Conda Environment**:
```bash
conda create -n yabble-theme python=3.11
conda activate yabble-theme
```

2. **Install Core Packages**:
```bash
conda install pandas numpy scikit-learn matplotlib seaborn jupyter nltk plotly
```

3. **Install NLP Packages**:
```bash
pip install sentence-transformers transformers bertopic hdbscan umap-learn
```

4. **Download NLTK Data**:
```python
import nltk
nltk.download('punkt')
nltk.download('stopwords') 
nltk.download('wordnet')
```

### Running the Analysis

1. **Open Jupyter Notebook**:
```bash
jupyter notebook theme-counting.ipynb
```

2. **Run All Cells**: Execute cells sequentially to reproduce the analysis

3. **View Results**: Interactive visualizations will display topic maps and charts

##  Project Structure

```
yabble-theme-counting-test/
├── README.md                                 # This documentation
├── theme-counting.ipynb                      # Main analysis notebook
├── thematic-analysis-workflow.excalidraw     # Process flow diagram
├── Data/
│   ├── raw/
│   │   └── walmart.csv                       # Original survey data
│   └── processed/                            # Processed datasets
├── articles/                                 # Reference materials
└── .gitignore                               # Git ignore rules
```

##  Business Insights & Recommendations

### Priority Action Items for Walmart:

1. **Immediate (High Impact)**:
   - **Staffing**: Add more cashiers during peak hours
   - **Training**: Implement customer service training program
   - **Checkout**: Improve self-checkout user experience

2. **Medium-term**:
   - **Store Maintenance**: Enhance cleaning protocols
   - **Product Quality**: Improve fresh food supply chain
   - **Store Layout**: Learn from Target's organization approach

3. **Long-term**:
   - **Brand Positioning**: Address overall customer experience gap with Target
   - **Employee Culture**: Foster more helpful, friendly staff culture

### Competitive Intelligence:
- Target's main advantage is **perceived quality and cleanliness**
- Walmart can compete by focusing on **operational excellence** in these areas
- Customer service training could significantly impact satisfaction

##  Technical Notes & Limitations

### Challenges Encountered:
- **Small Dataset**: Only 79 responses for Target comparison question
- **Visualization Errors**: IndexError with small topic counts - solved with fallback to bar charts
- **Geographic Bias**: Data only from Texas - may not generalize nationally

### Model Improvements:
- **Sentiment Analysis**: Could add positive/negative sentiment to each theme
- **Demographic Analysis**: Explore theme variations by age/gender
- **Temporal Analysis**: Track theme evolution over time

### Validation Approach:
- Manual review of topic assignments for accuracy
- Representative document analysis for topic coherence
- Cross-validation with traditional survey analysis methods

##  References & Inspiration

- [Sentence Transformers Documentation](https://sbert.net/) - Official documentation for the embedding models used in this analysis
- [BERTopic Documentation](https://maartengr.github.io/BERTopic/)
- [Thematic Analysis in Qualitative Research](https://fastercapital.com/content/Thematic-Analysis--Uncovering-Patterns--Thematic-Analysis-in-Qualitative-Research.html)
- [BERT: Pre-training of Deep Bidirectional Transformers](https://arxiv.org/abs/1810.04805)
- [HDBSCAN Clustering Algorithm](https://hdbscan.readthedocs.io/)
- [Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/abs/1908.10084) - Original paper behind Sentence Transformers
- [Excalidraw](https://excalidraw.com/) - Used for creating the workflow diagram visualization

##  Conclusion

This analysis successfully demonstrates how modern NLP techniques can automate traditional market research tasks while providing deeper insights than manual coding. The BERTopic approach identified actionable themes that align with business priorities and competitive positioning.

**Key Success Factors**:
- ✅ Automated theme discovery with minimal manual intervention
- ✅ Interpretable results with clear business implications  
- ✅ Scalable approach for larger datasets
- ✅ Robust handling of small dataset 
