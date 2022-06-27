```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
school_data = "Desktop/schools_complete.csv"
student_data= "Desktop/students_complete.csv"

# Read School and Student Data File and store into Pandas Data Frames
school_data = pd.read_csv(school_data)
student_data = pd.read_csv(student_data)

# Combine the data into a single dataset
school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])
school_data_complete.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total schools
Total_schools = len(school_data) #4
Total_schools
```




    15




```python
# Total students
Total_Students = len(student_data) #2
Total_Students
```




    39170




```python
# Total budget
Total_budget = school_data["budget"].sum()
Total_budget 
```




    24649428




```python
# Average math score
average_math_score = student_data[("math_score")].mean()
average_math_score 
```




    78.98537145774827




```python
# Average reading score
average_reading_score = student_data[("reading_score")].mean()
average_reading_score
```




    81.87784018381414




```python
# % passing math (the percentage of students who passed math) over
percentage_passed_math =(school_data_complete["math_score"] >=70).sum() / school_data_complete["math_score"].count()* 100
percentage_passed_math
```




    74.9808526933878




```python
# % passing reading (the percentage of students who passed reading over 70%
percentage_passed_reading = (school_data_complete["reading_score"]>=70).sum() / school_data_complete["reading_score"].count()* 100
percentage_passed_reading
```




    85.80546336482001




```python
# % overall passing (the percentage of students who passed math and reading)
overall_passing=((average_math_score + average_reading_score) /2)
overall_passing
```




    80.43160582078121




```python
# Dataframe
dataframe = pd.DataFrame({"Total Schools":[Total_schools], 
                          "Total Students":[Total_Students], 
                          "Total Budget":[Total_budget],
                          "Average Math Score":[average_math_score], 
                          "Average Reading Score":[average_reading_score],
                          "Percentage Passing Math":[percentage_passed_math],
                          "Percentage Passing Reading":[percentage_passed_reading],
                          "Percentage Overall Passing Rate":[overall_passing]})
dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Percentage Passing Math</th>
      <th>Percentage Passing Reading</th>
      <th>Percentage Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.431606</td>
    </tr>
  </tbody>
</table>
</div>




```python
# School count 
school_count= len(school_data_complete["school_name"].unique())
school_count
```




    15




```python
#Setting the school Name & type col as index 1st (Heading)
school_types=school_data.set_index(["school_name"])["type"]

```


```python
#Total Students in each school
student_per_school = school_data_complete["school_name"].value_counts()
student_per_school.head()
```




    Bailey High School       4976
    Johnson High School      4761
    Hernandez High School    4635
    Rodriguez High School    3999
    Figueroa High School     2949
    Name: school_name, dtype: int64




```python
#Total School Budget
school_budget = school_data_complete.groupby(["school_name"])["budget"].mean()
school_budget.head()
```




    school_name
    Bailey High School      3124928.0
    Cabrera High School     1081356.0
    Figueroa High School    1884411.0
    Ford High School        1763916.0
    Griffin High School      917500.0
    Name: budget, dtype: float64




```python
# Student Per Budget
per_student_budget = school_budget/student_per_school
per_student_budget
```




    Bailey High School       628.0
    Cabrera High School      582.0
    Figueroa High School     639.0
    Ford High School         644.0
    Griffin High School      625.0
    Hernandez High School    652.0
    Holden High School       581.0
    Huang High School        655.0
    Johnson High School      650.0
    Pena High School         609.0
    Rodriguez High School    637.0
    Shelton High School      600.0
    Thomas High School       638.0
    Wilson High School       578.0
    Wright High School       583.0
    dtype: float64




```python
#The Average Math Score per school
average_math_per_School = school_data_complete.groupby(["school_name"])["math_score"].mean()
average_math_per_School.head()
```




    school_name
    Bailey High School      77.048432
    Cabrera High School     83.061895
    Figueroa High School    76.711767
    Ford High School        77.102592
    Griffin High School     83.351499
    Name: math_score, dtype: float64




```python
#The Average Reading Score per school
average_reading_per_School= school_data_complete.groupby(["school_name"])["reading_score"].mean()
average_reading_per_School.head()
```




    school_name
    Bailey High School      81.033963
    Cabrera High School     83.975780
    Figueroa High School    81.158020
    Ford High School        80.746258
    Griffin High School     83.816757
    Name: reading_score, dtype: float64




```python
# Passing Math score per school over 70%
passing_math_score = school_data_complete.loc[school_data_complete["math_score"]>=70]
passing_math_score

