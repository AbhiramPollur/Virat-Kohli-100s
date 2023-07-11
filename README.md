# Virat Kohli 100s Analysis(Updated till July 11th 2023)

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

#KING KOHLI

data = pd.read_csv('/Users/mac/Desktop/CSV Files/Virat_Kohli_100s.csv', sep=',')
df = pd.DataFrame(data)
print(data.head(10))

   Number Format  Inning Position  Score  Balls  Strike Rate      Against  \
0       1    ODI       2        4    107    114    93.859649    Sri Lanka   
1       2    ODI       2        3    102     95   107.368421   Bangladesh   
2       3    ODI       2        3    118    121    97.520661    Australia   
3       4    ODI       1        3    105    104   100.961539  New Zealand   
4       5    ODI       1        4    100     83   120.481928   Bangladesh   
5       6    ODI       1        4    107     93   115.053763      England   
6       7    ODI       2        4    112     98   114.285714      England   
7       8    ODI       2        4    117    123    95.121951  West Indies   
8       9   Test       2        6    116    213    54.460094    Australia   
9      10    ODI       2        4    133     86   154.651163    Sri Lanka   

      Venue Host Nation      Series  Year  Team Total  Wickets lost Not Out  \
0   Kolkata       India   Bilateral  2009         316             3      No   
1    Mirpur  Bangladesh  Tri-Series  2010         249             4     Yes   
2     Vizag       India   Bilateral  2010         292             5      No   
3  Guwahati       India   Bilateral  2010         276            10      No   
4    Mirpur  Bangladesh   World Cup  2011         370             4     Yes   
5   Cardiff     England   Bilateral  2011         304             6      No   
6     Delhi       India   Bilateral  2011         238             2     Yes   
7     Vizag       India   Bilateral  2011         270             5      No   
8  Adelaide   Australia   Bilateral  2012         272            10      No   
9    Hobart   Australia  Tri-Series  2012         320             4     Yes   

  MOTM  Win Captain  
0   No  Yes      No  
1  Yes  Yes      No  
2  Yes  Yes      No  
3  Yes  Yes      No  
4   No  Yes      No  
5   No   No      No  
6  Yes  Yes      No  
7  Yes  Yes      No  
8   No   No      No  
9  Yes  Yes      No  

data_columns = data.columns
print(data_columns)

Index(['Number', 'Format', 'Inning', 'Position', 'Score', 'Balls',
       'Strike Rate', 'Against', 'Venue', 'Host Nation', 'Series', 'Year',
       'Team Total', 'Wickets lost', 'Not Out', 'MOTM', 'Win', 'Captain'],
      dtype='object')
      
career_score = data['Score'].sum()
print(career_score)

10691

format_runs = data.groupby(data['Format'])['Score'].sum()
print(format_runs)
format_runs.plot(kind='bar')
plt.show()

Format
ODI     5587
T20      731
T20i     122
Test    4251
Name: Score, dtype: int64

odi_runs = data.groupby(data['Format'] == 'ODI')['Score'].sum()
print(odi_runs) 

Format
False    5104
True     5587
Name: Score, dtype: int64

balls_faced = data['Balls'].sum()
print(balls_faced)

12114

strike_rate = career_score/balls_faced * 100
print(strike_rate)

88.25326069011061

yearly_runs = data.groupby(data['Year'])['Score'].sum()
print(yearly_runs)

Year
2009     107
2010     325
2011     436
2012     980
2013     658
2014    1055
2015     495
2016    1620
2017    1575
2018    1472
2019    1067
2022     235
2023     666
Name: Score, dtype: int64

yearly_runs.plot(kind='line', marker='o')
plt.show()

favourite_venue = data['Venue'].value_counts()
print(favourite_venue)

