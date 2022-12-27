# Movies_reviews_Sentiment_analysis
---
jupyter:
  colab:
    collapsed_sections:
    - XVshoq4VL6wM
    - g3-jKaA-R9dw
    - Xz9cKm8o_ROl
    - n7M8ELS10CHT
    - TFTH0kJ6EI1p
    - IOsLkzIn3IME
    - aJvi-NSee6q8
    - z_09fAuhHgmM
    - lJQqKtctjeo-
    - IBsG8REE_tR5
    - othUNV_tmOGT
    - XdCFpmFcgK4f
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .markdown id="-5xhN0kTAyrL"}
# Install and import packages
:::

::: {.cell .markdown id="XVshoq4VL6wM"}
## Install
:::

::: {.cell .code execution_count="1" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="fp7Nnl-gAqki" outputId="f59c1b3c-2875-4600-cc63-dc391f009330"}
``` {.python}
!pip install tmdbsimple
```

::: {.output .stream .stdout}
    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Collecting tmdbsimple
      Downloading tmdbsimple-2.9.1-py3-none-any.whl (38 kB)
    Requirement already satisfied: requests in /usr/local/lib/python3.8/dist-packages (from tmdbsimple) (2.23.0)
    Requirement already satisfied: idna<3,>=2.5 in /usr/local/lib/python3.8/dist-packages (from requests->tmdbsimple) (2.10)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.8/dist-packages (from requests->tmdbsimple) (2022.12.7)
    Requirement already satisfied: chardet<4,>=3.0.2 in /usr/local/lib/python3.8/dist-packages (from requests->tmdbsimple) (3.0.4)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /usr/local/lib/python3.8/dist-packages (from requests->tmdbsimple) (1.24.3)
    Installing collected packages: tmdbsimple
    Successfully installed tmdbsimple-2.9.1
:::
:::

::: {.cell .code execution_count="2" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="_JPkHU-v_pBm" outputId="95c99846-de23-4eb0-a0b5-b9dd54d9b346"}
``` {.python}
!pip install BeautifulSoup4
```

::: {.output .stream .stdout}
    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: BeautifulSoup4 in /usr/local/lib/python3.8/dist-packages (4.6.3)
:::
:::

::: {.cell .code execution_count="3" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="p6owR9Fi33KN" outputId="1ffc2edf-976d-4992-da0a-286ddc2414d2"}
``` {.python}
!pip install --upgrade gensim
```

::: {.output .stream .stdout}
    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: gensim in /usr/local/lib/python3.8/dist-packages (3.6.0)
    Collecting gensim
      Downloading gensim-4.3.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (24.1 MB)
    ent already satisfied: smart-open>=1.8.1 in /usr/local/lib/python3.8/dist-packages (from gensim) (6.3.0)
    Requirement already satisfied: scipy>=1.7.0 in /usr/local/lib/python3.8/dist-packages (from gensim) (1.7.3)
    Collecting FuzzyTM>=0.4.0
      Downloading FuzzyTM-2.0.5-py3-none-any.whl (29 kB)
    Requirement already satisfied: numpy>=1.18.5 in /usr/local/lib/python3.8/dist-packages (from gensim) (1.21.6)
    Collecting pyfume
      Downloading pyFUME-0.2.25-py3-none-any.whl (67 kB)
    ent already satisfied: pandas in /usr/local/lib/python3.8/dist-packages (from FuzzyTM>=0.4.0->gensim) (1.3.5)
    Requirement already satisfied: python-dateutil>=2.7.3 in /usr/local/lib/python3.8/dist-packages (from pandas->FuzzyTM>=0.4.0->gensim) (2.8.2)
    Requirement already satisfied: pytz>=2017.3 in /usr/local/lib/python3.8/dist-packages (from pandas->FuzzyTM>=0.4.0->gensim) (2022.6)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.8/dist-packages (from python-dateutil>=2.7.3->pandas->FuzzyTM>=0.4.0->gensim) (1.15.0)
    Collecting fst-pso
      Downloading fst-pso-1.8.1.tar.gz (18 kB)
    Collecting simpful
      Downloading simpful-2.9.0-py3-none-any.whl (30 kB)
    Collecting miniful
      Downloading miniful-0.0.6.tar.gz (2.8 kB)
    Requirement already satisfied: requests in /usr/local/lib/python3.8/dist-packages (from simpful->pyfume->FuzzyTM>=0.4.0->gensim) (2.23.0)
    Requirement already satisfied: chardet<4,>=3.0.2 in /usr/local/lib/python3.8/dist-packages (from requests->simpful->pyfume->FuzzyTM>=0.4.0->gensim) (3.0.4)
    Requirement already satisfied: idna<3,>=2.5 in /usr/local/lib/python3.8/dist-packages (from requests->simpful->pyfume->FuzzyTM>=0.4.0->gensim) (2.10)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.8/dist-packages (from requests->simpful->pyfume->FuzzyTM>=0.4.0->gensim) (2022.12.7)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /usr/local/lib/python3.8/dist-packages (from requests->simpful->pyfume->FuzzyTM>=0.4.0->gensim) (1.24.3)
    Building wheels for collected packages: fst-pso, miniful
      Building wheel for fst-pso (setup.py) ... e=fst_pso-1.8.1-py3-none-any.whl size=20443 sha256=5d40595babfea8e864b81b2abdd25a06c484a456482fbf96338889d5a0d8ed52
      Stored in directory: /root/.cache/pip/wheels/6a/65/c4/d27eeee9ba3fc150a0dae150519591103b9e0dbffde3ae77dc
      Building wheel for miniful (setup.py) ... iniful: filename=miniful-0.0.6-py3-none-any.whl size=3530 sha256=d4e236b14ac0bed0be2f2c2efabf710aa41d1eafdedeef637a96a4fe02db9ca4
      Stored in directory: /root/.cache/pip/wheels/ba/d9/a0/ddd93af16d5855dd9bad417623e70948fdac119d1d34fb17c8
    Successfully built fst-pso miniful
    Installing collected packages: miniful, simpful, fst-pso, pyfume, FuzzyTM, gensim
      Attempting uninstall: gensim
        Found existing installation: gensim 3.6.0
        Uninstalling gensim-3.6.0:
          Successfully uninstalled gensim-3.6.0
    Successfully installed FuzzyTM-2.0.5 fst-pso-1.8.1 gensim-4.3.0 miniful-0.0.6 pyfume-0.2.25 simpful-2.9.0
:::
:::

::: {.cell .markdown id="YeOMovd2L-le"}
## Import
:::

::: {.cell .code execution_count="4" id="Y0yqmqx5Az-K"}
``` {.python}
import tmdbsimple as tmdb
import requests
import time
import json


import pandas as pd
import numpy as np
```
:::

::: {.cell .code execution_count="5" id="ri5vH0MHi2KE"}
``` {.python}
from sklearn.model_selection import GridSearchCV
```
:::

::: {.cell .markdown id="g3-jKaA-R9dw"}
# Files from Google Drive
:::

::: {.cell .code execution_count="6" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="FCgteASoSA3L" outputId="55dde5cb-be13-4ffc-b37f-41d6214973d1"}
``` {.python}
from google.colab import drive
drive.mount('/content/drive')
```

::: {.output .stream .stdout}
    Mounted at /content/drive
:::
:::

::: {.cell .code execution_count="7" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="JUIHY1lXjk6O" outputId="85ccb806-c316-4c84-a32d-58463e9cb90b"}
``` {.python}
!ls -lh
```

::: {.output .stream .stdout}
    total 8.0K
    drwx------ 6 root root 4.0K Dec 21 07:30 drive
    drwxr-xr-x 1 root root 4.0K Dec 19 14:31 sample_data
:::
:::

::: {.cell .code execution_count="15" id="qNVKxB-H5kWY"}
``` {.python}
!cp /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/tmdb_api_key.txt /content/
!cp /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/movies500.csv /content/
!cp /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/300features_40minwords_10context /content/
```
:::

::: {.cell .code execution_count="9" id="j6AG8dokSJxd"}
``` {.python}
#!cp /content/movies500.csv /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/movies500.csv
#!cp /content/movies500.json /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/movies500.json
#!cp /content/300features_40minwords_10context /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/300features_40minwords_10context
```
:::

::: {.cell .markdown id="hrTiaYfoA-UO"}
# Main
:::

::: {.cell .markdown id="Xz9cKm8o_ROl"}
## Methods
:::

::: {.cell .code execution_count="10" id="JMFTvFskw_4o"}
``` {.python}
def format_reviews_json(tmdb_response_json, return_exceptions = False):
  reviews = []
  exceptions = {'rating':[], 'content':[]}

  for item in tmdb_response_json['results']:
    review = {'id': item['id']}

    try:
      review['rating'] = item['author_details']['rating']
    except:
      review['rating'] = None
      exceptions['rating'].append(item['id'])
    
    try:
      review['review'] = item['content']
    except:
      review['review'] = None
      exceptions['content'].append(item['id'])
    
    reviews.append(review)
  
  if return_exceptions:
    return reviews, exceptions
  else:
    return reviews
```
:::

::: {.cell .code execution_count="11" id="qQJnNYrCPogc"}
``` {.python}
def get_films_reviews(tmbd_api_key, films_dict: dict):
  tmdb.API_KEY = tmbd_api_key
  tmdb.REQUESTS_SESSION = requests.Session()

  dfs = []
  for key, value in films_dict.items():
    reviews_dict = format_reviews_json(tmdb.Movies(key).reviews())
    df = pd.DataFrame.from_dict(reviews_dict)
    df['film'] = value
    dfs.append(df)

  return pd.concat(dfs)
```
:::

::: {.cell .code execution_count="12" id="1YchwQvdVMS0"}
``` {.python}
def get_films_dict(films_dicts_list):
  films_dict = {}
  for film_dict in films_dicts_list:
    films_dict[film_dict['id']] = film_dict['original_title']
  return films_dict
```
:::

::: {.cell .code execution_count="13" id="JkeKoAGWTnD9"}
``` {.python}
def dict_list_to_json(dict_list: list, save_path: str):
  with open(save_path, 'w', encoding='utf-8') as f:
    json.dump({'count': len(dict_list), 'items': dict_list}, f, ensure_ascii=False, indent=4)
```
:::

