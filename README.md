# Automated Bioactive Peptide Literature Search and MBPDB Updates

## Overview

This project develops an automated system for searching biomedical literature to identify milk-derived bioactive peptides for incorporation into the Milk Bioactive Peptide Database (MBPDB). The system queries UniProt and PubMed APIs to extract peptide sequences, biological functions, and reference information, then compares findings with the existing MBPDB to identify novel peptides.

## Project Purpose

The primary goal is to automate the discovery and documentation of bioactive peptides from milk proteins, reducing manual research time and enabling regular database updates. The system:

- **Searches UniProt** using protein IDs from known milk proteins
- **Queries PubMed** for relevant literature and reference metadata
- **Extracts and associates** peptide sequences with their biological functions
- **Compares results** with existing MBPDB entries to identify novel peptides
- **Assists researchers** with AI-powered text extraction and summarization for bioactivity assessment

## Project Structure

```
uniprot/
├── UniProt Peptide Search.ipynb    # Main Jupyter notebook - demo workflow
├── requirements.txt                 # Python dependencies
├── README.md                        # This file
├── Project Overview.docx            # Detailed project documentation
│
├── data/                            # Output data files
│   ├── exported_data.tsv           # MBPDB exported data
│   ├── reff_merged_final_df.csv    # Peptides with references
│   ├── no_reff_merged_final_df.csv # Peptides without references
│   └── *.csv                        # Various processed datasets
│
├── protein_lists/                    # Protein ID lists
│   ├── HumanMilkProteinDatabase_v2.fasta
│   ├── CowMilkProteinDatabase_v2.fasta
│   └── *.tsv, *.txt                 # Additional protein lists
│
├── xml_examples/                    # Example XML files from UniProt/PubMed
│   └── *.xml                        # Sample API responses
│
└── venv/                            # Python virtual environment
```

## Installation

### Prerequisites

- Python 3.10 or higher
- Jupyter Notebook or JupyterLab
- Virtual environment (recommended)

### Setup Instructions