Venue
Adelaide              5
Bengaluru             5
Kolkata               4
Vizag                 4
Nagpur                4
Mirpur                4
Guwahati              3
Pune                  3
Colombo               3
Port Of Spain         3
Ranchi                2
Centurion             2
Hyderabad             2
Mumbai                2
Rajkot                2
Galle                 2
Melbourne             2
Delhi                 2
Chennai               2
Napier                1
Thiruvananthapuram    1
Chattogram            1
Dubai                 1
Perth                 1
Nottingham            1
Birmingham            1
Cape Town             1
Durban                1
Cardiff               1
Kanpur                1
Kingston              1
Hobart                1
Wellington            1
Hambantota            1
Mohali                1
Indore                1
North Sound           1
Canberra              1
Harare                1
Sydney                1
Jaipur                1
Johannesburg          1
Dharamshala           1
Fatullah              1
Ahmedabad             1
Name: count, dtype: int64

favourite_venue.plot(kind='pie')
#plt.legend()
plt.show()

number_of_centuries = data['Number'].count()
print(number_of_centuries)

82

centuries_count = data['Win'].value_counts()
print(centuries_count)
print('\n\n')

Win
Yes      58
No       16
Drawn     7
Tie       1
Name: count, dtype: int64


centuries_in_lose = data['Win'].value_counts()['No']
print(centuries_in_lose)
century_inloseperc = centuries_in_lose/ number_of_centuries * 100
print(century_inloseperc)

16
19.51219512195122

centuries_in_win = data['Win'].value_counts()['Yes']
print(centuries_in_win)
century_inwinperc = centuries_in_win/ number_of_centuries * 100
print(century_inwinperc)

58
70.73170731707317

centuries_drawn = data['Win'].value_counts()['Drawn']
centuries_tied = data['Win'].value_counts()['Tie']
print(centuries_drawn)
print(centuries_tied)

7
1

centuries_count.plot(kind='pie')
data = data['Win'].str.replace('Yes', 'Win')
plt.legend()
plt.show()

century_win_perc = centuries_in_win/number_of_centuries * 100
print(century_win_perc)

70.73170731707317

century_lose_perc = centuries_in_lose/number_of_centuries * 100
print(century_lose_perc)

19.51219512195122

motm_count = data['MOTM'].value_counts()
print(motm_count)

MOTM
Yes    48
No     34
Name: count, dtype: int64

motm_count.plot(kind='pie')
plt.title('MOTM when Century')
plt.show()

notout_count = data['Not Out'].value_counts()
print(notout_count)

Not Out
No     58
Yes    24
Name: count, dtype: int64

notout_count.plot(kind='pie')
plt.title('Not Out after Century')
plt.show()

opposite_teams = data['Against'].value_counts()
print(opposite_teams)

Against
Australia                  16
Sri Lanka                  15
West Indies                11
New Zealand                 8
England                     8
South Africa                7
Bangladesh                  6
Pakistan                    2
Gujarat Lions               2
Zimbabwe                    1
Rising Pune Supergiants     1
Kings XI Punjab             1
Kolkata Knight Riders       1
Afghanistan                 1
Sunrisers Hyderabad         1
Gujarat Titans              1
Name: count, dtype: int64

opposite_teams.plot(kind='pie')
plt.title('Opposition')
plt.show()

ipl_teams = ['Gujarat Lions', 'Sunrisers Hyderabad', 'Gujarat Titans', 'Kolkata Knight Riders', 'Kings XI Punjab', 'Rising Pune Supergiants']
for team in ipl_teams:
    if team in opposite_teams:
        print('yes')
    else:
        print('no')
yes
yes
yes
yes
yes
yes

strike_aus = data.groupby((data['Against'] == 'Australia'))['Strike Rate'].mean()
print(strike_aus)

Against
False    106.680459
True      92.047697
Name: Strike Rate, dtype: float64

for opp in data['Against'].unique():
    strike_ = data.groupby((data['Against'] == opp))['Strike Rate'].mean()
    print(opp, strike_)
    