::: {.cell .code execution_count="14" id="eBgRjH414oO0"}
``` {.python}
def get_movies(tmdb, page: int):
  discover = tmdb.Discover()
  results = []
  for page in range(1, page + 1):
    if page % 5 == 0:
      print('Page', page)
    response = discover.movie(sort_by = 'vote_count.desc', page = page)
    results.extend(response['results'])
    time.sleep(0.33)
  return results
```
:::

::: {.cell .markdown id="HGyMD8Om_T9D"}
## Main {#main}
:::

::: {.cell .markdown id="YV5C_lrFhDnC"}
## Get data
:::

::: {.cell .markdown id="n7M8ELS10CHT"}
### Via API
:::

::: {.cell .markdown id="ozO2YoL7oDtB"}
Options to eliminate score bias:

1.  vote_average.asc(n) + vote_average.desc(n)
2.  sort them by date - but consider vote_count.gte

**filter eng**
:::

::: {.cell .code id="epbw8IZ9A_Th"}
``` {.python}
with open('/content/tmdb_api_key.txt') as key_file:
  api_key = key_file.read()
```
:::

::: {.cell .code id="-VS8rcBdd0MN"}
``` {.python}
tmdb.API_KEY = api_key
tmdb.REQUESTS_SESSION = requests.Session()
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="LVhCM8mNkGYI" outputId="933e9674-f840-451c-b3db-8ab4b98e9a18"}
``` {.python}
movies500 = get_movies(tmdb, 500)
```

::: {.output .stream .stdout}
    Page 5
    Page 10
    Page 15
    Page 20
    Page 25
    Page 30
    Page 35
    Page 40
    Page 45
    Page 50
    Page 55
    Page 60
    Page 65
    Page 70
    Page 75
    Page 80
    Page 85
    Page 90
    Page 95
    Page 100
    Page 105
    Page 110
    Page 115
    Page 120
    Page 125
    Page 130
    Page 135
    Page 140
    Page 145
    Page 150
    Page 155
    Page 160
    Page 165
    Page 170
    Page 175
    Page 180
    Page 185
    Page 190
    Page 195
    Page 200
    Page 205
    Page 210
    Page 215
    Page 220
    Page 225
    Page 230
    Page 235
    Page 240
    Page 245
    Page 250
    Page 255
    Page 260
    Page 265
    Page 270
    Page 275
    Page 280
    Page 285
    Page 290
    Page 295
    Page 300
    Page 305
    Page 310
    Page 315
    Page 320
    Page 325
    Page 330
    Page 335
    Page 340
    Page 345
    Page 350
    Page 355
    Page 360
    Page 365
    Page 370
    Page 375
    Page 380
    Page 385
    Page 390
    Page 395
    Page 400
    Page 405
    Page 410
    Page 415
    Page 420
    Page 425
    Page 430
    Page 435
    Page 440
    Page 445
    Page 450
    Page 455
    Page 460
    Page 465
    Page 470
    Page 475
    Page 480
    Page 485
    Page 490
    Page 495
    Page 500
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="EDlzFP64leWR" outputId="7727f545-5508-4c74-9d82-0b8df98aaa96"}
``` {.python}
len(movies500)
```

::: {.output .execute_result execution_count="66"}
    10000
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="n8HEa178lDH2" outputId="613abe3e-7d62-454b-9a8f-e77dac7e5ec4"}
``` {.python}
movies500[0]
```

::: {.output .execute_result execution_count="58"}
    {'adult': False,
     'backdrop_path': '/s3TBrRGB1iav7gFOCNx3H31MoES.jpg',
     'genre_ids': [28, 878, 12],
     'id': 27205,
     'original_language': 'en',
     'original_title': 'Inception',
     'overview': 'Cobb, a skilled thief who commits corporate espionage by infiltrating the subconscious of his targets is offered a chance to regain his old life as payment for a task considered to be impossible: "inception", the implantation of another person\'s idea into a target\'s subconscious.',
     'popularity': 85.532,
     'poster_path': '/8IB2e4r4oVhHnANbnm7O3Tj6tF8.jpg',
     'release_date': '2010-07-15',
     'title': 'Inception',
     'video': False,
     'vote_average': 8.4,
     'vote_count': 32778}
:::
:::

::: {.cell .code colab="{\"height\":36,\"base_uri\":\"https://localhost:8080/\"}" id="vrMC8oY8OZl4" outputId="47bad832-ae4e-4ccd-f718-3e26c5c191d3"}
``` {.python}
ids_500 = get_films_dict(movies500)
ids_500[787]
```

::: {.output .execute_result execution_count="61"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .code id="w0__zNroQ1TZ"}
``` {.python}
df_500 = get_films_reviews(api_key, ids_500)
```
:::

::: {.cell .code colab="{\"height\":424,\"base_uri\":\"https://localhost:8080/\"}" id="86tTU9JERDrL" outputId="9e1d83dd-9bd4-43b8-e426-fc4f03892120"}
``` {.python}
df_500
```

::: {.output .execute_result execution_count="67"}
```{=html}
  <div id="df-0ffdbdb9-63bb-4cc7-96eb-dc54cb433341">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>rating</th>
      <th>review</th>
      <th>film</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>589c420fc3a3684cde007279</td>
      <td>NaN</td>
      <td>When I first saw the trailer for this film, I ...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5c842825925141277a1f5db9</td>
      <td>8.0</td>
      <td>Whether you watch Inception as a heist movie, ...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5da8071d944a570019251c8a</td>
      <td>NaN</td>
      <td>Is there anyone on earth who doesn't like Chri...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5e2f2902326c1900121c04ca</td>
      <td>9.0</td>
      <td>Ariadne: "Why is it so important to dream?"\r\...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5f639841069f0e0036ad1f9b</td>
      <td>NaN</td>
      <td>This is actually a Perfect movie. It is the 2n...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>56109278c3a368680e0106e3</td>
      <td>7.0</td>
      <td>The Magnificent Four!\r\n\r\nJohn, Tom, Matt a...</td>
      <td>The Sons of Katie Elder</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5424a5f50e0a26457600010d</td>
      <td>7.0</td>
      <td>Talk is never cheap when sourced from Tennesse...</td>
      <td>Suddenly, Last Summer</td>
    </tr>
    <tr>
      <th>1</th>
      <td>630ae958dcb6a3007bb3f54d</td>
      <td>6.0</td>
      <td>Howard Hawks defined a good film as “three goo...</td>
      <td>Suddenly, Last Summer</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5a8d38410e0a267c6b004729</td>
      <td>NaN</td>
      <td>Surinder (Shah Rukh Khan), a 40+ shy guy, come...</td>
      <td>रब ने बना दी जोड़ी</td>
    </tr>
    <tr>
      <th>0</th>
      <td>561098b59251415e53004554</td>
      <td>8.0</td>
      <td>Frosty reception assured.\r\n\r\nThe Spy Who C...</td>
      <td>The Spy Who Came in from the Cold</td>
    </tr>
  </tbody>
</table>
<p>11137 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0ffdbdb9-63bb-4cc7-96eb-dc54cb433341')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0ffdbdb9-63bb-4cc7-96eb-dc54cb433341 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0ffdbdb9-63bb-4cc7-96eb-dc54cb433341');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code colab="{\"height\":36,\"base_uri\":\"https://localhost:8080/\"}" id="EzHu0R1GSN0U" outputId="334d33cc-3c68-4680-8504-f49d2feb5eea"}
``` {.python}
'''dict_list_to_json(movies500, 'movies500.json')
df_500.to_csv('movies500.csv')'''
```

::: {.output .execute_result execution_count="72"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .markdown id="TAbvNUOc0LHm"}
### Via saved results
:::

::: {.cell .code id="lmBF0_RT0THk"}
``` {.python}
#!cp /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/desc199.csv /content/desc199.csv 
#!cp /content/desc199.json /content/drive/MyDrive/Colab_Notebooks/hse/web_data_analysis/big_nlp/desc199.json
```
:::

::: {.cell .code execution_count="17" colab="{\"height\":424,\"base_uri\":\"https://localhost:8080/\"}" id="kv1md_Lw0e5-" outputId="27b22ac8-ae53-4d1e-f363-72683ead44dd"}
``` {.python}
df_500 = pd.read_csv('/content/movies500.csv', index_col='Unnamed: 0')
df_500
```

::: {.output .execute_result execution_count="17"}
```{=html}
  <div id="df-ea441114-1a6e-49f5-80dd-0b09b49e6c20">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>rating</th>
      <th>review</th>
      <th>film</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>589c420fc3a3684cde007279</td>
      <td>NaN</td>
      <td>When I first saw the trailer for this film, I ...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5c842825925141277a1f5db9</td>
      <td>8.0</td>
      <td>Whether you watch Inception as a heist movie, ...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5da8071d944a570019251c8a</td>
      <td>NaN</td>
      <td>Is there anyone on earth who doesn't like Chri...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5e2f2902326c1900121c04ca</td>
      <td>9.0</td>
      <td>Ariadne: "Why is it so important to dream?"\r\...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5f639841069f0e0036ad1f9b</td>
      <td>NaN</td>
      <td>This is actually a Perfect movie. It is the 2n...</td>
      <td>Inception</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>56109278c3a368680e0106e3</td>
      <td>7.0</td>
      <td>The Magnificent Four!\r\n\r\nJohn, Tom, Matt a...</td>
      <td>The Sons of Katie Elder</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5424a5f50e0a26457600010d</td>
      <td>7.0</td>
      <td>Talk is never cheap when sourced from Tennesse...</td>
      <td>Suddenly, Last Summer</td>
    </tr>
    <tr>
      <th>1</th>
      <td>630ae958dcb6a3007bb3f54d</td>
      <td>6.0</td>
      <td>Howard Hawks defined a good film as “three goo...</td>
      <td>Suddenly, Last Summer</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5a8d38410e0a267c6b004729</td>
      <td>NaN</td>
      <td>Surinder (Shah Rukh Khan), a 40+ shy guy, come...</td>
      <td>रब ने बना दी जोड़ी</td>
    </tr>
    <tr>
      <th>0</th>
      <td>561098b59251415e53004554</td>
      <td>8.0</td>
      <td>Frosty reception assured.\r\n\r\nThe Spy Who C...</td>
      <td>The Spy Who Came in from the Cold</td>
    </tr>
  </tbody>
</table>
<p>11137 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ea441114-1a6e-49f5-80dd-0b09b49e6c20')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ea441114-1a6e-49f5-80dd-0b09b49e6c20 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ea441114-1a6e-49f5-80dd-0b09b49e6c20');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .markdown id="VRVifTyUhLLq"}
## Transform data
:::

::: {.cell .markdown id="TFTH0kJ6EI1p"}
### Basic preprocessing
:::

::: {.cell .code execution_count="18" id="Orn7UzE4EVxM"}
``` {.python}
import matplotlib.pyplot as plt
import seaborn as sns
```
:::

::: {.cell .code execution_count="19" id="o16OUc2qA4UW"}
``` {.python}
def preprocess_reviews_data(df: pd.DataFrame, train_percentage = 0.7, random_state=17):
  # Handle NaNs
  df_clean = df.dropna()

  # Rating binarization
  df_clean.loc[df_clean['rating'] < 7, 'sentiment'] = 0
  df_clean.loc[df_clean['rating'] >= 7, 'sentiment'] = 1

  # Train/Test split
  train = df_clean.sample(frac=train_percentage, random_state=random_state)
  test = df_clean[~df_clean['id'].isin(list(train.id))]

  return train, test