#Sorting out the maths score by school
by_maths_Per_School= passing_math_score["school_name"].value_counts()
by_maths_Per_School.head()

# Calcuting the final masths percentage result
percent_result_math = by_reading_Per_School/student_per_school*100
percent_result_math
```




    Bailey High School       81.933280
    Cabrera High School      97.039828
    Figueroa High School     80.739234
    Ford High School         79.299014
    Griffin High School      97.138965
    Hernandez High School    80.862999
    Holden High School       96.252927
    Huang High School        81.316421
    Johnson High School      81.222432
    Pena High School         95.945946
    Rodriguez High School    80.220055
    Shelton High School      95.854628
    Thomas High School       97.308869
    Wilson High School       96.539641
    Wright High School       96.611111
    Name: school_name, dtype: float64




```python
# % Passing Reading score per school over 70%
passing_reading_score = school_data_complete.loc[school_data_complete["reading_score"]>=70]

#assign the reading scoor by school
by_reading_Per_School = passing_reading_score["school_name"].value_counts()
by_reading_Per_School.head()

# Calculting the percentage reading result
percent_result_reading = by_reading_Per_School/student_per_school*100
percent_result_reading
```




    Bailey High School       81.933280
    Cabrera High School      97.039828
    Figueroa High School     80.739234
    Ford High School         79.299014
    Griffin High School      97.138965
    Hernandez High School    80.862999
    Holden High School       96.252927
    Huang High School        81.316421
    Johnson High School      81.222432
    Pena High School         95.945946
    Rodriguez High School    80.220055
    Shelton High School      95.854628
    Thomas High School       97.308869
    Wilson High School       96.539641
    Wright High School       96.611111
    Name: school_name, dtype: float64




```python
# % Overall Passing Rate (Average of the above two)
overall = percent_result_math + percent_result_reading/student_per_school
overall
```




    Bailey High School       81.949745
    Cabrera High School      97.092056
    Figueroa High School     80.766612
    Ford High School         79.327966
    Griffin High School      97.205136
    Hernandez High School    80.880445
    Holden High School       96.478344
    Huang High School        81.344298
    Johnson High School      81.239492
    Pena High School         96.045682
    Rodriguez High School    80.240115
    Shelton High School      95.909060
    Thomas High School       97.368385
    Wilson High School       96.581927
    Wright High School       96.664784
    Name: school_name, dtype: float64




```python
# New school summeary dataframe
new_school_summery_df = pd.DataFrame({"School Type":school_types, 
                                  "Total Students":student_per_school, 
                                  "Total School Budget":school_budget,
                                  "Per Student Budget":per_student_budget,
                                  "Average Math Score" :average_math_per_School,
                                  "Average Reading Score":average_reading_per_School,
                                  "% Passing Math":percent_result_math, 
                                   "% Passing Reading":percent_result_reading,
                                  "% Overall Passing Rate":overall})
new_school_summery_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928.0</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356.0</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411.0</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916.0</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500.0</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sorting Out table By Passing Rate
Top_School_summary_table_df = new_school_summery_df.sort_values(["% Passing Math","% Passing Reading","% Overall Passing Rate" ], 
                                        ascending=False)
Top_School_summary_table_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130.0</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>97.308869</td>
      <td>97.308869</td>
      <td>97.368385</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500.0</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356.0</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400.0</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>96.611111</td>
      <td>96.611111</td>
      <td>96.664784</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574.0</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>96.539641</td>
      <td>96.539641</td>
      <td>96.581927</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Formating the Top Performing Schools tabel
Top_School_summary_table_df["Total School Budget"]=Top_School_summary_table_df["Total School Budget"].map("${:,.2f}".format)
Top_School_summary_table_df["Per Student Budget"]=Top_School_summary_table_df["Per Student Budget"].map("${:,.2f}".format)

