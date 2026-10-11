# Airport Flight Network Analysis with PySpark and GraphFrames

A graph analytics project that models airport-to-airport flights as a directed network and explores airport connectivity using Apache Spark and GraphFrames.

## Project overview

This project uses 2018 flight records to build a directed graph:

- **Vertices:** airports identified by their airport codes.
- **Edges:** directed flights from an origin airport to a destination airport.
- **Edge aggregation:** repeated origin–destination pairs are grouped and counted as `flight_count`.

The notebook explores data preparation, in-degree and out-degree, triangle counting, a degree-based connectivity measure, PageRank, and network visualization.

## Research questions

1. Which airports have the highest direct connectivity?
2. How do in-degree and out-degree differ across airports?
3. What triangles or closed triplets appear in the flight network?
4. Which airports rank highly under the implemented PageRank calculation?
5. How do degree-based rankings compare with PageRank?

## Repository structure

```text
airport-flight-network-analysis/
├── airport_flight_network_analysis.ipynb  # Main analysis notebook
├── airport_network_visualization.html    # Exported interactive visualization
├── project_report.pdf                    # Project report
├── README.md                             # Project documentation
├── requirements.txt                      # Python package guidance
└── .gitignore                            # Common generated/local files
```

## Technology stack

- Python
- Apache Spark / PySpark
- GraphFrames
- pandas
- NetworkX
- Plotly
- Jupyter Notebook

## Data

The notebook expects a local CSV file named `2018.csv` containing flight records and columns including `ORIGIN` and `DEST`. **The raw dataset is not included in this repository.** Place the file in a `data/` directory and update the notebook's CSV path from `local/2018.csv` to `data/2018.csv`, or use the path appropriate to your environment.

Before publishing, add the dataset's original source URL and any applicable license/attribution here. Do not upload data you are not permitted to redistribute.

## Environment setup

Spark and GraphFrames versions must be compatible with each other and with the installed Java version. The notebook originally used a GraphFrames JAR configured for Spark 3.0 / Scala 2.12, so that setting may need to be updated for a newer environment.

1. Install a compatible Java runtime, Apache Spark, and GraphFrames.
2. Create and activate a Python environment.
3. Install the Python packages listed in `requirements.txt`.
4. Start Jupyter Notebook or JupyterLab.
5. Open `airport_flight_network_analysis.ipynb`.
6. Update the input CSV path and GraphFrames package/JAR configuration for your setup.
7. Run the notebook cells from top to bottom.

Example Python environment setup:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

> Installing the Python `graphframes` package alone may not provide the JVM-side GraphFrames dependency. Follow the installation instructions for the exact Spark/Scala versions in your environment.

## Analysis workflow

1. Load the 2018 flight CSV into a Spark DataFrame.
2. Inspect the schema and remove rows with missing origin or destination codes.
3. Build airport vertices and aggregate directed flight edges.
4. Calculate in-degree, out-degree, and total degree.
5. Count triangles with GraphFrames and compare with the notebook's manual approach.
6. Calculate a degree-based connectivity measure.
7. Run the notebook's PageRank implementation.
8. Visualize the network with NetworkX and Plotly.

## Important methodological notes

- **Degree is not closeness centrality.** The notebook uses total degree as a simple connectivity proxy; it should not be described as a closeness-centrality calculation.
- **Validate PageRank before interpreting rankings.** The custom iterative implementation should be checked against GraphFrames PageRank or another trusted implementation. In particular, verify rank normalization, dangling-node handling, and convergence.
- **Triangle counting needs a clear definition.** GraphFrames triangle counts are based on graph structure and may treat edges differently from the manual directed-cycle calculation. Do not compare the two numbers as equivalent without checking their definitions.
- **Visualization scale:** converting every Spark row to pandas/NetworkX can consume substantial memory. For large graphs, filter to a subset (for example, the top airports or strongest routes) before conversion.
- The exported HTML visualization is a static artifact; it does not rerun the analysis.

## Results and reproducibility

The repository includes the original report and an exported HTML visualization. Add a short results section after rerunning the notebook in your environment, including the dataset source, number of rows retained, number of airport vertices and aggregated edges, top airports by degree and PageRank, and any limitations. Do not report unverified values.

## Future improvements

- Use a reproducible environment and document tested Spark, Java, Scala, and GraphFrames versions.
- Move file paths and analysis parameters into a configuration section.
- Add validation tests for graph construction, PageRank, and triangle counts.
- Export summary tables for top airports and route frequencies.
- Add screenshots of the visualization to make the repository easier to browse.
- Record the dataset citation and its redistribution terms.

## Academic context

Course project for Data Processing and Analytics, International Master's in Data and Intelligence for Smart Systems (DISS), Université Claude Bernard Lyon 1. Update the author/contributor details to match the version you intend to publish.

## License

No license is specified yet. Add a license only after deciding what reuse permissions you want to grant and confirming the rights for included materials.
