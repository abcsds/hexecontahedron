---
layout: post
title: "Accessing World Bank Data from Julia"
date: "2016-10-07 23:55:24 -0500"
comments: true
tags: Julia , World Bank , DataFrames , Visualization
image: "{{ site.static_folder }}/img/WorldBank/worldbank.png"
---

While looking for ways to access the World Bank data bank programmatically, I found this very useful library to access it with Julia (along with many others for python and R). The library is [WorldBankData.jl](https://github.com/abcsds/WorldBankData.jl), by [4gh](https://github.com/4gh). Although the repo doesn't have much activity, the library works great. Here are some examples of what can be done with the World Bank data, and the powerful Julia dataframes. I will also use Plots.jl for visualizations;


```julia
using WorldBankData
using Plots
using DataFrames
```

The World Bank offers two kind of data sources: Countries and Indicators. Indicators are the variables being measured in every country. Every year 13,398 indicators are measured in 258 countries. I have selected some countries to work with, since not all data from the world bank is complete. This filtering will facilitate our task:


```julia
countries = ["AW","AF","AO","AL","AD","AE","AR","AM","AS","AG","AU","AT","AZ","BI","BE","BJ","BF","BD","BG","BH","BS","BA","BY","BZ","BM","BO","BR","BB","BN","BT","BW","CF","CA","CH","CL","CN","CI","CM","CD","CG","CO","KM","CV","CR","CU","KY","CY","CZ","DE","DJ","DM","DK","DO","DZ","EC","EG","ER","ES","EE","ET","FI","FJ","FR","FO","FM","GA","GB","GE","GH","GN","GM","GW","GQ","GR","GD","GL","GT","GU","GY","HK","HN","HR","HT","HU","ID","IM","IN","IE","IR","IQ","IS","IL","IT","JM","JO","JP","KZ","KE","KG","KH","KI","KN","KR","XK","KW","LA","LB","LR","LY","LC","LI","LK","LS","LT","LU","LV","MO","MA","MC","MD","MG","MV","MX","MH","MK","ML","MT","MM","ME","MN","MP","MZ","MR","MU","MW","MY","NA","NC","NE","NG","NI","NL","NO","NP","NZ","OM","PK","PA","PE","PH","PW","PG","PL","PR","KP","PT","PY","PF","QA","RO","RU","RW","SA","SD","SN","SG","SB","SL","SV","SM","SO","RS","SS","ST","SR","SK","SI","SE","SZ","SC","SY","TC","TD","TG","TH","TJ","TM","TL","TO","TT","TN","TR","TV","TZ","UG","UA","UY","US","UZ","VC","VE","VI","VN","VU","WS","YE","ZA","ZM","ZW"];
```

A list of countries has to be given to the `wdi()` function, along with an indicator. This function queries the WBDB and returns a dataframe with all data available. If a year is added to the query, only the data for that year will be returned. Let's work with total country population.


```julia
df=wdi("SP.POP.TOTL", countries, 2015)
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>year</th></tr><tr><th>1</th><td>AW</td><td>Aruba</td><td>103889.0</td><td>2015.0</td></tr><tr><th>2</th><td>AF</td><td>Afghanistan</td><td>3.2526562e7</td><td>2015.0</td></tr><tr><th>3</th><td>AO</td><td>Angola</td><td>2.5021974e7</td><td>2015.0</td></tr><tr><th>4</th><td>AL</td><td>Albania</td><td>2.889167e6</td><td>2015.0</td></tr><tr><th>5</th><td>AD</td><td>Andorra</td><td>70473.0</td><td>2015.0</td></tr><tr><th>6</th><td>AE</td><td>United Arab Emirates</td><td>9.156963e6</td><td>2015.0</td></tr><tr><th>7</th><td>AR</td><td>Argentina</td><td>4.3416755e7</td><td>2015.0</td></tr><tr><th>8</th><td>AM</td><td>Armenia</td><td>3.017712e6</td><td>2015.0</td></tr><tr><th>9</th><td>AS</td><td>American Samoa</td><td>55538.0</td><td>2015.0</td></tr><tr><th>10</th><td>AG</td><td>Antigua and Barbuda</td><td>91818.0</td><td>2015.0</td></tr><tr><th>11</th><td>AU</td><td>Australia</td><td>2.3781169e7</td><td>2015.0</td></tr><tr><th>12</th><td>AT</td><td>Austria</td><td>8.611088e6</td><td>2015.0</td></tr><tr><th>13</th><td>AZ</td><td>Azerbaijan</td><td>9.651349e6</td><td>2015.0</td></tr><tr><th>14</th><td>BI</td><td>Burundi</td><td>1.1178921e7</td><td>2015.0</td></tr><tr><th>15</th><td>BE</td><td>Belgium</td><td>1.1285721e7</td><td>2015.0</td></tr><tr><th>16</th><td>BJ</td><td>Benin</td><td>1.0879829e7</td><td>2015.0</td></tr><tr><th>17</th><td>BF</td><td>Burkina Faso</td><td>1.810557e7</td><td>2015.0</td></tr><tr><th>18</th><td>BD</td><td>Bangladesh</td><td>1.60995642e8</td><td>2015.0</td></tr><tr><th>19</th><td>BG</td><td>Bulgaria</td><td>7.177991e6</td><td>2015.0</td></tr><tr><th>20</th><td>BH</td><td>Bahrain</td><td>1.377237e6</td><td>2015.0</td></tr><tr><th>21</th><td>BS</td><td>Bahamas, The</td><td>388019.0</td><td>2015.0</td></tr><tr><th>22</th><td>BA</td><td>Bosnia and Herzegovina</td><td>3.810416e6</td><td>2015.0</td></tr><tr><th>23</th><td>BY</td><td>Belarus</td><td>9.513e6</td><td>2015.0</td></tr><tr><th>24</th><td>BZ</td><td>Belize</td><td>359287.0</td><td>2015.0</td></tr><tr><th>25</th><td>BM</td><td>Bermuda</td><td>65235.0</td><td>2015.0</td></tr><tr><th>26</th><td>BO</td><td>Bolivia</td><td>1.0724705e7</td><td>2015.0</td></tr><tr><th>27</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>2015.0</td></tr><tr><th>28</th><td>BB</td><td>Barbados</td><td>284215.0</td><td>2015.0</td></tr><tr><th>29</th><td>BN</td><td>Brunei Darussalam</td><td>423188.0</td><td>2015.0</td></tr><tr><th>30</th><td>BT</td><td>Bhutan</td><td>774830.0</td><td>2015.0</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></table>




Lets visualize the first 50 countries with a barplot.


```julia
bar(df[:iso2c][1:50], df[:SP_POP_TOTL][1:50], size=(900,400), label="Total Population")
```




<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA4QAAAGQCAYAAAD2lq6fAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAPYQAAD2EBqD+naQAAIABJREFUeJzt3X18lnXdx//3BhbMUlEQuXFMhQGJys7pA1FTSAS1rpmikgrJpgYapKaQ/agE0+sSTOsq8aJ+TjDtMcUovCm0LhMVNcydhKmAGrcpKiNvgmkqO35/HL+dl8jujn2PHce+n/P1fDx4lDu38Xm/z+/G+dm5HSsIgiAQAAAAACDvFKY9AAAAAAAgHSyEAAAAAJCnuqY9gO/q6ur0yCOPqKSkRN27d097HAAAAABo0vvvv6+NGzdq3Lhx6tmzpyQWQmePPPKIJk6cmPYYAAAAANAmd999ty644AJJLITOSkpKJIWlDh06tMnXueKKK/STn/wkwaniZyGDKzqw0QEZbKCDkO89+D6/ZCNDS9asWRN+4fv0/0c6aHD73sn2DdL9s1t8rGSBhbNABhta6qDxY7pxh5FYCJ01fpvo0KFDlclkmnyd/fbbr9nbfGEhgys6sNEBGWygg5DvPfg+v2QjQ5uUnSENKGvf225aJd0/u8XHShZYOAtksKEtHXzyR924qEwCPvzww7RHcGYhgys6sNEBGWygg5DvPfg+v2QjA+Jh4SyQwYaoHfAMYQL++te/pj2CMwsZXNGBjQ7IYAMdhHzvwff5JRsZEI/OdBY2b96surq6yG/3l7/8RdlstgMmSo6FDK4+2UHPnj1VXFzc4uuzECZg8OB2fs99J2Ihgys6sNEBGWygg5DvPfg+v2QjA+LRWc7C5s2bNXToUNXX17fr7cvLy2OeKHkWMrhq7KCoqEhr1qxpcSlkIUzA1KlT0x7BmYUMrujARgdksIEOQr734Pv8ko0MiEdnOQt1dXWqr683fxEftK7xAjJ1dXUshGk777zz0h7BmYUMrujARgdksIEOQr734Pv8ko0MiEdnOwvWL+KD+HBRGQAAAADIUyyECaiurk57BGcWMriiAxsdkMEGOgj53oPv80s2MiAenAX4ioUwARaudGQhgys6sNEBGWygg5DvPfg+v2QjA+LBWWhZSUmJhg4dqrKyMg0bNky33XZbh/1dd955p84888xWX2/16tW69957d3tZJpPRzp07Y5nj5z//ucrKylRWVqYDDjhA/fv3V1lZmTKZjB5//PFm3y4IAs2ZM0cff/xxm/6eL37xi/r973/f7jn5GcIEzJ8/P+0RnFnI4IoObHRABhvoIOR7D77PL9nIgHh09rNwyRMf64W343t/w3pI/++JbV8lCgoKtHjxYh1xxBHavHmzjjzySJ144okaNmxYfEN96u9rzapVq3T//fdrwoQJuZfFudhPmTJFU6ZMkSRVVlaqrKxM3/rWt1p9u127dmnOnDmaMWOGunbt+HWNZwgBAAAA4154W/rzW0Fsf9qzXAZBIEkqLi7W4MGD9fLLL0uSbrrpJg0bNkxHHXWUJk2apH/961+SpDlz5ujss8/WySefrKFDh+qMM87Q22+/nbvt29/+du59z58/X1VVVXv8nW+++aa+9KUv6ZhjjtERRxyRW8i2bduma6+9VsuXL1cmk9Fll10mSSosLNR7770nSXruued0/PHH66ijjtKxxx6rp59+WpK0adMm9ejRQ7Nnz9bRRx+t0tJSPfzww5H7eOWVVzRmzBgdddRRymQyeuihhyRJl156qQoKCnTccccpk8no7bff1t13360RI0aovLxcmUxGy5Yti/z3NYeFEAAAAEBi/va3v2ndunU66qijtGzZMi1atEjPPPOMVq9eraKiIl1zzTW5112xYoXuuecerVmzRv3799d3v/vdSH/Xfvvtp4ceekh/+ctftHr1am3YsEGLFy9Wr169dN1112n06NHKZrO5b2FtfGbxo48+0vjx4zVnzhytXr1aN998s8aPH5/7/Y7vvvuuhg8frueee04/+9nPdMUVV0Tu4bzzztPEiRO1evVq1dTUaPLkyXr99de1YMECBUGgZ555RtlsVj169NDpp5+ulStXqra2VkuWLFFVVZV27doV+e9sCgshAAAAgA43YcIEZTIZXXrppVq4cKEOO+wwPfroo5owYYI+//nPSwqfHfvjH/+Ye5svf/nL6tWrlyTpG9/4hv73f/830t/Z0NCgmTNnavjw4SorK1Ntba3++te/Nvv6jc9irlu3Tl26dNGYMWMkSccff7wOOuig3Nt2795dX/3qVyVJI0eO1Pr16yPN9c477+jFF1/U5MmTJUmDBw/WscceqxUrVuwxiyT9/e9/16mnnqojjjhCZ511lt5++21t2rQp0t/ZHBbCBFRUVKQ9gjMLGVzRgY0OyGADHYR878H3+SUbGRAPzkLrFi9erGw2qxUrVjR70ZfWfvav8fauXbvu9gzZBx980OTr33LLLdq2bVvuGcLzzjuv2ddty9/f6LOf/Wzu/3fp0iWWZ+ta+rvPPfdcffOb39Tf/vY3rVq1Sp/97GdbzBEFC2ECpk2blvYIzixkcEUHNjoggw10EPK9B9/nl2xkQDw6+1kY1kM69sCC2P4M6xF9hk8+49VozJgxWrx4sXbs2CEpvDLnuHHjcrf//ve/17Zt2yRJt99+e+4Zu4EDB+q5555TQ0OD6uvrtWTJkib/zrffflsHHXSQ9tprL73xxhu67777crfts88+evfdd5uccfDgwWpoaNCjjz4qSXr66af15ptvavjw4U1maSpbS/bbbz8NGzZMd955pyTp5Zdf1sqVK/XFL35RXbp00d57773bbO+++65KSkokSYsWLcr1FQeuMpqAsWPHpj2CMwsZXNGBjQ7IYAMdhHzvwff5JRsZEI/OfhaiXBG0IzT37Nepp56qF198Uccee6y6dOmiI488crdfSfHFL35R5513nl577TWVlpZq0aJFkqSzzjpL9913n77whS+of//+ymQyuZ/v+6TLL79cZ599to444gj17dtXp5xySu62k08+WTfffLOGDx+u4447Trfddltuzr322ku/+c1vNH36dF111VXq1q2blixZoqKioibztPWZzU+qqanRlClTdMstt6hLly5atGiR+vTpI0m66qqrNGrUKO2999569NFH9ZOf/EQVFRU64IADNGbMGPXr16/Nf3drCoKo6yx2k81mVV5ertraWmUymbTHAQAAiE3j4xzNWikNKGvfO9m0SrphBI+VEmLpsemcOXP07rvv6pZbbkl7FC81dRaaehnfMgoAAAAAeYqFMAFLly5NewRnFjK4ogMbHZDBBjoI+d6D7/NLNjIgHpyF+F177bU8O5gAFsIE1NTUpD2CMwsZXNGBjQ7IYAMdhHzvwff5JRsZEA/OAnzFQpiAe++9N+0RnFnI4IoObHRABhvoIOR7D77PL9nIgHhwFuArrjIKAAAAGLNmzZq0R0DK2noGWAgBAAAAI3r27KmioiJNnDgx7VHQCRQVFalnz54tvg4LIQAAAGBEcXGx1qxZo7q6urRHQSfQs2dPFRcXt/g6LIQJqKys1MKFC9Mew4mFDK7owEYHZLCBDkK+9+D7/JKNDIhHZzoLxcXFrS4BTelMGdrLQgZXUTvg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AAB0au1aCIMgUFPfabp48WJNnTpVknT00UerX79+evzxxyVJ9957b+62kpISjRo1Sr/97W9zb3fJJZdIknr06KEJEyaopqYmd9ukSZPUrVs3feYzn1FVVVXutiVLluiMM85Qr169JElTp07N3bZs2TJlMhkNGjRIknTZZZflbqutrdVee+2lE088UVK4AD744IP68MMPtW3bNtXW1uqCCy6QJI0fP15btmzR+vXr21MVAAAAAHRa7b6ozKRJk3TUUUfpkksu0fbt2/XPf/5TH3/8sQ488MDc6wwYMECbN2+WJG3evFkDBgzI3VZSUpL4bW+88YYaGhr2uO1zn/uc9t13X73++uvasmWL+vTpo8LC/6umuLg4937bY8aMGe1+287CQgZXdGCjAzLYQAch33vwfX7JRgbEw8JZIIMNUTto10L45JNPavXq1cpmszrggANy31Lp8/VpOnL24uLiDnvfSbGQwRUd2OiADDbQQcj3HnyfX7KRAfGwcBbIYEPUDtq1EPbv31+S1KVLF11xxRV68skntf/++6tr16566623cq+3cePG3EADBgzQpk2bmrytuLi4Q27buHFj7rYNGzbknvn79G07duzQe++9p759++rggw/W1q1b1dDQkLt98+bNrRZ7+umnq6KiYrc/I0eO1NKlSzV9+vTc6/3hD39QRUXFHm//zW9+U9XV1bu9LJvNqqKiQnV1dbu9/Nprr9XcuXN3e9nmzZtVUVGhtWvX7vbyn/3sZ3t8laC+vl4VFRV7/I6SmpoaVVZW7jHbhAkTdPDBB+/2Ml9zLF26tN05jj/+eBM5XO6PxrPsc45Pfjz6muOUU07Z7eW+5nD5+OjZs6eJHK73x/Tp073O8cmPR19zfDKDzzk+rakccegMOTrq/rjooou8zzF9+nTv74/Gj0nfczRyedxeU1OT20kOOuggVVRU6IorrtjjbRREtHPnzuCdd97J/ffNN98cnHTSSUEQBEFlZWUwe/bsIAiC4Nlnnw369+8ffPzxx0EQBMHs2bODysrKIAiCYP369UHv3r2D7du3B0EQBIsWLQrGjBkT7Nq1K9i+fXswYMCA4IUXXgiCIAiWL18eDBs2LKivrw8++OCD4Oijjw5+97vf5d5Pv379gjfffDNoaGgIKioqgvnz5wdBEAT/+te/gt69ewfr1q0LgiAIpk2bFsyYMSMI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1665zyuZTEa/+MUv0h43di3lLyws3O3fzZ07d+7267usaK6D9957T2+99ZYuuugiHXbYYSorK9Pw4cN12WWX6e2330577D00lWPKlCnq0qWLXnrppd1ed9u2bfrc5z6nbdu2pTRt0w455JDc469///vfOuOMM7T//vvr+OOP3+315s2bp4qKijRGTETj59fhw4ertLRUZ555pp555hlJ0p133qkzzzyz9XcSIBa33357UFFREfTq1SvYuXNnEARBcNFFFwU33HBD7nWGDBkSHH300cGmTZuCIAiCZ555JigpKUll3pY0lWX58uVBWVlZypMlo7n8paWlwWGHHRZ89NFHQRAEwXvvvRcMHDgwOPjgg9xQYS4AAAoLSURBVIPVq1enOXKHaKqHRrNnzw6uvPLKlCZrm5KSkuD555/P/feXv/zl4LbbbvPmLLd1/h07dgSXXHJJkMlkgoaGhjRG7VDN9dDohBNOCM4999xg8uTJaYzX4ZrL//rrrwcHHnhgcM899+Ruq6mpCQ466KDgzTffTGPUFrV0nvv06RP07t072L59exAEQfDCCy8EhxxySFqjtujrX/96UFFREbz77ru5l/36178O1q9fH/To0SPFyZLRUv6999476NevX7BmzZogCMLPTYWFhWmN2mGa6+Cll14KBg8eHFx//fW5z8UfffRRsGDBguBvf/tbWuM2q7kcFRUVwdVXX73b6/7oRz8KzjrrrKRHbFVJSUmwevXq4L333gtGjx4dTJ06NQiC8PPLLbfcEgRBELz44otB//79g7feeivNUTvUpz+//uY3vwn222+/4Nlnnw0WLVoUnHnmma2+D3tfuklJdXW1rrzySn3pS1/SvffeK0kaNWqUli9fLkn6xz/+oR49eujLX/5y7mXLly/X6NGjU5q4eU1lySfN5S8qKtLJJ5+s+++/X5J0zz336Oyzz1bXrjYv1mvhHAT//49If/DBB6qvr1ePHj1Sniiatsy/995767bbblNdXZ0efvjhpEdMRHM9rFu3Tq+99poWLFigBx98UDt27EhzzA7TVP7bbrtNo0eP1oQJE3Kv97WvfU0nnniibrvttrRGbVFz92Pv3r01adIkXXfddWmO16q///3vWrJkiRYtWqR99tkn9/Lx48ebfCbs01rLv9dee+m73/2urrnmmhSn7FgtdfD0009r//3316xZs1RQUCBJ6tq1q6ZMmaJhw4alNXKTWspx3XXX6a677tKuXbtyL1+4cKEuvvjiNEZtVV1dnU4++WSNHDlS//M//yNJuv322/XjH/9Ya9as0eTJk/WTn/xEvXr1SnnSjhV84pIwZ555pqZOnaqbbrqpzW9v/zNYAtasWaOtW7dq1KhRuvDCC3X77bdLkkaPHq2nn35aH3/8sR577DGNGjVKJ510kh577DFJ0mOPPaYvfelLaY6+h09nqa6uTnukRLWUv6CgQJWVlbmXLVy4UFVVVbt9EFrR3Jn2zYQJE1RWVqY+ffqoS5cuOvfccyVJa9eu3e1bu77zne+kPGnTmpv/07p27aqysjK9+OKLCU+YjOZ6uOOOO/T1r39dPXr00JgxY3TPPfekPGnH+HT+c845R9lsViNHjtzjdUeOHKna2toUpmxdc/djQUGBZs2apZqaGm3atCnlKZuXzWY1aNCgZr+w9N577+32eeW1115LeMKO1Vr+goICTZ06VS+88ELu29WsaamDbDarESNGpDBVdC3lOOqoo3TwwQfrd7/7nSTpz3/+s959912deuqpSY/ZJhMmTNApp5yy27edH3TQQbrpppt03HHHqbS0tFP+WEhHGzFihF566aXcFydaw0IYg+rqak2aNEmSNHbsWG3cuFHr1q1Tv3791K9fP/35z3/W8uXLNWrUKB177LG5JfHpp5/udM8QfjrLhg0bOu3PpHSE1vIfe+yx2rJli/7whz+oa9euGjRoUFqjdqjmzrRvFi9erFWrVmn79u0aMGCAZs6cKUkaMmSIstmsVq1apWw2q7lz56Y8adOam78pFr8w0ejTPXznO9/Rrl279Mtf/jJ3Tn3+wkVrPpm/pKRE3/nOd9r8j3xn0tJ53m+//XTFFVdo1qxZKU7oZp999tnt80q/fv3SHilxXbp00Q9/+MPcF9ksf15qzeLFi1VWVqZDDz3Uuy+uV1VV6Y477pAUfvH7wgsv7LSfc77yla/o17/+tf7xj3/s9vIJEyZon3320VVXXZXSZOmK+rHHQujo448/1l133aWFCxfq0EMP1cCBA1VfX5/74B81apQee+wxPfXUUzrhhBPUvXt3HXjggbrnnnvUt2/fTvUPRmtZrGtr/kmTJmnixImqqqpKadKOZekcNH5CLCws1Pjx4/XII4+kPFE0bZ3/o48+0l//+tdO921Jcfl0Dw8//LAeeughvfPOOzrllFN06KGH6tJLL9WqVav2uBiCBZ/Mf9ZZZ+nhhx9WJpPZ7aJljZ555hllMpmkR2yT1s7zFVdcoSeeeEKrVq1KY7xWZTIZvfLKK53yAiFJaGv+8847Tzt37tT999/faZeI9mqpg7KyMj377LO5/z733HO1atUqnXTSSdq5c2eSY7aqtfvy/PPP1/Lly7VhwwYtXry4Uz/eufLKKzV16lSNGjVKW7Zs2e22wsJCdenSJaXJ0vWXv/xFw4YNa/NiyELo6P7779dhhx2mLVu2aP369dqwYYOeeeYZ/fKXv9SuXbs0evRo3X333TrggANUVFQkSTrxxBP1wx/+sNM9O9hSlo8++sj8V/ramr+yslJXX311s9++57vWzrSv/vSnP2nw4MGS/PyqdXPz79y5U9OnT1evXr00bty4tMZLTGMP1dXV+u///m+tX79e69ev18aNG/Xtb3/b7LOEjf70pz9pyJAhuvTSS7V8+fLdvk22pqZGjz/+uC677LIUJ2ybps5z9+7d9f3vf18/+MEP0hytWYcddpjGjx+viy66SO+++27u5b/5zW/U0NDg5eeVKKLkv/HGG/W9730vjTE7VEsdHHfccaqrq9N//dd/qaGhIXdbfX19GqO2qKUcGzdu1L777qv/+I//yH2b96GHHpritK278sorNX36dI0ePVqbN29Oe5zU3X///VqwYEGkZ0dtXg0jQXfccYcmTpy428uGDBmi/v3768EHH9SoUaP06quv6uyzz87dftJJJ+nGG2/U9ddfn/S4LWopy44dO7RmzRoVFxcrCAIVFBRo5MiR3l5spCmt5W/8SmevXr12+1Yna18Bbe1Mf/WrX01psmgKCgo0YcIEde/eXR999JFKSkq0YMECvfrqq3r55Zdzz6IEQaB99tlHjz/+eMoT764t83/44YeSpHHjxunRRx81dxalPXs45JBDNH/+fA0dOlR33nnnbq97/vnna8yYMZo3b56Ziz01dw769Omj5cuX66qrrtKsWbNUWFiowYMH64knnlDv3r3THnsPLZ3nT57bqqoq3Xzzzfroo49SnLZ5d9xxh374wx9qxIgR2muvvdTQ0KATTzxRhx12mMmPv09ra/7GZ+4tPjhvroMxY8boiSee0DXXXKOBAweqR48e6t69u4YPH66zzjor7bH30FIOSbrooot08skn66677kp50uZ98sxdfvnlKiwszH1n3oABA/LiY1L6v8+v3bp1086dO/WFL3xBy5Yt0zHHHKPnn39e3bp1a/19BNa/pAUAAAAAeWbatGnq2bOnZs+e3eLr2fgSKgAAAABAH3zwgUaMGKFevXq16QrcPEMIAAAAAHmKi8oAAAAAQJ5iIQQAAACAPMVCCAAAAAB56v8DrFd8VkfWVmYAAAAASUVORK5CYII=" />



The result is somehow expected. China is within the first 50 countries in the list, and it scales the graph for itself. Let's find out exactly how much is big.


```julia
maximum(df[:SP_POP_TOTL])
```




    1.37122e9



More than one billion people live only in china. This is almost 20% of the world's population:


```julia
maximum(df[:SP_POP_TOTL])/sum(df[:SP_POP_TOTL])
```




    0.18750300206223874



Right now we have the population for 208 countries. Almost all the countries measured by the WB.


```julia
size(df[:SP_POP_TOTL])
```




    (208,)



In julia to find the index of the maximum value, the `indmax()` function can be used. This is useful if you want to know more about the element with the maximum value in a column.


```julia
indmax(df[:SP_POP_TOTL])
```




    36



In fact, element number 36 in our dataframe is China:


```julia
df[:country][36]
```




    "China"



Now let's try something else. We want to see the most populated countries in the world. The first thought to come to mind is to sort the dataframe, right?


```julia
sort(df)
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>year</th></tr><tr><th>1</th><td>AD</td><td>Andorra</td><td>70473.0</td><td>2015.0</td></tr><tr><th>2</th><td>AE</td><td>United Arab Emirates</td><td>9.156963e6</td><td>2015.0</td></tr><tr><th>3</th><td>AF</td><td>Afghanistan</td><td>3.2526562e7</td><td>2015.0</td></tr><tr><th>4</th><td>AG</td><td>Antigua and Barbuda</td><td>91818.0</td><td>2015.0</td></tr><tr><th>5</th><td>AL</td><td>Albania</td><td>2.889167e6</td><td>2015.0</td></tr><tr><th>6</th><td>AM</td><td>Armenia</td><td>3.017712e6</td><td>2015.0</td></tr><tr><th>7</th><td>AO</td><td>Angola</td><td>2.5021974e7</td><td>2015.0</td></tr><tr><th>8</th><td>AR</td><td>Argentina</td><td>4.3416755e7</td><td>2015.0</td></tr><tr><th>9</th><td>AS</td><td>American Samoa</td><td>55538.0</td><td>2015.0</td></tr><tr><th>10</th><td>AT</td><td>Austria</td><td>8.611088e6</td><td>2015.0</td></tr><tr><th>11</th><td>AU</td><td>Australia</td><td>2.3781169e7</td><td>2015.0</td></tr><tr><th>12</th><td>AW</td><td>Aruba</td><td>103889.0</td><td>2015.0</td></tr><tr><th>13</th><td>AZ</td><td>Azerbaijan</td><td>9.651349e6</td><td>2015.0</td></tr><tr><th>14</th><td>BA</td><td>Bosnia and Herzegovina</td><td>3.810416e6</td><td>2015.0</td></tr><tr><th>15</th><td>BB</td><td>Barbados</td><td>284215.0</td><td>2015.0</td></tr><tr><th>16</th><td>BD</td><td>Bangladesh</td><td>1.60995642e8</td><td>2015.0</td></tr><tr><th>17</th><td>BE</td><td>Belgium</td><td>1.1285721e7</td><td>2015.0</td></tr><tr><th>18</th><td>BF</td><td>Burkina Faso</td><td>1.810557e7</td><td>2015.0</td></tr><tr><th>19</th><td>BG</td><td>Bulgaria</td><td>7.177991e6</td><td>2015.0</td></tr><tr><th>20</th><td>BH</td><td>Bahrain</td><td>1.377237e6</td><td>2015.0</td></tr><tr><th>21</th><td>BI</td><td>Burundi</td><td>1.1178921e7</td><td>2015.0</td></tr><tr><th>22</th><td>BJ</td><td>Benin</td><td>1.0879829e7</td><td>2015.0</td></tr><tr><th>23</th><td>BM</td><td>Bermuda</td><td>65235.0</td><td>2015.0</td></tr><tr><th>24</th><td>BN</td><td>Brunei Darussalam</td><td>423188.0</td><td>2015.0</td></tr><tr><th>25</th><td>BO</td><td>Bolivia</td><td>1.0724705e7</td><td>2015.0</td></tr><tr><th>26</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>2015.0</td></tr><tr><th>27</th><td>BS</td><td>Bahamas, The</td><td>388019.0</td><td>2015.0</td></tr><tr><th>28</th><td>BT</td><td>Bhutan</td><td>774830.0</td><td>2015.0</td></tr><tr><th>29</th><td>BW</td><td>Botswana</td><td>2.262485e6</td><td>2015.0</td></tr><tr><th>30</th><td>BY</td><td>Belarus</td><td>9.513e6</td><td>2015.0</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></table>



Well, not really. This function will sort only by the first column. To sort by other column we can add the `cols` argument to the function.


```julia
sort(df, cols=[:SP_POP_TOTL])
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>year</th></tr><tr><th>1</th><td>TV</td><td>Tuvalu</td><td>9916.0</td><td>2015.0</td></tr><tr><th>2</th><td>PW</td><td>Palau</td><td>21291.0</td><td>2015.0</td></tr><tr><th>3</th><td>SM</td><td>San Marino</td><td>31781.0</td><td>2015.0</td></tr><tr><th>4</th><td>TC</td><td>Turks and Caicos Islands</td><td>34339.0</td><td>2015.0</td></tr><tr><th>5</th><td>LI</td><td>Liechtenstein</td><td>37531.0</td><td>2015.0</td></tr><tr><th>6</th><td>MC</td><td>Monaco</td><td>37731.0</td><td>2015.0</td></tr><tr><th>7</th><td>FO</td><td>Faroe Islands</td><td>48199.0</td><td>2015.0</td></tr><tr><th>8</th><td>MH</td><td>Marshall Islands</td><td>52993.0</td><td>2015.0</td></tr><tr><th>9</th><td>MP</td><td>Northern Mariana Islands</td><td>55070.0</td><td>2015.0</td></tr><tr><th>10</th><td>AS</td><td>American Samoa</td><td>55538.0</td><td>2015.0</td></tr><tr><th>11</th><td>KN</td><td>St. Kitts and Nevis</td><td>55572.0</td><td>2015.0</td></tr><tr><th>12</th><td>GL</td><td>Greenland</td><td>56114.0</td><td>2015.0</td></tr><tr><th>13</th><td>KY</td><td>Cayman Islands</td><td>59967.0</td><td>2015.0</td></tr><tr><th>14</th><td>BM</td><td>Bermuda</td><td>65235.0</td><td>2015.0</td></tr><tr><th>15</th><td>AD</td><td>Andorra</td><td>70473.0</td><td>2015.0</td></tr><tr><th>16</th><td>DM</td><td>Dominica</td><td>72680.0</td><td>2015.0</td></tr><tr><th>17</th><td>IM</td><td>Isle of Man</td><td>87780.0</td><td>2015.0</td></tr><tr><th>18</th><td>AG</td><td>Antigua and Barbuda</td><td>91818.0</td><td>2015.0</td></tr><tr><th>19</th><td>SC</td><td>Seychelles</td><td>92900.0</td><td>2015.0</td></tr><tr><th>20</th><td>VI</td><td>Virgin Islands (U.S.)</td><td>103574.0</td><td>2015.0</td></tr><tr><th>21</th><td>AW</td><td>Aruba</td><td>103889.0</td><td>2015.0</td></tr><tr><th>22</th><td>FM</td><td>Micronesia, Fed. Sts.</td><td>104460.0</td><td>2015.0</td></tr><tr><th>23</th><td>TO</td><td>Tonga</td><td>106170.0</td><td>2015.0</td></tr><tr><th>24</th><td>GD</td><td>Grenada</td><td>106825.0</td><td>2015.0</td></tr><tr><th>25</th><td>VC</td><td>St. Vincent and the Grenadines</td><td>109462.0</td><td>2015.0</td></tr><tr><th>26</th><td>KI</td><td>Kiribati</td><td>112423.0</td><td>2015.0</td></tr><tr><th>27</th><td>GU</td><td>Guam</td><td>169885.0</td><td>2015.0</td></tr><tr><th>28</th><td>LC</td><td>St. Lucia</td><td>184999.0</td><td>2015.0</td></tr><tr><th>29</th><td>ST</td><td>Sao Tome and Principe</td><td>190344.0</td><td>2015.0</td></tr><tr><th>30</th><td>WS</td><td>Samoa</td><td>193228.0</td><td>2015.0</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></table>



Just one more little detail. This last query has given us a dataframe with the smallest cities in the world. We want to revert the order of the sorting. This time I'll use the `sort!()` function, to save the ordered dataframe into the `df` variable.


```julia
sort!(df, cols=[:SP_POP_TOTL], rev=true)
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>year</th></tr><tr><th>1</th><td>CN</td><td>China</td><td>1.37122e9</td><td>2015.0</td></tr><tr><th>2</th><td>IN</td><td>India</td><td>1.311050527e9</td><td>2015.0</td></tr><tr><th>3</th><td>US</td><td>United States</td><td>3.2141882e8</td><td>2015.0</td></tr><tr><th>4</th><td>ID</td><td>Indonesia</td><td>2.57563815e8</td><td>2015.0</td></tr><tr><th>5</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>2015.0</td></tr><tr><th>6</th><td>PK</td><td>Pakistan</td><td>1.88924874e8</td><td>2015.0</td></tr><tr><th>7</th><td>NG</td><td>Nigeria</td><td>1.82201962e8</td><td>2015.0</td></tr><tr><th>8</th><td>BD</td><td>Bangladesh</td><td>1.60995642e8</td><td>2015.0</td></tr><tr><th>9</th><td>RU</td><td>Russian Federation</td><td>1.44096812e8</td><td>2015.0</td></tr><tr><th>10</th><td>MX</td><td>Mexico</td><td>1.27017224e8</td><td>2015.0</td></tr><tr><th>11</th><td>JP</td><td>Japan</td><td>1.26958472e8</td><td>2015.0</td></tr><tr><th>12</th><td>PH</td><td>Philippines</td><td>1.00699395e8</td><td>2015.0</td></tr><tr><th>13</th><td>ET</td><td>Ethiopia</td><td>9.939075e7</td><td>2015.0</td></tr><tr><th>14</th><td>VN</td><td>Vietnam</td><td>9.17038e7</td><td>2015.0</td></tr><tr><th>15</th><td>EG</td><td>Egypt, Arab Rep.</td><td>9.1508084e7</td><td>2015.0</td></tr><tr><th>16</th><td>DE</td><td>Germany</td><td>8.1413145e7</td><td>2015.0</td></tr><tr><th>17</th><td>IR</td><td>Iran, Islamic Rep.</td><td>7.9109272e7</td><td>2015.0</td></tr><tr><th>18</th><td>TR</td><td>Turkey</td><td>7.866583e7</td><td>2015.0</td></tr><tr><th>19</th><td>CD</td><td>Congo, Dem. Rep.</td><td>7.7266814e7</td><td>2015.0</td></tr><tr><th>20</th><td>TH</td><td>Thailand</td><td>6.7959359e7</td><td>2015.0</td></tr><tr><th>21</th><td>FR</td><td>France</td><td>6.6808385e7</td><td>2015.0</td></tr><tr><th>22</th><td>GB</td><td>United Kingdom</td><td>6.5138232e7</td><td>2015.0</td></tr><tr><th>23</th><td>IT</td><td>Italy</td><td>6.0802085e7</td><td>2015.0</td></tr><tr><th>24</th><td>ZA</td><td>South Africa</td><td>5.495692e7</td><td>2015.0</td></tr><tr><th>25</th><td>MM</td><td>Myanmar</td><td>5.3897154e7</td><td>2015.0</td></tr><tr><th>26</th><td>TZ</td><td>Tanzania</td><td>5.347042e7</td><td>2015.0</td></tr><tr><th>27</th><td>KR</td><td>Korea, Rep.</td><td>5.0617045e7</td><td>2015.0</td></tr><tr><th>28</th><td>CO</td><td>Colombia</td><td>4.8228704e7</td><td>2015.0</td></tr><tr><th>29</th><td>ES</td><td>Spain</td><td>4.6418269e7</td><td>2015.0</td></tr><tr><th>30</th><td>KE</td><td>Kenya</td><td>4.6050302e7</td><td>2015.0</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></table>



Ready! now our `df` variable is in order. Let's try to visualize it again.


```julia
bar(df[:iso2c][1:50], df[:SP_POP_TOTL][1:50],
    size=(1000,400),
    label="Population Total")
```




<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA+gAAAGQCAYAAAA9TUphAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xt4VPW5/v87gApoqyhY8RCiQgAFJRO9EM9VC9XaYMWaolAg1kItKFZB3fZbwGovoVZtRav9yaniTkVRpNZTt91F8QCaQaw2Qa0cbD2UKGIhWBXm9wc7U5DAZ2Wtlaw1z+f9ui6v3T0zzDz3HQg8M5nPFOVyuZwAAAAAAECi2iQ9AAAAAAAAYEEHAAAAACAV2iU9QKGrr6/XE088oZKSEnXo0CHpcQAAAAAABWDTpk1atWqVBg0apM6dO0tiQY/siSee0LBhw5IeAwAAAABQgObOnasLL7xQEgt6ZCUlJVv/xwlVUs9Twt/RByulhydr7ty56t27dyyztZbx48fr1ltvTXqMVKMjN8sdkc1vdBSM1Z6s5pJsZ4sTPblZ7ohsfnN1VFtbq2HDhv1npxQLemT5H2vveYp03NDwd7R6mfTwZPXu3VuZTCae4VrJPvvsU3AztzY6crPcEdn8RkfBWO3Jai7JdrY40ZOb5Y7I5regHW37VmkOiUNkn376adIjpB4duVnuiGx+o6NgrPZkNZdkO1uc6MnNckdk81uYjngFHZG9/PLLSY+QenTkZrkjsvmNjoKx2pPVXJLtbHGiJzfLHb388stas2aN6uvrkx4ldi+++KKy2WzSY6TaFzvq3LmziouLd/lrWNARWc+ePZMeIfXoyM1yR2TzGx0FY7Unq7kk29niRE9uljvq1q2bevfurYaGhqRHaRHl5eVJj5B623bUsWNH1dbW7nJJZ0FHZGPGjEl6hNSjIzfLHZHNb3QUjNWerOaSbGeLEz25We5o8ODBWrp0aUEeBI14NR4IV19fv8sFvSiXy+VacS5zstns1mdFquZEPyTuhv6qqanhsAUAAADAgMZdgX/jo6nfC01dxiFxAAAAAACkAAs6IpsxY0bSI6QeHblZ7ohsfqOjYKz2ZDWXZDtbnOjJzXJHCxYsSHoEFBgWdETG6Y1udORmuSOy+Y2OgrHak9Vcku1scaInN8sd1dXVJT1Ck0pKStS7d2+VlZWpT58+uuOOO1rssebMmaNvfetbztstX75c991333aXZTIZbdy4MZY57rrrLpWVlamsrEz77befDj74YJWVlSmTyWjRokU7/XW5XE5TpkzR559/HuhxTjrpJD366KOh5+Q96BHxHnQAAAAATdnZe9Avfvpzvbouvsfp00n6/04Ofv73oYceqoULF6pv375as2aNjjrqKC1evFh9+vSJb6j/M2fOHD388MN68MEHd3m72bNn6+GHH9ZDDz0U+wxfNGrUKJWVlenSSy913vbzzz/X7rvvrg0bNqhjx47O25900km65pprdNZZZ213Oe9BBwAAAIAUenWd9MI/c7H9F2bZb3ydtri4WD179tTrr78uSfr5z3+uPn366Oijj9bw4cP1r3/9S5I0ZcoUnXfeeTr99NPVu3dvDR48WOvWrctf96Mf/Sh/37fffruqqqp2eMz3339fp512mo499lj17ds3vyCvXbtWkyZN0p///GdlMhldcsklkqQ2bdro448/liS99NJLOuGEE3T00UfruOOO03PPPSdJWr16tTp16qTJkyfrmGOOUWlpqR5//PFm9/HGG2/ojDPO0NFHH61MJqNHHnlEkvSDH/xARUVFOv7445XJZLRu3TrNnTtX/fv3V3l5uTKZjB577LFmP97OsKADAAAAgKf+8pe/aMWKFTr66KP12GOPafbs2Xr++ee1fPlydezYUVdffXX+tosXL9bvfvc71dbW6uCDD9Y111zTrMfaZ5999Mgjj+jFF1/U8uXLtXLlSs2bN09dunTRddddp69+9avKZrP5H7kvKiqSJH322WcaMmSIpkyZouXLl+sXv/iFhgwZkv98+fXr16tfv3566aWXdNttt2n8+PHN7mHo0KEaNmyYli9frurqao0cOVLvvPOO7rzzTuVyOT3//PPKZrPq1KmTzjrrLC1ZskQ1NTWaP3++qqqqtHnz5mY/ZlNY0AEAAADAM5WVlcpkMvrBD36gWbNm6fDDD9dTTz2lyspKfelLX5K09dXjP/7xj/lf841vfENdunSRJH3/+9/X//zP/zTrMbds2aKJEyeqX79+KisrU01NjV5++eWd3r7xVf4VK1aobdu2OuOMMyRJJ5xwgg444ID8r+3QoYPOOeccSdKAAQP01ltvNWuujz76SK+99ppGjhwpSerZs6eOO+44LV68eIdZJOlvf/ubvv71r6tv374699xztW7dOq1evbpZj7kzwd+ogFZRW1sb+T46d+6s4uLiGKYJpqKiQgsXLmy1xytEdORm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85d169ZNa9askSStWbNG3bp1y19XUlLS6te999572rJlyw7X7bXXXtp77731zjvv6O2331bXrl3Vps1/ohcXF2vNmjXOjGjalClTkh4h9ejIzXJHZPMbHQVjtSeruSTb2eJET26WOyKb38J05M0hcV/8aQAAAAAAANIk8IK+7777ql27dvrnP/+Zv2zVqlX5o+O7deum1atXN3ldcXFxi1y3atWq/HUrV67MvzL+xes2bNigjz/+WAceeKAOOeQQvfvuu9qyZUv++sZX3F0ZC9Ftt92mCRMmbHdZQ0ODKioqtHjx4u0ur66u1qhRo3a4j8rKSi1YsGC7y5588klVVFTscNsf/vCHmjFjxnaXZbNZVVRUqL6+frvLJ02atMP7MtasWaOKigrV1dWRgxzkIAc5yEEOcpCDHOQgh4kc1dXVqqio0IABA3TAAQeooqJC48eP3+HXFOV28dLyoYceqocfflhHHXWUJKmqqkrdunXTpEmT9OKLL+rcc8/VqlWr1LZtW02ZMkWrV6/WzJkztXLlSg0YMEB//etfte+++2rOnDmaO3eunnjiCX300UfKZDL6wx/+oCOPPFKLFi3S2LFjtXTpUrVp00YnnniipkyZorPOOksrV67USSedpGw2qy5duuicc87RoEGDdMkll2jDhg3q3r27nn76aZWWlmrcuHHq0KGDpk2bplwup9LSUt1999065ZRTdNNNN2np0qWaN2+eJOm0007TiBEjNGLECD3wwAOaNm2ali5d6szYlGw2q/LycqlqjnTc0J1V6fZCtTRzhHTtEqlbWfj7Wb1MuqG/ampqlMlkwt9PM9TX16tz586t8liFio7cLHdENr/RUTBWe7KaS7KdLU705Ga5I7L5zdVR4y657e7W5CvoY8aM0SGHHKJ//OMfGjRokEpLSyVJN954o5577jmVlpaqqqpK9957b35xnTBhghoaGtS9e3edeeaZuv3227XvvvtKkoYPH65evXqpR48e6t+/v6688kodeeSRkqRTTjlFlZWV6tOnj4488kgNGjRIZ511lqStTxBMmTJFxx9/vEpLS/WVr3xFo0ePlrT1feV33323Bg8erNLSUv3jH//Q//t//0+SVFRUpLlz5+rSSy9Vr1699Oijj+qWW27J57vzzjt11113qWfPnpo2bZpmzZqVv25XGdG0qqqqpEdIPTpys9wR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f/pT0iMnYldf68bvA43d9e3bV3fffXfSI7eqpn4fZTIZDR06VJMmTcpf39jRPvvso7POOivpsZtlZ98HHnzwQR1zzDHKZDLq3bu3zjjjjKRHbbYNGzboS1/60nb/ltn293W/fv100kknafny5QlOmazm/P3mM9fvpcY/O4888kiCUzZPU/9eafw3c01NzXbf3zKZjA477DC1a9dO7733XkITB1dSUqIjjjhCW7ZsyV927LHH6umnn9aUKVO0//7757+3Dx06VOvXr09w2uQ0fr0l6d///rfOOeccVVZW6sILL9TBBx+sTCajI444QmPGjNHmzZt3fWc5xOa73/1urqKiIrd+/fr8ZQ888EDurbfeyvP/HfwAAAqUSURBVO255565gw46KFdbW5vL5XK5DRs25Nq0aZPUqKEdeuihueXLl+dGjhyZ++Uvf5m//OWXX8717Nkzd8sttyQ4XbJKSkpyr7zySv7//8Y3vpG74447cn/+859zZWVl+cs3bNiQu/jii3OZTCa3ZcuWJEZN1LY9rV69OrfPPvvkXnnllVynTp12uG2bNm22+/OUZl/8+je68MILc9/61re2y/HUU0/l5s2b15rjxWLVqlU7fJ2+eNkjjzyS69y5c2uPlgq7+lp/8fvA3//+99wee+yR27BhQxKjJqqp30df9NJLL+U6d+6ce/XVV1tpqng09X3g3XffzXXu3Dn39ttv5y9btmxZa48W2d13352rqKjIdenSJbdx48ZcLpfb4ff19OnTc+Xl5UmNmLjm/P3msyC/lwpNU/9eKSkpyS1fvnyH23766ae5448/Pjdp0qRWmi6akpKS3GGHHZa766678pcde+yxuUWLFuUmT56cu/zyy3O5XC63ZcuW3Lnnnpu78sorkxo1UY1f748//jj31a9+NTdmzJhcLpfbbmf697//nevfv39u+vTpu7yvwnsJN6X+9re/af78+Zo9e7a+/OUv5y8fMmSI2rRpo912203XXHONrr766gSnjC63kyMLjj76aP3yl7/UjTfe2MoTpUtjP5988okaGhqafNZ8zz331B133KH6+no9/vjjrT1iKjT2VFxcrNLSUj355JO7vF2h+OK8b7zxhh5++GHNmjVru+8Lp512mr797W+39nit4vTTT9cHH3yg+vr6pEdpVW+++Wazvtbr16/XXnvtpd122601xywIa9eu1ZAhQ3T77bcX5OGsX/w+8P7776tdu3baZ5998pf169evtceKbMaMGbr88st12mmn6b777mvyNqeffrrq6iJ+tnCBC/r3m8+C/F4qNM3598qll16qTp06afLkyS03UMwmT56sn/70p/rkk08kNZ23qKhIZ5xxhlasWNHa46VGfX29Tj/9dA0YMEC//vWvd7h+99131ymnnOLsiAU9JtlsVj169NjpjzEVFRVpzJgxevXVV/X888+38nSto3///lq7dq13/zDfVmVlpcrKytS1a1e1bdtW559/fpO3a9euncrKyvTaa6+18oTp8pe//EUrVqzQOeeco48//ni7H20rKytTUVFR0iM2S2Vl5XYZnn/+eXXv3l1777130qO1mvvvv1/FxcXq3Llz0qO0qmXLljm/1nV1dfkfAywvL9eNN96o3XffvRWnTL/NmzfrO9/5js4///ydfv9Muy9+HygtLdUJJ5ygbt266dxzz9VNN92kd955J+kxm6W2tlbvvvuuTj31VI0YMUIzZsxo8nb333+/MplMK0+XTtv+/Yb/2NXvpcbvkY1/dgrtSfogZs6cqaeeekr//d//nfQozXL00UfrtNNO0y233LLT22zatEkLFixQeXl5K06WLpWVlfra176mG264ocnr161bp8cff9zZEZ+D3oratm2rn/70p7rqqqv02GOPmfvGYy1PGPPmzVPfvn21ZcsWff/739fEiRP1zW9+s8nb+txXZWWl2rdvrz333FOzZs1Su3bt9OUvf1nZbHa72xXaOQ2NX/9G999//3bXv/XWWxoyZIg2bdqkE044Yaf/yC00jU+ufPDBB1q7dq2eeuqppEdK3Be/1t/97nfVq1ev/O/xd955R8cff7yOOeaYgnw1taVMmDBBRUVFmjp1atKjhPbF7wOS9MADD+j111/XokWL9Oijj+pnP/uZXnrpJR122GEJTdk8M2bM0PDhwyVJAwcO1Pe+9738K0CNS9W7776rTz/9VC+++GKSoyauqb/f8B+7+r207ffIQrOzFxS2vfzFF1/UVVddpUWLFm33k1aF4rrrrlP//v01evTo7S6fO3euFi1aJEk65ZRTCv6nhaM4++yz9cADD+gHP/iBDj744Pzl06ZN0+zZs9WmTRudf/75GjFixC7vp7D+9ZtimUxGb7zxhtatW7fL2w0dOlQbN27Uww8/XHCvDko7/wYkSUuXLtX+++/v3Stn22pcutu0aaMhQ4boiSeeaPJ2n332mV5++WX16dOnNcdLjXnz5mnZsmVavHixvvWtb+30doX2Z+SLT7qUlZXpzTffzB+Ycthhh2nZsmW65pprnN8rCknjkyurV6/Wf/3Xf+nKK69MeqRW19yv9YEHHqj+/fvzZMY2qqur9dBDD2nevHkF92d/Wzt78rW0tFQXX3yxHnroIfXv318LFy5s5cnC+fzzz3XPPfdo1qxZOuyww9S9e3c1NDTkn2BsXKr+/ve/67zzztO1116b8MTJCvr3m49cv5cKWZcuXfTBBx9sd1l9fb32339/SdI///lPnXfeefr1r3+tI444IokRI+vWrZsuuOACXX/99dt9jx42bJhqampUU1Ojm2++WXvssUeCUybr8ssv15gxY3Tqqafq73//e/7yiRMnKpvN6qWXXgr0PZIFPSaHH364hgwZoosuumi70wsffPBBbdmyZbu/sG+88Ub9+Mc/TmLMyLbNse3/fuWVV3T55Zd7/azZF/3pT39Sz549JW3f1caNGzVu3Dh16dJFgwYNSmq8RDX1D9iglxWS7t27a/DgwTt8X9i4cWOCU0Xj+jr9+Mc/1meffaZZs2a15liJC/K13ran9evXq6amJv89wjdf/H30yiuvaNy4cXrwwQe17777JjRVy3jnnXf03HPP5f//devWaeXKlTr88MMTnCq4hx9+WIcffrjefvttvfXWW1q5cqWef/55/fa3v9Vnn32W/1q2bdtWt956q5599tn8q2k+svh3WVyC/l4qRIMGDdJdd92V//9/+9vf6vDDD9dXvvIVbd68WZWVlfrOd76j8847L8Epo7v22ms1d+7cgnubTmu6/PLLNW7cOJ166qlas2ZNqPvg525iNHPmTP30pz9V//79tdtuu2nLli06+eSTdfjhh2/3TNPXvvY1HXbYYaG/aEnaNsdNN92kOXPmaOPGjfrKV76ia6+9VhdeeGGC0yWrqKhIlZWV6tChgz777DOVlJTozjvv1JtvvqnXX39dmUxGn376qaSt38ifeuqpgn6VKKwgPwbmum0abfv1z+VyKioq0i233KLZs2fr+uuvz39f6NSpk7p06aKrrroq6ZFDCfJ1uummmzRs2DBdcMEFXj2Tvquv9SeffJL/PpDL5fTpp5/qu9/9rs4+++ykx07EF3/PXHXVVdq8ebMuuuii/GW5XE4HHXRQQX3UUlPfBy6//HLde++9WrVqlTp27KjPP/9co0aN2unbn9Jm5syZGjZs2HaX9erVSwcffLA2bNiw3deyQ4cOuv766zVhwgQtXbq0tUdN3M7+zvrXv/6l4uJiSVt/XxcXF+vZZ59tzdFSoTm/lwrNLbfcovHjx+voo49W27ZtdcABB+Tf5vbAAw/o6aef1ocffqgnn3xSRUVF+e8Pd999d+rPbdj267Lffvvp0ksv1aRJkxKcKJ227emyyy5T27Ztdeqpp+qUU05p/n3lCvnpqv+/XTsgAQAAYBDWv/VryNlaCAIAAMAJizsAAAAECHQAAAAIEOgAAAAQINABAAAgQKADAABAwAA4rD1e1H8oKwAAAABJRU5ErkJggg==" />



There it is! Clean and tidy. In fact, let's only use these 50 cities.


```julia
biggest = df[1:50,:]
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>year</th></tr><tr><th>1</th><td>CN</td><td>China</td><td>1.37122e9</td><td>2015.0</td></tr><tr><th>2</th><td>IN</td><td>India</td><td>1.311050527e9</td><td>2015.0</td></tr><tr><th>3</th><td>US</td><td>United States</td><td>3.2141882e8</td><td>2015.0</td></tr><tr><th>4</th><td>ID</td><td>Indonesia</td><td>2.57563815e8</td><td>2015.0</td></tr><tr><th>5</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>2015.0</td></tr><tr><th>6</th><td>PK</td><td>Pakistan</td><td>1.88924874e8</td><td>2015.0</td></tr><tr><th>7</th><td>NG</td><td>Nigeria</td><td>1.82201962e8</td><td>2015.0</td></tr><tr><th>8</th><td>BD</td><td>Bangladesh</td><td>1.60995642e8</td><td>2015.0</td></tr><tr><th>9</th><td>RU</td><td>Russian Federation</td><td>1.44096812e8</td><td>2015.0</td></tr><tr><th>10</th><td>MX</td><td>Mexico</td><td>1.27017224e8</td><td>2015.0</td></tr><tr><th>11</th><td>JP</td><td>Japan</td><td>1.26958472e8</td><td>2015.0</td></tr><tr><th>12</th><td>PH</td><td>Philippines</td><td>1.00699395e8</td><td>2015.0</td></tr><tr><th>13</th><td>ET</td><td>Ethiopia</td><td>9.939075e7</td><td>2015.0</td></tr><tr><th>14</th><td>VN</td><td>Vietnam</td><td>9.17038e7</td><td>2015.0</td></tr><tr><th>15</th><td>EG</td><td>Egypt, Arab Rep.</td><td>9.1508084e7</td><td>2015.0</td></tr><tr><th>16</th><td>DE</td><td>Germany</td><td>8.1413145e7</td><td>2015.0</td></tr><tr><th>17</th><td>IR</td><td>Iran, Islamic Rep.</td><td>7.9109272e7</td><td>2015.0</td></tr><tr><th>18</th><td>TR</td><td>Turkey</td><td>7.866583e7</td><td>2015.0</td></tr><tr><th>19</th><td>CD</td><td>Congo, Dem. Rep.</td><td>7.7266814e7</td><td>2015.0</td></tr><tr><th>20</th><td>TH</td><td>Thailand</td><td>6.7959359e7</td><td>2015.0</td></tr><tr><th>21</th><td>FR</td><td>France</td><td>6.6808385e7</td><td>2015.0</td></tr><tr><th>22</th><td>GB</td><td>United Kingdom</td><td>6.5138232e7</td><td>2015.0</td></tr><tr><th>23</th><td>IT</td><td>Italy</td><td>6.0802085e7</td><td>2015.0</td></tr><tr><th>24</th><td>ZA</td><td>South Africa</td><td>5.495692e7</td><td>2015.0</td></tr><tr><th>25</th><td>MM</td><td>Myanmar</td><td>5.3897154e7</td><td>2015.0</td></tr><tr><th>26</th><td>TZ</td><td>Tanzania</td><td>5.347042e7</td><td>2015.0</td></tr><tr><th>27</th><td>KR</td><td>Korea, Rep.</td><td>5.0617045e7</td><td>2015.0</td></tr><tr><th>28</th><td>CO</td><td>Colombia</td><td>4.8228704e7</td><td>2015.0</td></tr><tr><th>29</th><td>ES</td><td>Spain</td><td>4.6418269e7</td><td>2015.0</td></tr><tr><th>30</th><td>KE</td><td>Kenya</td><td>4.6050302e7</td><td>2015.0</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></table>



Next we want to add another indicator: Female population percentage. This indicator has the code: 'SP.POP.TOTL.FE.ZS', and it represents the percentage of the total population that are registered as female.


```julia
df1 = wdi("SP.POP.TOTL.FE.ZS", countries, 2015)
println(size(df1))
println(size(df))
```

    (191,4)
    (208,4)


As you can see, the size of the two data frames we have right now are not the same. This is because some information is missing from the female percentage indicator. Not all indicators can be accurately measured in all countries. therefore, once in a while we can find missing values in them.

A workaround for this is to create a new dataframe with the countries we DO have the information for.


```julia
df = DataFrame(iso2c=[],country=[],SP_POP_TOTL=[],SP_POP_TOTL_FE_ZS=[])
for country in biggest[:iso2c]
    push!(df, @data([country,biggest[biggest[:iso2c].==country,:][:country][1],
                    biggest[biggest[:iso2c].==country,:][:SP_POP_TOTL][1],
                    df1[df1[:iso2c].==country,:][:SP_POP_TOTL_FE_ZS][1]]))
end
df[1:5,:]
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>SP_POP_TOTL</th><th>SP_POP_TOTL_FE_ZS</th></tr><tr><th>1</th><td>CN</td><td>China</td><td>1.37122e9</td><td>48.4773329025405</td></tr><tr><th>2</th><td>IN</td><td>India</td><td>1.311050527e9</td><td>48.1676415969283</td></tr><tr><th>3</th><td>US</td><td>United States</td><td>3.2141882e8</td><td>50.4329265563715</td></tr><tr><th>4</th><td>ID</td><td>Indonesia</td><td>2.57563815e8</td><td>49.648253579409</td></tr><tr><th>5</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>50.828985562917</td></tr></table>



See, now we have a dataframe with no missing values. Still, percentage of female population is actually a variable that depends on the total population. Let's create a new dataframe with absolute values.


```julia
population = DataFrame(iso2c=df[:,1],
    country=df[:,2],
    total=df[:,3],
    females=df[:,3].*(df[:,4]./100),
    males=df[:,3].*(df[:,4].+(-100))./-100)
population[1:5,:]
```




<table class="data-frame"><tr><th></th><th>iso2c</th><th>country</th><th>total</th><th>females</th><th>males</th></tr><tr><th>1</th><td>CN</td><td>China</td><td>1.37122e9</td><td>6.64730884226216e8</td><td>7.064891157737842e8</td></tr><tr><th>2</th><td>IN</td><td>India</td><td>1.311050527e9</td><td>6.315021189999998e8</td><td>6.795484080000004e8</td></tr><tr><th>3</th><td>US</td><td>United States</td><td>3.2141882e8</td><td>1.6210091742895588e8</td><td>1.593179025710441e8</td></tr><tr><th>4</th><td>ID</td><td>Indonesia</td><td>2.57563815e8</td><td>1.2787593599999988e8</td><td>1.2968787900000012e8</td></tr><tr><th>5</th><td>BR</td><td>Brazil</td><td>2.07847528e8</td><td>1.0564678999999987e8</td><td>1.0220073800000013e8</td></tr></table>



Of course, this is now an approximation, but it will work for our visualization. Lastly, to plot these three variables we need to set the bounds to plot. This is done with the `minimum()` and `maximum()` functions.


```julia
minimum(population[:total])
```




    2.5155317e7



Lastly, let's create a visualization to describe all information we have acquired. Since there are three variables we have the option of plotting 3D points in space, but It will look clearer if we use the total population as color or size of a scatterplot. I like to use `gr` backend for my plots, but this code will work with almost all of Plots.jl backends.


```julia
gr()                                                                   # GR backend
plt = scatter(population[:,end],population[:,end-1],                   # Ploting male vs female
xlim=(minimum(population[:total])/2,maximum(population[:total])/1.07), # Limits for the X axis
ylim=(minimum(population[:total])/2,maximum(population[:total])/1.25), # Limits for the Y axis
size=(1000,1000), left_margin=[50px 0px],label="",                     # Window Size, lateral margins and label
ylabel="Female population",xlabel="Male Papulation",                   # X and Y labels
xscale=:log10, yscale=:log10, bottom_margin=50px,                      # Logarithmic scale and bottom margin
markersize=population[:,end-2]./minimum(population[:total]),           # The size of the marker is given by the total population
zcolor=map(log,convert(Array,population[:,end-2]./minimum(population[:total]))), # The color is given by the logarithm of the total population
grid=false)                                                            # NoGrid Science is art ;)

# Last a line is added to mark weather a coutry hase more male or female population
plot!(plt,x->x,minimum(population[:total])/2,maximum(population[:total])/2,label="", color=:green)
```




<?xml version="1.0" encoding="utf-8"?>
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="1000" height="1000" viewBox="0 0 1000 1000">
<defs>
  <clipPath id="clip00">
    <rect x="0" y="0" width="1000" height="1000"/>
  </clipPath>
</defs>
<polygon clip-path="url(#clip00)" points="
0,1000 1000,1000 1000,0 0,0
  " fill="#ffffff" fill-opacity="1"/>
<defs>
  <clipPath id="clip01">
    <rect x="200" y="100" width="701" height="701"/>
  </clipPath>
</defs>
<polygon clip-path="url(#clip00)" points="
96.7738,915.737 996.063,915.737 996.063,3.93701 96.7738,3.93701
  " fill="#ffffff" fill-opacity="1"/>
<defs>
  <clipPath id="clip02">
    <rect x="96" y="3" width="800" height="912"/>
  </clipPath>
</defs>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,915.737 896.063,915.737
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,3.93701 896.063,3.93701
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  256.144,915.737 256.144,902.06
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  256.144,3.93701 256.144,17.614
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  455.158,915.737 455.158,902.06
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  455.158,3.93701 455.158,17.614
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  654.172,915.737 654.172,902.06
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  654.172,3.93701 654.172,17.614
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  853.186,915.737 853.186,902.06
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  853.186,3.93701 853.186,17.614
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,915.737 96.7738,3.93701
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  896.063,915.737 896.063,3.93701
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,727.607 108.763,727.607
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  896.063,727.607 884.074,727.607
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,492.679 108.763,492.679
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  896.063,492.679 884.074,492.679
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,257.752 108.763,257.752
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  896.063,257.752 884.074,257.752
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,22.8238 108.763,22.8238
  "/>
<polyline clip-path="url(#clip02)" style="stroke:#00002d; stroke-width:2; stroke-opacity:1; fill:none" points="
  896.063,22.8238 884.074,22.8238
  "/>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 242.862, 941.489)" x="242.862" y="941.489">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 256.041, 934.636)" x="256.041" y="934.636">7.5</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 441.876, 941.489)" x="441.876" y="941.489">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 455.055, 934.636)" x="455.055" y="934.636">8.0</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 640.89, 941.489)" x="640.89" y="941.489">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 654.069, 934.636)" x="654.069" y="934.636">8.5</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 839.904, 941.489)" x="839.904" y="941.489">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 853.083, 934.636)" x="853.083" y="934.636">9.0</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 60.2094, 733.539)" x="60.2094" y="733.539">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 73.3887, 726.686)" x="73.3887" y="726.686">7.5</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 60.2094, 498.611)" x="60.2094" y="498.611">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 73.3887, 491.759)" x="73.3887" y="491.759">8.0</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 60.2094, 263.683)" x="60.2094" y="263.683">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 73.3887, 256.831)" x="73.3887" y="256.831">8.5</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 60.2094, 28.7557)" x="60.2094" y="28.7557">10</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:10; text-anchor:start;" transform="rotate(0, 73.3887, 21.9031)" x="73.3887" y="21.9031">9.0</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:16; text-anchor:middle;" transform="rotate(0, 496.418, 997.6)" x="496.418" y="997.6">Male Papulation</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:16; text-anchor:middle;" transform="rotate(-90, 14.4, 459.837)" x="14.4" y="459.837">Female population</text>
