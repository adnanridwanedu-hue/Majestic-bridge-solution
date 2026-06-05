# Majestic-bridge-solution
A lightweight Python library that bridges messy data into clean DataFrames.
import pandas as pd
import json
import io

def majestic_bridge(data, source_type='auto'):
    """Bridge messy data into a clean DataFrame."""
    if source_type == 'auto':
        if isinstance(data, str):
            try:
                return pd.DataFrame(json.loads(data))
            except:
                pass
            try:
                return pd.read_csv(io.StringIO(data))
            except:
                pass
    elif source_type == 'csv':
        return pd.read_csv(io.StringIO(data))
    elif source_type == 'json':
        return pd.DataFrame(json.loads(data))
    raise ValueError("Could not bridge data")
