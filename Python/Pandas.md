Update df with contents from another

```python
import pandas as pd

forecast = pd.DataFrame([
[6,'[0,0,0]'],
[7,'[0,0,0]'],
[10,'[0,0,0]'],
],  columns =  ["user_id", "item_id"]).set_index("user_id")
print("forecast".center(80,"*"))
print(forecast)


recs = pd.DataFrame([
[8,'[1,2,3]'],
[7,'[1,2,3]'],
],  columns =  ["user_id", "item_id"]).set_index("user_id")
print("recs".center(80,"*"))
print(recs)


forecast.loc[forecast.index.isin(recs.index)] = recs

print("updated forecast".center(80,"*"))
print(forecast)
```
