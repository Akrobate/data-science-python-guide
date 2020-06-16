# Data loading

In this section we are going to overview ways to quick load data, save data, connect to a MySql database in order to load it in a panda dataframe

## Mysql

Simpliest way to load data from mysql database to a panda Dataframe is to user sqlalchemy package

```python
import pandas as pd
from sqlalchemy import create_engine

connection_string = "mysql+pymysql://DB_USER:DB_PASSWORD@DB_HOST:DB_PORT/DB_NAME"
engine = create_engine(connection_string)

query = "Select id, name from my_table where 1"
my_dataframe = pd.read_sql_query(query, engine)

```

Note that sqlachemy has a lot of connectors to connect to other databases as pgSQL...

## Load from CSV

## Save to CSV

```python
import pandas as pd
my_dataframe.to_csv("data.csv", index=False)
```

index=False indicate that index column must not be exported in csv file
