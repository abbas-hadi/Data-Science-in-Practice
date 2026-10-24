# Economic Development Strategies

Indiana University, DSCI-D 592 Data Science in Practice, Fall 2023 (team of eight)

## Problem

The U.S. Economic Development Administration (EDA) requires a Comprehensive Economic Development Strategy (CEDS) before a region can receive implementation grants or keep its Economic Development District (EDD) status. EDDs are multi-county regions, and many of them in rural areas, tribal lands and inner cities don't have the staff to write a strong CEDS. Our sponsor asked whether generative AI could help these regions draft one from public data and existing plans.

## Approach

1. **Prompting general models:** we asked GPT-3.5 and Bard the sponsor's CEDS questions for a real region.
2. **Retrieval-augmented generation (RAG):** we built a pipeline that grounds the model's answers in source documents and cites the passages it used, so its output reflects a region's actual plans rather than generic advice.

## Test region

We tested the models on a nine-county region in Southeastern Indiana: Dearborn, Decatur, Franklin, Jefferson, Jennings, Ohio, Ripley, Shelby and Switzerland counties. That's the area covered by the Southeastern Indiana Regional Planning Commission's [2020 CEDS](https://www.sirpc.org/images/pdfs/CEDS-SIRPC_2020_Final_for_EDA.pdf). Prompts gave each model the region's leading industries, chosen by location quotient (manufacturing, healthcare, agriculture), and its main workforce skills.

## Findings

- **GPT-3.5 beat Bard.** It tailored some answers to Indiana, such as natural disaster risks, though most of its answers were still generic.
- **Bard's answers were generic.** It drew on patterns common to other CEDS and didn't reflect the region's own trade, agriculture and manufacturing situation.
- **RAG works best.** Grounding answers in source documents made them more accurate and traceable.
- **Inconsistent document formats are the main blocker.** CEDS layouts vary from region to region, which limits what retrieval can find. Converting them to a standard format would help future teams.

## Files

| File | What it is |
| --- | --- |
| `RAG.ipynb` | RAG pipeline: loads a folder of PDFs, splits them into 1,000-character chunks with 200-character overlap, embeds them with OpenAI embeddings into a Chroma vector store, and answers questions with source citations. Shown here on a sample PDF set. |
| `Bard vs GPT 3.5.docx` | Side-by-side answers from both models to the sponsor's CEDS questions for the Southeastern Indiana region |
| `Economic Development Strategies Report.pdf` | Final report: problem, approach, findings and recommendations |
| `Full Statement from Sponsor Fall 2023.docx` | Sponsor's challenge statement and CEDS requirements |

## Data sources

- [EDA CEDS guidelines](https://www.eda.gov/resources/comprehensive-economic-development-strategy)
- [Southeastern Indiana Regional Planning Commission 2020 CEDS](https://www.sirpc.org/images/pdfs/CEDS-SIRPC_2020_Final_for_EDA.pdf)
- Additional CEDS documents provided by the sponsor

## Tools

Python, LangChain, Chroma, OpenAI embeddings and GPT-3.5, Google Bard, PyPDF