Top_School_summary_table_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>$638.00</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>97.308869</td>
      <td>97.308869</td>
      <td>97.368385</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>96.611111</td>
      <td>96.611111</td>
      <td>96.664784</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>96.539641</td>
      <td>96.539641</td>
      <td>96.581927</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>96.252927</td>
      <td>96.252927</td>
      <td>96.478344</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>95.945946</td>
      <td>95.945946</td>
      <td>96.045682</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>95.854628</td>
      <td>95.854628</td>
      <td>95.909060</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>$628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>81.316421</td>
      <td>81.316421</td>
      <td>81.344298</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>81.222432</td>
      <td>81.222432</td>
      <td>81.239492</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>80.862999</td>
      <td>80.862999</td>
      <td>80.880445</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>80.220055</td>
      <td>80.220055</td>
      <td>80.240115</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sorting out the scoroing by the lowet school results 
Lowest_School_results_df=new_school_summery_df.sort_values("% Overall Passing Rate")
Lowest_School_results_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916.0</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363.0</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>80.220055</td>
      <td>80.220055</td>
      <td>80.240115</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411.0</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020.0</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>80.862999</td>
      <td>80.862999</td>
      <td>80.880445</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650.0</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>81.222432</td>
      <td>81.222432</td>
      <td>81.239492</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formating the lowest shcool data results table 