</g>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="793.126" cy="106.155" r="99"/>
<circle clip-path="url(#clip02)" style="fill:#fcfea4; stroke:none; fill-opacity:1" cx="793.126" cy="106.155" r="98"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="786.405" cy="116.619" r="95"/>
<circle clip-path="url(#clip02)" style="fill:#f8fa98; stroke:none; fill-opacity:1" cx="786.405" cy="116.619" r="93"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="535.665" cy="394.11" r="24"/>
<circle clip-path="url(#clip02)" style="fill:#e55c2f; stroke:none; fill-opacity:1" cx="535.665" cy="394.11" r="22"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="500.095" cy="442.504" r="20"/>
<circle clip-path="url(#clip02)" style="fill:#d64a3f; stroke:none; fill-opacity:1" cx="500.095" cy="442.504" r="18"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="458.921" cy="481.47" r="16"/>
<circle clip-path="url(#clip02)" style="fill:#c53d4d; stroke:none; fill-opacity:1" cx="458.921" cy="481.47" r="14"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="449.986" cy="509.977" r="15"/>
<circle clip-path="url(#clip02)" style="fill:#bd3853; stroke:none; fill-opacity:1" cx="449.986" cy="509.977" r="13"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="442.221" cy="515.514" r="14"/>
<circle clip-path="url(#clip02)" style="fill:#b83555; stroke:none; fill-opacity:1" cx="442.221" cy="515.514" r="13"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="419.323" cy="538.932" r="13"/>
<circle clip-path="url(#clip02)" style="fill:#ac2f5c; stroke:none; fill-opacity:1" cx="419.323" cy="538.932" r="11"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="385.78" cy="545.6" r="12"/>
<circle clip-path="url(#clip02)" style="fill:#a12b61; stroke:none; fill-opacity:1" cx="385.78" cy="545.6" r="10"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="375.787" cy="584.271" r="10"/>
<circle clip-path="url(#clip02)" style="fill:#952666; stroke:none; fill-opacity:1" cx="375.787" cy="584.271" r="9"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="371.814" cy="579.916" r="10"/>
<circle clip-path="url(#clip02)" style="fill:#952666; stroke:none; fill-opacity:1" cx="371.814" cy="579.916" r="9"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="338.126" cy="634.582" r="9"/>
<circle clip-path="url(#clip02)" style="fill:#7d1d6c; stroke:none; fill-opacity:1" cx="338.126" cy="634.582" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="333.978" cy="635.007" r="8"/>
<circle clip-path="url(#clip02)" style="fill:#7d1d6c; stroke:none; fill-opacity:1" cx="333.978" cy="635.007" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="318.512" cy="649.623" r="8"/>
<circle clip-path="url(#clip02)" style="fill:#731a6d; stroke:none; fill-opacity:1" cx="318.512" cy="649.623" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="321.828" cy="654.409" r="8"/>
<circle clip-path="url(#clip02)" style="fill:#731a6d; stroke:none; fill-opacity:1" cx="321.828" cy="654.409" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="296.805" cy="672.612" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#68166e; stroke:none; fill-opacity:1" cx="296.805" cy="672.612" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="296.053" cy="683.391" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#64156e; stroke:none; fill-opacity:1" cx="296.053" cy="683.391" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="290.942" cy="679.698" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#64156e; stroke:none; fill-opacity:1" cx="290.942" cy="679.698" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="290.309" cy="686.218" r="7"/>
<circle clip-path="url(#clip02)" style="fill:#63146e; stroke:none; fill-opacity:1" cx="290.309" cy="686.218" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="266.086" cy="710.047" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#550f6d; stroke:none; fill-opacity:1" cx="266.086" cy="710.047" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="260.96" cy="711.07" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#540e6d; stroke:none; fill-opacity:1" cx="260.96" cy="711.07" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="258.77" cy="718.714" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#520e6c; stroke:none; fill-opacity:1" cx="258.77" cy="718.714" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="244.472" cy="730.065" r="6"/>
<circle clip-path="url(#clip02)" style="fill:#4a0c6a; stroke:none; fill-opacity:1" cx="244.472" cy="730.065" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="228.996" cy="752.944" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#400a66; stroke:none; fill-opacity:1" cx="228.996" cy="752.944" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="224.514" cy="755.651" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#3e0a65; stroke:none; fill-opacity:1" cx="224.514" cy="755.651" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="226.078" cy="760.642" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#3c0964; stroke:none; fill-opacity:1" cx="226.078" cy="760.642" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="216.596" cy="771.83" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#370961; stroke:none; fill-opacity:1" cx="216.596" cy="771.83" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="206.608" cy="779.806" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#32095d; stroke:none; fill-opacity:1" cx="206.608" cy="779.806" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="199.364" cy="786.895" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#2c0a57; stroke:none; fill-opacity:1" cx="199.364" cy="786.895" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="201.235" cy="792.279" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#2c0a57; stroke:none; fill-opacity:1" cx="201.235" cy="792.279" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="184.829" cy="781.646" r="5"/>
<circle clip-path="url(#clip02)" style="fill:#290b54; stroke:none; fill-opacity:1" cx="184.829" cy="781.646" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="187.385" cy="800.056" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#250b50; stroke:none; fill-opacity:1" cx="187.385" cy="800.056" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="178.643" cy="820.708" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#1d0b44; stroke:none; fill-opacity:1" cx="178.643" cy="820.708" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="176.582" cy="824.086" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#1b0b42; stroke:none; fill-opacity:1" cx="176.582" cy="824.086" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="172.636" cy="825.997" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#1a0b3f; stroke:none; fill-opacity:1" cx="172.636" cy="825.997" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="162.324" cy="824.988" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#170b3a; stroke:none; fill-opacity:1" cx="162.324" cy="824.988" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="162.882" cy="842.747" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#140a36; stroke:none; fill-opacity:1" cx="162.882" cy="842.747" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="156.635" cy="841.81" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#130a34; stroke:none; fill-opacity:1" cx="156.635" cy="841.81" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="148.746" cy="849.649" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#10092d; stroke:none; fill-opacity:1" cx="148.746" cy="849.649" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="146.539" cy="869.804" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#0b0724; stroke:none; fill-opacity:1" cx="146.539" cy="869.804" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="157.153" cy="898.229" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#090620; stroke:none; fill-opacity:1" cx="157.153" cy="898.229" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="134.808" cy="870.444" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#090620; stroke:none; fill-opacity:1" cx="134.808" cy="870.444" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="131.666" cy="867.796" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#090620; stroke:none; fill-opacity:1" cx="131.666" cy="867.796" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="132.745" cy="871.521" r="4"/>
<circle clip-path="url(#clip02)" style="fill:#090620; stroke:none; fill-opacity:1" cx="132.745" cy="871.521" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="134.567" cy="884.202" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#07051b; stroke:none; fill-opacity:1" cx="134.567" cy="884.202" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="113.012" cy="883.958" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#030312; stroke:none; fill-opacity:1" cx="113.012" cy="883.958" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="111.122" cy="889.383" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#030211; stroke:none; fill-opacity:1" cx="111.122" cy="889.383" r="2"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="110.732" cy="897.189" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#02010d; stroke:none; fill-opacity:1" cx="110.732" cy="897.189" r="1"/>
<circle clip-path="url(#clip02)" style="fill:#00002d; stroke:none; fill-opacity:1" cx="109.688" cy="904.666" r="3"/>
<circle clip-path="url(#clip02)" style="fill:#02010b; stroke:none; fill-opacity:1" cx="109.688" cy="904.666" r="1"/>
<defs>
  <clipPath id="clip03">
    <rect x="916" y="3" width="31" height="912"/>
  </clipPath>
