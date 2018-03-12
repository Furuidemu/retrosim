# retrosim

### summary

This repository contains the data and code needed to test a similarity-based approach to one-step retrosynthesis.

Please note that ```rdchiral``` is a work-in-progress. The current version as of June 19, 2017 has been copied into this repository for result reproducibility. An up-to-date version can be found at the public repo http://github.com/connorcoley/rdchiral

### data

The set of 50k reactions comes from http://pubs.acs.org/doi/abs/10.1021/acs.jcim.6b00564. Each reaction is pre-labeled with a class number (1-10). The dataset is further cleaned following Liu et al. (2017) (https://arxiv.org/pdf/1706.01643.pdf) so that each reaction has a single product and trivial products are excluded. Atom maps are removed for reactant atoms that do not contribute atoms to the product of interest. ```data_processed.csv``` is a Pandas dataframe and is meant to work with the functions in ```get_data.py```.

### usage

All of the "heavy lifting" occurs inside the ```scripts``` folder. ```extract_templates``` is just used for examining the templates corresponding to the training data. Likewise, ```analyze_templates``` looks at the some trends and the most common templates, but is not needed in the workflow.

After an initial data processing using ```proc_data```, the ```test_similarity``` script actually applies the similarity method using the training data as a corpus. The Jupyter notebook is meant to look at a single condition (i.e., class, fingerprint type, similarity metric) at a time. The standalone script can test the whole suite of conditions. Results are written into ```results.txt``` and are saved in separate files.

The notebook ```process_results``` reads from ```results.txt``` and examines the validation performance visually. This is how the metric was selected for use on the test data, which required a simple modification of the ```test_similarity``` script. Test results are also read using ```process_results``` and output in a tabular form at the end of the notebook.

### contact

For any questions, feel free to email ccoley@mit.edu
 
### Comments From xg590@nyu.edu
The following ipynbs are for playing with the knowledge base (reaction precedents)
1. retrosim/retrosim/scripts/extract_templates.ipynb # Read data/data_processed.csv and write to data/templates_general.json
2. retrosim/retrosim/scripts/analyze_templates.ipynb # Read data/templates_general.json

The following ipynbs are for method evaluation (How is the accuracy based on the knowledge of reaction precedents)
3. retrosim/retrosim/scripts/proc_data.ipynb # Read data/from_schneider/dataSetB.csv and write to data/data_processed.csv
4. retrosim/retrosim/scripts/get_test_examples.ipynb # Read data/data_processed.csv and apply retrosim method on an exemplary reaction
5. retrosim/retrosim/scripts/test_similarity.ipynb # Apply retrosim method on each reaction within the test set of all class 1 reactions
6. retrosim/retrosim/scripts/test_similarity.py # An independent script that is different from test_similarity.ipynb. Read from data/data_processed.csv and write to retrosim/retrosim/scripts/out/*.txt
7. retrosim/retrosim/scripts/process_results.ipynb # Read retrosim/retrosim/scripts/out/*.txt and evaluate every combination of fingerprint and similarity alogrithms.

Test retrosim method on several cases
8.retrosim/retrosim/scripts/usable_model.ipynb # Read data/data_processed.csv
