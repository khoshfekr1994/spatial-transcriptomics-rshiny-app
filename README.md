# Spatial Transcriptomics Data Analysis Tool

[![R](https://img.shields.io/badge/R-%3E%3D4.0-blue.svg)](https://www.r-project.org/)
[![Shiny](https://img.shields.io/badge/Shiny-Interactive-brightgreen.svg)](https://shiny.rstudio.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An interactive Shiny web application for comprehensive analysis of spatial transcriptomics data using Seurat objects. This tool provides researchers with an intuitive interface to explore gene expression patterns, define lesion areas, perform cell type annotation, and generate publication-ready visualizations.

## 🚀 Features

### 📊 Core Analysis Capabilities
- **Multi-Gene Expression Analysis**: Analyze custom gene sets with circular and violin plots
- **Automated Lesion Detection**: Define lesion areas using customizable marker genes and thresholds
- **Multiple Assay Support**: Work with Spatial, SCT, and Log-Normalized assays
- **Statistical Testing**: Comprehensive statistical analysis with p-value calculations

### 🔬 Visualization Suite
- **Circular Plots**: Mean expression and fraction of expressing cells across tissue regions
- **Violin Plots**: Expression distribution comparisons with statistical significance testing
- **Spatial Images**: Gene expression patterns overlaid directly on tissue sections
- **Cell Type Analysis**: Distribution, enrichment, and expression analysis by predicted cell types

### 🧬 Cell Type Annotation
- **SingleR Integration**: Automated cell type identification using reference datasets
- **Multiple References**: Support for ImmGen (immune cells) and MouseRNAseq (broad coverage)
- **Comparative Analysis**: Cell type distribution differences between lesion and normal regions
- **Gene Expression Profiling**: Cell type-specific expression patterns

### 📥 Data Management
- **Flexible Input**: Upload Seurat RDS files with spatial transcriptomics data
- **Assay Creation**: Automatic Log-Normalized assay generation when needed
- **Batch Downloads**: Export all plots and statistics in organized ZIP files

## 🛠️ Installation

### Prerequisites

Ensure you have R (≥ 4.0) installed on your system.

### Quick Setup

1. **Clone the repository**:
```bash
git clone https://github.com/yourusername/spatial-transcriptomics-app.git
cd spatial-transcriptomics-app
```

2. **Install required packages**:
```r
# Run the requirements script
source("requirements.R")
```

Or install manually:
```r
# Install CRAN packages
install.packages(c("shiny", "dplyr", "ggplot2", "stringr", 
                   "reshape2", "RColorBrewer", "patchwork", "tidyr"))

# Install Bioconductor packages
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("Seurat", "SingleR", "celldex"))
```

3. **Launch the application**:
```r
# Run the app
shiny::runApp("app.R")
```

## 📋 Usage Guide

### Quick Start Workflow

1. **📁 Upload Data**: Load your Seurat RDS file containing spatial transcriptomics data
2. **🧬 Select Genes**: Enter genes of interest (one per line) in the gene input area
3. **🏷️ Choose Groups**: Select sample groups/conditions to analyze
4. **🎯 Define Lesions**: Set marker genes and expression thresholds for lesion identification
5. **⚙️ Configure Analysis**: Choose assay type and normalization options
6. **🔬 Annotate Cell Types**: Run automated cell type annotation using SingleR
7. **📊 Generate Results**: Click "Generate Plots" to create comprehensive visualizations
8. **💾 Export**: Download individual plots or complete analysis packages

### Data Requirements

Your Seurat object should contain:
- **Spatial expression data** in the "Spatial" assay
- **Sample identifiers** in the `orig.ident` metadata column
- **Spatial coordinates** for tissue visualization
- **Valid gene symbols** matching your analysis genes

Example data structure:
```r
# Check your Seurat object
str(seurat_object@meta.data)
# Should include: orig.ident, spatial coordinates

# Check available assays
names(seurat_object@assays)
# Should include: "Spatial" (required)

# Verify gene presence
head(rownames(seurat_object[["Spatial"]]))
```

### Lesion Definition

The app identifies lesions based on dual marker expression:

- **Default Configuration**:
  - Marker Gene 1: Gene 1
  - Marker Gene 2: Gene 2
- **Logic**: Cells exceeding BOTH thresholds = "Lesion", others = "Other"
- **Customization**: Modify genes and thresholds based on your research needs

### Cell Type Annotation Options

| Reference Dataset | Description | Best For |
|-------------------|-------------|----------|
| **ImmGen** | Immunological Genome Project | Immune cell identification |
| **MouseRNAseq** | Comprehensive mouse reference | Broad cell type coverage |

## 📊 Output Examples

### Generated Visualizations

1. **Circular Plots**: 
   - Bubble plots showing mean expression and expressing cell fractions
   - Faceted by sample groups for comparison

2. **Violin Plots**: 
   - Expression distribution comparisons
   - Statistical significance testing between regions

3. **Spatial Plots**: 
   - Gene expression overlaid on tissue sections
   - Lesion area visualization with custom markers

4. **Cell Type Analysis**: 
   - Distribution plots by sample and histology
   - Enrichment analysis (lesion vs. normal)
   - Dot plots for gene expression across cell types

### Downloadable Outputs

- **Individual Plots**: High-resolution PNG files (300 DPI)
- **Statistics**: CSV files with expression summaries and p-values
- **Batch Downloads**: ZIP archives with complete analysis results

## 🔧 Advanced Features

### Assay Management
- **Automatic Normalization**: Creates Log-Normalized assays when needed
- **SCT Preservation**: Option to maintain SCT assays during normalization
- **Flexible Analysis**: Switch between assays for different analysis steps

### Statistical Analysis
- **Wilcoxon Tests**: Non-parametric testing for expression differences
- **Z-score Normalization**: Optional standardization for comparative analysis
- **Multiple Comparisons**: Analysis across multiple sample groups

### Customization Options
- **Gene Sets**: Flexible input for any gene combination
- **Plotting Parameters**: Adjustable point sizes and visualization settings
- **Export Formats**: Multiple download options for different use cases

## 🐛 Troubleshooting

### Common Issues

**Problem**: "Gene not found in dataset"
- **Solution**: Check gene naming (case-sensitive) and ensure genes exist in your data

**Problem**: App crashes during cell type annotation
- **Solution**: Ensure sufficient memory and verify assay data integrity

**Problem**: Spatial plots not displaying
- **Solution**: Confirm spatial coordinates are present in your Seurat object

### Performance Tips
- **Large datasets**: Consider subsetting for initial exploration
- **Memory management**: Close other R sessions when running the app
- **Plot generation**: Allow sufficient time for complex visualizations


## 📖 Citation

If you use this tool in your research, please cite:

```bibtex
@software{rudsari2024spatial,
  title = {Spatial Transcriptomics Data Analysis Tool},
  author = {Hamid Khoshfekr Rudsari},
  year = {2024},
  url = {https://github.com/khoshfekr1994/spatial-transcriptomics-rshiny-app}
}
```

## 👨‍💼 Contact & Support

**Hamid Khoshfekr Rudsari, PhD**  

📧 **Email**: 
- khoshfekr1994@gmail.com


### Development Guidelines
- Follow existing code style and structure
- Add comments for complex functions
- Update documentation for new features
- Test thoroughly before submitting

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **[Shiny](https://shiny.rstudio.com/)** - Interactive web application framework
- **[Seurat](https://satijalab.org/seurat/)** - Spatial transcriptomics analysis toolkit
- **[SingleR](https://bioconductor.org/packages/SingleR/)** - Automated cell type annotation
- **[ggplot2](https://ggplot2.tidyverse.org/)** - Grammar of graphics visualization
- **[patchwork](https://patchwork.data-imaginist.com/)** - Plot composition and layout

## 📈 Version History

- **v1.0.0** - Initial release with core functionality
- **v1.1.0** - Added cell type annotation features
- **v1.2.0** - Enhanced spatial visualization capabilities