```
:::

::: {.cell .code execution_count="20" colab="{\"height\":297,\"base_uri\":\"https://localhost:8080/\"}" id="K1xMewezR0Q-" outputId="febee5b0-bbc2-47c1-8b7a-6cfa1b6dd4bd"}
``` {.python}
sns.histplot(df_500.rating)
```

::: {.output .execute_result execution_count="20"}
    <matplotlib.axes._subplots.AxesSubplot at 0x7ff6b65d99d0>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/ed6e675555419b8a7277f08d99bb947c54cc2588.png)
:::
:::

::: {.cell .code execution_count="212" colab="{\"height\":297,\"base_uri\":\"https://localhost:8080/\"}" id="q-6aK9sJZXxd" outputId="d505cde2-b053-4324-ff9a-4fe801b8aa21"}
``` {.python}
sns.histplot(train.sentiment)
```

::: {.output .execute_result execution_count="212"}
    <matplotlib.axes._subplots.AxesSubplot at 0x7ff6afda0940>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/9f38ac4cfe60bd9cfe5eea54c4d681f6f1b94209.png)
:::
:::

::: {.cell .code execution_count="21" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="fncl9FOPVV3J" outputId="6612efd2-a320-471b-d7c9-501ba1473631"}
``` {.python}
df_500.rating.describe()
```

::: {.output .execute_result execution_count="21"}
    count    10007.000000
    mean         6.613670
    std          2.065922
    min          0.500000
    25%          5.000000
    50%          7.000000
    75%          8.000000
    max         10.000000
    Name: rating, dtype: float64
:::
:::

::: {.cell .code execution_count="22" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="UpDFSHqICk93" outputId="6ab96bd5-ddb0-4c5f-a91c-05f18c0b6675"}
``` {.python}
train, test = preprocess_reviews_data(df_500)
```

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/pandas/core/indexing.py:1684: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self.obj[key] = infer_fill_value(value)
    /usr/local/lib/python3.8/dist-packages/pandas/core/indexing.py:1817: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self._setitem_single_column(loc, value, pi)
:::
:::

::: {.cell .code execution_count="23" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="0TC0AAraBtng" outputId="18078783-e548-4e43-8a8e-257ce627803f"}
``` {.python}
print(len(list(train[train['rating'].isna()].id)))
print(len(train) / len(df_500.dropna()))
print(set(test.id) & set(train.id))
```

::: {.output .stream .stdout}
    0
    0.7000099930048965
    set()
:::
:::

::: {.cell .code execution_count="24" colab="{\"height\":455,\"base_uri\":\"https://localhost:8080/\"}" id="GxpY-LikXixQ" outputId="738c44be-4754-4eca-afd0-bc765212438e"}
``` {.python}
train.groupby(['film']).count().sort_values(['review'], ascending = False)
```

::: {.output .execute_result execution_count="24"}
```{=html}
  <div id="df-a7cee6f9-0b66-4057-9a48-cfbea7a50898">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>rating</th>
      <th>review</th>
      <th>sentiment</th>
    </tr>
    <tr>
      <th>film</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Batman</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>Top Gun: Maverick</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
    <tr>
      <th>Star Wars: The Rise of Skywalker</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>The Mummy</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>Spider-Man: Far from Home</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Dirty Rotten Scoundrels</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Dirty Grandpa</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Diego Maradona</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Pixels</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Coach Carter</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>4034 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a7cee6f9-0b66-4057-9a48-cfbea7a50898')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a7cee6f9-0b66-4057-9a48-cfbea7a50898 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a7cee6f9-0b66-4057-9a48-cfbea7a50898');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code execution_count="25" id="z4XcApRv_brd"}
``` {.python}
train = train[['id','sentiment','review','film']]
test = test[['id','sentiment','review','film']]
```
:::

::: {.cell .code execution_count="26" colab="{\"height\":36,\"base_uri\":\"https://localhost:8080/\"}" id="svjjEE9n2p8r" outputId="8977b92d-e0b7-4c2c-e5fa-d74ae0b1c72b"}
``` {.python}
'''train.to_csv('film_train.csv')
train.to_csv('film_test.csv')'''
```

::: {.output .execute_result execution_count="26"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .markdown id="PXKBpJL_EKxs"}
### Reviews text to Bag of words
:::

::: {.cell .code execution_count="29" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="W459Obavm_ps" outputId="c699f4fc-f1a8-4094-c3aa-d5f9964d0371"}
``` {.python}
from bs4 import BeautifulSoup 
import re

import nltk
import nltk.data

nltk.download('stopwords')
from nltk.corpus import stopwords

from sklearn.feature_extraction.text import CountVectorizer
```

::: {.output .stream .stderr}
    [nltk_data] Downloading package stopwords to /root/nltk_data...
    [nltk_data]   Unzipping corpora/stopwords.zip.
:::
:::

::: {.cell .code execution_count="222" colab="{\"height\":424,\"base_uri\":\"https://localhost:8080/\"}" id="aTxFqGEHbKb-" outputId="0a4e5601-29fc-4a87-a59d-5c1d6f4a3897"}
``` {.python}
train
```

::: {.output .execute_result execution_count="222"}
```{=html}
  <div id="df-4fd7a351-a5a8-4ede-a3fd-c5d555896142">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>sentiment</th>
      <th>review</th>
      <th>film</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55d9073192514143e6002fa9</td>
      <td>0.0</td>
      <td>Doogtooth, the official Greek entry to the 201...</td>
      <td>Κυνόδοντας</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5ee0d7baf03174001fdd4c55</td>
      <td>0.0</td>
      <td>I've made no secret about my opinions on Samar...</td>
      <td>Guns Akimbo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>637b5dd45b2f47007fd76d02</td>
      <td>1.0</td>
      <td>"Snatcher" is determined to get himself a whit...</td>
      <td>The Boxtrolls</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5851b75e92514146c9009316</td>
      <td>0.0</td>
      <td>**They are not superheroes, they are supervill...</td>
      <td>Suicide Squad</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5d945aa887ae7b001ca46290</td>
      <td>0.0</td>
      <td>When I hear the drumming of hooves, I don't th...</td>
      <td>Red Lights</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>619018d388634800437ad225</td>
      <td>0.0</td>
      <td>_**Manor-in-the-woods thriller/horror**_\r\n\r...</td>
      <td>Cold Creek Manor</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5a5b08c5c3a36867e401affe</td>
      <td>1.0</td>
      <td>Perplexed by the storyline at the beginning, d...</td>
      <td>The Prestige</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5ea722a2514c4a001f8aa263</td>
      <td>0.0</td>
      <td>_**Rambo goes to Afghanistan to fight Russians...</td>
      <td>Rambo III</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5ec47bcf28723c0021489870</td>
      <td>1.0</td>
      <td>Click here for a video version of this review:...</td>
      <td>Watchmen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>62c4ddc0dcb6a30053dd7f15</td>
      <td>1.0</td>
      <td>**An excellent film.**\r\n\r\nI confess that t...</td>
      <td>Silver Linings Playbook</td>
    </tr>
  </tbody>
</table>
<p>7005 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-4fd7a351-a5a8-4ede-a3fd-c5d555896142')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-4fd7a351-a5a8-4ede-a3fd-c5d555896142 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4fd7a351-a5a8-4ede-a3fd-c5d555896142');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code execution_count="223" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="CNMwt3KvaEDQ" outputId="25e8ed8f-f827-41ab-cb2e-aad219603f2b"}
``` {.python}
print(str(train.review[2]))
```

::: {.output .stream .stdout}
    2    I've made no secret about my opinions on Samar...
    2    "Marty" (Michael J Fox) is stuck in 1955 when ...
    2    "Bambi" is born into an idyllic forest life - ...
    2    How is this not super entertaining?\r\n\r\n<em...
    2    Iron Man did a lot more than just launch the M...
                               ...                        
    2    > Review From **_Horror Focus_**\r\n\r\nGainin...
    2    Probably my favorite of the Stephen King adapt...
    2    Humanity’s worst kept secret is that the world...
    2    Not a great film, but two things that made it ...
    2    **An excellent film.**\r\n\r\nI confess that t...
    Name: review, Length: 840, dtype: object
:::
:::

::: {.cell .code execution_count="56" id="BjojD7nDBP8v"}
``` {.python}
def review_to_words(raw_review, remove_stopwords=False):
    # Function to convert a raw review to a string of words
    # The input is a single string (a raw movie review), and 
    # the output is a single string (a preprocessed movie review)
    
    # 1. Remove HTML
    review_text = BeautifulSoup(raw_review).get_text()
    # 2. Remove non-letters        
    letters_only = re.sub("[^a-zA-Z]", " ", review_text)
    # 3. Convert to lower case, split into individual words
    words = letters_only.lower().split()     
    # 5. Remove stop words
    if remove_stopwords:
      stops = set(stopwords.words("english"))
      words = [w for w in words if not w in stops]
    # 6. Join the words back into one string separated by space, and return the result.
    return(" ".join(words))
```
:::

::: {.cell .code execution_count="118" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="i_0AsciyfR-U" outputId="753d195f-9a5a-4bcb-aaa9-c0c61e0e9d88"}
``` {.python}
print("Cleaning and parsing the training set movie reviews...\n")
num_reviews = len(train.review)
train_cl_bw = []

