Title: Dealing With Outliers In Pandas
Slug: pandas_outliers
Summary: Dealing With Outliers In Pandas
Date: 2016-05-01 12:00
Category: Python
Tags: Data Wrangling
Authors: Chris Albon



### import modules


```python
import pandas as pd
import numpy as np
```

### Create dataframe


```python
df = pd.DataFrame(np.random.randn(20, 5))
df.columns = ['score_1', 'score_2', 'score_3', 'score_4', 'score_5']
df
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>score_1</th>
      <th>score_2</th>
      <th>score_3</th>
      <th>score_4</th>
      <th>score_5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0 </th>
      <td> 0.809013</td>
      <td>-0.043927</td>
      <td> 0.928440</td>
      <td>-1.110457</td>
      <td> 1.623501</td>
    </tr>
    <tr>
      <th>1 </th>
      <td> 1.626228</td>
      <td>-0.304158</td>
      <td> 1.249759</td>
      <td>-1.851839</td>
      <td> 1.081616</td>
    </tr>
    <tr>
      <th>2 </th>
      <td> 1.894077</td>
      <td> 1.068677</td>
      <td>-0.111965</td>
      <td>-1.064986</td>
      <td> 0.035659</td>
    </tr>
    <tr>
      <th>3 </th>
      <td>-0.386469</td>
      <td>-1.188364</td>
      <td> 0.831405</td>
      <td>-0.014511</td>
      <td>-0.260195</td>
    </tr>
    <tr>
      <th>4 </th>
      <td>-1.242064</td>
      <td> 0.294049</td>
      <td> 0.714657</td>
      <td>-0.396795</td>
      <td>-1.219513</td>
    </tr>
    <tr>
      <th>5 </th>
      <td> 0.852891</td>
      <td> 0.355283</td>
      <td> 0.839451</td>
      <td> 0.746963</td>
      <td>-0.715827</td>
    </tr>
    <tr>
      <th>6 </th>
      <td> 0.191754</td>
      <td>-0.244156</td>
      <td>-0.238739</td>
      <td> 0.797857</td>
      <td>-1.355429</td>
    </tr>
    <tr>
      <th>7 </th>
      <td> 0.175954</td>
      <td>-0.465887</td>
      <td> 1.882503</td>
      <td>-0.174788</td>
      <td> 0.646117</td>
    </tr>
    <tr>
      <th>8 </th>
      <td>-0.404646</td>
      <td>-0.755381</td>
      <td> 0.419163</td>
      <td> 0.918593</td>
      <td> 0.923306</td>
    </tr>
    <tr>
      <th>9 </th>
      <td>-0.108578</td>
      <td> 0.166226</td>
      <td> 0.890846</td>
      <td>-0.016745</td>
      <td>-1.375534</td>
    </tr>
    <tr>
      <th>10</th>
      <td> 0.101022</td>
      <td>-0.132286</td>
      <td> 0.274950</td>
      <td>-0.678942</td>
      <td> 0.053938</td>
    </tr>
    <tr>
      <th>11</th>
      <td> 1.673355</td>
      <td>-0.164933</td>
      <td> 1.086568</td>
      <td>-1.621484</td>
      <td>-0.135308</td>
    </tr>
    <tr>
      <th>12</th>
      <td> 1.128543</td>
      <td> 0.355407</td>
      <td>-1.380984</td>
      <td> 0.604208</td>
      <td>-1.095205</td>
    </tr>
    <tr>
      <th>13</th>
      <td>-1.602945</td>
      <td> 0.614549</td>
      <td>-0.089838</td>
      <td> 0.652979</td>
      <td> 1.721376</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-1.272730</td>
      <td>-0.916772</td>
      <td>-0.594153</td>
      <td> 0.123623</td>
      <td>-0.655120</td>
    </tr>
    <tr>
      <th>15</th>
      <td> 0.140682</td>
      <td>-0.364991</td>
      <td>-0.522412</td>
      <td> 0.863911</td>
      <td> 1.106638</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.265389</td>
      <td>-0.293563</td>
      <td> 1.066478</td>
      <td>-0.485762</td>
      <td>-2.222239</td>
    </tr>
    <tr>
      <th>17</th>
      <td> 2.465491</td>
      <td>-0.437448</td>
      <td>-1.577115</td>
      <td> 0.243174</td>
      <td>-0.186260</td>
    </tr>
    <tr>
      <th>18</th>
      <td> 0.927383</td>
      <td>-0.615659</td>
      <td>-0.075537</td>
      <td> 0.939576</td>
      <td>-0.662184</td>
    </tr>
    <tr>
      <th>19</th>
      <td>-0.426472</td>
      <td> 0.990325</td>
      <td> 0.314062</td>
      <td>-0.678511</td>
      <td> 0.570545</td>
    </tr>
  </tbody>
</table>
<p>20 rows × 5 columns</p>
</div>



### Describe the dataframe


```python
df.describe()
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>score_1</th>
      <th>score_2</th>
      <th>score_3</th>
      <th>score_4</th>
      <th>score_5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td> 20.000000</td>
      <td> 20.000000</td>
      <td> 20.000000</td>
      <td> 20.000000</td>
      <td> 20.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>  0.313855</td>
      <td> -0.104151</td>
      <td>  0.295377</td>
      <td> -0.110197</td>
      <td> -0.106006</td>
    </tr>
    <tr>
      <th>std</th>
      <td>  1.101752</td>
      <td>  0.592899</td>
      <td>  0.879432</td>
      <td>  0.860297</td>
      <td>  1.081506</td>
    </tr>
    <tr>
      <th>min</th>
      <td> -1.602945</td>
      <td> -1.188364</td>
      <td> -1.577115</td>
      <td> -1.851839</td>
      <td> -2.222239</td>
    </tr>
    <tr>
      <th>25%</th>
      <td> -0.391013</td>
      <td> -0.444558</td>
      <td> -0.143658</td>
      <td> -0.678619</td>
      <td> -0.810672</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>  0.158318</td>
      <td> -0.204545</td>
      <td>  0.366613</td>
      <td> -0.015628</td>
      <td> -0.160784</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>  0.977673</td>
      <td>  0.309358</td>
      <td>  0.900244</td>
      <td>  0.676475</td>
      <td>  0.715414</td>
    </tr>
    <tr>
      <th>max</th>
      <td>  2.465491</td>
      <td>  1.068677</td>
      <td>  1.882503</td>
      <td>  0.939576</td>
      <td>  1.721376</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 5 columns</p>
</div>



### Are there any values inthe score_1 above or below 2?


```python
col = df['score_1']
col[np.abs(col) > 2]
```
