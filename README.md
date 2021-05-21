def remove_whitespace(df):
  """
    Date: 20210519
    This function is used to remove left and right white space in str columns, and normalize None values
    """
    import re
    import numpy as np
    
    df.columns = df.columns.str.strip()  # remove white space on the left and right sides of column name
    for i in df.columns.to_list():
        if df[i].dtypes == 'O':
            df[i] = df[i].str.strip()  # remove white space on the left and right sides of object column
            df[i] = df[i].str.replace('^nan$','nan', flags=re.I).replace({'nan': np.nan})  # 'nan' = np.nan, any cases
            df[i] = df[i].str.replace('^null$','null', flags=re.I).replace({'null': np.nan}) # 'null' = np.nan, any cases
        else:
            df[i] = df[i]
    return df