for review in train.review:
  train_cl_bw.append(review_to_words(review, remove_stopwords=True))
```

::: {.output .stream .stdout}
    Cleaning and parsing the training set movie reviews...
:::

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/bs4/__init__.py:270: UserWarning: "b'.'" looks like a filename, not markup. You should probably open this file and pass the filehandle into Beautiful Soup.
      warnings.warn(
:::
:::

::: {.cell .code execution_count="225" colab="{\"height\":91,\"base_uri\":\"https://localhost:8080/\"}" id="bW8g0kUODRSG" outputId="6d19b1d8-c4fd-4420-8360-faa20c24d522"}
``` {.python}
train_cl_bw[1]
```

::: {.output .execute_result execution_count="225"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .code execution_count="120" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="IyQzgFq9EQo8" outputId="107a0c93-0289-408b-cda9-3eb45467e144"}
``` {.python}
print("Creating the bag of words...\n")

# Initialize the "CountVectorizer" object, which is scikit-learn's
# bag of words tool.  
vectorizer = CountVectorizer(analyzer = "word",   
                             tokenizer = None,    
                             preprocessor = None, 
                             stop_words = None,   
                             max_features = 5000) 

# fit_transform() does two functions: First, it fits the model
# and learns the vocabulary; second, it transforms our training data
# into feature vectors. The input to fit_transform should be a list of 
# strings.
train_features_bw = vectorizer.fit_transform(train_cl_bw)

# Numpy arrays are easy to work with, so convert the result to an 
# array
train_features_bw = train_features_bw.toarray()
```

::: {.output .stream .stdout}
    Creating the bag of words...
:::
:::

::: {.cell .code execution_count="121" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="Q7wgrpXNFdAI" outputId="6eb9108b-c0fd-4f94-e600-7881fad93de8"}
``` {.python}
train_features_bw.shape
```

::: {.output .execute_result execution_count="121"}
    (7005, 5000)
:::
:::

::: {.cell .code execution_count="63" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="4SmFFfqUF4TV" outputId="8bf0ffd8-54d5-4f1b-8864-1afa8f133c85"}
``` {.python}
# Take a look at the words in the vocabulary
vocab = vectorizer.get_feature_names()
vocab[:10]
```

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/sklearn/utils/deprecation.py:87: FutureWarning: Function get_feature_names is deprecated; get_feature_names is deprecated in 1.0 and will be removed in 1.2. Please use get_feature_names_out instead.
      warnings.warn(msg, category=FutureWarning)
:::

::: {.output .execute_result execution_count="63"}
    ['aaron',
     'abandoned',
     'abigail',
     'abilities',
     'ability',
     'able',
     'abrams',
     'abrupt',
     'absence',
     'absent']
:::
:::

::: {.cell .code execution_count="123" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="dsCK1_wjGHik" outputId="7e93cfc6-00d8-4e5e-90d6-e96a14c20743"}
``` {.python}
# Sum up the counts of each vocabulary word
dist = np.sum(train_features_bw, axis=0)

# For each, print the vocabulary word and the number of times it appears in the training set
word_count_dict = dict(sorted(dict(zip(vocab, dist)).items(), key=lambda item: item[1], reverse=True))
temp = 0

for tag, count in word_count_dict.items():
    print(count, tag)
    temp = temp + 1
    if temp == 20:
      break
```

::: {.output .stream .stdout}
    12818 film
    8811 movie
    7916 one
    5902 like
    5086 story
    4655 good
    4122 well
    3956 time
    3493 much
    3420 even
    3397 really
    3252 would
    3060 also
    2867 first
    2799 great
    2631 character
    2512 way
    2422 characters
    2398 two
    2334 get
:::
:::

::: {.cell .markdown id="IOsLkzIn3IME"}
### Reviews text to word vectors
:::

::: {.cell .markdown id="aJvi-NSee6q8"}
#### Parse reviews texts
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="uTndIrxHE7Ks" outputId="6e804e3c-0da4-40ea-fce5-e9b815471849"}
``` {.python}
from bs4 import BeautifulSoup 
import re

import nltk
import nltk.data

nltk.download('stopwords')
nltk.download('punkt')

from nltk.corpus import stopwords
```

::: {.output .stream .stderr}
    [nltk_data] Downloading package stopwords to /root/nltk_data...
    [nltk_data]   Package stopwords is already up-to-date!
    [nltk_data] Downloading package punkt to /root/nltk_data...
    [nltk_data]   Unzipping tokenizers/punkt.zip.
:::
:::

::: {.cell .code id="KE_AiWa3-l-p"}
``` {.python}
# Define a function to split a review into parsed sentences
def review_to_sentences(review, tokenizer, remove_stopwords=False):
    # Function to split a review into parsed sentences. Returns a 
    # list of sentences, where each sentence is a list of words
    #
    # 1. Use the NLTK tokenizer to split the paragraph into sentences
    raw_sentences = tokenizer.tokenize(review.strip())
    #
    # 2. Loop over each sentence
    sentences = []
    for raw_sentence in raw_sentences:
        # If a sentence is empty, skip it
        if len(raw_sentence) > 0:
            # Otherwise, call review_to_wordlist to get a list of words
            sentences.append(review_to_wordlist( raw_sentence, remove_stopwords ))
    #
    # Return the list of sentences (each sentence is a list of words,
    # so this returns a list of lists
    return sentences
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="3X4lVZiR-5Ho" outputId="86c954b6-839e-4713-ff01-019572c42d52"}
``` {.python}
tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')
sentences = []

print("Parsing sentences from training set")
for review in train["review"]:
    sentences += review_to_sentences(review, tokenizer)
```

::: {.output .stream .stdout}
    Parsing sentences from training set
:::

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/bs4/__init__.py:270: UserWarning: "b'.'" looks like a filename, not markup. You should probably open this file and pass the filehandle into Beautiful Soup.
      warnings.warn(
    /usr/local/lib/python3.8/dist-packages/bs4/__init__.py:332: UserWarning: "https://letterboxd.com/mayurpanchamia/film/schindlers-list/

    https://mayurpanchamia.wordpress.com/2022/03/27/schindlers-list/

    https://www.themoviedb.org/review/62405d62706e56005dc24c03" looks like a URL. Beautiful Soup is not an HTTP client. You should probably use an HTTP client like requests to get the document behind the URL, and feed that document to Beautiful Soup.
      warnings.warn(
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="NnxoW8ndGTrI" outputId="fc645011-1d6e-4817-ac1a-3149c4f31f19"}
``` {.python}
print(len(sentences))
print(sentences[0])
print(sentences[1])
```

::: {.output .stream .stdout}
    89945
    ['doogtooth', 'the', 'official', 'greek', 'entry', 'to', 'the', 'academy', 'awards', 'is', 'nominated', 'for', 'best', 'foreign', 'film']
    ['released', 'in', 'and', 'directed', 'by', 'giorgos', 'lanthimos', 'dogtooth', 'is', 'a', 'strikingly', 'original', 'film', 'that', 'captures', 'a', 'world', 'that', 'is', 'at', 'once', 'like', 'nothing', 'you', 've', 'ever', 'seen', 'but', 'oddly', 'familiar', 'at', 'the', 'same', 'time']
:::
:::

::: {.cell .markdown id="z_09fAuhHgmM"}
#### Train Word2Vec model
:::

::: {.cell .code id="tjZfMlGXHsa1"}
``` {.python}
import logging
from gensim.models import word2vec
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="yQbJSbX5HmDZ" outputId="70940199-5ce2-4019-a45d-f8c7df6b7d2a"}
``` {.python}
# Import the built-in logging module and configure it so that Word2Vec creates nice output messages
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

# Set values for various parameters
num_features = 300    # Word vector dimensionality                      
min_word_count = 40   # Minimum word count                        
num_workers = 4       # Number of threads to run in parallel
context = 10          # Context window size                                                                                    
downsampling = 1e-3   # Downsample setting for frequent words

# Initialize and train the model (this will take some time)
print("Training model...")
model = word2vec.Word2Vec(sentences, workers=num_workers, vector_size=num_features, min_count = min_word_count, window = context, sample = downsampling)

# If you don't plan to train the model any further, calling 
# init_sims will make the model much more memory-efficient.
model.init_sims(replace=True)

# It can be helpful to create a meaningful model name and 
# save the model for later use. You can load it later using Word2Vec.load()
model_name = "300features_40minwords_10context"
model.save(model_name)
```

::: {.output .stream .stdout}
    Training model...
:::

::: {.output .stream .stderr}
    <ipython-input-96-fe91a3bb84dd>:17: DeprecationWarning: Call to deprecated `init_sims` (Gensim 4.0.0 implemented internal optimizations that make calls to init_sims() unnecessary. init_sims() is now obsoleted and will be completely removed in future versions. See https://github.com/RaRe-Technologies/gensim/wiki/Migrating-from-Gensim-3.x-to-4).
      model.init_sims(replace=True)
    WARNING:gensim.models.keyedvectors:destructive init_sims(replace=True) deprecated & no longer required for space-efficiency
:::
:::

::: {.cell .code colab="{\"height\":36,\"base_uri\":\"https://localhost:8080/\"}" id="sLmVjwGpJVeV" outputId="1b91a361-95ec-412b-a190-30d774f6e85f"}
``` {.python}
model.wv.doesnt_match("man woman child dog".split())
```

::: {.output .execute_result execution_count="125"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .code colab="{\"height\":36,\"base_uri\":\"https://localhost:8080/\"}" id="yg9dirhIeLm-" outputId="f6aae2f5-4660-4987-fa25-ab8a6234b9df"}
``` {.python}
model.wv.doesnt_match("france england germany usa".split())
```

::: {.output .execute_result execution_count="121"}
``` {.json}
{"type":"string"}
```
:::
:::

::: {.cell .code execution_count="226" colab="{\"height\":171,\"base_uri\":\"https://localhost:8080/\"}" id="utfPlsQkJ5b0" outputId="f8ba6b9e-3020-468f-acb2-416307dd8e09"}
``` {.python}
model.wv.most_similar("man")
```

::: {.output .error ename="NameError" evalue="ignored"}
    ---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)
    <ipython-input-226-d5e2e8d4f792> in <module>
    ----> 1 model.wv.most_similar("man")

    NameError: name 'model' is not defined
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="VETWJ2BeKPtd" outputId="ff5903cd-5135-414d-a56b-f344418d8a00"}
``` {.python}
model.wv.most_similar("awful")
```

::: {.output .execute_result execution_count="104"}
    [('alright', 0.7079287767410278),
     ('terrible', 0.6673869490623474),
     ('weak', 0.660750150680542),
     ('unrealistic', 0.6487579345703125),
     ('lame', 0.6106228828430176),
     ('plain', 0.6099332571029663),
     ('acceptable', 0.6097782254219055),
     ('underdeveloped', 0.6063912510871887),
     ('forgettable', 0.6037163138389587),
     ('amazing', 0.6019044518470764)]
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="j_bdy050K_O4" outputId="656c6015-3498-4c5a-8acc-19cc5c292ae0"}
``` {.python}
model.wv.most_similar("abuse")
```

::: {.output .execute_result execution_count="105"}
    [('freedom', 0.8331371545791626),
     ('sexual', 0.8257376551628113),
     ('rights', 0.8134576678276062),
     ('corruption', 0.811524510383606),
     ('threat', 0.8114864826202393),
     ('gender', 0.8093193173408508),
     ('paranoia', 0.8065980076789856),
     ('corrupt', 0.8031841516494751),
     ('rage', 0.8017250895500183),
     ('victims', 0.798363208770752)]
:::
:::

::: {.cell .markdown id="lJQqKtctjeo-"}
### Numeric Representations of Words
:::

::: {.cell .markdown id="hPpkPQwukC88"}
#### From Words To Paragraphs: Vector Averaging
:::

::: {.cell .code execution_count="228" colab="{\"height\":268,\"base_uri\":\"https://localhost:8080/\"}" id="YRHuPP2lgo8K" outputId="30ae6f10-3fca-4eca-d675-e09972720628"}
``` {.python}
# Load the model that we created in Part 2
from gensim.models import Word2Vec
model = Word2Vec.load("300features_40minwords_10context")
```

::: {.output .error ename="ValueError" evalue="ignored"}
    ---------------------------------------------------------------------------
    ValueError                                Traceback (most recent call last)
    <ipython-input-228-6eb810613f90> in <module>
          1 # Load the model that we created in Part 2
    ----> 2 from gensim.models import Word2Vec
          3 model = Word2Vec.load("300features_40minwords_10context")

    /usr/local/lib/python3.8/dist-packages/gensim/__init__.py in <module>
          9 import logging
         10 
    ---> 11 from gensim import parsing, corpora, matutils, interfaces, models, similarities, utils  # noqa:F401
         12 
         13 

    /usr/local/lib/python3.8/dist-packages/gensim/corpora/__init__.py in <module>
          4 
          5 # bring corpus classes directly into package namespace, to save some typing
    ----> 6 from .indexedcorpus import IndexedCorpus  # noqa:F401 must appear before the other classes
          7 
          8 from .mmcorpus import MmCorpus  # noqa:F401

    /usr/local/lib/python3.8/dist-packages/gensim/corpora/indexedcorpus.py in <module>
         12 import numpy
         13 
    ---> 14 from gensim import interfaces, utils
         15 
         16 logger = logging.getLogger(__name__)

    /usr/local/lib/python3.8/dist-packages/gensim/interfaces.py in <module>
         17 import logging
         18 
    ---> 19 from gensim import utils, matutils
         20 
         21 

    /usr/local/lib/python3.8/dist-packages/gensim/matutils.py in <module>
       1028 try:
       1029     # try to load fast, cythonized code if possible
    -> 1030     from gensim._matutils import logsumexp, mean_absolute_difference, dirichlet_expectation
       1031 
       1032 except ImportError:

    /usr/local/lib/python3.8/dist-packages/gensim/_matutils.pyx in init gensim._matutils()

    ValueError: numpy.ndarray size changed, may indicate binary incompatibility. Expected 96 from C header, got 88 from PyObject
:::
:::

::: {.cell .code id="ff1SBqzBkRiy"}
``` {.python}
import numpy as np
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="tOldOIzwjslb" outputId="95822660-b7df-4c72-d643-a047e2803ecf"}
``` {.python}
type(model.wv.vectors)
```

