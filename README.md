
# iceDP project description
The iceDP package processes genome interaction data using a density peaks algorithm to identify inter-chromatin interactions. Below is the procedure for using iceDP effectively.

<br>

## Installation
Use pip to install:
```shell
pip install iceDP
```

Or directly copy source code:
```shell
# copy to:
${python_path}/site-packages
```

<br>

## Usage
* **Data required**

iceDP receive any genome interaction data in a three-column format as input. Before running analyses, we need to prepare genome interaction data in a three-column format:

    Column 1 (chr_one_site) → Genomic position on the first chromosome.

    Column 2 (chr_two_site) → Genomic position on the second chromosome.

    Column 3 (interaction_value) → Interaction strength between the two positions (typically observed in Hi-C experiments).

 Check the sample data:
```shell
head -5 play_data/chr4_chr11_mm10.txt
3090000 3100000 1.0
3795000 3100000 1.0
4205000 3100000 1.0
4255000 3100000 1.0
4230000 3105000 1.0
```
  This file represents genomic interactions between chromosome 4 and chromosome 11 in the mouse genome (mm10).


  If your data is stored in .hic format, you can extract interaction values using [Juicer Tools](https://github.com/aidenlab/juicertools):

```shell
java -jar juicer_tools.jar dump observed NONE yourdata.hic chr4 chr11 BP 50000 chr4_chr11_mm10.txt
```

<br>

* **iceDP procedure**
```python
import iceDP

# Initialize data processing
x = iceDP.main_procedure.bunchDots()

# Read interaction data from file
x.readData('play_data/chr4_chr11_mm10.txt')

# Compute parameter for decision tree
x.get_rho()    # Calculate rho values
x.get_delta()  # Calculate delta values

# Statistical analysis of interaction sites
x.do_chi_square_test()  # Perform chi-square test
x.define_border()       # Define interaction borders
x.horizontal_and_vertical_fold_change()  # Fold change for horizontal and vertical

# Save the results to a formatted output file
iceDP.main_procedure.save_reult(x, 'chr4_chr11_mm10_DPresult')
```

<br>

* **Output format**

After processing, iceDP generates a comma-separated 15-column table, filtering out low-confidence interaction spots. Each row in the saved output file (chr4_chr11_mm10_DPresult) contains the following columns:

| Column Name     | Description                                      |
|----------------|--------------------------------------------------|
| index          | Spot identifier                                  |
| start1         | Position on chromosome 1                        |
| start2         | Position on chromosome 2                        |
| counts         | Interaction counts                              |
| rho            | Density metric                      |
| delta          | Peak distance metric                            |
| p_value        | Statistical significance (Chi-square test)      |
| fillN          | Number of square near center with counts                          |
| center_x       | Center of interaction site (X)                  |
| center_y       | Center of interaction site (Y)                  |
| side_length_x  | Interaction region size (X axis)                |
| side_length_y  | Interaction region size (Y axis)                |
| fold_change    | Center square to surround square fold change                             |
| vertical_fc    | Vertical axis fold change                       |
| horizontal_fc  | Horizontal axis fold change                     |

<br>

* **Plot**
```python
iceDP.plot_spots.plot_one_spot(x.data_filted2.values[1], x)
```
![plot result ](https://github.com/CreataNameIsHard/iceDP/blob/main/image/bin1_72275000_bin2_101650000.png)

