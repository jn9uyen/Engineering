# Python Notes

### Append paths
```
sys.path.append('/Users/joe/Documents/a00_repos/')
```

### Notebook show all lines
```
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

### Show all rows / columns
```
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)
```

### Reload local package
```
import sys
import importlib
importlib.reload(sys.modules['analytics_engine'])
from analytics_engine import AnalyticsEngine    # need to re-import
```

### Read all files from GCS
```
import pandas as pd
from google.cloud import storage

project = 'gcp-wow-rwds-ai-mmm-super-dev'
bucket  = 'wx-lty-mmm-super-dev'
storage_client  = storage.Client(project)

folder = 'data/dev/2021-07-19-aj-tur856-test5/predicted'
df = pd.concat((
    pd.read_parquet(f'gs://{bucket}/{f.name}')
    for f in storage_client.list_blobs(bucket, prefix=folder)
))
df.shape
df.head(2)
cond = df['crn'] == '1000000000000001225'
df[cond]
```

### Read all files (locally) into df
```
import os
import glob
import pandas as pd

path = './data/bws_ratings_2021_06_15'

df = pd.concat((
    pd.read_parquet(f)
    for f in glob.glob(os.path.join(path, "*.parquet"))
))
df.shape
df.head()
```

### Python to BQ table
```
import os
import pandas as pd
import pandas_gbq

project = 'gcp-wow-rwds-ai-mmm-super-dev'
os.environ['GOOGLE_APPLICATION_CREDENTIALS']=f"/home/jovyan/.config/gcloud/legacy_credentials/{os.getenv('JUPYTERHUB_USER')}/adc.json"
os.environ['PROJECT']=project

table_id = "test_mmm_super.AR_Team_Benefits_TEST_2021-07-19"

df = pd.read_parquet('gs://wx-lty-mmm-super-dev/data/dev/2021-07-19-aj-tur856-test4/incoming/scoring_pre_selected.parquet')
df.shape

df.to_gbq('wx-bq-poc.personal.ar_test_team_benefits', project_id=project, chunksize=10000)
```

### Read from BQ
```
import os
from google.cloud import bigquery, storage

project = 'gcp-wow-rwds-ai-mmm-dev'
# os.environ['GOOGLE_APPLICATION_CREDENTIALS']=f"/home/jovyan/.config/gcloud/legacy_credentials/{os.getenv('JUPYTERHUB_USER')}/adc.json"
os.environ['PROJECT']=project

client_bq = bigquery.Client(project)

# Contestable boosters
sql = '''
select *
from `gcp-wow-rwds-ai-mmm-dev.DEV_MMM.MMM_TEST_CARDS`
;
'''
df_bst = client_bq.query(sql).to_dataframe()
df_bst.shape
df_bst.head(2)
```

### Global plot layout
```
import matplotlib.pyplot as plt
import seaborn as sns
import seaborn.objects as so

plt.style.use('seaborn-v0_8-whitegrid')
sns.set_context('notebook', font_scale=1.0, rc={
    'axes.titlesize': 18,
    'axes.labelsize': 13,
    'axes.ticksize': 13,
    'axes.textsize': 13,
    'font.size': 11,
    'legend.fontsize': 13
})
# sns.set_style('darkgrid', rc={'legend.frameon': True})
plt.rcParams['figure.figsize'] = (9, 5)
```

#### Auto Layout
```
import matplotlib.pyplot as plt
from matplotlib import rcParams
import seaborn as sns

rcParams.update({"figure.autolayout": True})
```

### Run `http.server` function (from cmd line)
```
python -m http.server
```
- `-m`: module
- this command creates a web connection to the (local) current directory, on port `8000`
- in a browser, connect via `localhost:8000`; OR

On Mac, use these commands to get [IP address](https://constellix.com/news/what-is-my-ip-address)
-> local IP address is from "wireless connection" when connected on wifi
- `ipconfig getifaddr en1`: system will return the IP address for a wired Ethernet connection
- `ipconfig getifaddr en0`: return the IP address of your wireless connection
- `curl ifconfig.me`: returns the public IP address of the Mac Terminal

e.g.
```
10.0.0.2:8000
```

### Print `PYTHONPATH`
```
import os
import sys

print(sys.path)
print(os.environ.get('PYTHONPATH', '').split(os.pathsep))
```

### Create pandas df using loop
```
# Apply stats test: t-test, Mann-Whitney U, PSI
default_grp = pdf.groupby("has_defaulted_flag")

res = []
for col in score_cols:
    default = default_grp.get_group("y")[col]
    non_default = default_grp.get_group("n")[col]
    t_pval = stats.ttest_ind(default, non_default, equal_var=False)[1]
    mwu_pval = stats.mannwhitneyu(default, non_default)[1]
    psi = calc_psi(default, non_default)
    # psi = None
    res.append(
        {
            "metric": col,
            "t_pval": t_pval,
            "mwu_pval": mwu_pval,
            "psi": psi,
        }
    )
res = pd.DataFrame(res)
res
```
Note, do NOT use `pd.concat` on a list of lists because it is inefficient.

## Conda

### List conda envs
```
conda env list
```

### Create env cloning another `env`
```
conda create --name <env_name> --clone <clone_env_name>
# e.g.
conda create --name <env_name> --clone base
```

### Create env with python version
```
conda create -n <env_name> python=<version>
# e.g.
conda create -n test_env python=3.6.5
```

### Activate env
```
source activate <env_name>
```

### Install from requirements.txt
```
pip install -r requirements.txt
```

### Create env and ensure it's available in Jupyter notebook as a kernel

In terminal:
```
conda create -n <env_name> ipykernel
python -m ipykernel install --user --name <env_name>

e.g.
conda create -n test_env --clone base
conda install -n test_env ipykernel
python -m ipykernel install --user --name test_env
```

### Delete env
```
conda env remove -n <env_name>
```

# Pip notes

### Check package version (in terminal)
```
pip show <package>
pip show rankstrategy
```
