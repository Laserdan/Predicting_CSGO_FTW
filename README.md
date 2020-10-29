# Predicting CS:GO FTW

<br>

**Victor Lucia**

**Ironhack Madrid 2020 Part-time**
##

<br>

The objective of the project is to **predict relevant information** on the fly of ranked matches in the competitive video-game Counter-Strike: Global Offensive (CS:GO), played daily by more than 800.000 players worldwide. With this information the teams can anticipate and coordinate for the next round, creating good strategies either defense or attack, depending on the side they are playing:
- Counter Terrorist (CT): Defense
- Terrorist (T): Attack

Counter-Strike: Global Offensive forms part of the eSports, a growing market that is living his golden years with followers all over the world and moving big amounts of money. Only in tournament prizes, [CS:GO has passed $100M](https://esportsobserver.com/csgo-passes-100m-totalprize-money/)  from his beginning.

![Image](https://esports.as.com/2018/07/04/cs-go/ESL-organizar-Major-Counter-Strike_1150994903_93102_1440x600.jpg)

## :floppy_disk: Data Source

The original data came from a [Kaggle dataset](https://www.kaggle.com/skihikingkevin/csgo-matchmaking-damage), where more than 12.000 matches are tracked. 

An important fact is that matches are not from the in-game matchmaking system. They are from a third-party service called [ESEA](https://play.esea.net/), a competitive environment with experimented players and where professional teams train and compete. This makes that we can consider the reliability of the data, knowing that most of the information will be relevant and usable.

[Here](https://www.kaggle.com/danielmazzone/csgo-data-analysis-and-machine-learning) you can find an exploratory analysis of the data made by Daniel Mazzone


## :printer: Output


|round|ct_val_pred|t_val_pred|ct_round_type|t_round_type|ct_nxt_rnd_type_pred|t_nxt_rnd_type_pred|nxt_ct_winner_pred|
|----|----|----|----|----|----|----|----|
|	1|  4078.134589|	3943.272665 |	PISTOL_ROUND|	PISTOL_ROUND |	MEDIUM |	ECO |	0|
|	2|	17819.702711|	6290.616771 |	MEDIUM|	        ECO |	        MEDIUM|     FULL|   0|
|	3| 	7038.468589| 	19600.790638| 	MEDIUM| 	    FULL| 	        ECO| 	    MEDIUM| 1|
| 	4| 	1452.468928| 	22568.098741| 	ECO| 	        MEDIUM|         FULL| 	    FULL| 	0|
| 	5| 	22676.205763| 	24459.855175| 	FULL| 	        FULL| 	        ECO| 	    FULL| 	0|
| ...| 	...| 	        ...| 	        ...| 	        ...| 	        ...| 	    ...| 	...|

Where:
- <code>round</code>: Number of the round analyzed.
- <code>ct_val_pred</code>: **Prediction** of the value of all the equipment the ct side is carrying.
- <code>t_val_pred</code>: **Prediction** of the value of all the equipment the t side is carrying.
- <code>ct_round_type</code>: Type of round of the ct side.
- <code>t_round_type</code>: Type of round of the t side.
- <code>ct_nxt_rnd_type_pred</code>: **Prediction** of the type of round of the ct side for the next round.
- <code>t_nxt_rnd_type_pred</code>: **Prediction** of the type of round of the t side for the next round.
- <code>nxt_ct_winner_pred</code>: **Prediction** of the winner side for the next round: 1 if ct side, 0 if t side.

There are more parameters also relevant that are not included to the output to get it more condensed and clear. You can see them in the [6_Output.ipynb notebook](https://github.com/Laserdan/Predicting_CSGO_FTW/blob/master/notebooks/6_Output.ipynb).

This will be the output when the code will be implemented in-game.

For the stage we are, we have reached to make the predictions of the data we have with 3 different models:
- Value of the team: 2 regression models.
- Next round type: 2 multiclass classification models. 
- Winner for the next round: 1 classification model.

## :rocket: Next Steps

#### Sort term
The next step is to create a pipeline that returns the predictions when a round is passed manually.

#### Medium term
Get the round information directly from the game and pass it to the pipeline to get the prediction in real-time.

## :computer: Requirements 

| Technology | Version | Documentation | 
| --- | --- | --- |
| Python | 3.7.3 | [www.python.org](https://www.python.org/doc/) |
| Pandas | 1.1.3 | [pandas.pydata.org](https://pandas.pydata.org/docs/reference/index.html) |
| Pandas-profiling | 2.9.0 | [GitHub repo](https://github.com/pandas-profiling/pandas-profiling) |
| Scikit-Learn | 0.23.1 | [scikit-learn.org](https://scikit-learn.org/stable/user_guide.html) |
| Numpy | 1.19.1 | [numpy.org](https://numpy.org/doc/stable/reference/index.html) |
| LightGBM | 2.3.0 | [lightgbm.readthedocs.io](https://lightgbm.readthedocs.io/en/latest/index.html) |
| Joblib | 0.15.1 | [joblib.readthedocs.io](https://joblib.readthedocs.io/en/latest/) |

## :file_folder: Folder structure
```
└── project
    ├── .gitignore
    ├── requeriments.txt
    ├── README.md
    ├── data
    │   ├── processed
    │   └── results
    ├── models
    │   ├── ct_team_value.joblib
    │   ├── t_team_value.joblib
    │   ├── ct_nxt_rnd_type.joblib
    │   ├── t_nxt_rnd_type.joblib
    │   └── nxt_ct_winner.joblib
    └── notebooks
        ├── archive
        ├── 0_join_data.ipynb
        ├── 1_direct_estimation.ipynb
        ├── 2_1_ml_preprocessingdata.ipynb
        ├── 2_1_optimization.ipynb
        ├── 2_2_ml_regressor_original_data.ipynb
        ├── 2_3_ml_regressor_modified_data.ipynb
        ├── 2_4_ml_regressor_lgbm_tuning.ipynb
        ├── 3_1_preprocessing_ml_reg_nxt_rnd_val.ipynb
        ├── 3_2_ml_regressor_next_round_value.ipynb
        ├── 4_1_prepr_ml_clas_nxt_rnd_val.ipynb
        ├── 4_2_algorithm_election_gridsearch_ml_clas_nxt_rnd_val.ipynb
        ├── 4_3_ml_clas_nxt_rnd_val.ipynb
        ├── 5_1_prepr_ml_clas_winner_team.ipynb
        ├── 5_2_algorithm_election_ml_clas_winner_team.ipynb
        └── 6_output.ipynb
```



### :love_letter: Contact info
Getting help, getting involved, hire me please.

 ----
 ----
 ------------
 ----
 ----
 
 
 
The README file describes the essence of the project playing the most important role. Most visitors will simply scroll down about twice on the README and leave if they are not interested. So, the README file should provide the reason **why** to checkout your project!!!). 
Bearing that in mind, your job is to: 
- Tell them what it is (with context).
- Show them what it looks like in action.
- Show them how they use it.
- Tell them any other relevant details.



---

## **Formatting**
Your readers will most likely view your README in a browser so please keep that in mind when formatting its content: 
- Use proper format when necesary (e.g.: `import pandas as pd`). 
- Categorize content using two or three levels of header beneath. 
- Make use of **emphasis** to call out important words. 
- Link to project pages for related libraries you mention. Link to Wikipedia, Wiktionary, even Urban Dictionary definitions for words of which a reader may not be familiar. Make amusing cultural references. 
- Add links to related projects or services. 

> Here you have a markdown cheatsheet [Link](https://commonmark.org/help/) and tutorial [Link](https://commonmark.org/help/tutorial/).


## **Start writing ASAP:**
*Last but not least, by writing your README soon you give yourself some pretty significant advantages. Most importantly, you’re giving yourself a chance to think through the project without the overhead of having to change code every time you change your mind about how something should be organized or what should be included.*


## **Suggested Structure:**

### :raising_hand: **Name** 
Self-explanatory names are best. If the name sounds too vague or unrelated, it may be a signal to move on. It also must be catchy. Images, Logo, Gif or some color is strongly recommended.

### :baby: **Status**
Alpha, Beta, 1.1, Ironhack Data Analytics Final Project, etc... It's OK to write a sentence, too. The goal is to let interested people know where this project is at.

### :running: **One-liner**
Having a one-liner that describes the pipeline/api/app is useful for getting an idea of what your code does in slightly greater detail. 

### :computer: **Technology stack**
Python, Pandas, Scipy, Scikit-learn, etc. Indicate the technological nature of the software, including primary programming language(s), main libraries and whether the software is intended as standalone or as a module in a framework or other ecosystem.

### :boom: **Core technical concepts and inspiration**
Why does it exist? Frame your project for the potential user. Compare/contrast your project with other, similar projects so the user knows how it is different from those projects. Highlight the technical concepts that your project demonstrates or supports. Keep it very brief.

### :wrench: **Configuration**
Requeriments, prerequisites, dependencies, installation instructions.

### :see_no_evil: **Usage**
Parameters, return values, known issues, thrown errors.

### :file_folder: **Folder structure**
```
└── project
    ├── __trash__
    ├── .gitignore
    ├── .env
    ├── requeriments.txt
    ├── README.md
    ├── main_script.py
    ├── notebooks
    │   ├── notebook1.ipynb
    │   └── notebook2.ipynb
    ├── package1
    │   ├── module1.py
    │   └── module2.py
    └── data
        ├── raw
        ├── processed
        └── results
```

> Do not forget to include `__trash__` and `.env` in `.gitignore` 

### :shit: **ToDo**
Next steps, features planned, known bugs (shortlist).

### :information_source: **Further info**
Credits, alternatives, references, license.

### :love_letter: **Contact info**
Getting help, getting involved, hire me please.