Lowest_School_results_df.style.format({"Total School Budget":"${:,.2f}","Per Student Budget":"${:,.2f}"})
```




<style type="text/css">
</style>
<table id="T_a30af_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >School Type</th>
      <th class="col_heading level0 col1" >Total Students</th>
      <th class="col_heading level0 col2" >Total School Budget</th>
      <th class="col_heading level0 col3" >Per Student Budget</th>
      <th class="col_heading level0 col4" >Average Math Score</th>
      <th class="col_heading level0 col5" >Average Reading Score</th>
      <th class="col_heading level0 col6" >% Passing Math</th>
      <th class="col_heading level0 col7" >% Passing Reading</th>
      <th class="col_heading level0 col8" >% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_a30af_level0_row0" class="row_heading level0 row0" >Ford High School</th>
      <td id="T_a30af_row0_col0" class="data row0 col0" >District</td>
      <td id="T_a30af_row0_col1" class="data row0 col1" >2739</td>
      <td id="T_a30af_row0_col2" class="data row0 col2" >$1,763,916.00</td>
      <td id="T_a30af_row0_col3" class="data row0 col3" >$644.00</td>
      <td id="T_a30af_row0_col4" class="data row0 col4" >77.102592</td>
      <td id="T_a30af_row0_col5" class="data row0 col5" >80.746258</td>
      <td id="T_a30af_row0_col6" class="data row0 col6" >79.299014</td>
      <td id="T_a30af_row0_col7" class="data row0 col7" >79.299014</td>
      <td id="T_a30af_row0_col8" class="data row0 col8" >79.327966</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row1" class="row_heading level0 row1" >Rodriguez High School</th>
      <td id="T_a30af_row1_col0" class="data row1 col0" >District</td>
      <td id="T_a30af_row1_col1" class="data row1 col1" >3999</td>
      <td id="T_a30af_row1_col2" class="data row1 col2" >$2,547,363.00</td>
      <td id="T_a30af_row1_col3" class="data row1 col3" >$637.00</td>
      <td id="T_a30af_row1_col4" class="data row1 col4" >76.842711</td>
      <td id="T_a30af_row1_col5" class="data row1 col5" >80.744686</td>
      <td id="T_a30af_row1_col6" class="data row1 col6" >80.220055</td>
      <td id="T_a30af_row1_col7" class="data row1 col7" >80.220055</td>
      <td id="T_a30af_row1_col8" class="data row1 col8" >80.240115</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row2" class="row_heading level0 row2" >Figueroa High School</th>
      <td id="T_a30af_row2_col0" class="data row2 col0" >District</td>
      <td id="T_a30af_row2_col1" class="data row2 col1" >2949</td>
      <td id="T_a30af_row2_col2" class="data row2 col2" >$1,884,411.00</td>
      <td id="T_a30af_row2_col3" class="data row2 col3" >$639.00</td>
      <td id="T_a30af_row2_col4" class="data row2 col4" >76.711767</td>
      <td id="T_a30af_row2_col5" class="data row2 col5" >81.158020</td>
      <td id="T_a30af_row2_col6" class="data row2 col6" >80.739234</td>
      <td id="T_a30af_row2_col7" class="data row2 col7" >80.739234</td>
      <td id="T_a30af_row2_col8" class="data row2 col8" >80.766612</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row3" class="row_heading level0 row3" >Hernandez High School</th>
      <td id="T_a30af_row3_col0" class="data row3 col0" >District</td>
      <td id="T_a30af_row3_col1" class="data row3 col1" >4635</td>
      <td id="T_a30af_row3_col2" class="data row3 col2" >$3,022,020.00</td>
      <td id="T_a30af_row3_col3" class="data row3 col3" >$652.00</td>
      <td id="T_a30af_row3_col4" class="data row3 col4" >77.289752</td>
      <td id="T_a30af_row3_col5" class="data row3 col5" >80.934412</td>
      <td id="T_a30af_row3_col6" class="data row3 col6" >80.862999</td>
      <td id="T_a30af_row3_col7" class="data row3 col7" >80.862999</td>
      <td id="T_a30af_row3_col8" class="data row3 col8" >80.880445</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row4" class="row_heading level0 row4" >Johnson High School</th>
      <td id="T_a30af_row4_col0" class="data row4 col0" >District</td>
      <td id="T_a30af_row4_col1" class="data row4 col1" >4761</td>
      <td id="T_a30af_row4_col2" class="data row4 col2" >$3,094,650.00</td>
      <td id="T_a30af_row4_col3" class="data row4 col3" >$650.00</td>
      <td id="T_a30af_row4_col4" class="data row4 col4" >77.072464</td>
      <td id="T_a30af_row4_col5" class="data row4 col5" >80.966394</td>
      <td id="T_a30af_row4_col6" class="data row4 col6" >81.222432</td>
      <td id="T_a30af_row4_col7" class="data row4 col7" >81.222432</td>
      <td id="T_a30af_row4_col8" class="data row4 col8" >81.239492</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row5" class="row_heading level0 row5" >Huang High School</th>
      <td id="T_a30af_row5_col0" class="data row5 col0" >District</td>
      <td id="T_a30af_row5_col1" class="data row5 col1" >2917</td>
      <td id="T_a30af_row5_col2" class="data row5 col2" >$1,910,635.00</td>
      <td id="T_a30af_row5_col3" class="data row5 col3" >$655.00</td>
      <td id="T_a30af_row5_col4" class="data row5 col4" >76.629414</td>
      <td id="T_a30af_row5_col5" class="data row5 col5" >81.182722</td>
      <td id="T_a30af_row5_col6" class="data row5 col6" >81.316421</td>
      <td id="T_a30af_row5_col7" class="data row5 col7" >81.316421</td>
      <td id="T_a30af_row5_col8" class="data row5 col8" >81.344298</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row6" class="row_heading level0 row6" >Bailey High School</th>
      <td id="T_a30af_row6_col0" class="data row6 col0" >District</td>
      <td id="T_a30af_row6_col1" class="data row6 col1" >4976</td>
      <td id="T_a30af_row6_col2" class="data row6 col2" >$3,124,928.00</td>
      <td id="T_a30af_row6_col3" class="data row6 col3" >$628.00</td>
      <td id="T_a30af_row6_col4" class="data row6 col4" >77.048432</td>
      <td id="T_a30af_row6_col5" class="data row6 col5" >81.033963</td>
      <td id="T_a30af_row6_col6" class="data row6 col6" >81.933280</td>
      <td id="T_a30af_row6_col7" class="data row6 col7" >81.933280</td>
      <td id="T_a30af_row6_col8" class="data row6 col8" >81.949745</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row7" class="row_heading level0 row7" >Shelton High School</th>
      <td id="T_a30af_row7_col0" class="data row7 col0" >Charter</td>
      <td id="T_a30af_row7_col1" class="data row7 col1" >1761</td>
      <td id="T_a30af_row7_col2" class="data row7 col2" >$1,056,600.00</td>
      <td id="T_a30af_row7_col3" class="data row7 col3" >$600.00</td>
      <td id="T_a30af_row7_col4" class="data row7 col4" >83.359455</td>
      <td id="T_a30af_row7_col5" class="data row7 col5" >83.725724</td>
      <td id="T_a30af_row7_col6" class="data row7 col6" >95.854628</td>
      <td id="T_a30af_row7_col7" class="data row7 col7" >95.854628</td>
      <td id="T_a30af_row7_col8" class="data row7 col8" >95.909060</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row8" class="row_heading level0 row8" >Pena High School</th>
      <td id="T_a30af_row8_col0" class="data row8 col0" >Charter</td>
      <td id="T_a30af_row8_col1" class="data row8 col1" >962</td>
      <td id="T_a30af_row8_col2" class="data row8 col2" >$585,858.00</td>
      <td id="T_a30af_row8_col3" class="data row8 col3" >$609.00</td>
      <td id="T_a30af_row8_col4" class="data row8 col4" >83.839917</td>
      <td id="T_a30af_row8_col5" class="data row8 col5" >84.044699</td>
      <td id="T_a30af_row8_col6" class="data row8 col6" >95.945946</td>
      <td id="T_a30af_row8_col7" class="data row8 col7" >95.945946</td>
      <td id="T_a30af_row8_col8" class="data row8 col8" >96.045682</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row9" class="row_heading level0 row9" >Holden High School</th>
      <td id="T_a30af_row9_col0" class="data row9 col0" >Charter</td>
      <td id="T_a30af_row9_col1" class="data row9 col1" >427</td>
      <td id="T_a30af_row9_col2" class="data row9 col2" >$248,087.00</td>
      <td id="T_a30af_row9_col3" class="data row9 col3" >$581.00</td>
      <td id="T_a30af_row9_col4" class="data row9 col4" >83.803279</td>
      <td id="T_a30af_row9_col5" class="data row9 col5" >83.814988</td>
      <td id="T_a30af_row9_col6" class="data row9 col6" >96.252927</td>
      <td id="T_a30af_row9_col7" class="data row9 col7" >96.252927</td>
      <td id="T_a30af_row9_col8" class="data row9 col8" >96.478344</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row10" class="row_heading level0 row10" >Wilson High School</th>
      <td id="T_a30af_row10_col0" class="data row10 col0" >Charter</td>
      <td id="T_a30af_row10_col1" class="data row10 col1" >2283</td>
      <td id="T_a30af_row10_col2" class="data row10 col2" >$1,319,574.00</td>
      <td id="T_a30af_row10_col3" class="data row10 col3" >$578.00</td>
      <td id="T_a30af_row10_col4" class="data row10 col4" >83.274201</td>
      <td id="T_a30af_row10_col5" class="data row10 col5" >83.989488</td>
      <td id="T_a30af_row10_col6" class="data row10 col6" >96.539641</td>
      <td id="T_a30af_row10_col7" class="data row10 col7" >96.539641</td>
      <td id="T_a30af_row10_col8" class="data row10 col8" >96.581927</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row11" class="row_heading level0 row11" >Wright High School</th>
      <td id="T_a30af_row11_col0" class="data row11 col0" >Charter</td>
      <td id="T_a30af_row11_col1" class="data row11 col1" >1800</td>
      <td id="T_a30af_row11_col2" class="data row11 col2" >$1,049,400.00</td>
      <td id="T_a30af_row11_col3" class="data row11 col3" >$583.00</td>
      <td id="T_a30af_row11_col4" class="data row11 col4" >83.682222</td>
      <td id="T_a30af_row11_col5" class="data row11 col5" >83.955000</td>
      <td id="T_a30af_row11_col6" class="data row11 col6" >96.611111</td>
      <td id="T_a30af_row11_col7" class="data row11 col7" >96.611111</td>
      <td id="T_a30af_row11_col8" class="data row11 col8" >96.664784</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row12" class="row_heading level0 row12" >Cabrera High School</th>
      <td id="T_a30af_row12_col0" class="data row12 col0" >Charter</td>
      <td id="T_a30af_row12_col1" class="data row12 col1" >1858</td>
      <td id="T_a30af_row12_col2" class="data row12 col2" >$1,081,356.00</td>
      <td id="T_a30af_row12_col3" class="data row12 col3" >$582.00</td>
      <td id="T_a30af_row12_col4" class="data row12 col4" >83.061895</td>
      <td id="T_a30af_row12_col5" class="data row12 col5" >83.975780</td>
      <td id="T_a30af_row12_col6" class="data row12 col6" >97.039828</td>
      <td id="T_a30af_row12_col7" class="data row12 col7" >97.039828</td>
      <td id="T_a30af_row12_col8" class="data row12 col8" >97.092056</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row13" class="row_heading level0 row13" >Griffin High School</th>
      <td id="T_a30af_row13_col0" class="data row13 col0" >Charter</td>
      <td id="T_a30af_row13_col1" class="data row13 col1" >1468</td>
      <td id="T_a30af_row13_col2" class="data row13 col2" >$917,500.00</td>
      <td id="T_a30af_row13_col3" class="data row13 col3" >$625.00</td>
      <td id="T_a30af_row13_col4" class="data row13 col4" >83.351499</td>
      <td id="T_a30af_row13_col5" class="data row13 col5" >83.816757</td>
      <td id="T_a30af_row13_col6" class="data row13 col6" >97.138965</td>
      <td id="T_a30af_row13_col7" class="data row13 col7" >97.138965</td>
      <td id="T_a30af_row13_col8" class="data row13 col8" >97.205136</td>
    </tr>
    <tr>
      <th id="T_a30af_level0_row14" class="row_heading level0 row14" >Thomas High School</th>
      <td id="T_a30af_row14_col0" class="data row14 col0" >Charter</td>
      <td id="T_a30af_row14_col1" class="data row14 col1" >1635</td>
      <td id="T_a30af_row14_col2" class="data row14 col2" >$1,043,130.00</td>
      <td id="T_a30af_row14_col3" class="data row14 col3" >$638.00</td>
      <td id="T_a30af_row14_col4" class="data row14 col4" >83.418349</td>
      <td id="T_a30af_row14_col5" class="data row14 col5" >83.848930</td>
      <td id="T_a30af_row14_col6" class="data row14 col6" >97.308869</td>
      <td id="T_a30af_row14_col7" class="data row14 col7" >97.308869</td>
      <td id="T_a30af_row14_col8" class="data row14 col8" >97.368385</td>
    </tr>
  </tbody>
</table>





```python
#Creating  a table showing maths socres by grades 
math_grade_9th=student_data.loc[student_data["grade"] == "9th"].groupby(["school_name"])['math_score'].mean()
math_grade_9th.head()