</defs>
<g clip-path="url(#clip03)">
<image width="30" height="911" xlink:href="data:;base64,
iVBORw0KGgoAAAANSUhEUgAAAB4AAAOPCAYAAADc4nHZAAACRElEQVR4nO3cQVFFMRBFwUBFAA6Q
gH81WMABKDgL/ibzKn0MdFUWc3d5+/z6/l0Hej+BgsFgMPhf7fVxBr7vqcFgMPh5sJEAg8Hg+bBb
DQaDweDMSIDBYDA4MxJgMBg8H3arwWAwGJwZCTAYDAZnRgIMBoPnw241GAwGgzMjAQaDweDMSIDB
YPB8eK/1cwS+76nBYDD4ebCRAIPBYHBmJMBgMHg+7FaDwWAwODMSYDAYDM6MBBgMBs+H3WowGAwG
Z0YCDAaDwZmRAIPB4PmwWw0Gg8HgzEiAwWAwODMSYDAYPB/eh75gu/CpwWAw+HmwkQCDweD5sFsN
BoPB4MxIgMFgMDgzEmAwGDwfdqvBYDAYnBkJMBgMBmdGAgwGg+fDbjUYDAaDMyMBBoPB4MxIgMFg
8HzYrQaDwWBwtg99wXbhU4PBYPDzYCMBBoPB82G3GgwGg8GZkQCDwWBwZiTAYDB4PuxWg8FgMDgz
EmAwGAzOjAQYDAbPh91qMBgMBmdGAgwGg8GZkQCDweD5sFsNBoPB4Gyvdeb7t/ueGgwGg1/OrQaD
wWBwZiTAYDAYnBkJMBgMng+71WAwGAzOjAQYDAaDMyMBBoPB82G3GgwGg8GZkQCDwWBwZiTAYDB4
PuxWg8FgMDgzEmAwGAzO9qG/3y58ajAYDH45txoMBoPBmZEAg8FgcGYkwGAweD7sVoPBYDA4MxJg
MBgMzowEGAwGz4fdajAYDAZnRgIMBoPBmZEAg8Hg+bBbDQaDweDMSIDBYPB8+A+xny3IgoRyfQAA
AABJRU5ErkJggg==
" transform="translate(916, 3)"/>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 919.15)" x="947.914" y="919.15">0</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 457.165)" x="947.914" y="457.165">0.1</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 326.614)" x="947.914" y="326.614">0.2</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 247.64)" x="947.914" y="247.64">0.3</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 190.844)" x="947.914" y="190.844">0.4</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 146.464)" x="947.914" y="146.464">0.5</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 110.033)" x="947.914" y="110.033">0.6</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 79.1311)" x="947.914" y="79.1311">0.7</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 52.2994)" x="947.914" y="52.2994">0.8</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 28.5894)" x="947.914" y="28.5894">0.9</text>
</g>
<g clip-path="url(#clip00)">
<text style="fill:#00002d; fill-opacity:1; font-family:Arial,Helvetica Neue,Helvetica,sans-serif; font-size:12; text-anchor:start;" transform="rotate(0, 947.914, 7.34981)" x="947.914" y="7.34981">1.0</text>
</g>
<polyline clip-path="url(#clip02)" style="stroke:#008100; stroke-width:2; stroke-opacity:1; fill:none" points="
  96.7738,915.737 171.469,827.562 223.456,766.194 263.37,719.078 295.774,680.826 323.052,648.625 346.607,620.82 367.333,596.353 385.839,574.508 402.553,554.778
  417.793,536.788 431.797,520.256 444.751,504.964 456.802,490.738 468.068,477.44 478.643,464.956 488.609,453.192 498.032,442.069 506.967,431.521 515.463,421.492
  523.561,411.932 531.297,402.801 538.701,394.061 545.801,385.679 552.621,377.629 559.182,369.884 565.503,362.422 571.601,355.224 577.491,348.271 583.187,341.547
  588.701,335.037 594.045,328.729 599.229,322.61 604.261,316.669 609.152,310.896 613.907,305.282 618.536,299.819 623.044,294.497 627.437,289.312 631.721,284.254
  635.902,279.319 639.984,274.501 643.971,269.793 647.869,265.192 651.681,260.692 655.411,256.29 659.061,251.98 662.637,247.759 666.14,243.624 669.573,239.572
  672.939,235.598 676.241,231.7 679.482,227.875 682.662,224.12 685.785,220.433 688.853,216.812 691.867,213.254 694.83,209.757 697.743,206.318 700.607,202.937
  703.425,199.611 706.197,196.338 708.926,193.117 711.612,189.946 714.257,186.823 716.863,183.748 719.429,180.718 721.958,177.733 724.451,174.79 726.908,171.89
  729.331,169.03 731.72,166.209 734.077,163.427 736.402,160.683 738.696,157.974 740.96,155.302 743.195,152.664 745.401,150.059 747.58,147.488 749.731,144.948
  751.856,142.44 753.955,139.962 756.029,137.513 758.079,135.094 760.104,132.703 762.106,130.34 764.085,128.004 766.041,125.695 767.976,123.411 769.889,121.152
  771.782,118.918 773.653,116.709 775.505,114.523 777.337,112.36 779.15,110.22 780.944,108.102 782.72,106.006 784.478,103.931 786.218,101.877 787.94,99.8439

  "/>
</svg>