Sri Lanka Against
False    104.028292
True     102.918527
Name: Strike Rate, dtype: float64
Bangladesh Against
False    103.909763
True     102.755251
Name: Strike Rate, dtype: float64
Australia Against
False    106.680459
True      92.047697
Name: Strike Rate, dtype: float64
New Zealand Against
False    105.334811
True      89.862178
Name: Strike Rate, dtype: float64
England Against
False    106.527801
True      78.827020
Name: Strike Rate, dtype: float64
West Indies Against
False    104.267810
True     100.968996
Name: Strike Rate, dtype: float64
Pakistan Against
False    103.813802
True     104.284642
Name: Strike Rate, dtype: float64
Zimbabwe Against
False    103.792494
True     106.481482
Name: Strike Rate, dtype: float64
South Africa Against
False    104.988433
True      91.363002
Name: Strike Rate, dtype: float64
Gujarat Lions Against
False    101.959519
True     178.455988
Name: Strike Rate, dtype: float64
Rising Pune Supergiants Against
False    102.808229
True     186.206897
Name: Strike Rate, dtype: float64
Kings XI Punjab Against
False    102.316956
True     226.000000
Name: Strike Rate, dtype: float64
Kolkata Knight Riders Against
False    102.978514
True     172.413793
Name: Strike Rate, dtype: float64
Afghanistan Against
False    102.637944
True     200.000000
Name: Strike Rate, dtype: float64
Sunrisers Hyderabad Against
False    103.147448
True     158.730159
Name: Strike Rate, dtype: float64
Gujarat Titans Against
False    103.062959
True     165.573770
Name: Strike Rate, dtype: float64

host = data['Host Nation'].value_counts()
print(host)

Host Nation
India           40
Australia       11
Bangladesh       6
Sri Lanka        6
West Indies      5
South Africa     5
New Zealand      4
England          3
Zimbabwe         1
UAE              1
Name: count, dtype: int64

host.plot(kind='pie')
plt.title('Countries where Century')
plt.show()

year = data['Year'].value_counts()
print(year)

Year
2016    11
2017    11
2018    11
2012     8
2014     8
2019     8
2013     6
2023     5
2011     4
2015     4
2010     3
2022     2
2009     1
Name: count, dtype: int64

year.plot(kind='bar')
plt.title('Year of Centuries')
plt.show()

team_total = data['Team Total'].mean()
print(team_total)

335.3170731707317

teamtotal_win = data.groupby(data['Win'])['Team Total'].mean()
print(teamtotal_win)

Win
Drawn    413.000000
No       291.875000
Tie      321.000000
Yes      338.172414
Name: Team Total, dtype: float64

teamtotal_win.plot(kind='bar')
plt.show()

meanscore_opposition = data.groupby(data['Against'])['Team Total'].mean()
print(meanscore_opposition)

Against
Afghanistan                212.000000
Australia                  367.625000
Bangladesh                 390.333333
England                    367.000000
Gujarat Lions              214.000000
Gujarat Titans             197.000000
Kings XI Punjab            211.000000
Kolkata Knight Riders      213.000000
New Zealand                315.750000
Pakistan                   315.000000
Rising Pune Supergiants    195.000000
South Africa               323.714286
Sri Lanka                  352.466667
Sunrisers Hyderabad        187.000000
West Indies                341.272727
Zimbabwe                   230.000000
Name: Team Total, dtype: float64

meanscore_opposition.plot(kind='bar', color='red')
plt.show()

wicketslost = data['Wickets lost'].value_counts()
print(wicketslost)

Wickets lost
10    19
4     13
3      9
6      9
5      8
2      7
7      7
8      5
9      4
1      1
Name: count, dtype: int64

wicketslost.plot(kind='bar', color='red')
plt.xlabel('Wickets Lost')
plt.ylabel('Number of Times')
plt.show()

captain = data['Captain'].value_counts()
print(captain)

Captain
Yes    46
No     36
Name: count, dtype: int64

captain.plot(kind='pie')
plt.legend()
plt.show()

centurycount_performat = data['Format'].value_counts()
print(centurycount_performat)

Format
ODI     46
Test    28
T20      7
T20i     1
Name: count, dtype: int64

centurycount_performat.plot(kind='pie')
plt.show()

series = data['Series'].value_counts()
print(series)

Series
Bilateral     66
IPL            7
Asia Cup       4
Tri-Series     3
World Cup      2
Name: count, dtype: int64
series.plot(kind='pie')
plt.show()

position_of_batting = data['Position'].value_counts()
print(position_of_batting)

Position
3       39
4       31
Open     8
5        3
6        1
Name: count, dtype: int64

position_of_batting.plot(kind='bar')
plt.show()