::: {.output .execute_result execution_count="136"}
    numpy.ndarray
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="asM72j4Cju1w" outputId="36447ed6-d8e0-46a9-fd6d-34eb098261fb"}
``` {.python}
model.wv.vectors.shape
```

::: {.output .execute_result execution_count="137"}
    (3778, 300)
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="JhWnpXI_jw72" outputId="cfae07bb-fcd7-4dc8-9dad-c3ee61936037"}
``` {.python}
model.wv['usa'][:50]
```

::: {.output .execute_result execution_count="150"}
    array([-0.00111733,  0.04008844,  0.02902143,  0.05420322,  0.0197289 ,
           -0.06436826,  0.04677751,  0.17267807,  0.08071426, -0.13992894,
            0.04710537, -0.10228179,  0.02617793, -0.04400246, -0.08553369,
           -0.00946794,  0.02194865, -0.00435099,  0.06130483, -0.06793958,
           -0.06607263,  0.03427673,  0.09409263, -0.02322325,  0.10338218,
            0.1340662 , -0.1640573 ,  0.04998573, -0.19810176, -0.10649951,
            0.01827611, -0.05863674,  0.05691682, -0.02426377, -0.01570731,
           -0.0436501 , -0.02619314,  0.01380917,  0.00720511, -0.1404223 ,
            0.01345169, -0.03388495, -0.07173538, -0.05137645,  0.00039205,
            0.02092239,  0.04286343,  0.00738833, -0.05806842,  0.1023173 ],
          dtype=float32)
:::
:::

::: {.cell .code id="sNNO1GpXkUSD"}
``` {.python}
def makeFeatureVec(words, model, num_features):
    # Function to average all of the word vectors in a given
    # paragraph
    #
    # Pre-initialize an empty numpy array (for speed)
    featureVec = np.zeros((num_features,), dtype="float32")
    #
    nwords = 0.
    # 
    # Index2word is a list that contains the names of the words in 
    # the model's vocabulary. Convert it to a set, for speed 
    index2word_set = set(model.wv.index_to_key)
    #
    # Loop over each word in the review and, if it is in the model's
    # vocaublary, add its feature vector to the total
    for word in words:
        if word in index2word_set: 
            nwords = nwords + 1.
            featureVec = np.add(featureVec,model.wv[word])
    # 
    # Divide the result by the number of words to get the average
    featureVec = np.divide(featureVec,nwords)
    return featureVec
```
:::

::: {.cell .code id="2eehxXIHj3go"}
``` {.python}
def getAvgFeatureVecs(reviews, model, num_features):
    # Given a set of reviews (each one a list of words), calculate 
    # the average feature vector for each one and return a 2D numpy array 
    # 
    # Initialize a counter
    counter = 0.
    # 
    # Preallocate a 2D numpy array, for speed
    reviewFeatureVecs = np.zeros((len(reviews),num_features), dtype="float32")
    # 
    # Loop through the reviews
    for review in reviews:
       #
       # Print a status message every 1000th review
       if counter%1000. == 0.:
           print("Review %d of %d" % (counter, len(reviews)))
       # 
       # Call the function (defined above) that makes average feature vectors
       reviewFeatureVecs[int(counter)] = makeFeatureVec(review, model, num_features)
       #
       # Increment the counter
       counter = counter + 1.
    return reviewFeatureVecs
```
:::

::: {.cell .code id="cIgecjOHrweu"}
``` {.python}
# ****************************************************************
# Calculate average feature vectors for training and testing sets,
# using the functions we defined above. Notice that we now use stop word
# removal.
```
:::

::: {.cell .code id="5bXyKysjmZuM"}
``` {.python}
clean_train_reviews = []
for review in train["review"]:
    clean_train_reviews.append( review_to_wordlist( review, remove_stopwords=True ))
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="QW9E6DXNmcZL" outputId="e8cf86de-d43a-4df6-946d-24a0c70c60ca"}
``` {.python}
clean_train_reviews[0][:5]
```

::: {.output .execute_result execution_count="189"}
    ['doogtooth', 'official', 'greek', 'entry', 'academy']
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="KNtKDNoLmoGX" outputId="96792c55-ba65-4c6c-a043-46860f1273de"}
``` {.python}
len(clean_train_reviews[0])
```

::: {.output .execute_result execution_count="159"}
    453
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="8Jln1eXjm3js" outputId="b532de03-fec4-4c68-9012-44982f2ffdd6"}
``` {.python}
trainDataVecs = getAvgFeatureVecs(clean_train_reviews, model, num_features )
```

::: {.output .stream .stdout}
    Review 0 of 7005
    Review 1000 of 7005
    Review 2000 of 7005
    Review 3000 of 7005
    Review 4000 of 7005
:::

::: {.output .stream .stderr}
    <ipython-input-193-3b304ab948a9>:22: RuntimeWarning: invalid value encountered in true_divide
      featureVec = np.divide(featureVec,nwords)
:::

::: {.output .stream .stdout}
    Review 5000 of 7005
    Review 6000 of 7005
    Review 7000 of 7005
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="Xv2w8PWnlPYl" outputId="4f9e3d22-1340-4288-e1ce-dba64f471e42"}
``` {.python}
print("Creating average feature vecs for test reviews")
clean_test_reviews = []
for review in test["review"]:
    clean_test_reviews.append(review_to_wordlist(review, remove_stopwords=True ))

