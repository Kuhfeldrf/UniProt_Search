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
├── UniProt Peptide Search.ipynb    # Main Jupyter notebook - complete workflow
├── requirements.txt                 # Python dependencies
├── README.md                        # This file
│
├── data/                            # Output data files
│   ├── exported_data.tsv           # MBPDB exported data (input for comparison)
│   └── _novel_peptides_for_addition_to_MBPDB_*.csv
│                                   # Generated output files with novel peptides
│                                   # (timestamped: YYYYMMDD_HHMMSS format)
│
├── protein_lists/                   # Protein ID lists (input files)
│   ├── HumanMilkProteinDatabase_v2.fasta
│   ├── CowMilkProteinDatabase_v2.fasta
│   ├── hummbpdbchec.tsv            # Human MBPDB check list
│   ├── sheep milk.tsv              # Sheep milk protein list
│   ├── cows milk.txt               # Cow milk protein list
│   └── protein_header.txt          # Protein header reference
│
└── venv/                            # Python virtual environment (optional)
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

4. **Configure API credentials:**
   - Create a `.env` file in the project root with:
     ```
     OPENAI_API_KEY=your_api_key_here
     PUBMED_EMAIL=your_email@example.com
     OPENAI_MODEL=gpt-4o-mini  # Optional, defaults to gpt-4o-mini
     ```
   - The notebook automatically loads these from the `.env` file using `python-dotenv`
   - **Note**: OpenAI API key is required for GPT-based bioactivity classification

## Usage

### Running the Notebook

The complete workflow is implemented in `UniProt Peptide Search.ipynb`:

1. **Open the notebook:**
   ```bash
   jupyter notebook "UniProt Peptide Search.ipynb"
   # or
   jupyter lab "UniProt Peptide Search.ipynb"
   ```

2. **Execute cells sequentially** from top to bottom. The notebook includes:
   - UniProt API functions for fetching protein and peptide data
   - PubMed API functions for retrieving abstracts and metadata
   - Data processing and merging functions
   - GPT-4 classification functions for bioactivity assessment
   - MBPDB matching functions to identify novel peptides

## Key Features

### ✅ Completed

- **UniProt & PubMed API Integration**: Automated data extraction from protein databases and literature
- **GPT-4 Bioactivity Classification**: AI-powered classification of peptides into MBPDB function categories
- **MBPDB Matching**: Automatic comparison with existing database entries to identify novel peptides
- **Data Processing Pipeline**: Complete workflow from protein lists to export-ready CSV files

### 🚧 Planned

- Additional species protein lists (sheep, goat, etc.)
- PubMed keyword search automation
- Quantitative data extraction (IC50, PTM)
- Direct MBPDB upload format generation

## Dependencies

Key dependencies: `biopython`, `requests`, `pandas`, `numpy`, `openai`, `python-dotenv`, `jupyter`

See `requirements.txt` for complete list and versions.

## Notes

- **API Requirements**: OpenAI API key required for GPT classification. PubMed email configured via `.env` file.
- **Input Files**: Load protein lists from `protein_lists/` directory and MBPDB export from `data/exported_data.tsv`
- **Output Files**: Generated CSV files are saved to `data/` with timestamped filenames
- **Performance**: ~2 seconds per protein (UniProt), ~1 second per row (PubMed), variable for GPT classification

## Contributing

This project is part of ongoing research to expand the MBPDB. For questions or contributions, please contact the project maintainers.

## References

- **MBPDB**: [Milk Bioactive Peptide Database](https://mbpdb.nws.oregonstate.edu/)
- **UniProt**: https://www.uniprot.org/
- **PubMed**: https://pubmed.ncbi.nlm.nih.gov/
- **NCBI E-utilities**: https://www.ncbi.nlm.nih.gov/books/NBK25501/

## Contact

For questions about this project or the MBPDB, please contact:
- Email: kuhfeldrf@oregonstate.edu

---

**Last Updated**: November 2025
**Version**: 2.0 (Demo)

