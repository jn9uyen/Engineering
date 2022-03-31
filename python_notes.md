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
importlib.reload(sys.modules['qb5001_utils'])
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

project = 'gcp-wow-rwds-ai-mmm-super-dev'
os.environ['GOOGLE_APPLICATION_CREDENTIALS']=f"/home/jovyan/.config/gcloud/legacy_credentials/{os.getenv('JUPYTERHUB_USER')}/adc.json"
os.environ['PROJECT']=project

client_bq = bigquery.Client(project)

# Contestable boosters
sql = '''
select *
from `gcp-wow-rwds-ai-mmm-super-dev.PROD_MMM.CONTEST_BOOSTERS_20210305_refactor_dynamic`
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

plt.style.use('ggplot')
sns.set_context('notebook', font_scale=1.2, rc={
    'axes.titlesize': 20,
    'axes.labelsize': 18,
    'axes.ticksize': 18,
    'axes.textsize': 18,
    'font.size': 12,
    'legend.fontsize': 14
})
sns.set_style('darkgrid', rc={'legend.frameon': True})
plt.rcParams['figure.figsize'] = (9, 5)
```

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