testDataVecs = getAvgFeatureVecs( clean_test_reviews, model, num_features )
```

::: {.output .stream .stdout}
    Creating average feature vecs for test reviews
:::

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/bs4/__init__.py:270: UserWarning: "b'.'" looks like a filename, not markup. You should probably open this file and pass the filehandle into Beautiful Soup.
      warnings.warn(
:::

::: {.output .stream .stdout}
    Review 0 of 3002
:::

::: {.output .stream .stderr}
    <ipython-input-193-3b304ab948a9>:22: RuntimeWarning: invalid value encountered in true_divide
      featureVec = np.divide(featureVec,nwords)
:::

::: {.output .stream .stdout}
    Review 1000 of 3002
    Review 2000 of 3002
    Review 3000 of 3002
:::
:::

::: {.cell .markdown id="IgJhNhvgGtL4"}
## Modeling
:::

::: {.cell .code execution_count="110" id="By-hYdBoBaHN"}
``` {.python}
import pickle
```
:::

::: {.cell .markdown id="UfsH3iYKBrwo"}
### Hyperopt code
:::

::: {.cell .code execution_count="116" id="-yGU8KDIBvGL"}
``` {.python}
from hyperopt import hp
import hyperopt
```
:::

::: {.cell .code execution_count="129" id="cpG_Q_SgCrhk"}
``` {.python}
def objective2(space, x_train, y_train, x_test, y_test):
    model = xgb.XGBClassifier(n_estimators = int(space['n_estimators']), max_depth = int(space['max_depth']), gamma = space['gamma'],
                    min_child_weight=int(space['min_child_weight']), colsample_bytree=space['colsample_bytree'], learning_rate=space['learning_rate'])
    model.fit(x_train, y_train)
    preds = model.predict(x_test)
    test_auc = roc_auc_score(y_test, preds)
    #print("Hyperparameters : {}".format(params_dict))
    #print("test ROC-AUC : {}\n".format(test_auc))

    return {'loss': -test_auc, 'params': space, 'status': hyperopt.STATUS_OK}
```
:::

::: {.cell .code execution_count="139" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="t4tG1FZFHFhV" outputId="2d796025-d7be-4e99-f332-ad2339295cc3"}
``` {.python}
xgb_model.get_params()
```

::: {.output .execute_result execution_count="139"}
    {'base_score': 0.5,
     'booster': 'gbtree',
     'colsample_bylevel': 1,
     'colsample_bynode': 1,
     'colsample_bytree': 1,
     'gamma': 0,
     'learning_rate': 0.1,
     'max_delta_step': 0,
     'max_depth': 3,
     'min_child_weight': 1,
     'missing': None,
     'n_estimators': 100,
     'n_jobs': 1,
     'nthread': None,
     'objective': 'binary:logistic',
     'random_state': 0,
     'reg_alpha': 0,
     'reg_lambda': 1,
     'scale_pos_weight': 1,
     'seed': None,
     'silent': None,
     'subsample': 1,
     'verbosity': 1}
:::
:::

::: {.cell .code execution_count="227" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="dgeF2pIKJYth" outputId="f56fcbda-23b0-44b5-ac7a-3d80588d0d83"}
``` {.python}
xgb_model.get_xgb_params()
```

::: {.output .execute_result execution_count="227"}
    {'base_score': 0.5,
     'booster': 'gbtree',
     'colsample_bylevel': 1,
     'colsample_bynode': 1,
     'colsample_bytree': 1,
     'gamma': 0,
     'learning_rate': 0.1,
     'max_delta_step': 0,
     'max_depth': 3,
     'min_child_weight': 1,
     'missing': None,
     'n_estimators': 100,
     'nthread': 1,
     'objective': 'binary:logistic',
     'reg_alpha': 0,
     'reg_lambda': 1,
     'scale_pos_weight': 1,
     'seed': 0,
     'subsample': 1,
     'verbosity': 1}
:::
:::

::: {.cell .code execution_count="144" id="RMqMfqTCCCA3"}
``` {.python}
def objective_xgb(space):
    model = xgb.XGBClassifier(n_estimators = int(space['n_estimators']), max_depth = int(space['max_depth']), gamma = space['gamma'],
                    min_child_weight=int(space['min_child_weight']), colsample_bytree=space['colsample_bytree'], learning_rate=space['learning_rate'])
    model.fit(x_train_bw, y_train_bw)
    preds = model.predict(x_test_bw)
    test_auc = roc_auc_score(y_test_bw, preds)
    print("Hyperparameters : {}".format(model.get_params()))
    print("test ROC-AUC : {}\n".format(test_auc))

    return {'loss': -test_auc, 'params': space, 'status': hyperopt.STATUS_OK}
```
:::

::: {.cell .code execution_count="145" id="VzeUjU3hCmsu"}
``` {.python}
space = {
    'max_depth': hp.choice('max_depth', list(range(5,16,2))),
    'learning_rate': hp.uniform('learning_rate', 0.05, 0.5),
    'gamma': hp.uniform('gamma', 0.05, 0.5),
    'min_child_weight': hp.choice('min_child_weight', list(range(1,61,5))),
    'colsample_bytree': hp.uniform('colsample_bytree', 0, 1),
    'n_estimators': hp.choice('n_estimators', list(range(10,81,5)))
}
```
:::

::: {.cell .code execution_count="146" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="7VhQAmf-HXnI" outputId="17bbc357-822f-4666-f503-f05ff01411be"}
``` {.python}
trials_obj = hyperopt.Trials()
best_results = hyperopt.fmin(objective_xgb,
                             space=space,
                             algo=hyperopt.tpe.suggest,
                             trials=trials_obj,
                             max_evals=10)
```

::: {.output .stream .stdout}
    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.2720299330988213, 'gamma': 0.06483558829271696, 'learning_rate': 0.2109406749892621, 'max_delta_step': 0, 'max_depth': 15, 'min_child_weight': 16, 'missing': None, 'n_estimators': 75, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7843646115419055

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.4223573785656689, 'gamma': 0.05486356540587481, 'learning_rate': 0.378844872759047, 'max_delta_step': 0, 'max_depth': 13, 'min_child_weight': 31, 'missing': None, 'n_estimators': 80, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7630887774744695

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.07716725619561682, 'gamma': 0.11101838307948131, 'learning_rate': 0.30060716431556367, 'max_delta_step': 0, 'max_depth': 7, 'min_child_weight': 16, 'missing': None, 'n_estimators': 55, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7667692597708151

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.5034333392246534, 'gamma': 0.3615140216124094, 'learning_rate': 0.234500536004544, 'max_delta_step': 0, 'max_depth': 15, 'min_child_weight': 6, 'missing': None, 'n_estimators': 40, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7792100330980579

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.9364706136820735, 'gamma': 0.36068768385940086, 'learning_rate': 0.4971935545995662, 'max_delta_step': 0, 'max_depth': 5, 'min_child_weight': 1, 'missing': None, 'n_estimators': 75, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.776979176862536

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.02134375399576738, 'gamma': 0.17636247968949403, 'learning_rate': 0.3366334495964025, 'max_delta_step': 0, 'max_depth': 5, 'min_child_weight': 36, 'missing': None, 'n_estimators': 75, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7341171011466501

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.061096099899583645, 'gamma': 0.17358230682372255, 'learning_rate': 0.2903036827547228, 'max_delta_step': 0, 'max_depth': 9, 'min_child_weight': 31, 'missing': None, 'n_estimators': 30, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7315821814266603

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.1502916131479093, 'gamma': 0.15005970480737174, 'learning_rate': 0.4234070379921088, 'max_delta_step': 0, 'max_depth': 13, 'min_child_weight': 36, 'missing': None, 'n_estimators': 80, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7584258665129583

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.6114174493087502, 'gamma': 0.18804953328934765, 'learning_rate': 0.1312875556894742, 'max_delta_step': 0, 'max_depth': 15, 'min_child_weight': 36, 'missing': None, 'n_estimators': 25, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7404290240604392

    Hyperparameters : {'base_score': 0.5, 'booster': 'gbtree', 'colsample_bylevel': 1, 'colsample_bynode': 1, 'colsample_bytree': 0.9416261150384357, 'gamma': 0.23442010786341777, 'learning_rate': 0.11292747411120763, 'max_delta_step': 0, 'max_depth': 7, 'min_child_weight': 46, 'missing': None, 'n_estimators': 75, 'n_jobs': 1, 'nthread': None, 'objective': 'binary:logistic', 'random_state': 0, 'reg_alpha': 0, 'reg_lambda': 1, 'scale_pos_weight': 1, 'seed': None, 'silent': None, 'subsample': 1, 'verbosity': 1}
    test ROC-AUC : 0.7364453845791326

    100%|██████████| 10/10 [09:17<00:00, 55.73s/it, best loss: -0.7843646115419055]
:::
:::

::: {.cell .code execution_count="147" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="cGK0Bb3UIEsQ" outputId="a508b5ea-ad3f-4986-ca04-19645e4a247d"}
``` {.python}
xgb_hyperopt_params = hyperopt.space_eval(space, best_results)
xgb_hyperopt_params
```

::: {.output .execute_result execution_count="147"}
    {'colsample_bytree': 0.2720299330988213,
     'gamma': 0.06483558829271696,
     'learning_rate': 0.2109406749892621,
     'max_depth': 15,
     'min_child_weight': 16,
     'n_estimators': 75}
:::
:::

::: {.cell .code id="k1TRPNs7XMFa"}
``` {.python}
```
:::

::: {.cell .code execution_count="124" id="6HgeukT3EQ6T"}
``` {.python}
x_train_bw, y_train_bw, x_test_bw, y_test_bw = train_features_bw, train.sentiment, test_features_bw, test.sentiment
```
:::

::: {.cell .code execution_count="188" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="DwnXCiB5DyHe" outputId="cb8c93f5-f4d4-4e4d-a893-8be8fbd45706"}
``` {.python}
s = hp.quniform('min_samples_leaf',1,10)
print(s)
```

::: {.output .stream .stdout}
    0 float
    1   hyperopt_param
    2     Literal{min_samples_leaf}
    3     quniform
    4       Literal{1}
    5       Literal{10}
:::
:::

::: {.cell .code execution_count="193" id="ECMg0M1dNTln"}
``` {.python}
space_forest={'n_estimators': hp.choice("n_estimators", np.arange(5, 500, 5, dtype=int)),
              'max_depth': hp.choice("max_depth", np.arange(5, 50, 2, dtype=int)),
              'min_samples_split': hp.choice("min_samples_split", np.arange(2, 100, 1, dtype=int)),
              'min_samples_leaf': hp.choice("min_samples_leaf", np.arange(1, 100, 1, dtype=int)),
              'criterion': hp.choice('criterion',['gini','entropy']),
              'max_features': hp.choice('max_features',['sqrt', 'log2'])}
```
:::

::: {.cell .code execution_count="184" id="iyLQPeTQMeNc"}
``` {.python}
def objective_rnd_forest(space_forest):
    model = RandomForestClassifier(**space_forest, random_state=42)
    model.fit(x_train_bw, y_train_bw)
    preds = model.predict(x_test_bw)
    test_auc = roc_auc_score(y_test_bw, preds)
    print("Hyperparameters : {}".format(model.get_params()))
    print("test ROC-AUC : {}\n".format(test_auc))

    return {'loss': -test_auc, 'params': space, 'status': hyperopt.STATUS_OK}
