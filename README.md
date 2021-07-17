# Madripiso
This past year I have lived in Madrid (Spain) to study the Computational Biology Master in the Universidad Politécnica de Madrid. Because I wanted to help in the peaceful coexistence with my flatmates, I wrote some Python and R code to easily maintain the accounts of the house.

The only requirement is **pandas** to be installed with **xlrd**.

## 1. Files

- **cuentas-del-madripiso.ipynb**: given an Excel file with the format specified in section 2, this Jupyter notebook computes the household accounts. At the end of every month (accounts were computed monthly), this notebook showed how much money was owed among flatmates; the code in this notebook can be easily executed thanks to [Google Colab](https://colab.research.google.com/github/edu9as-old/madripiso/blob/master/cuentas-del-madripiso.ipynb). This code was adapted and deployed in a [Shiny app](https://edu9as.shinyapps.io/madripiso/) to ease the computation of the accounts (source code in **app/**).
- **sample.xlsx**: sample Excel file to easily test the code in **cuentas-del-madripiso.ipynb**. Data is totally made up.
- **app/**: source code of the Shiny app built from this project.

## 2. Expected format of the Excel files
Excel files for this project can contain as many rows as desired; each row represents an item that was bought by some flatmate for another flatmate. Also, the input files must contain up to seven columns; only the first four are compulsory. The names of these columns are:
- **Que**: the item that was bought. Required field.
- **Quien**: the person who bought the item. Required field.
- **ParaQuién**: the receptor or the person who benefited from the item that was purchased. Required field.
- **Cuanto**: the cost of the item. Required field.
- **Cuando**: the date when the item was bought. Optional.
- **Donde**: the establishment where the item was purchased. Optional.
- **Incidencias**: some additional comments about the purchase. Totally optional.

## 3. Usage

Some example Excel file for three flatmates called C, E and R might look like this:

| Que | Quien | ParaQuien | Cuanto | Cuando | Donde | Incidencias |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Spanish omelette | C | RXXX | 50.00 | 2022-09-05 | Eiffel tower | - |
| Stuff | E | C | 5.00 | 2022-09-06 | London | - |
| More stuff | R | E | 2.00 | 2022-09-07 | Boston | - |

Each row means that: 
1. Flatmate **C** bought item **Spanish omelette** with a cost of **50.00** for flatmate **R** and three other people (three times **X**) that do not live with them and hence their accounts must be computed separately (because this project focuses on the wellbeing of the flatmates and nobody else). 
    - R owes **12.5** (50.00 divided by 4) to C.
    - Each of the other people owe 12.5 to C, but they must **settle the accounts separately** because they are not flatmates of C.
2. Flatmate **E** bought item **Stuff** to flatmate **C** paying **5.00**.
    - C owes **5.00** to E.
3. Flatmate **R** purchased item **More stuff** with a cost of **2.00** for flatmate **E**.
    - E owes **2.50** to R.

Given this input table (**sample.xlsx**), the output of this application is:

```
Rose debe 12.50 euros a Charles.
Charles debe 5.00 euros a Eduardo.
Eduardo debe 2.00 euros a Rose.
```