math_grade_10th=student_data.loc[student_data["grade"] == "10th"].groupby(["school_name"])['math_score'].mean()
math_grade_10th.head()

math_grade_11th=student_data.loc[student_data["grade"] == "11th"].groupby(["school_name"])["math_score"].mean()
math_grade_11th.head()

math_grade_12th=student_data.loc[student_data["grade"] == "12th"].groupby(["school_name"])["math_score"].mean()
math_grade_12th.head()

#Creating the Dataframe table 
maths_score_by_grades=pd.DataFrame({"9th":math_9th, "10th": math_10th, "11th":math_11th, "12th":math_12th })
maths_score_by_grades
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Creating  a table showing reading socres by grades 
reading_grade_9th=student_data.loc[student_data["grade"] == "9th" ].groupby(["school_name"])["reading_score"].mean()
reading_grade_9th.head()

reading_grade_10th=student_data.loc[student_data["grade"] == "10th" ].groupby(["school_name"])["reading_score"].mean()
reading_grade_10th.head()

reading_grade_11th=student_data.loc[student_data["grade"] == "11th" ].groupby(["school_name"])["reading_score"].mean()
reading_grade_11th.head()

reading_grade_12th=student_data.loc[student_data["grade"] == "12th" ].groupby(["school_name"])["reading_score"].mean()
reading_grade_12th.head()