```
:::

::: {.cell .code id="aRid-cPwNSsE"}
``` {.python}
```
:::

::: {.cell .code execution_count="194" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="UDw2WkYxMp6X" outputId="089522b0-15a7-4109-9611-4a3afd0a726a"}
``` {.python}
trials_forest = hyperopt.Trials()
best_results = hyperopt.fmin(fn=objective_rnd_forest,
                             space=space_forest,
                             algo=hyperopt.tpe.suggest,
                             trials=trials_forest,
                             max_evals=20)
```

::: {.output .stream .stdout}
    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 35, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 70, 'min_samples_split': 20, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 105, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6206325426776438

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 37, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 56, 'min_samples_split': 50, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 310, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.643765837583878

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 13, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 22, 'min_samples_split': 38, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 110, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6456115165290904

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 25, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 59, 'min_samples_split': 17, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 305, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5132192846034215

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 45, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 37, 'min_samples_split': 24, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 385, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5559875583203733

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 13, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 33, 'min_samples_split': 44, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 480, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5377138413685847

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 41, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 11, 'min_samples_split': 57, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 150, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6335568267916635

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 29, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 58, 'min_samples_split': 22, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 220, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5143856920684292

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 11, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 74, 'min_samples_split': 13, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 190, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6064380798051093

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 9, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 87, 'min_samples_split': 40, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 135, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5937041185874778

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 21, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 24, 'min_samples_split': 86, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 450, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6839126399779588

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 17, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 36, 'min_samples_split': 30, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 395, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5486003110419907

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 47, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 12, 'min_samples_split': 24, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 340, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6362775379105083

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 17, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 53, 'min_samples_split': 15, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 265, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.640654511377684

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 37, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 29, 'min_samples_split': 84, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 55, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5898142811051054

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 7, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 4, 'min_samples_split': 67, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 195, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5066096423017108

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 31, 'max_features': 'sqrt', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 66, 'min_samples_split': 4, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 35, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.6221913778290139

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'entropy', 'max_depth': 21, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 43, 'min_samples_split': 23, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 195, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5392690513219285

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 35, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 36, 'min_samples_split': 95, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 45, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5672637367816217

    Hyperparameters : {'bootstrap': True, 'ccp_alpha': 0.0, 'class_weight': None, 'criterion': 'gini', 'max_depth': 33, 'max_features': 'log2', 'max_leaf_nodes': None, 'max_samples': None, 'min_impurity_decrease': 0.0, 'min_samples_leaf': 48, 'min_samples_split': 57, 'min_weight_fraction_leaf': 0.0, 'n_estimators': 380, 'n_jobs': None, 'oob_score': False, 'random_state': 42, 'verbose': 0, 'warm_start': False}
    test ROC-AUC : 0.5252721617418352

    100%|██████████| 20/20 [04:35<00:00, 13.77s/it, best loss: -0.6839126399779588]
:::
:::

::: {.cell .code execution_count="198" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="O2s6fNgXWBzg" outputId="92da557e-0ca6-4171-f859-f0d1841f179a"}
``` {.python}
forest_hyperopt_params = hyperopt.space_eval(space_forest, best_results)
forest_hyperopt_params
```

::: {.output .execute_result execution_count="198"}
    {'criterion': 'gini',
     'max_depth': 21,
     'max_features': 'sqrt',
     'min_samples_leaf': 24,
     'min_samples_split': 86,
     'n_estimators': 450}
:::
:::

::: {.cell .markdown id="wGKakYqmgGbU"}
### Models on bag of words
:::

::: {.cell .markdown id="tMVPW2bImSG2"}
#### Random Forest
:::

::: {.cell .code execution_count="80" id="LHBiIbD3HEUj"}
``` {.python}
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import roc_auc_score
```
:::

::: {.cell .code execution_count="65" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="pvYw_mL_GyaP" outputId="8503bc14-43be-4e72-a8ea-b9fa04e27031"}
``` {.python}
print( "Training the random forest...")
forest = RandomForestClassifier(n_estimators = 100) 
forest = forest.fit(train_features_bw, train["sentiment"])
```

::: {.output .stream .stdout}
    Training the random forest...
:::
:::

::: {.cell .code execution_count="206" id="UO3mo-kzYMwO"}
``` {.python}
forest_opt = RandomForestClassifier(**forest_hyperopt_params) 
forest_opt = forest.fit(train_features_bw, train["sentiment"])
```
:::

::: {.cell .code execution_count="207" id="3OnLiPgyYUVG"}
``` {.python}
pred_forest_opt = forest_opt.predict(test_features_bw)
```
:::

::: {.cell .code execution_count="66" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="nyMGaIXPHHiR" outputId="c79f6c28-e7df-418d-cc77-d0c96fb41516"}
``` {.python}
forest.feature_importances_
```

::: {.output .execute_result execution_count="66"}
    array([7.87755579e-05, 1.33047764e-04, 2.77821049e-05, ...,
           2.40899407e-04, 9.72981785e-05, 7.12419816e-05])
:::
:::

::: {.cell .code execution_count="81" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="M3VXmOtEHyby" outputId="d84c0a50-ad83-4a64-bba1-58a2c8a57519"}
``` {.python}
print("Cleaning and parsing the test set movie reviews...\n")
num_reviews = len(test.review)
test_cl_bw = []

for review in test.review:
  test_cl_bw.append(review_to_words(review))

# Get a bag of words for the test set, and convert to a numpy array
test_features_bw = vectorizer.transform(test_cl_bw)
test_features_bw = test_features_bw.toarray()

# Use the random forest to make sentiment label predictions
pred_rndf_100 = forest.predict(test_features_bw)

# Copy the results to a pandas dataframe with an "id" column and a "sentiment" column
#output = pd.DataFrame( data={"id":test["id"], "sentiment":result} )
```

::: {.output .stream .stdout}
    Cleaning and parsing the test set movie reviews...
:::

::: {.output .stream .stderr}
    /usr/local/lib/python3.8/dist-packages/bs4/__init__.py:270: UserWarning: "b'.'" looks like a filename, not markup. You should probably open this file and pass the filehandle into Beautiful Soup.
      warnings.warn(
:::
:::

::: {.cell .code execution_count="82" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="aZZSsQQKJTMG" outputId="5d3f6d16-b84e-45bb-d7f5-1a54caa24e09"}
``` {.python}
roc_auc_score(test.sentiment, pred_rndf_100)
```

::: {.output .execute_result execution_count="82"}
    0.7736548702722887
:::
:::

::: {.cell .code execution_count="83" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="EWbTEd37wuLo" outputId="8970a96a-e6e4-4189-e95b-8207ad94c308"}
``` {.python}
result_train = forest.predict(train_features_bw)
roc_auc_score(train.sentiment, result_train)
```

::: {.output .execute_result execution_count="83"}
    0.9997091056533249
:::
:::

::: {.cell .markdown id="IBsG8REE_tR5"}
#### SVM
:::

::: {.cell .code execution_count="107" id="8Aq4F2gZ_wQv"}
``` {.python}
from sklearn import svm
from sklearn.svm import SVC
```
:::

::: {.cell .code execution_count="108" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="QBG0e06A_xPr" outputId="609e50aa-c714-480c-b997-d835c6ef1989"}
``` {.python}
svm_bw = SVC(gamma='auto')
svm_bw.fit(train_data_features_bw, train["sentiment"])
```

::: {.output .execute_result execution_count="108"}
    SVC(gamma='auto')
:::
:::

::: {.cell .code id="E3EwEIquBYTF"}
``` {.python}
```
:::

::: {.cell .code execution_count="109" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="kkelbcD4ASRo" outputId="0fbfcdbf-7bfa-47be-f670-53d8061cd629"}
``` {.python}
pred_svm_def = svm_bw.predict(test_features_bw)
print("heldout AUC = {}".format(roc_auc_score(test.sentiment, pred_svm_def)))
```

::: {.output .stream .stdout}
    heldout AUC = 0.5733934934945821
:::
:::

::: {.cell .markdown id="othUNV_tmOGT"}
#### Gradient boosting
:::

::: {.cell .code execution_count="71" id="XGYkrc_ejDhQ"}
``` {.python}
import xgboost as xgb
from sklearn.metrics import confusion_matrix
from sklearn.metrics import ConfusionMatrixDisplay
```
:::

::: {.cell .code execution_count="72" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="z7676-bWjDkY" outputId="08ceed81-42f4-4471-a8db-160b7dac8c46"}
``` {.python}
xgb_model = xgb.XGBClassifier()#make_pipeline(StandardScaler(), xgb.XGBClassifier())
xgb_model.fit(train_data_features_bw, train["sentiment"])
```

::: {.output .execute_result execution_count="72"}
    XGBClassifier()
:::
:::

::: {.cell .code execution_count="203" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="i97GIyZlXQEn" outputId="47aee823-b980-47fb-da2f-f8eade822a20"}
``` {.python}
xgb_model_opt = xgb.XGBClassifier(**xgb_hyperopt_params)
xgb_model_opt.fit(train_features_bw, train["sentiment"])
```

::: {.output .execute_result execution_count="203"}
    XGBClassifier(colsample_bytree=0.2720299330988213, gamma=0.06483558829271696,
                  learning_rate=0.2109406749892621, max_depth=15,
                  min_child_weight=16, n_estimators=75)
:::
:::

::: {.cell .code execution_count="100" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="ni4GWQxYjaNp" outputId="eaef1ee7-e29c-40cf-e81c-a2d3831612be"}
``` {.python}
pred_xgb_def = xgb_model.predict(test_features_bw)
print("heldout AUC = {}".format(roc_auc_score(test.sentiment, preds)))
```

::: {.output .stream .stdout}
    heldout AUC = 0.7484819483264273
:::
:::

::: {.cell .code execution_count="204" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="3eIavGHeXYnw" outputId="007a7740-c9f2-48fc-de3e-0b5e7c3d4568"}
``` {.python}
pred_xgb_opt = xgb_model_opt.predict(test_features_bw)
print("heldout AUC = {}".format(roc_auc_score(test.sentiment, pred_xgb_opt)))
```

::: {.output .stream .stdout}
    heldout AUC = 0.7843646115419055
:::
:::

::: {.cell .markdown id="XdCFpmFcgK4f"}
### Models on Word2Vec
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="kifEkXrMv-Gm" outputId="4f126377-51c0-472e-c674-3743ccb7f282"}
``` {.python}
np.any(np.isnan(trainDataVecs))
```

::: {.output .execute_result execution_count="200"}
    True
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="clIFGobuwKAU" outputId="0ff43e18-9f25-406f-89a6-d6e9dfb3cec3"}
``` {.python}
np.all(np.isfinite(trainDataVecs))
```

::: {.output .execute_result execution_count="201"}
    False
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="VTt94lqFwo4C" outputId="d1435dcb-84a1-46d0-c676-a4029163a5da"}
``` {.python}
np.argwhere(np.isnan(trainDataVecs)).shape
```

::: {.output .execute_result execution_count="205"}
    (900, 2)
:::
:::

::: {.cell .code id="-4mLYTg-wvdY"}
``` {.python}
x = trainDataVecs[~np.isnan(trainDataVecs)]
```
:::

::: {.cell .code id="Y6hc15QywYZZ"}
``` {.python}
train = train.reset_index()
```
:::

::: {.cell .code colab="{\"height\":471,\"base_uri\":\"https://localhost:8080/\"}" id="vCIXLsz4sOaD" outputId="39bb1148-0dac-4ced-e487-af0c5339a194"}
``` {.python}
# Fit a random forest to the training data, using 100 trees
from sklearn.ensemble import RandomForestClassifier
forest_w2v = RandomForestClassifier( n_estimators = 100 )