1. **Clone or navigate to the project directory:**
   ```bash
   cd uniprot
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure API credentials (optional):**
   - For OpenAI API (if using GPT functionality), create a `.env` file:
     ```
     OPENAI_API_KEY=your_api_key_here
     ```
   - For PubMed API, set your email in the notebook:
     ```python
     Entrez.email = "your_email@example.com"
     ```

## Usage

### Running the Demo Notebook

The main workflow is demonstrated in `UniProt Peptide Search.ipynb`:

1. **Open the notebook:**
   ```bash
   jupyter notebook "UniProt Peptide Search.ipynb"
   # or
   jupyter lab "UniProt Peptide Search.ipynb"
   ```

2. **Execute cells sequentially:**
   - Cell 1-2: Install packages and import libraries
   - Cell 3-12: Define core functions for UniProt/PubMed data extraction
   - Cell 13-14: Load protein lists (human/cow milk proteins)
   - Cell 15: Execute search on protein list
   - Cell 16: Merge peptide and reference data
   - Cell 17: Fetch PubMed details (abstracts, titles, authors, DOIs)
   - Cell 18+: Data exploration, export, and analysis

### Key Functions

#### UniProt Functions
- `fetch_protein_info(protein_id)`: Fetches protein data from UniProt API
- `extract_peptide_and_function(data, protein_id)`: Extracts peptide features and functions
- `extract_references(data, protein_id)`: Extracts reference metadata
- `associate_peptide_with_function()`: Links peptides with their biological functions

#### PubMed Functions
- `fetch_details(row, row_num, total_rows)`: Retrieves abstracts, titles, authors, and DOIs from PubMed

#### Data Processing
- `process_species_data(protein_ids_list)`: Processes a list of protein IDs and returns DataFrames
- `update_associated_function(row)`: Updates associated functions from non-associated functions
- `print_critical_info(df, df_name)`: Prints summary statistics for DataFrames

## Key Features

### ✅ Completed Features

- **UniProt API Integration**: Automated queries for protein metadata, peptide sequences, and functions
- **PubMed API Integration**: Automated retrieval of abstracts, titles, authors, and DOIs
- **Data Extraction**: Automated extraction of:
  - Peptide sequences and intervals
  - Protein names and descriptions
  - Biological functions (associated and non-associated)
  - Reference metadata (PubMed IDs, DOIs, titles, authors)
- **Data Merging**: Intelligent merging of peptide and reference data
- **CSV Export/Import**: Save and load processed datasets

### 🚧 In Progress / Planned Features

- **AI Text Analysis**: GPT-4 integration for bioactivity classification (requires OpenAI API key)
- **Comprehensive Protein Lists**: Expansion to additional species (sheep, goat, pig, yak, rabbit, donkey, camel, buffalo)
- **PubMed Keyword Searches**: Automated searches using predefined keywords
- **Peptide-based PubMed Searches**: Use MBPDB peptides as keywords to find new references
- **IC50 and PTM Extraction**: Extract quantitative data from literature
- **MBPDB Upload Format**: Generate TSV files formatted for MBPDB upload
- **Documentation Tables**: Generate audit trails for bioactivity reclassifications

## Methodology

### Literature Search

1. **UniProt Search**: Query UniProt API using protein IDs from curated milk protein lists
2. **PubMed Integration**: Fetch reference details (abstracts, titles, authors, DOIs) for peptides with PubMed IDs
3. **Future**: Keyword-based PubMed searches and peptide-based reference discovery

### Text Extraction

- Extract peptide sequences, intervals, and descriptions from UniProt XML
- Associate peptides with biological functions based on evidence keys
- Retrieve and parse PubMed metadata for references

### Text Analysis (Planned)

- AI-powered bioactivity classification using GPT-4
- Legitimacy assessment of bioactivity claims
- Classification into existing MBPDB function categories
- Extraction of quantitative data (IC50, inhibition types, etc.)

### Data Compilation

- Merge peptide and reference data into structured DataFrames
- Compare with existing MBPDB entries to identify novel peptides
- Export results in MBPDB-compatible formats

## Current Status

### Completed ✅

- [x] UniProt API integration and data extraction
- [x] PubMed API integration for reference metadata
- [x] Peptide-function association logic
- [x] Data merging and processing pipeline
- [x] CSV export/import functionality
- [x] Demo notebook with example workflow

### In Progress 🚧

- [ ] GPT-4 integration for bioactivity classification
- [ ] Comprehensive protein lists for all MBPDB species
- [ ] PubMed keyword search automation
- [ ] IC50 and PTM data extraction
- [ ] MBPDB upload format generation

### Future Work 🔮

- [ ] Custom LLM trained on bioactive peptide literature
- [ ] Natural language query interface
- [ ] Autonomous AI agent for PubMed article discovery
- [ ] Post-transcriptional modification peptide support
- [ ] Web application integration
- [ ] Macro analysis tools for database insights

## Dependencies

See `requirements.txt` for complete list. Key dependencies:

- **biopython**: PubMed API access
- **requests**: HTTP requests for UniProt API
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical operations
- **openai**: GPT-4 API access (optional, for AI features)
- **jupyter**: Notebook environment

## Notes

### Important Compatibility Notes

- **OpenAI API**: The notebook uses the legacy OpenAI API format. For `openai>=1.0.0`, you'll need to update the API calls (see OpenAI migration guide).

### Data Files

- `data/exported_data.tsv`: Current MBPDB export for comparison
- `protein_lists/*.fasta`: FASTA files with protein IDs (format: `>sp|PROTEIN_ID|...`)
- Output CSV files are saved in the `data/` directory

## Contributing

This project is part of ongoing research to expand the MBPDB. For questions or contributions, please contact the project maintainers.

## License

[Specify license if applicable]

## References

- **MBPDB**: [Milk Bioactive Peptide Database](https://mbpdb.nws.oregonstate.edu/)
- **UniProt**: https://www.uniprot.org/
- **PubMed**: https://pubmed.ncbi.nlm.nih.gov/
- **NCBI E-utilities**: https://www.ncbi.nlm.nih.gov/books/NBK25501/

## Contact

For questions about this project or the MBPDB, please contact:
- Email: kuhfeldrf@oregonstate.edu

---

**Last Updated**: 2024
**Version**: 1.0 (Demo)

