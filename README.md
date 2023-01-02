# Prediction of prices of apartments in Prague

### Instructions for SU2

Working example url is here https://8862-95-103-189-152.eu.ngrok.io/ . Web will run on my machine and will be forwarded to internet by https://ngrok.com/. Therefore you do not need to install dependencies and create environment. Please do not use web simultaneously on more computers/ browser tabs as it can result in unexpected behaviour.


Web interface looks like this


![Screenshot from 2022-12-21 11-18-33](https://user-images.githubusercontent.com/65658910/208881956-e89c9af9-3827-42b3-bcca-66d909583c0c.png)

You can use 

* `Predikce pomocí URL` option
 >> Here please provide url of apartment from Prague from (https://www.sreality.cz/hledani/prodej/byty/praha?strana=1 or bezrealitky.cz)
   or try whatever link you want it should handle it... 
   
* `Predikce pomocí ručně zadaných příznaků`
 >> Here expand please `Zadej příznaky` block and provide some attributes of apartment. Usable area and location are required.
 
Your result should be similar to this one


![Screenshot from 2022-12-21 11-28-09](https://user-images.githubusercontent.com/65658910/208883815-cceb3a81-733c-4f2f-a764-42562008dbbd.png)


### Requirements

-----------------------------------------------------------------------------------
Make sure you first create (e.g. conda) environmnent with either of commands

- ``conda env create re && conda activate re && pip install -r requirements.txt``
- ``conda env create -f environment.yml``

We use ``python 3.10.6``

### Run the code

---------------------------------------------------------------------
There are two options:

- use web interface which can be launched locally using following command
  * ``streamlit run web.py``
- use CLI (for details use `python main.py --help`) e.g.
  * `python main.py --train --tune` -> performs hyperparameter search (data loaded from `../data/dataset.csv`)
  * `python main.py` -> runs prediction on data from `../data/dataset.csv` and saves result in `../data/result.csv`
  * `python main.py --train --scrape` -> scrapes new data and performs training
  
There is no jupyter notebook demo as we (or just Many98) do not like Jupyter notebooks :sunglasses:


### Processing logic is as follows

-------------------------------------------------------------------------------------
Processing runs in two phases:
* `train` -> all advertisements are obtained by crawlers
* `inference` -> advertisement url/data is/are provided by user via web app

Implementation is also implemented in 2 main classes:
* `ETL` class handles data obtaining and preprocessings
* `Model` class operates on preprocessed data by `ETL`
   and the model itself is based on XGBoost
   
#### Graphical proposal of processing logic 


![etl](https://user-images.githubusercontent.com/65658910/201643260-06bb1a57-564a-4413-9df0-c344095bff66.png)