forest_w2v = forest_w2v.fit( x, train["sentiment"] )

# Test & extract results 
result = forest_w2v.predict( testDataVecs )

# Write the test results 
output = pd.DataFrame( data={"id":test["id"], "sentiment":result} )
output.to_csv( "Word2Vec_AverageVectors.csv", index=False, quoting=3 )
```

::: {.output .error ename="ValueError" evalue="ignored"}
    ---------------------------------------------------------------------------
    ValueError                                Traceback (most recent call last)
    <ipython-input-207-0cd1f8f45473> in <module>
          3 forest_w2v = RandomForestClassifier( n_estimators = 100 )
          4 
    ----> 5 forest_w2v = forest_w2v.fit( x, train["sentiment"] )
          6 
          7 # Test & extract results

    /usr/local/lib/python3.8/dist-packages/sklearn/ensemble/_forest.py in fit(self, X, y, sample_weight)
        325         if issparse(y):
        326             raise ValueError("sparse multilabel-indicator for y is not supported.")
    --> 327         X, y = self._validate_data(
        328             X, y, multi_output=True, accept_sparse="csc", dtype=DTYPE
        329         )

    /usr/local/lib/python3.8/dist-packages/sklearn/base.py in _validate_data(self, X, y, reset, validate_separately, **check_params)
        579                 y = check_array(y, **check_y_params)
        580             else:
    --> 581                 X, y = check_X_y(X, y, **check_params)
        582             out = X, y
        583 

    /usr/local/lib/python3.8/dist-packages/sklearn/utils/validation.py in check_X_y(X, y, accept_sparse, accept_large_sparse, dtype, order, copy, force_all_finite, ensure_2d, allow_nd, multi_output, ensure_min_samples, ensure_min_features, y_numeric, estimator)
        962         raise ValueError("y cannot be None")
        963 
    --> 964     X = check_array(
        965         X,
        966         accept_sparse=accept_sparse,

    /usr/local/lib/python3.8/dist-packages/sklearn/utils/validation.py in check_array(array, accept_sparse, accept_large_sparse, dtype, order, copy, force_all_finite, ensure_2d, allow_nd, ensure_min_samples, ensure_min_features, estimator)
        767             # If input is 1D raise error
        768             if array.ndim == 1:
    --> 769                 raise ValueError(
        770                     "Expected 2D array, got 1D array instead:\narray={}.\n"
        771                     "Reshape your data either using array.reshape(-1, 1) if "

    ValueError: Expected 2D array, got 1D array instead:
    array=[-0.0008759   0.03668336 -0.0306208  ... -0.00456893  0.01631427
     -0.00952523].
    Reshape your data either using array.reshape(-1, 1) if your data has a single feature or array.reshape(1, -1) if it contains a single sample.
:::
:::

::: {.cell .markdown id="wXBm_yimHuHw"}
## Models comparison
:::

::: {.cell .code execution_count="84" id="N1hny8O-lGuC"}
``` {.python}
from sklearn.metrics import auc
from sklearn.metrics import roc_curve
from sklearn.metrics import RocCurveDisplay
```
:::

::: {.cell .code execution_count="85" id="YWhpaZen0FOU"}
``` {.python}
fpr, tpr, thresholds = roc_curve(test.sentiment, pred_rndf_100)
roc_auc = auc(fpr, tpr)
```
:::

::: {.cell .code execution_count="96" id="670R2rPh2nk4"}
``` {.python}
auc = round(roc_auc_score(test.sentiment, pred_rndf_100), 3)
```
:::

::: {.cell .code id="pWsdJgpXBzEE"}
``` {.python}
```
:::

::: {.cell .code execution_count="248" colab="{\"height\":501,\"base_uri\":\"https://localhost:8080/\"}" id="3WgX51-r0tPy" outputId="402f83d3-a588-4354-b18b-b6c600e0e18a"}
``` {.python}
plt.figure(0, figsize = (12,8)).clf()

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_xgb_opt)
auc = round(roc_auc_score(test.sentiment, pred_xgb_opt), 3)
plt.plot(fpr, tpr, label="XGBoost hyperopt; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_rndf_100)
auc = round(roc_auc_score(test.sentiment, pred_rndf_100), 3)
plt.plot(fpr, tpr, label="Random Forest deafault; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_forest_opt)
auc = round(roc_auc_score(test.sentiment, pred_forest_opt), 3)
plt.plot(fpr, tpr, label="Random Forest hyperopt; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_xgb_def)
auc = round(roc_auc_score(test.sentiment, pred_xgb_def), 3)
plt.plot(fpr, tpr, label="XGBoost default; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_svm_def)
auc = round(roc_auc_score(test.sentiment, pred_svm_def), 3)
plt.plot(fpr, tpr, label="SVM default; AUC = " + str(auc))

plt.plot([0, 1], [0, 1], linestyle="--", lw=2, color="blue", label="Chance", alpha=0.5)

plt.legend()
```

::: {.output .execute_result execution_count="248"}
    <matplotlib.legend.Legend at 0x7ff6b1bfb3d0>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/1ab4ba36b9924e86845d2b029616aacc9ff53de0.png)
:::
:::

::: {.cell .code execution_count="231" colab="{\"height\":501,\"base_uri\":\"https://localhost:8080/\"}" id="jZqXFfvKVaxm" outputId="bfa4ffe1-a311-45b8-be0d-9f04a2464a6f"}
``` {.python}
plt.figure(0, figsize = (12,8)).clf()

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_rndf_100)
auc = round(roc_auc_score(test.sentiment, pred_rndf_100), 3)
plt.plot(fpr, tpr, label="Random Forest deafault; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_xgb_def)
auc = round(roc_auc_score(test.sentiment, pred_xgb_def), 3)
plt.plot(fpr, tpr, label="XGBoost default; AUC = " + str(auc))

fpr, tpr, thresholds = roc_curve(test.sentiment, pred_svm_def)
auc = round(roc_auc_score(test.sentiment, pred_svm_def), 3)
plt.plot(fpr, tpr, label="SVM default; AUC = " + str(auc))

plt.plot([0, 1], [0, 1], linestyle="--", lw=2, color="blue", label="Chance", alpha=0.5)

plt.legend()
```

::: {.output .execute_result execution_count="231"}
    <matplotlib.legend.Legend at 0x7ff6b1898820>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/16d0f8d18e2685df64ebc2a73e85098bc52f3ace.png)
:::
:::

::: {.cell .code execution_count="247" colab="{\"height\":513,\"base_uri\":\"https://localhost:8080/\"}" id="28xqtnRAjKLx" outputId="702d42d3-fff6-4c46-abc9-e3bb011d880f"}
``` {.python}
ax = xgb.plot_importance(xgb_model, height=0.2, max_num_features = 15)
fig = ax.figure
fig.set_size_inches(10, 8)
```

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/a75e8097ad0d3a28662d55c04e100846a80a2d45.png)
:::
:::

::: {.cell .code execution_count="234" id="QbqfPrtDjKOE"}
``` {.python}
from sklearn.metrics import confusion_matrix
```
:::

::: {.cell .code execution_count="238" id="YH0qCkknjKQ7"}
``` {.python}
cm = confusion_matrix(test.sentiment, pred_xgb_opt)
```
:::

::: {.cell .code execution_count="241" colab="{\"height\":297,\"base_uri\":\"https://localhost:8080/\"}" id="IlmzAm-Rj4mG" outputId="9ae58a06-31c4-4b4b-87e0-c41257ba8ccc"}
``` {.python}
disp = ConfusionMatrixDisplay(confusion_matrix=cm)#, display_labels=[])
disp.plot()
```

::: {.output .execute_result execution_count="241"}
    <sklearn.metrics._plot.confusion_matrix.ConfusionMatrixDisplay at 0x7ff6af973250>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/94f78cc4f9cf2f9448cb128071ccab25888172d0.png)
:::
:::

::: {.cell .code execution_count="243" colab="{\"height\":297,\"base_uri\":\"https://localhost:8080/\"}" id="ukqV8YRzj4u-" outputId="eb6b7874-a69d-43b4-f4b5-4c9e7e5aa1ea"}
``` {.python}
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=['Negative','Positive'])
disp.plot()
```

::: {.output .execute_result execution_count="243"}
    <sklearn.metrics._plot.confusion_matrix.ConfusionMatrixDisplay at 0x7ff6af0c1790>
:::

::: {.output .display_data}
![](vertopal_8cb9a353409a4d338e815dc5626d05b9/95d2f7858db47a150080d626d4eee15c90c1bad2.png)
:::
:::

::: {.cell .code id="rccN1S0jVa0J"}
``` {.python}
while 1 < 2:
 1 + 1
```
:::

::: {.cell .code id="AkS-ZMdgVe36"}
``` {.python}
```
:::