#Creating the Dataframe table 
reading_score_by_grade=pd.DataFrame({"9th":reading_grade_9th,"10th":reading_grade_10th, "11th":reading_grade_11th, "12th":reading_grade_12th })
reading_score_by_grade
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Scores by School Spending
new_school_summery_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928.0</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356.0</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411.0</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916.0</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500.0</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Bins vaules
bins = [0, 585, 630, 645, 680]
group_names = ["<$585", "$585-630", "$630-645", "$645-680"]

new_school_summery_df["Spending Ranges (Per Student)"]=pd.cut(new_school_summery_df["Total School Budget"]/new_school_summery_df["Total Students"]
                                            ,bins , labels=group_names)
new_school_summery_df.head()
scores_by_school_spending = new_school_summery_df .drop(columns=["Total Students", "Total School Budget","School Type", "Per Student Budget"])
scores_by_school_spending

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (Per Student)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>80.862999</td>
      <td>80.862999</td>
      <td>80.880445</td>
      <td>$645-680</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>96.252927</td>
      <td>96.252927</td>
      <td>96.478344</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>81.316421</td>
      <td>81.316421</td>
      <td>81.344298</td>
      <td>$645-680</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>81.222432</td>
      <td>81.222432</td>
      <td>81.239492</td>
      <td>$645-680</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>95.945946</td>
      <td>95.945946</td>
      <td>96.045682</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>80.220055</td>
      <td>80.220055</td>
      <td>80.240115</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>95.854628</td>
      <td>95.854628</td>
      <td>95.909060</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>97.308869</td>
      <td>97.308869</td>
      <td>97.368385</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>96.539641</td>
      <td>96.539641</td>
      <td>96.581927</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>96.611111</td>
      <td>96.611111</td>
      <td>96.664784</td>
      <td>&lt;$585</td>
    </tr>
  </tbody>
