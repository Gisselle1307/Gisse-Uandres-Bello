cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p style=\"text-align:center\">\n",
    "    <a href=\"https://skills.network/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork900-2022-01-01\" target=\"_blank\">\n",
    "    <img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png\" width=\"200\" alt=\"Skills Network Logo\">\n",
    "    </a>\n",
    "</p>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Extracting and Visualizing Stock Data</h1>\n",
    "<h2>Description</h2>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some stock data, you will then display this data in a graph.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Table of Contents</h2>\n",
    "<div class=\"alert alert-block alert-info\" style=\"margin-top: 20px\">\n",
    "    <ul>\n",
    "        <li>Define a Function that Makes a Graph</li>\n",
    "        <li>Question 1: Use yfinance to Extract Stock Data</li>\n",
    "        <li>Question 2: Use Webscraping to Extract Tesla Revenue Data</li>\n",
    "        <li>Question 3: Use yfinance to Extract Stock Data</li>\n",
    "        <li>Question 4: Use Webscraping to Extract GME Revenue Data</li>\n",
    "        <li>Question 5: Plot Tesla Stock Graph</li>\n",
    "        <li>Question 6: Plot GameStop Stock Graph</li>\n",
    "    </ul>\n",
    "<p>\n",
    "    Estimated Time Needed: <strong>30 min</strong></p>\n",
    "</div>\n",
    "\n",
    "<hr>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***Note***:- If you are working Locally using anaconda, please uncomment the following code and execute it.\n",
    "Use the version as per your python version.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Requirement already satisfied: yfinance in /opt/conda/lib/python3.11/site-packages (0.2.49)\n",
      "Requirement already satisfied: pandas>=1.3.0 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2.2.3)\n",
      "Requirement already satisfied: numpy>=1.16.5 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2.1.3)\n",
      "Requirement already satisfied: requests>=2.31 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2.31.0)\n",
      "Requirement already satisfied: multitasking>=0.0.7 in /opt/conda/lib/python3.11/site-packages (from yfinance) (0.0.11)\n",
      "Requirement already satisfied: lxml>=4.9.1 in /opt/conda/lib/python3.11/site-packages (from yfinance) (5.3.0)\n",
      "Requirement already satisfied: platformdirs>=2.0.0 in /opt/conda/lib/python3.11/site-packages (from yfinance) (4.2.1)\n",
      "Requirement already satisfied: pytz>=2022.5 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2024.1)\n",
      "Requirement already satisfied: frozendict>=2.3.4 in /opt/conda/lib/python3.11/site-packages (from yfinance) (2.4.6)\n",
      "Requirement already satisfied: peewee>=3.16.2 in /opt/conda/lib/python3.11/site-packages (from yfinance) (3.17.8)\n",
      "Requirement already satisfied: beautifulsoup4>=4.11.1 in /opt/conda/lib/python3.11/site-packages (from yfinance) (4.12.3)\n",
      "Requirement already satisfied: html5lib>=1.1 in /opt/conda/lib/python3.11/site-packages (from yfinance) (1.1)\n",
      "Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.11/site-packages (from beautifulsoup4>=4.11.1->yfinance) (2.5)\n",
      "Requirement already satisfied: six>=1.9 in /opt/conda/lib/python3.11/site-packages (from html5lib>=1.1->yfinance) (1.16.0)\n",
      "Requirement already satisfied: webencodings in /opt/conda/lib/python3.11/site-packages (from html5lib>=1.1->yfinance) (0.5.1)\n",
      "Requirement already satisfied: python-dateutil>=2.8.2 in /opt/conda/lib/python3.11/site-packages (from pandas>=1.3.0->yfinance) (2.9.0)\n",
      "Requirement already satisfied: tzdata>=2022.7 in /opt/conda/lib/python3.11/site-packages (from pandas>=1.3.0->yfinance) (2024.2)\n",
      "Requirement already satisfied: charset-normalizer<4,>=2 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (3.3.2)\n",
      "Requirement already satisfied: idna<4,>=2.5 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (3.7)\n",
      "Requirement already satisfied: urllib3<3,>=1.21.1 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (2.2.1)\n",
      "Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.11/site-packages (from requests>=2.31->yfinance) (2024.6.2)\n",
      "Requirement already satisfied: bs4 in /opt/conda/lib/python3.11/site-packages (0.0.2)\n",
      "Requirement already satisfied: beautifulsoup4 in /opt/conda/lib/python3.11/site-packages (from bs4) (4.12.3)\n",
      "Requirement already satisfied: soupsieve>1.2 in /opt/conda/lib/python3.11/site-packages (from beautifulsoup4->bs4) (2.5)\n",
      "Requirement already satisfied: nbformat in /opt/conda/lib/python3.11/site-packages (5.10.4)\n",
      "Requirement already satisfied: fastjsonschema>=2.15 in /opt/conda/lib/python3.11/site-packages (from nbformat) (2.19.1)\n",
      "Requirement already satisfied: jsonschema>=2.6 in /opt/conda/lib/python3.11/site-packages (from nbformat) (4.22.0)\n",
      "Requirement already satisfied: jupyter-core!=5.0.*,>=4.12 in /opt/conda/lib/python3.11/site-packages (from nbformat) (5.7.2)\n",
      "Requirement already satisfied: traitlets>=5.1 in /opt/conda/lib/python3.11/site-packages (from nbformat) (5.14.3)\n",
      "Requirement already satisfied: attrs>=22.2.0 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (23.2.0)\n",
      "Requirement already satisfied: jsonschema-specifications>=2023.03.6 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (2023.12.1)\n",
      "Requirement already satisfied: referencing>=0.28.4 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (0.35.1)\n",
      "Requirement already satisfied: rpds-py>=0.7.1 in /opt/conda/lib/python3.11/site-packages (from jsonschema>=2.6->nbformat) (0.18.0)\n",
      "Requirement already satisfied: platformdirs>=2.5 in /opt/conda/lib/python3.11/site-packages (from jupyter-core!=5.0.*,>=4.12->nbformat) (4.2.1)\n",
      "Collecting matplotlib\n",
      "  Downloading matplotlib-3.9.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)\n",
      "Collecting contourpy>=1.0.1 (from matplotlib)\n",
      "  Downloading contourpy-1.3.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.4 kB)\n",
      "Collecting cycler>=0.10 (from matplotlib)\n",
      "  Downloading cycler-0.12.1-py3-none-any.whl.metadata (3.8 kB)\n",
      "Collecting fonttools>=4.22.0 (from matplotlib)\n",
      "  Downloading fonttools-4.54.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (163 kB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m163.7/163.7 kB\u001b[0m \u001b[31m17.1 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hCollecting kiwisolver>=1.3.1 (from matplotlib)\n",
      "  Downloading kiwisolver-1.4.7-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.3 kB)\n",
      "Requirement already satisfied: numpy>=1.23 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (2.1.3)\n",
      "Requirement already satisfied: packaging>=20.0 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (24.0)\n",
      "Collecting pillow>=8 (from matplotlib)\n",
      "  Downloading pillow-11.0.0-cp311-cp311-manylinux_2_28_x86_64.whl.metadata (9.1 kB)\n",
      "Collecting pyparsing>=2.3.1 (from matplotlib)\n",
      "  Downloading pyparsing-3.2.0-py3-none-any.whl.metadata (5.0 kB)\n",
      "Requirement already satisfied: python-dateutil>=2.7 in /opt/conda/lib/python3.11/site-packages (from matplotlib) (2.9.0)\n",
      "Requirement already satisfied: six>=1.5 in /opt/conda/lib/python3.11/site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)\n",
      "Downloading matplotlib-3.9.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (8.3 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m8.3/8.3 MB\u001b[0m \u001b[31m100.5 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m00:01\u001b[0m0:01\u001b[0m\n",
      "\u001b[?25hDownloading contourpy-1.3.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (326 kB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m326.2/326.2 kB\u001b[0m \u001b[31m41.3 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hDownloading cycler-0.12.1-py3-none-any.whl (8.3 kB)\n",
      "Downloading fonttools-4.54.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.9 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m4.9/4.9 MB\u001b[0m \u001b[31m125.6 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m00:01\u001b[0m\n",
      "\u001b[?25hDownloading kiwisolver-1.4.7-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.4 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m1.4/1.4 MB\u001b[0m \u001b[31m92.9 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hDownloading pillow-11.0.0-cp311-cp311-manylinux_2_28_x86_64.whl (4.4 MB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m4.4/4.4 MB\u001b[0m \u001b[31m121.0 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m00:01\u001b[0m\n",
      "\u001b[?25hDownloading pyparsing-3.2.0-py3-none-any.whl (106 kB)\n",
      "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m106.9/106.9 kB\u001b[0m \u001b[31m11.9 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hInstalling collected packages: pyparsing, pillow, kiwisolver, fonttools, cycler, contourpy, matplotlib\n",
      "Successfully installed contourpy-1.3.1 cycler-0.12.1 fonttools-4.54.1 kiwisolver-1.4.7 matplotlib-3.9.2 pillow-11.0.0 pyparsing-3.2.0\n"
     ]
    }
   ],
   "source": [
    "!pip install yfinance\n",
    "!pip install bs4\n",
    "!pip install nbformat\n",
    "!pip install matplotlib\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "import pandas as pd\n",
    "import requests\n",
    "from bs4 import BeautifulSoup\n",
    "import plotly.graph_objects as go\n",
    "from plotly.subplots import make_subplots"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In Python, you can ignore warnings using the warnings module. You can use the filterwarnings function to filter or ignore specific warning messages or categories.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "import warnings\n",
    "# Ignore all warnings\n",
    "warnings.filterwarnings(\"ignore\", category=FutureWarning)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Define Graphing Function\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In this section, we define the function `make_graph`. **You don't have to know how the function works, you should only care about the inputs. It takes a dataframe with stock data (dataframe must contain Date and Close columns), a dataframe with revenue data (dataframe must contain Date and Revenue columns), and the name of the stock.**\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "def make_graph(stock_data, revenue_data, stock):\n",
    "    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=(\"Historical Share Price\", \"Historical Revenue\"), vertical_spacing = .3)\n",
    "    stock_data_specific = stock_data[stock_data.Date <= '2021--06-14']\n",
    "    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), y=stock_data_specific.Close.astype(\"float\"), name=\"Share Price\"), row=1, col=1)\n",
    "    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), y=revenue_data_specific.Revenue.astype(\"float\"), name=\"Revenue\"), row=2, col=1)\n",
    "    fig.update_xaxes(title_text=\"Date\", row=1, col=1)\n",
    "    fig.update_xaxes(title_text=\"Date\", row=2, col=1)\n",
    "    fig.update_yaxes(title_text=\"Price ($US)\", row=1, col=1)\n",
    "    fig.update_yaxes(title_text=\"Revenue ($US Millions)\", row=2, col=1)\n",
    "    fig.update_layout(showlegend=False,\n",
    "    height=900,\n",
    "    title=stock,\n",
    "    xaxis_rangeslider_visible=True)\n",
    "    fig.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the make_graph function that we’ve already defined. You’ll need to invoke it in questions 5 and 6 to display the graphs and create the dashboard. \n",
    "> **Note: You don’t need to redefine the function for plotting graphs anywhere else in this notebook; just use the existing function.**\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 1: Use yfinance to Extract Stock Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is `TSLA`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {},
   "outputs": [],
   "source": [
    "Tesla = yf.Ticker(\"TSLA\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [],
   "source": [
    "Tesla = yf.Ticker(\"TSLA\")\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Dividends</th>\n",
       "      <th>Stock Splits</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2010-06-29 00:00:00-04:00</td>\n",
       "      <td>1.266667</td>\n",
       "      <td>1.666667</td>\n",
       "      <td>1.169333</td>\n",
       "      <td>1.592667</td>\n",
       "      <td>281494500</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2010-06-30 00:00:00-04:00</td>\n",
       "      <td>1.719333</td>\n",
       "      <td>2.028000</td>\n",
       "      <td>1.553333</td>\n",
       "      <td>1.588667</td>\n",
       "      <td>257806500</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2010-07-01 00:00:00-04:00</td>\n",
       "      <td>1.666667</td>\n",
       "      <td>1.728000</td>\n",
       "      <td>1.351333</td>\n",
       "      <td>1.464000</td>\n",
       "      <td>123282000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2010-07-02 00:00:00-04:00</td>\n",
       "      <td>1.533333</td>\n",
       "      <td>1.540000</td>\n",
       "      <td>1.247333</td>\n",
       "      <td>1.280000</td>\n",
       "      <td>77097000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2010-07-06 00:00:00-04:00</td>\n",
       "      <td>1.333333</td>\n",
       "      <td>1.333333</td>\n",
       "      <td>1.055333</td>\n",
       "      <td>1.074000</td>\n",
       "      <td>103003500</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                       Date      Open      High       Low     Close  \\\n",
       "0 2010-06-29 00:00:00-04:00  1.266667  1.666667  1.169333  1.592667   \n",
       "1 2010-06-30 00:00:00-04:00  1.719333  2.028000  1.553333  1.588667   \n",
       "2 2010-07-01 00:00:00-04:00  1.666667  1.728000  1.351333  1.464000   \n",
       "3 2010-07-02 00:00:00-04:00  1.533333  1.540000  1.247333  1.280000   \n",
       "4 2010-07-06 00:00:00-04:00  1.333333  1.333333  1.055333  1.074000   \n",
       "\n",
       "      Volume  Dividends  Stock Splits  \n",
       "0  281494500        0.0           0.0  \n",
       "1  257806500        0.0           0.0  \n",
       "2  123282000        0.0           0.0  \n",
       "3   77097000        0.0           0.0  \n",
       "4  103003500        0.0           0.0  "
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "tesla_data.reset_index(inplace=True)\n",
    "tesla_data.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 2: Use Webscraping to Extract Tesla Revenue Data\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm\"\n",
    "html_data = requests.get(url).text"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [],
   "source": [
    "soup = BeautifulSoup(html_data, 'html.parser')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "rows = []\n",
    "for table in soup.find_all('table'):\n",
    "    if table.find('th').getText().startswith(\"Tesla Quarterly Revenue\"):\n",
    "        for row in table.find(\"tbody\").find_all(\"tr\"):\n",
    "            col = row.find_all(\"td\")\n",
    "            if len(col) != 2:\n",
    "                continue\n",
    "            Date = col[0].text\n",
    "            Revenue = col[1].text.replace(\"$\", \"\").replace(\",\", \"\")\n",
    "            rows.append({\"Date\": Date, \"Revenue\": Revenue})\n",
    "\n",
    "tesla_revenue = pd.DataFrame(rows, columns=[\"Date\", \"Revenue\"])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [],
   "source": [
    "tesla_revenue[\"Revenue\"] = tesla_revenue['Revenue'].str.replace(',|\\$',\"\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [],
   "source": [
    "tesla_revenue.dropna(inplace=True)\n",
    "\n",
    "tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != \"\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Display the last 5 row of the `tesla_revenue` dataframe using the `tail` function. Take a screenshot of the results.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "editable": true,
    "slideshow": {
     "slide_type": ""
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Revenue</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>48</th>\n",
       "      <td>2010-09-30</td>\n",
       "      <td>31</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>49</th>\n",
       "      <td>2010-06-30</td>\n",
       "      <td>28</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50</th>\n",
       "      <td>2010-03-31</td>\n",
       "      <td>21</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>52</th>\n",
       "      <td>2009-09-30</td>\n",
       "      <td>46</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>53</th>\n",
       "      <td>2009-06-30</td>\n",
       "      <td>27</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          Date Revenue\n",
       "48  2010-09-30      31\n",
       "49  2010-06-30      28\n",
       "50  2010-03-31      21\n",
       "52  2009-09-30      46\n",
       "53  2009-06-30      27"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "tesla_revenue.tail()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 3: Use yfinance to Extract Stock Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is `GME`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [],
   "source": [
    "GameStop = yf.Ticker(\"GME\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the ticker object and the function `history` extract stock information and save it in a dataframe named `gme_data`. Set the `period` parameter to ` \"max\" ` so we get information for the maximum amount of time.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [],
   "source": [
    "gme_data = pd.DataFrame(GameStop.history(period=\"max\"))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Reset the index** using the `reset_index(inplace=True)` function on the gme_data DataFrame and display the first five rows of the `gme_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Dividends</th>\n",
       "      <th>Stock Splits</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2002-02-13 00:00:00-05:00</td>\n",
       "      <td>1.620128</td>\n",
       "      <td>1.693349</td>\n",
       "      <td>1.603295</td>\n",
       "      <td>1.691666</td>\n",
       "      <td>76216000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2002-02-14 00:00:00-05:00</td>\n",
       "      <td>1.712707</td>\n",
       "      <td>1.716074</td>\n",
       "      <td>1.670626</td>\n",
       "      <td>1.683250</td>\n",
       "      <td>11021600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2002-02-15 00:00:00-05:00</td>\n",
       "      <td>1.683250</td>\n",
       "      <td>1.687458</td>\n",
       "      <td>1.658002</td>\n",
       "      <td>1.674834</td>\n",
       "      <td>8389600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2002-02-19 00:00:00-05:00</td>\n",
       "      <td>1.666418</td>\n",
       "      <td>1.666418</td>\n",
       "      <td>1.578047</td>\n",
       "      <td>1.607504</td>\n",
       "      <td>7410400</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2002-02-20 00:00:00-05:00</td>\n",
       "      <td>1.615920</td>\n",
       "      <td>1.662209</td>\n",
       "      <td>1.603296</td>\n",
       "      <td>1.662209</td>\n",
       "      <td>6892800</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                       Date      Open      High       Low     Close    Volume  \\\n",
       "0 2002-02-13 00:00:00-05:00  1.620128  1.693349  1.603295  1.691666  76216000   \n",
       "1 2002-02-14 00:00:00-05:00  1.712707  1.716074  1.670626  1.683250  11021600   \n",
       "2 2002-02-15 00:00:00-05:00  1.683250  1.687458  1.658002  1.674834   8389600   \n",
       "3 2002-02-19 00:00:00-05:00  1.666418  1.666418  1.578047  1.607504   7410400   \n",
       "4 2002-02-20 00:00:00-05:00  1.615920  1.662209  1.603296  1.662209   6892800   \n",
       "\n",
       "   Dividends  Stock Splits  \n",
       "0        0.0           0.0  \n",
       "1        0.0           0.0  \n",
       "2        0.0           0.0  \n",
       "3        0.0           0.0  \n",
       "4        0.0           0.0  "
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gme_data.reset_index(inplace=True)\n",
    "gme_data.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 4: Use Webscraping to Extract GME Revenue Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html. Save the text of the response as a variable named `html_data_2`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [],
   "source": [
    "url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html\"\n",
    "html_data2 = requests.get(url).text"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Parse the html data using `beautiful_soup` using parser i.e `html5lib` or `html.parser`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [],
   "source": [
    "soup = BeautifulSoup(html_data2, \"html.parser\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using `BeautifulSoup` or the `read_html` function extract the table with `GameStop Revenue` and store it into a dataframe named `gme_revenue`. The dataframe should have columns `Date` and `Revenue`. Make sure the comma and dollar sign is removed from the `Revenue` column.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "> **Note: Use the method similar to what you did in question 2.**  \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Click here if you need help locating the table</summary>\n",
    "\n",
    "```\n",
    "    \n",
    "Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab\n",
    "    \n",
    "soup.find_all(\"tbody\")[1]\n",
    "    \n",
    "If you want to use the read_html function the table is located at index 1\n",
    "\n",
    "\n",
    "```\n",
    "\n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "rows = []\n",
    "for table in soup.find_all('table'):\n",
    "    if table.find('th').getText().startswith(\"GameStop Quarterly Revenue\"):\n",
    "        for row in table.find(\"tbody\").find_all(\"tr\"):\n",
    "            col = row.find_all(\"td\")\n",
    "            if len(col) != 2:\n",
    "                continue\n",
    "            Date = col[0].text\n",
    "            Revenue = col[1].text.replace(\"$\", \"\").replace(\",\", \"\")\n",
    "            rows.append({\"Date\": Date, \"Revenue\": Revenue})\n",
    "gme_revenue = pd.DataFrame(rows, columns=[\"Date\", \"Revenue\"])\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Display the last five rows of the `gme_revenue` dataframe using the `tail` function. Take a screenshot of the results.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Revenue</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>57</th>\n",
       "      <td>2006-01-31</td>\n",
       "      <td>1667</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>58</th>\n",
       "      <td>2005-10-31</td>\n",
       "      <td>534</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>59</th>\n",
       "      <td>2005-07-31</td>\n",
       "      <td>416</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>60</th>\n",
       "      <td>2005-04-30</td>\n",
       "      <td>475</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>61</th>\n",
       "      <td>2005-01-31</td>\n",
       "      <td>709</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          Date Revenue\n",
       "57  2006-01-31    1667\n",
       "58  2005-10-31     534\n",
       "59  2005-07-31     416\n",
       "60  2005-04-30     475\n",
       "61  2005-01-31     709"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "gme_revenue.tail()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Question 5: Plot Tesla Stock Graph\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the `make_graph` function to graph the Tesla Stock Data, also provide a title for the graph. Note the graph will only show data upto June 2021.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<details><summary>Hint</summary>\n",
    "\n",
    "```\n",
    "\n",
    "You just need to invoke the make_graph function with the required parameter to print the graphs.The structure to call the `make_graph` function is `make_graph(tesla_data, tesla_revenue, 'Tesla')`.\n",
    "\n",
    "```\n",
    "    \n",
    "</details>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "/tmp/ipykernel_164/3211625836.py:8: SettingWithCopyWarning:\n",
      "\n",
      "\n",
      "A value is trying to be set on a copy of a slice from a DataFrame.\n",
      "Try using .loc[row_indexer,col_indexer] = value instead\n",
      "\n",
      "See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy\n",
      "\n",
      "/tmp/ipykernel_164/3211625836.py:10: SettingWithCopyWarning:\n",
      "\n",
      "\n",
      "A value is trying to be set on a copy of a slice from a DataFrame.\n",
      "Try using .loc[row_indexer,col_indexer] = value instead\n",
      "\n",
      "See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy\n",
      "\n"
     ]
    },
    {
     "data":