</table>
</div>




```python
#creting a table for Scores by School Spending
scores_table_by_spending =scores_by_school_spending.groupby(["Spending Ranges (Per Student)"])
scores_table_by_spending.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>96.610877</td>
      <td>96.610877</td>
      <td>96.704278</td>
    </tr>
    <tr>
      <th>$585-630</th>
      <td>81.899826</td>
      <td>83.155286</td>
      <td>92.718205</td>
      <td>92.718205</td>
      <td>92.777406</td>
    </tr>
    <tr>
      <th>$630-645</th>
      <td>78.518855</td>
      <td>81.624473</td>
      <td>84.391793</td>
      <td>84.391793</td>
      <td>84.425769</td>
    </tr>
    <tr>
      <th>$645-680</th>
      <td>76.997210</td>
      <td>81.027843</td>
      <td>81.133951</td>
      <td>81.133951</td>
      <td>81.154745</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Scores by School Size
new_school_summery_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (Per Student)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928.0</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356.0</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411.0</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916.0</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500.0</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
      <td>$585-630</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Bins Vaules
school_size_bins = [0, 1000, 2000, 5000]
school_group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]
```


```python
type("scores by size school")
```




    str




```python
#cretaing table for school size by score 
scores_by_sch["School Size"]=pd.cut(new_school_summery_df["Total Students"],school_size_bins , labels=school_group_names)
scores_by_sch.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (Per Student)</th>
      <th>School Size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
      <td>$585-630</td>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
      <td>&lt;$585</td>
      <td>Medium (1000-2000)</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
      <td>$630-645</td>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
      <td>$630-645</td>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
      <td>$585-630</td>
      <td>Medium (1000-2000)</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Grouping the results by school sizes 
by_school_Size = scores_by_sch.groupby(["School Size"])
by_school_Size.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.821598</td>
      <td>83.929843</td>
      <td>96.099437</td>
      <td>96.099437</td>
      <td>96.262013</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.374684</td>
      <td>83.864438</td>
      <td>96.790680</td>
      <td>96.790680</td>
      <td>96.847884</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.746417</td>
      <td>81.344493</td>
      <td>82.766634</td>
      <td>82.766634</td>
      <td>82.791325</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Scores by School type
new_school_summery_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (Per Student)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928.0</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356.0</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411.0</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916.0</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500.0</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
      <td>$585-630</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores_by_school_type = new_school_summery_df.drop(columns=["Total Students","Total School Budget", "Per Student Budget"])
scores_by_school_type.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
      <th>Spending Ranges (Per Student)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>81.933280</td>
      <td>81.933280</td>
      <td>81.949745</td>
      <td>$585-630</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>97.039828</td>
      <td>97.039828</td>
      <td>97.092056</td>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>80.739234</td>
      <td>80.739234</td>
      <td>80.766612</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>79.299014</td>
      <td>79.299014</td>
      <td>79.327966</td>
      <td>$630-645</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>97.138965</td>
      <td>97.138965</td>
      <td>97.205136</td>
      <td>$585-630</td>
    </tr>
  </tbody>
</table>
</div>




```python
# grouping the results by School Type
group_by_school_Type = scores_by_type.groupby(["School Type"])
group_by_school_Type.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>96.586489</td>
      <td>96.586489</td>
      <td>96.668172</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>80.799062</td>
      <td>80.799062</td>
      <td>80.821239</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Oberstaion Report 

####
#15 Charter schools has a higher scores than the Distict schools 
# whereas on;y 39,170 student in the 15 schools has a passing rate of 80.821239
```


```python
#print obersation 

file_txt = "15 Charter schools has a higher scores than the Distict schools"
file_txt = " whereas on;y 39,170 student in the 15 schools has a passing rate of 80.821239"
```


```python
print (file_txt)
```

     whereas on;y 39,170 student in the 15 schools has a passing rate of 80.821239



```python

```


```python

```
