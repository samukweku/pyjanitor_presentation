<h1 align='center'>Helping Pandas with Pyjanitor</h1>

<h2>Outline</h2>

- A bit about me
- What is Pyjanitor?
- Why Pyjanitor?
- Examples
- A peek at some functions
- Clarion call


<h2>About Me</h2>

- Core dev on pyjanitor; also a contributor to datatable(python).
- Senior Engineer at Slalom Australia.
- Blogger : https://samukweku.github.io/data-wrangling-blog/.
- Tennis and soccer.


<h2> What is Pyjanitor? </h2>

- Python implementation of R's [janitor](https://garthtarr.github.io/meatR/janitor.html)
- Provides a clean, verb-like API for cleaning data
- Wrapper around Pandas functions
- Focus is on user friendliness and ease of use
- Method-chainable - read like a flow from top to bottom


<h2> Why Pyjanitor? </h2>

- Data is wild and messy
- To get good results for ML or dashboards, clean data is required
- Data cleaning is intensive, repetitive, boring
- Intuitive, easy to remember/understand cleaning options are desirable.
- Document your solution - why not make your code part of the documentation?
- Write helper functions, or use pyjanitor


<h2 align='center'> What is <em>not</em> Messy Data? </h2>

- Every column is a variable
- Every row is an observation
- Every cell is a single value

Messy data is any other arrangement of the data.

[Source](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)


```python
# import libraries
# pip install pyjanitor
import pandas as pd
import janitor
import numpy as np
```


```python
url = "https://github.com/pyjanitor-devs/pyjanitor/blob/dev/examples/notebooks/dirty_data.xlsx?raw=true"

dirty = pd.read_excel(url, engine = 'openpyxl')
dirty
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
      <th>First Name</th>
      <th>Last Name</th>
      <th>Employee Status</th>
      <th>Subject</th>
      <th>Hire Date</th>
      <th>% Allocated</th>
      <th>Full time?</th>
      <th>do not edit! ---&gt;</th>
      <th>Certification</th>
      <th>Certification.1</th>
      <th>Certification.2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>Theater</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>Theater</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Instr. music</td>
      <td>Vocal music</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>Computers</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Science 6-12</td>
      <td>Physics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Science 6-12</td>
      <td>Physics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>English 6-12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Political sci.</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>NaN</td>
      <td>Vocal music</td>
      <td>English</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



<h4> Some observations </h4>

- row 7 is completely empty; same goes for columns do not edit!---> and certification 2
- multiple columns representing the same thing?
- Hire Date is not in date format

<h2 align='center'>Let's clean</h2>


```python
dirty.clean_names()
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>%_allocated</th>
      <th>full_time_</th>
      <th>do_not_edit!_&gt;</th>
      <th>certification</th>
      <th>certification_1</th>
      <th>certification_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>Theater</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>Theater</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Instr. music</td>
      <td>Vocal music</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>Computers</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Science 6-12</td>
      <td>Physics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>Science 6-12</td>
      <td>Physics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>English 6-12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>PENDING</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>Physical ed</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Political sci.</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>NaN</td>
      <td>Vocal music</td>
      <td>English</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
(dirty
 .clean_names()
 .remove_empty()
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>%_allocated</th>
      <th>full_time_</th>
      <th>certification</th>
      <th>certification_1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
      <td>Vocal music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>Computers</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>7</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
      <td>English</td>
    </tr>
  </tbody>
</table>
</div>




```python
(dirty
 .clean_names()
 .remove_empty()
 .rename_column("%_allocated", "percent_allocated")
 .rename_column("full_time_", "full_time")
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>percent_allocated</th>
      <th>full_time</th>
      <th>certification</th>
      <th>certification_1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
      <td>Vocal music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>Computers</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>7</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>NaN</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>NaN</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
      <td>English</td>
    </tr>
  </tbody>
</table>
</div>




```python
(dirty
 .clean_names()
 .remove_empty()
 .rename_column("%_allocated", "percent_allocated")
 .rename_column("full_time_", "full_time")
 .coalesce('certification', 'certification_1')
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>percent_allocated</th>
      <th>full_time</th>
      <th>certification</th>
      <th>certification_1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
      <td>Theater</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
      <td>Vocal music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>Computers</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
      <td>Physics</td>
    </tr>
    <tr>
      <th>7</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>English 6-12</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Political sci.</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
      <td>English</td>
    </tr>
  </tbody>
</table>
</div>




```python
(dirty
 .clean_names()
 .remove_empty()
 .rename_column("%_allocated", "percent_allocated")
 .rename_column("full_time_", "full_time")
 .coalesce('certification', 'certification_1')
 .remove_columns('certification_1')
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>percent_allocated</th>
      <th>full_time</th>
      <th>certification</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>39690.0</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>39690.0</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>37118.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>27515.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>41431.0</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>11037.0</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>7</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>32994.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>27919.0</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>42221.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>34700.0</td>
      <td>NaN</td>
      <td>No</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>40071.0</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
    </tr>
  </tbody>
</table>
</div>




```python
(dirty
 .clean_names()
 .remove_empty()
 .rename_column("%_allocated", "percent_allocated")
 .rename_column("full_time_", "full_time")
 .coalesce('certification', 'certification_1')
 .remove_columns('certification_1')
 .convert_excel_date("hire_date")
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>percent_allocated</th>
      <th>full_time</th>
      <th>certification</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>2008-08-30</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>2008-08-30</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>2001-08-15</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>1975-05-01</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>2013-06-06</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>1930-03-20</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>1930-03-20</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>7</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>1990-05-01</td>
      <td>0.50</td>
      <td>No</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>1976-06-08</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>2015-08-05</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>1995-01-01</td>
      <td>NaN</td>
      <td>No</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>2009-09-15</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
    </tr>
  </tbody>
</table>
</div>




```python
# alternative route
(dirty
 .clean_names()
 .dropna(axis='columns', how='all')
 .dropna(axis='rows', how='all')
 .rename(columns={"%_allocated": "percent_allocated", "full_time_": "full_time"})
 .assign(certification = lambda df: df.certification.combine_first(df.certification_1))
 .drop(columns='certification_1')
 .assign(hire_date = lambda df: pd.to_datetime(df.hire_date, unit='D', origin='1899-12-30')) 
)
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
      <th>first_name</th>
      <th>last_name</th>
      <th>employee_status</th>
      <th>subject</th>
      <th>hire_date</th>
      <th>percent_allocated</th>
      <th>full_time</th>
      <th>certification</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>PE</td>
      <td>2008-08-30</td>
      <td>0.75</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jason</td>
      <td>Bourne</td>
      <td>Teacher</td>
      <td>Drafting</td>
      <td>2008-08-30</td>
      <td>0.25</td>
      <td>Yes</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alicia</td>
      <td>Keys</td>
      <td>Teacher</td>
      <td>Music</td>
      <td>2001-08-15</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>Instr. music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ada</td>
      <td>Lovelace</td>
      <td>Teacher</td>
      <td>NaN</td>
      <td>1975-05-01</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Desus</td>
      <td>Nice</td>
      <td>Administration</td>
      <td>Dean</td>
      <td>2013-06-06</td>
      <td>1.00</td>
      <td>Yes</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Physics</td>
      <td>1930-03-20</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chien-Shiung</td>
      <td>Wu</td>
      <td>Teacher</td>
      <td>Chemistry</td>
      <td>1930-03-20</td>
      <td>0.50</td>
      <td>Yes</td>
      <td>Science 6-12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>James</td>
      <td>Joyce</td>
      <td>Teacher</td>
      <td>English</td>
      <td>1990-05-01</td>
      <td>0.50</td>
      <td>No</td>
      <td>English 6-12</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Hedy</td>
      <td>Lamarr</td>
      <td>Teacher</td>
      <td>Science</td>
      <td>1976-06-08</td>
      <td>0.50</td>
      <td>No</td>
      <td>PENDING</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Carlos</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>Basketball</td>
      <td>2015-08-05</td>
      <td>NaN</td>
      <td>No</td>
      <td>Physical ed</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Young</td>
      <td>Boozer</td>
      <td>Coach</td>
      <td>NaN</td>
      <td>1995-01-01</td>
      <td>NaN</td>
      <td>No</td>
      <td>Political sci.</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Micheal</td>
      <td>Larsen</td>
      <td>Teacher</td>
      <td>English</td>
      <td>2009-09-15</td>
      <td>0.80</td>
      <td>No</td>
      <td>Vocal music</td>
    </tr>
  </tbody>
</table>
</div>



<h2 align='center'>Another Example - Tidy Up Web-Scraped Media Franchise Data</h2>


```python
url = "https://raw.githubusercontent.com/pyjanitor-devs/pyjanitor/dev/examples/data/medium_franchise_raw_table.csv"
df = pd.read_csv(url)
df
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
      <th>Franchise</th>
      <th>Year of inception</th>
      <th>Total revenue (USD)</th>
      <th>Revenue breakdown (est.)</th>
      <th>Original media</th>
      <th>Creator(s)</th>
      <th>Owner(s)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>$19.9 billion[da]</td>
      <td>Book sales – $9.125 billion[245] Box office – ...</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James Bond</td>
      <td>1953</td>
      <td>est. $19.9 billion[db]</td>
      <td>Box office – $7.078 billion[249] Home video sa...</td>
      <td>Novel</td>
      <td>Ian Fleming</td>
      <td>Metro-Goldwyn-Mayer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peanuts</td>
      <td>1950</td>
      <td>est. $19.1 billion</td>
      <td>Retail sales – $18.805 billion[dc] Box office ...</td>
      <td>Comic strip</td>
      <td>Charles M. Schulz</td>
      <td>Sony Music Entertainment Japan (Sony) WildBrai...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Super Sentai (Power Rangers)</td>
      <td>1975</td>
      <td>est. $16.8 billion</td>
      <td>Retail sales – $16.557 billion[de] Licensed me...</td>
      <td>Television series</td>
      <td>Shotaro Ishinomori Haim Saban Shuki Levy</td>
      <td>Toei Company Hasbro Bandai Namco (toys)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neon Genesis Evangelion (Shinseiki Evangelion)</td>
      <td>1994</td>
      <td>est. $16.6 billion</td>
      <td>Pachinko sales – $11.9 billion[bp] Merchandise...</td>
      <td>Anime</td>
      <td>Hideaki Anno Gainax Tatsunoko Production</td>
      <td>Khara[dl][274][275]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KochiKame</td>
      <td>1976</td>
      <td>est. $16.3 billion</td>
      <td>Manga magazine – $15.448 billion[ab] Manga vol...</td>
      <td>Manga</td>
      <td>Osamu Akimoto</td>
      <td>Osamu Akimoto Shueisha (Hitotsubashi Group) (m...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Dora the Explorer</td>
      <td>2000</td>
      <td>est. $15.8 billion</td>
      <td>Retail sales – $15.413 billion[dm] Home video ...</td>
      <td>Animated series</td>
      <td>Chris Gifford Valerie Walsh Eric Weiner</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>7</th>
      <td>The Simpsons</td>
      <td>1987</td>
      <td>est. $15.8 billion</td>
      <td>Merchandise sales – $7.073 billion[do] TV adve...</td>
      <td>Animated series</td>
      <td>Matt Groening</td>
      <td>20th Century Studios (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Lion King</td>
      <td>1994</td>
      <td>est. $15.4 billion</td>
      <td>Musical theatre – $8.252 billion[dq] Merchandi...</td>
      <td>Animated film</td>
      <td>Roger Allers Rob Minkoff</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avengers</td>
      <td>1963</td>
      <td>est. $15.3 billion</td>
      <td>Box office – $7.765 billion[289] Merchandise s...</td>
      <td>Comic book</td>
      <td>Stan Lee Jack Kirby</td>
      <td>Marvel Entertainment (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pac-Man</td>
      <td>1980</td>
      <td>est. $15.1 billion</td>
      <td>Video games – $14.098 billion[c][du] Merchandi...</td>
      <td>Video game</td>
      <td>Toru Iwatani Namco</td>
      <td>Bandai Namco Entertainment (Bandai Namco Holdi...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Looney Tunes</td>
      <td>1930</td>
      <td>est. $15 billion</td>
      <td>Retail sales – $14.477 billion[dw] Box office ...</td>
      <td>Animated cartoon</td>
      <td>Warner Bros.</td>
      <td>Warner Bros. (AT&amp;T)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>SpongeBob SquarePants</td>
      <td>1999</td>
      <td>est. $14.8 billion</td>
      <td>Retail sales – $14.378 billion[dy] Box office ...</td>
      <td>Animated series</td>
      <td>Stephen Hillenburg</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii series</td>
      <td>2006</td>
      <td>est. $14.8 billion</td>
      <td>Video games – $14.808 billion[c]</td>
      <td>Video game</td>
      <td>Nintendo EAD</td>
      <td>Nintendo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Teenage Mutant Ninja Turtles</td>
      <td>1984</td>
      <td>est. $14.6 billion</td>
      <td>Merchandise sales – $13.2 billion[dz] Box offi...</td>
      <td>Comic book</td>
      <td>Kevin Eastman Peter Laird</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sailor Moon</td>
      <td>1991</td>
      <td>est. $14.3 billion</td>
      <td>Merchandise sales – $13 billion[310] Home ente...</td>
      <td>Manga</td>
      <td>Naoko Takeuchi</td>
      <td>Naoko Takeuchi Kodansha (manga)Toei Animation ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Space Invaders</td>
      <td>1978</td>
      <td>est. $13.9 billion</td>
      <td>Video game – $13.93 billion[329][ef] Music sin...</td>
      <td>Video game</td>
      <td>Tomohiro Nishikado</td>
      <td>Taito (Square Enix)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Frozen</td>
      <td>2013</td>
      <td>est. $13.4 billion</td>
      <td>Merchandise sales – $10.588 billion[eh] Box of...</td>
      <td>Animated film</td>
      <td>Chris Buck Jennifer Lee</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Dungeon Fighter Online (DFO)</td>
      <td>2005</td>
      <td>est. $13.4 billion</td>
      <td>Computer game – $13.4 billion[c]</td>
      <td>Video game</td>
      <td>Neople</td>
      <td>Nexon Tencent</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dragon Quest (Dragon Warrior)</td>
      <td>1986</td>
      <td>est. $12.9 billion</td>
      <td>Video games – $6.501 billion[c] Manga magazine...</td>
      <td>Video game</td>
      <td>Yuji Horii Koichi Nakamura Akira Toriyama</td>
      <td>Square Enix Yuji Horii (Armor Project) Akira T...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Street Fighter</td>
      <td>1987</td>
      <td>est. $12.2 billion</td>
      <td>Video games – $12.009 billion[c] Box office &amp; ...</td>
      <td>Video game</td>
      <td>Takashi Nishiyama Hiroshi Matsumoto</td>
      <td>Capcom</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Final Fantasy</td>
      <td>1987</td>
      <td>est. $12.2 billion</td>
      <td>Video games – $10.958 billion[c] Licensed merc...</td>
      <td>Video game</td>
      <td>Hironobu Sakaguchi Hiromichi Tanaka Nasir Gebelli</td>
      <td>Square Enix</td>
    </tr>
    <tr>
      <th>22</th>
      <td>CrossFire</td>
      <td>2007</td>
      <td>est. $12 billion</td>
      <td>Computer game – $12 billion[c]</td>
      <td>Video game</td>
      <td>Smilegate</td>
      <td>Smilegate Tencent</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Warcraft</td>
      <td>1994</td>
      <td>est. $11.7 billion</td>
      <td>Video games – $11.227 billion[c] Box office – ...</td>
      <td>Video game</td>
      <td>Allen Adham Frank Pearce Michael Morhaime</td>
      <td>Blizzard Entertainment (Activision Blizzard)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ultra Series (Ultraman)</td>
      <td>1966</td>
      <td>est. $11.7 billion</td>
      <td>Merchandise sales – $10.406 billion[es] Pachin...</td>
      <td>Television series</td>
      <td>Eiji Tsuburaya</td>
      <td>Tsuburaya Productions (Bandai Namco Holdings)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>FIFA</td>
      <td>1993</td>
      <td>est. $11.5 billion</td>
      <td>Video games – $11.479 billion[c]</td>
      <td>Video game</td>
      <td>EA Canada</td>
      <td>Electronic Arts</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Superman</td>
      <td>1938</td>
      <td>est. $11.1 billion</td>
      <td>Retail sales – $6.015 billion[ew] Merchandise ...</td>
      <td>Comic book</td>
      <td>Jerry Siegel Joe Shuster</td>
      <td>DC Entertainment (AT&amp;T)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Star Trek</td>
      <td>1966</td>
      <td>est. $10.8 billion[fd]</td>
      <td>Retail sales – $4.753 billion[fe] TV revenue –...</td>
      <td>Television series</td>
      <td>Gene Roddenberry</td>
      <td>ViacomCBS</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>est. $10.3 billion</td>
      <td>Manga magazine – $6.53 billion[ab] Manga volum...</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>est. $10.1 billion</td>
      <td>Video games – $10.098 billion[c] Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
</div>




```python
# change column names to something more understandable

df.set_axis(('franchise','year_created',
             'total_revenue','revenue_items', 
             'original_media','creators','owners'), 
            axis='columns')
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>$19.9 billion[da]</td>
      <td>Book sales – $9.125 billion[245] Box office – ...</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James Bond</td>
      <td>1953</td>
      <td>est. $19.9 billion[db]</td>
      <td>Box office – $7.078 billion[249] Home video sa...</td>
      <td>Novel</td>
      <td>Ian Fleming</td>
      <td>Metro-Goldwyn-Mayer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peanuts</td>
      <td>1950</td>
      <td>est. $19.1 billion</td>
      <td>Retail sales – $18.805 billion[dc] Box office ...</td>
      <td>Comic strip</td>
      <td>Charles M. Schulz</td>
      <td>Sony Music Entertainment Japan (Sony) WildBrai...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Super Sentai (Power Rangers)</td>
      <td>1975</td>
      <td>est. $16.8 billion</td>
      <td>Retail sales – $16.557 billion[de] Licensed me...</td>
      <td>Television series</td>
      <td>Shotaro Ishinomori Haim Saban Shuki Levy</td>
      <td>Toei Company Hasbro Bandai Namco (toys)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neon Genesis Evangelion (Shinseiki Evangelion)</td>
      <td>1994</td>
      <td>est. $16.6 billion</td>
      <td>Pachinko sales – $11.9 billion[bp] Merchandise...</td>
      <td>Anime</td>
      <td>Hideaki Anno Gainax Tatsunoko Production</td>
      <td>Khara[dl][274][275]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KochiKame</td>
      <td>1976</td>
      <td>est. $16.3 billion</td>
      <td>Manga magazine – $15.448 billion[ab] Manga vol...</td>
      <td>Manga</td>
      <td>Osamu Akimoto</td>
      <td>Osamu Akimoto Shueisha (Hitotsubashi Group) (m...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Dora the Explorer</td>
      <td>2000</td>
      <td>est. $15.8 billion</td>
      <td>Retail sales – $15.413 billion[dm] Home video ...</td>
      <td>Animated series</td>
      <td>Chris Gifford Valerie Walsh Eric Weiner</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>7</th>
      <td>The Simpsons</td>
      <td>1987</td>
      <td>est. $15.8 billion</td>
      <td>Merchandise sales – $7.073 billion[do] TV adve...</td>
      <td>Animated series</td>
      <td>Matt Groening</td>
      <td>20th Century Studios (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Lion King</td>
      <td>1994</td>
      <td>est. $15.4 billion</td>
      <td>Musical theatre – $8.252 billion[dq] Merchandi...</td>
      <td>Animated film</td>
      <td>Roger Allers Rob Minkoff</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avengers</td>
      <td>1963</td>
      <td>est. $15.3 billion</td>
      <td>Box office – $7.765 billion[289] Merchandise s...</td>
      <td>Comic book</td>
      <td>Stan Lee Jack Kirby</td>
      <td>Marvel Entertainment (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pac-Man</td>
      <td>1980</td>
      <td>est. $15.1 billion</td>
      <td>Video games – $14.098 billion[c][du] Merchandi...</td>
      <td>Video game</td>
      <td>Toru Iwatani Namco</td>
      <td>Bandai Namco Entertainment (Bandai Namco Holdi...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Looney Tunes</td>
      <td>1930</td>
      <td>est. $15 billion</td>
      <td>Retail sales – $14.477 billion[dw] Box office ...</td>
      <td>Animated cartoon</td>
      <td>Warner Bros.</td>
      <td>Warner Bros. (AT&amp;T)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>SpongeBob SquarePants</td>
      <td>1999</td>
      <td>est. $14.8 billion</td>
      <td>Retail sales – $14.378 billion[dy] Box office ...</td>
      <td>Animated series</td>
      <td>Stephen Hillenburg</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii series</td>
      <td>2006</td>
      <td>est. $14.8 billion</td>
      <td>Video games – $14.808 billion[c]</td>
      <td>Video game</td>
      <td>Nintendo EAD</td>
      <td>Nintendo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Teenage Mutant Ninja Turtles</td>
      <td>1984</td>
      <td>est. $14.6 billion</td>
      <td>Merchandise sales – $13.2 billion[dz] Box offi...</td>
      <td>Comic book</td>
      <td>Kevin Eastman Peter Laird</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sailor Moon</td>
      <td>1991</td>
      <td>est. $14.3 billion</td>
      <td>Merchandise sales – $13 billion[310] Home ente...</td>
      <td>Manga</td>
      <td>Naoko Takeuchi</td>
      <td>Naoko Takeuchi Kodansha (manga)Toei Animation ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Space Invaders</td>
      <td>1978</td>
      <td>est. $13.9 billion</td>
      <td>Video game – $13.93 billion[329][ef] Music sin...</td>
      <td>Video game</td>
      <td>Tomohiro Nishikado</td>
      <td>Taito (Square Enix)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Frozen</td>
      <td>2013</td>
      <td>est. $13.4 billion</td>
      <td>Merchandise sales – $10.588 billion[eh] Box of...</td>
      <td>Animated film</td>
      <td>Chris Buck Jennifer Lee</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Dungeon Fighter Online (DFO)</td>
      <td>2005</td>
      <td>est. $13.4 billion</td>
      <td>Computer game – $13.4 billion[c]</td>
      <td>Video game</td>
      <td>Neople</td>
      <td>Nexon Tencent</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dragon Quest (Dragon Warrior)</td>
      <td>1986</td>
      <td>est. $12.9 billion</td>
      <td>Video games – $6.501 billion[c] Manga magazine...</td>
      <td>Video game</td>
      <td>Yuji Horii Koichi Nakamura Akira Toriyama</td>
      <td>Square Enix Yuji Horii (Armor Project) Akira T...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Street Fighter</td>
      <td>1987</td>
      <td>est. $12.2 billion</td>
      <td>Video games – $12.009 billion[c] Box office &amp; ...</td>
      <td>Video game</td>
      <td>Takashi Nishiyama Hiroshi Matsumoto</td>
      <td>Capcom</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Final Fantasy</td>
      <td>1987</td>
      <td>est. $12.2 billion</td>
      <td>Video games – $10.958 billion[c] Licensed merc...</td>
      <td>Video game</td>
      <td>Hironobu Sakaguchi Hiromichi Tanaka Nasir Gebelli</td>
      <td>Square Enix</td>
    </tr>
    <tr>
      <th>22</th>
      <td>CrossFire</td>
      <td>2007</td>
      <td>est. $12 billion</td>
      <td>Computer game – $12 billion[c]</td>
      <td>Video game</td>
      <td>Smilegate</td>
      <td>Smilegate Tencent</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Warcraft</td>
      <td>1994</td>
      <td>est. $11.7 billion</td>
      <td>Video games – $11.227 billion[c] Box office – ...</td>
      <td>Video game</td>
      <td>Allen Adham Frank Pearce Michael Morhaime</td>
      <td>Blizzard Entertainment (Activision Blizzard)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ultra Series (Ultraman)</td>
      <td>1966</td>
      <td>est. $11.7 billion</td>
      <td>Merchandise sales – $10.406 billion[es] Pachin...</td>
      <td>Television series</td>
      <td>Eiji Tsuburaya</td>
      <td>Tsuburaya Productions (Bandai Namco Holdings)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>FIFA</td>
      <td>1993</td>
      <td>est. $11.5 billion</td>
      <td>Video games – $11.479 billion[c]</td>
      <td>Video game</td>
      <td>EA Canada</td>
      <td>Electronic Arts</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Superman</td>
      <td>1938</td>
      <td>est. $11.1 billion</td>
      <td>Retail sales – $6.015 billion[ew] Merchandise ...</td>
      <td>Comic book</td>
      <td>Jerry Siegel Joe Shuster</td>
      <td>DC Entertainment (AT&amp;T)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Star Trek</td>
      <td>1966</td>
      <td>est. $10.8 billion[fd]</td>
      <td>Retail sales – $4.753 billion[fe] TV revenue –...</td>
      <td>Television series</td>
      <td>Gene Roddenberry</td>
      <td>ViacomCBS</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>est. $10.3 billion</td>
      <td>Manga magazine – $6.53 billion[ab] Manga volum...</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>est. $10.1 billion</td>
      <td>Video games – $10.098 billion[c] Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9 billion[da]</td>
      <td>Book sales – $9.125 billion[245] Box office – ...</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James Bond</td>
      <td>1953</td>
      <td>19.9 billion[db]</td>
      <td>Box office – $7.078 billion[249] Home video sa...</td>
      <td>Novel</td>
      <td>Ian Fleming</td>
      <td>Metro-Goldwyn-Mayer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peanuts</td>
      <td>1950</td>
      <td>19.1 billion</td>
      <td>Retail sales – $18.805 billion[dc] Box office ...</td>
      <td>Comic strip</td>
      <td>Charles M. Schulz</td>
      <td>Sony Music Entertainment Japan (Sony) WildBrai...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Super Sentai (Power Rangers)</td>
      <td>1975</td>
      <td>16.8 billion</td>
      <td>Retail sales – $16.557 billion[de] Licensed me...</td>
      <td>Television series</td>
      <td>Shotaro Ishinomori Haim Saban Shuki Levy</td>
      <td>Toei Company Hasbro Bandai Namco (toys)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neon Genesis Evangelion (Shinseiki Evangelion)</td>
      <td>1994</td>
      <td>16.6 billion</td>
      <td>Pachinko sales – $11.9 billion[bp] Merchandise...</td>
      <td>Anime</td>
      <td>Hideaki Anno Gainax Tatsunoko Production</td>
      <td>Khara[dl][274][275]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KochiKame</td>
      <td>1976</td>
      <td>16.3 billion</td>
      <td>Manga magazine – $15.448 billion[ab] Manga vol...</td>
      <td>Manga</td>
      <td>Osamu Akimoto</td>
      <td>Osamu Akimoto Shueisha (Hitotsubashi Group) (m...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Dora the Explorer</td>
      <td>2000</td>
      <td>15.8 billion</td>
      <td>Retail sales – $15.413 billion[dm] Home video ...</td>
      <td>Animated series</td>
      <td>Chris Gifford Valerie Walsh Eric Weiner</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>7</th>
      <td>The Simpsons</td>
      <td>1987</td>
      <td>15.8 billion</td>
      <td>Merchandise sales – $7.073 billion[do] TV adve...</td>
      <td>Animated series</td>
      <td>Matt Groening</td>
      <td>20th Century Studios (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Lion King</td>
      <td>1994</td>
      <td>15.4 billion</td>
      <td>Musical theatre – $8.252 billion[dq] Merchandi...</td>
      <td>Animated film</td>
      <td>Roger Allers Rob Minkoff</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avengers</td>
      <td>1963</td>
      <td>15.3 billion</td>
      <td>Box office – $7.765 billion[289] Merchandise s...</td>
      <td>Comic book</td>
      <td>Stan Lee Jack Kirby</td>
      <td>Marvel Entertainment (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pac-Man</td>
      <td>1980</td>
      <td>15.1 billion</td>
      <td>Video games – $14.098 billion[c][du] Merchandi...</td>
      <td>Video game</td>
      <td>Toru Iwatani Namco</td>
      <td>Bandai Namco Entertainment (Bandai Namco Holdi...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Looney Tunes</td>
      <td>1930</td>
      <td>15 billion</td>
      <td>Retail sales – $14.477 billion[dw] Box office ...</td>
      <td>Animated cartoon</td>
      <td>Warner Bros.</td>
      <td>Warner Bros. (AT&amp;T)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>SpongeBob SquarePants</td>
      <td>1999</td>
      <td>14.8 billion</td>
      <td>Retail sales – $14.378 billion[dy] Box office ...</td>
      <td>Animated series</td>
      <td>Stephen Hillenburg</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii series</td>
      <td>2006</td>
      <td>14.8 billion</td>
      <td>Video games – $14.808 billion[c]</td>
      <td>Video game</td>
      <td>Nintendo EAD</td>
      <td>Nintendo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Teenage Mutant Ninja Turtles</td>
      <td>1984</td>
      <td>14.6 billion</td>
      <td>Merchandise sales – $13.2 billion[dz] Box offi...</td>
      <td>Comic book</td>
      <td>Kevin Eastman Peter Laird</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sailor Moon</td>
      <td>1991</td>
      <td>14.3 billion</td>
      <td>Merchandise sales – $13 billion[310] Home ente...</td>
      <td>Manga</td>
      <td>Naoko Takeuchi</td>
      <td>Naoko Takeuchi Kodansha (manga)Toei Animation ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Space Invaders</td>
      <td>1978</td>
      <td>13.9 billion</td>
      <td>Video game – $13.93 billion[329][ef] Music sin...</td>
      <td>Video game</td>
      <td>Tomohiro Nishikado</td>
      <td>Taito (Square Enix)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Frozen</td>
      <td>2013</td>
      <td>13.4 billion</td>
      <td>Merchandise sales – $10.588 billion[eh] Box of...</td>
      <td>Animated film</td>
      <td>Chris Buck Jennifer Lee</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Dungeon Fighter Online (DFO)</td>
      <td>2005</td>
      <td>13.4 billion</td>
      <td>Computer game – $13.4 billion[c]</td>
      <td>Video game</td>
      <td>Neople</td>
      <td>Nexon Tencent</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dragon Quest (Dragon Warrior)</td>
      <td>1986</td>
      <td>12.9 billion</td>
      <td>Video games – $6.501 billion[c] Manga magazine...</td>
      <td>Video game</td>
      <td>Yuji Horii Koichi Nakamura Akira Toriyama</td>
      <td>Square Enix Yuji Horii (Armor Project) Akira T...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Street Fighter</td>
      <td>1987</td>
      <td>12.2 billion</td>
      <td>Video games – $12.009 billion[c] Box office &amp; ...</td>
      <td>Video game</td>
      <td>Takashi Nishiyama Hiroshi Matsumoto</td>
      <td>Capcom</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Final Fantasy</td>
      <td>1987</td>
      <td>12.2 billion</td>
      <td>Video games – $10.958 billion[c] Licensed merc...</td>
      <td>Video game</td>
      <td>Hironobu Sakaguchi Hiromichi Tanaka Nasir Gebelli</td>
      <td>Square Enix</td>
    </tr>
    <tr>
      <th>22</th>
      <td>CrossFire</td>
      <td>2007</td>
      <td>12 billion</td>
      <td>Computer game – $12 billion[c]</td>
      <td>Video game</td>
      <td>Smilegate</td>
      <td>Smilegate Tencent</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Warcraft</td>
      <td>1994</td>
      <td>11.7 billion</td>
      <td>Video games – $11.227 billion[c] Box office – ...</td>
      <td>Video game</td>
      <td>Allen Adham Frank Pearce Michael Morhaime</td>
      <td>Blizzard Entertainment (Activision Blizzard)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ultra Series (Ultraman)</td>
      <td>1966</td>
      <td>11.7 billion</td>
      <td>Merchandise sales – $10.406 billion[es] Pachin...</td>
      <td>Television series</td>
      <td>Eiji Tsuburaya</td>
      <td>Tsuburaya Productions (Bandai Namco Holdings)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>FIFA</td>
      <td>1993</td>
      <td>11.5 billion</td>
      <td>Video games – $11.479 billion[c]</td>
      <td>Video game</td>
      <td>EA Canada</td>
      <td>Electronic Arts</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Superman</td>
      <td>1938</td>
      <td>11.1 billion</td>
      <td>Retail sales – $6.015 billion[ew] Merchandise ...</td>
      <td>Comic book</td>
      <td>Jerry Siegel Joe Shuster</td>
      <td>DC Entertainment (AT&amp;T)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Star Trek</td>
      <td>1966</td>
      <td>10.8 billion[fd]</td>
      <td>Retail sales – $4.753 billion[fe] TV revenue –...</td>
      <td>Television series</td>
      <td>Gene Roddenberry</td>
      <td>ViacomCBS</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3 billion</td>
      <td>Manga magazine – $6.53 billion[ab] Manga volum...</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1 billion</td>
      <td>Video games – $10.098 billion[c] Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Book sales – $9.125 billion[245] Box office – ...</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James Bond</td>
      <td>1953</td>
      <td>19.9</td>
      <td>Box office – $7.078 billion[249] Home video sa...</td>
      <td>Novel</td>
      <td>Ian Fleming</td>
      <td>Metro-Goldwyn-Mayer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peanuts</td>
      <td>1950</td>
      <td>19.1</td>
      <td>Retail sales – $18.805 billion[dc] Box office ...</td>
      <td>Comic strip</td>
      <td>Charles M. Schulz</td>
      <td>Sony Music Entertainment Japan (Sony) WildBrai...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Super Sentai (Power Rangers)</td>
      <td>1975</td>
      <td>16.8</td>
      <td>Retail sales – $16.557 billion[de] Licensed me...</td>
      <td>Television series</td>
      <td>Shotaro Ishinomori Haim Saban Shuki Levy</td>
      <td>Toei Company Hasbro Bandai Namco (toys)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neon Genesis Evangelion (Shinseiki Evangelion)</td>
      <td>1994</td>
      <td>16.6</td>
      <td>Pachinko sales – $11.9 billion[bp] Merchandise...</td>
      <td>Anime</td>
      <td>Hideaki Anno Gainax Tatsunoko Production</td>
      <td>Khara[dl][274][275]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KochiKame</td>
      <td>1976</td>
      <td>16.3</td>
      <td>Manga magazine – $15.448 billion[ab] Manga vol...</td>
      <td>Manga</td>
      <td>Osamu Akimoto</td>
      <td>Osamu Akimoto Shueisha (Hitotsubashi Group) (m...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Dora the Explorer</td>
      <td>2000</td>
      <td>15.8</td>
      <td>Retail sales – $15.413 billion[dm] Home video ...</td>
      <td>Animated series</td>
      <td>Chris Gifford Valerie Walsh Eric Weiner</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>7</th>
      <td>The Simpsons</td>
      <td>1987</td>
      <td>15.8</td>
      <td>Merchandise sales – $7.073 billion[do] TV adve...</td>
      <td>Animated series</td>
      <td>Matt Groening</td>
      <td>20th Century Studios (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Lion King</td>
      <td>1994</td>
      <td>15.4</td>
      <td>Musical theatre – $8.252 billion[dq] Merchandi...</td>
      <td>Animated film</td>
      <td>Roger Allers Rob Minkoff</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avengers</td>
      <td>1963</td>
      <td>15.3</td>
      <td>Box office – $7.765 billion[289] Merchandise s...</td>
      <td>Comic book</td>
      <td>Stan Lee Jack Kirby</td>
      <td>Marvel Entertainment (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pac-Man</td>
      <td>1980</td>
      <td>15.1</td>
      <td>Video games – $14.098 billion[c][du] Merchandi...</td>
      <td>Video game</td>
      <td>Toru Iwatani Namco</td>
      <td>Bandai Namco Entertainment (Bandai Namco Holdi...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Looney Tunes</td>
      <td>1930</td>
      <td>15</td>
      <td>Retail sales – $14.477 billion[dw] Box office ...</td>
      <td>Animated cartoon</td>
      <td>Warner Bros.</td>
      <td>Warner Bros. (AT&amp;T)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>SpongeBob SquarePants</td>
      <td>1999</td>
      <td>14.8</td>
      <td>Retail sales – $14.378 billion[dy] Box office ...</td>
      <td>Animated series</td>
      <td>Stephen Hillenburg</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii series</td>
      <td>2006</td>
      <td>14.8</td>
      <td>Video games – $14.808 billion[c]</td>
      <td>Video game</td>
      <td>Nintendo EAD</td>
      <td>Nintendo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Teenage Mutant Ninja Turtles</td>
      <td>1984</td>
      <td>14.6</td>
      <td>Merchandise sales – $13.2 billion[dz] Box offi...</td>
      <td>Comic book</td>
      <td>Kevin Eastman Peter Laird</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sailor Moon</td>
      <td>1991</td>
      <td>14.3</td>
      <td>Merchandise sales – $13 billion[310] Home ente...</td>
      <td>Manga</td>
      <td>Naoko Takeuchi</td>
      <td>Naoko Takeuchi Kodansha (manga)Toei Animation ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Space Invaders</td>
      <td>1978</td>
      <td>13.9</td>
      <td>Video game – $13.93 billion[329][ef] Music sin...</td>
      <td>Video game</td>
      <td>Tomohiro Nishikado</td>
      <td>Taito (Square Enix)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Frozen</td>
      <td>2013</td>
      <td>13.4</td>
      <td>Merchandise sales – $10.588 billion[eh] Box of...</td>
      <td>Animated film</td>
      <td>Chris Buck Jennifer Lee</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Dungeon Fighter Online (DFO)</td>
      <td>2005</td>
      <td>13.4</td>
      <td>Computer game – $13.4 billion[c]</td>
      <td>Video game</td>
      <td>Neople</td>
      <td>Nexon Tencent</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dragon Quest (Dragon Warrior)</td>
      <td>1986</td>
      <td>12.9</td>
      <td>Video games – $6.501 billion[c] Manga magazine...</td>
      <td>Video game</td>
      <td>Yuji Horii Koichi Nakamura Akira Toriyama</td>
      <td>Square Enix Yuji Horii (Armor Project) Akira T...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Street Fighter</td>
      <td>1987</td>
      <td>12.2</td>
      <td>Video games – $12.009 billion[c] Box office &amp; ...</td>
      <td>Video game</td>
      <td>Takashi Nishiyama Hiroshi Matsumoto</td>
      <td>Capcom</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Final Fantasy</td>
      <td>1987</td>
      <td>12.2</td>
      <td>Video games – $10.958 billion[c] Licensed merc...</td>
      <td>Video game</td>
      <td>Hironobu Sakaguchi Hiromichi Tanaka Nasir Gebelli</td>
      <td>Square Enix</td>
    </tr>
    <tr>
      <th>22</th>
      <td>CrossFire</td>
      <td>2007</td>
      <td>12</td>
      <td>Computer game – $12 billion[c]</td>
      <td>Video game</td>
      <td>Smilegate</td>
      <td>Smilegate Tencent</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Warcraft</td>
      <td>1994</td>
      <td>11.7</td>
      <td>Video games – $11.227 billion[c] Box office – ...</td>
      <td>Video game</td>
      <td>Allen Adham Frank Pearce Michael Morhaime</td>
      <td>Blizzard Entertainment (Activision Blizzard)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ultra Series (Ultraman)</td>
      <td>1966</td>
      <td>11.7</td>
      <td>Merchandise sales – $10.406 billion[es] Pachin...</td>
      <td>Television series</td>
      <td>Eiji Tsuburaya</td>
      <td>Tsuburaya Productions (Bandai Namco Holdings)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>FIFA</td>
      <td>1993</td>
      <td>11.5</td>
      <td>Video games – $11.479 billion[c]</td>
      <td>Video game</td>
      <td>EA Canada</td>
      <td>Electronic Arts</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Superman</td>
      <td>1938</td>
      <td>11.1</td>
      <td>Retail sales – $6.015 billion[ew] Merchandise ...</td>
      <td>Comic book</td>
      <td>Jerry Siegel Joe Shuster</td>
      <td>DC Entertainment (AT&amp;T)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Star Trek</td>
      <td>1966</td>
      <td>10.8</td>
      <td>Retail sales – $4.753 billion[fe] TV revenue –...</td>
      <td>Television series</td>
      <td>Gene Roddenberry</td>
      <td>ViacomCBS</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Manga magazine – $6.53 billion[ab] Manga volum...</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video games – $10.098 billion[c] Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>[Book sales – $9.125 billion, 245] Box office ...</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James Bond</td>
      <td>1953</td>
      <td>19.9</td>
      <td>[Box office – $7.078 billion, 249] Home video ...</td>
      <td>Novel</td>
      <td>Ian Fleming</td>
      <td>Metro-Goldwyn-Mayer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Peanuts</td>
      <td>1950</td>
      <td>19.1</td>
      <td>[Retail sales – $18.805 billion, dc] Box offic...</td>
      <td>Comic strip</td>
      <td>Charles M. Schulz</td>
      <td>Sony Music Entertainment Japan (Sony) WildBrai...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Super Sentai (Power Rangers)</td>
      <td>1975</td>
      <td>16.8</td>
      <td>[Retail sales – $16.557 billion, de] Licensed ...</td>
      <td>Television series</td>
      <td>Shotaro Ishinomori Haim Saban Shuki Levy</td>
      <td>Toei Company Hasbro Bandai Namco (toys)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neon Genesis Evangelion (Shinseiki Evangelion)</td>
      <td>1994</td>
      <td>16.6</td>
      <td>[Pachinko sales – $11.9 billion, bp] Merchandi...</td>
      <td>Anime</td>
      <td>Hideaki Anno Gainax Tatsunoko Production</td>
      <td>Khara[dl][274][275]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KochiKame</td>
      <td>1976</td>
      <td>16.3</td>
      <td>[Manga magazine – $15.448 billion, ab] Manga v...</td>
      <td>Manga</td>
      <td>Osamu Akimoto</td>
      <td>Osamu Akimoto Shueisha (Hitotsubashi Group) (m...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Dora the Explorer</td>
      <td>2000</td>
      <td>15.8</td>
      <td>[Retail sales – $15.413 billion, dm] Home vide...</td>
      <td>Animated series</td>
      <td>Chris Gifford Valerie Walsh Eric Weiner</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>7</th>
      <td>The Simpsons</td>
      <td>1987</td>
      <td>15.8</td>
      <td>[Merchandise sales – $7.073 billion, do] TV ad...</td>
      <td>Animated series</td>
      <td>Matt Groening</td>
      <td>20th Century Studios (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Lion King</td>
      <td>1994</td>
      <td>15.4</td>
      <td>[Musical theatre – $8.252 billion, dq] Merchan...</td>
      <td>Animated film</td>
      <td>Roger Allers Rob Minkoff</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Avengers</td>
      <td>1963</td>
      <td>15.3</td>
      <td>[Box office – $7.765 billion, 289] Merchandise...</td>
      <td>Comic book</td>
      <td>Stan Lee Jack Kirby</td>
      <td>Marvel Entertainment (The Walt Disney Company)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pac-Man</td>
      <td>1980</td>
      <td>15.1</td>
      <td>[Video games – $14.098 billion, c], du] Mercha...</td>
      <td>Video game</td>
      <td>Toru Iwatani Namco</td>
      <td>Bandai Namco Entertainment (Bandai Namco Holdi...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Looney Tunes</td>
      <td>1930</td>
      <td>15</td>
      <td>[Retail sales – $14.477 billion, dw] Box offic...</td>
      <td>Animated cartoon</td>
      <td>Warner Bros.</td>
      <td>Warner Bros. (AT&amp;T)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>SpongeBob SquarePants</td>
      <td>1999</td>
      <td>14.8</td>
      <td>[Retail sales – $14.378 billion, dy] Box offic...</td>
      <td>Animated series</td>
      <td>Stephen Hillenburg</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii series</td>
      <td>2006</td>
      <td>14.8</td>
      <td>[Video games – $14.808 billion, c]]</td>
      <td>Video game</td>
      <td>Nintendo EAD</td>
      <td>Nintendo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Teenage Mutant Ninja Turtles</td>
      <td>1984</td>
      <td>14.6</td>
      <td>[Merchandise sales – $13.2 billion, dz] Box of...</td>
      <td>Comic book</td>
      <td>Kevin Eastman Peter Laird</td>
      <td>Nickelodeon</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sailor Moon</td>
      <td>1991</td>
      <td>14.3</td>
      <td>[Merchandise sales – $13 billion, 310] Home en...</td>
      <td>Manga</td>
      <td>Naoko Takeuchi</td>
      <td>Naoko Takeuchi Kodansha (manga)Toei Animation ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Space Invaders</td>
      <td>1978</td>
      <td>13.9</td>
      <td>[Video game – $13.93 billion, 329], ef] Music ...</td>
      <td>Video game</td>
      <td>Tomohiro Nishikado</td>
      <td>Taito (Square Enix)</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Frozen</td>
      <td>2013</td>
      <td>13.4</td>
      <td>[Merchandise sales – $10.588 billion, eh] Box ...</td>
      <td>Animated film</td>
      <td>Chris Buck Jennifer Lee</td>
      <td>The Walt Disney Company</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Dungeon Fighter Online (DFO)</td>
      <td>2005</td>
      <td>13.4</td>
      <td>[Computer game – $13.4 billion, c]]</td>
      <td>Video game</td>
      <td>Neople</td>
      <td>Nexon Tencent</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dragon Quest (Dragon Warrior)</td>
      <td>1986</td>
      <td>12.9</td>
      <td>[Video games – $6.501 billion, c] Manga magazi...</td>
      <td>Video game</td>
      <td>Yuji Horii Koichi Nakamura Akira Toriyama</td>
      <td>Square Enix Yuji Horii (Armor Project) Akira T...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Street Fighter</td>
      <td>1987</td>
      <td>12.2</td>
      <td>[Video games – $12.009 billion, c] Box office ...</td>
      <td>Video game</td>
      <td>Takashi Nishiyama Hiroshi Matsumoto</td>
      <td>Capcom</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Final Fantasy</td>
      <td>1987</td>
      <td>12.2</td>
      <td>[Video games – $10.958 billion, c] Licensed me...</td>
      <td>Video game</td>
      <td>Hironobu Sakaguchi Hiromichi Tanaka Nasir Gebelli</td>
      <td>Square Enix</td>
    </tr>
    <tr>
      <th>22</th>
      <td>CrossFire</td>
      <td>2007</td>
      <td>12</td>
      <td>[Computer game – $12 billion, c]]</td>
      <td>Video game</td>
      <td>Smilegate</td>
      <td>Smilegate Tencent</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Warcraft</td>
      <td>1994</td>
      <td>11.7</td>
      <td>[Video games – $11.227 billion, c] Box office ...</td>
      <td>Video game</td>
      <td>Allen Adham Frank Pearce Michael Morhaime</td>
      <td>Blizzard Entertainment (Activision Blizzard)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ultra Series (Ultraman)</td>
      <td>1966</td>
      <td>11.7</td>
      <td>[Merchandise sales – $10.406 billion, es] Pach...</td>
      <td>Television series</td>
      <td>Eiji Tsuburaya</td>
      <td>Tsuburaya Productions (Bandai Namco Holdings)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>FIFA</td>
      <td>1993</td>
      <td>11.5</td>
      <td>[Video games – $11.479 billion, c]]</td>
      <td>Video game</td>
      <td>EA Canada</td>
      <td>Electronic Arts</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Superman</td>
      <td>1938</td>
      <td>11.1</td>
      <td>[Retail sales – $6.015 billion, ew] Merchandis...</td>
      <td>Comic book</td>
      <td>Jerry Siegel Joe Shuster</td>
      <td>DC Entertainment (AT&amp;T)</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Star Trek</td>
      <td>1966</td>
      <td>10.8</td>
      <td>[Retail sales – $4.753 billion, fe] TV revenue...</td>
      <td>Television series</td>
      <td>Gene Roddenberry</td>
      <td>ViacomCBS</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>[Manga magazine – $6.53 billion, ab] Manga vol...</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>[Video games – $10.098 billion, c] Comics – ?]</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Book sales – $9.125 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>245] Box office – $5.896 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>246] Home video sales – $4.194 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>245] Merchandise sales – $435 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>245] Licensing – $225 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>fg] Anime box office – $147.1 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>x] Home entertainment – $104 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>fh]</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video games – $10.098 billion</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>c] Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>158 rows × 7 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_items</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Book sales – $9.125 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box office – $5.896 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home video sales – $4.194 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise sales – $435 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Licensing – $225 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Anime box office – $147.1 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home entertainment – $104 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td></td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video games – $10.098 billion</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Comics – ?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>158 rows × 7 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
 .deconcatenate_column('revenue_items', 
                       sep="–", 
                       new_column_names=['revenue_category', 'revenue'], 
                       preserve_position = True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Book sales</td>
      <td>$9.125 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box office</td>
      <td>$5.896 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home video sales</td>
      <td>$4.194 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise sales</td>
      <td>$435 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Licensing</td>
      <td>$225 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Anime box office</td>
      <td>$147.1 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home entertainment</td>
      <td>$104 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td></td>
      <td>None</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video games</td>
      <td>$10.098 billion</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Comics</td>
      <td>?</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>158 rows × 8 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
 .deconcatenate_column('revenue_items', 
                       sep="–", 
                       new_column_names=['revenue_category', 'revenue'], 
                       preserve_position = True)
 .query("revenue.str.contains('illion', na=False)")
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Book sales</td>
      <td>$9.125 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box office</td>
      <td>$5.896 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home video sales</td>
      <td>$4.194 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise sales</td>
      <td>$435 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Licensing</td>
      <td>$225 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Licensed merchandise</td>
      <td>$1.27 billion</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Video games</td>
      <td>$761 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Anime box office</td>
      <td>$147.1 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home entertainment</td>
      <td>$104 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video games</td>
      <td>$10.098 billion</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 8 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
 .deconcatenate_column('revenue_items', 
                       sep="–", 
                       new_column_names=['revenue_category', 'revenue'], 
                       preserve_position = True)
 .query("revenue.str.contains('illion', na=False)")
 .process_text('revenue_category', string_function='lower')
 .process_text('revenue_category', string_function='strip')
 .replace({"revenue_category":{
    '.*(box office).*': 'Box Office',
    '.*(dvd|blu|vhs|home video|video rentals|video sales|streaming|home entertainment).*': 'Home Video/Entertainment',
    '.*(video game|computer game|mobile game|console|game|pachinko|pet|card).*': 'Video Games/Games',
    '.*(comic|manga).*': 'Comic or Manga',
    '.*(music|soundtrac).*': 'Music',
    '.*(tv).*': 'TV',
    '.*(merchandise|licens|mall|stage|retail).*': 'Merchandise, Licensing & Retail'}}, 
    regex=True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>book sales</td>
      <td>$9.125 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box Office</td>
      <td>$5.896 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home Video/Entertainment</td>
      <td>$4.194 billion</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>$435 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>$225 million</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>$1.27 billion</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Video Games/Games</td>
      <td>$761 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Box Office</td>
      <td>$147.1 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home Video/Entertainment</td>
      <td>$104 million</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video Games/Games</td>
      <td>$10.098 billion</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 8 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
 .deconcatenate_column('revenue_items', 
                       sep="–", 
                       new_column_names=['revenue_category', 'revenue'], 
                       preserve_position = True)
 .query("revenue.str.contains('illion', na=False)")
 .process_text('revenue_category', string_function='lower')
 .process_text('revenue_category', string_function='strip')
 .replace({"revenue_category":{
    '.*(box office).*': 'Box Office',
    '.*(dvd|blu|vhs|home video|video rentals|video sales|streaming|home entertainment).*': 'Home Video/Entertainment',
    '.*(video game|computer game|mobile game|console|game|pachinko|pet|card).*': 'Video Games/Games',
    '.*(comic|manga).*': 'Comic or Manga',
    '.*(music|soundtrac).*': 'Music',
    '.*(tv).*': 'TV',
    '.*(merchandise|licens|mall|stage|retail).*': 'Merchandise, Licensing & Retail'}}, 
    regex=True)
 .process_text('revenue', string_function='replace', pat='\$|illion',repl='', regex=True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>book sales</td>
      <td>9.125 b</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box Office</td>
      <td>5.896 b</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home Video/Entertainment</td>
      <td>4.194 b</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>435 m</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>225 m</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>1.27 b</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Video Games/Games</td>
      <td>761 m</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Box Office</td>
      <td>147.1 m</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home Video/Entertainment</td>
      <td>104 m</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video Games/Games</td>
      <td>10.098 b</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 8 columns</p>
</div>




```python
(df
 .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
            axis='columns')
 .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
 .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
 .process_text('revenue_items', string_function="split", pat="[")
 .explode('revenue_items')
 .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
 .deconcatenate_column('revenue_items', 
                       sep="–", 
                       new_column_names=['revenue_category', 'revenue'], 
                       preserve_position = True)
 .query("revenue.str.contains('illion', na=False)")
 .process_text('revenue_category', string_function='lower')
 .process_text('revenue_category', string_function='strip')
 .replace({"revenue_category":{
    '.*(box office).*': 'Box Office',
    '.*(dvd|blu|vhs|home video|video rentals|video sales|streaming|home entertainment).*': 'Home Video/Entertainment',
    '.*(video game|computer game|mobile game|console|game|pachinko|pet|card).*': 'Video Games/Games',
    '.*(comic|manga).*': 'Comic or Manga',
    '.*(music|soundtrac).*': 'Music',
    '.*(tv).*': 'TV',
    '.*(merchandise|licens|mall|stage|retail).*': 'Merchandise, Licensing & Retail'}}, 
    regex=True)
 .process_text('revenue', string_function='replace', pat='\$|illion',repl='', regex=True)
 .process_text('revenue', string_function='replace', pat='[\s+]b', repl='', regex=True)
 .process_text('revenue', string_function='replace', pat='[\s+]m', repl='e-3', regex=True)
)
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>book sales</td>
      <td>9.125</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box Office</td>
      <td>5.896</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home Video/Entertainment</td>
      <td>4.194</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>435e-3</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>225e-3</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>1.27</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Video Games/Games</td>
      <td>761e-3</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Box Office</td>
      <td>147.1e-3</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home Video/Entertainment</td>
      <td>104e-3</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video Games/Games</td>
      <td>10.098</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 8 columns</p>
</div>




```python
df_clean = (df
             .set_axis(('franchise','year_created','total_revenue','revenue_items','original_media','creators','owners'), 
                        axis='columns')
             .process_text('total_revenue', string_function = 'replace', pat = '\$|est.', repl='', regex=True)
             .process_text('total_revenue', string_function = 'extract', pat = '(\d+\.?\d?)', expand = False)
             .process_text('revenue_items', string_function="split", pat="[")
             .explode('revenue_items')
             .process_text('revenue_items', string_function="replace", pat=".+\]", repl='', regex=True)
             .deconcatenate_column('revenue_items', 
                                   sep="–", 
                                   new_column_names=['revenue_category', 'revenue'], 
                                   preserve_position = True)
             .query("revenue.str.contains('illion', na=False)")
             .process_text('revenue_category', string_function='lower')
             .process_text('revenue_category', string_function='strip')
             .replace({"revenue_category":{
                '.*(box office).*': 'Box Office',
                '.*(dvd|blu|vhs|home video|video rentals|video sales|streaming|home entertainment).*': 'Home Video/Entertainment',
                '.*(video game|computer game|mobile game|console|game|pachinko|pet|card).*': 'Video Games/Games',
                '.*(comic|manga).*': 'Comic or Manga',
                '.*(music|soundtrac).*': 'Music',
                '.*(tv).*': 'TV',
                '.*(merchandise|licens|mall|stage|retail).*': 'Merchandise, Licensing & Retail'}}, 
                regex=True)
             .process_text('revenue', string_function='replace', pat='\$|illion',repl='', regex=True)
             .process_text('revenue', string_function='replace', pat='[\s+]b', repl='', regex=True)
             .process_text('revenue', string_function='replace', pat='[\s+]m', repl='e-3', regex=True)
             .transform(pd.to_numeric, errors='ignore')
             .reset_index(drop = True)
            )
```


```python
df_clean
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
      <th>franchise</th>
      <th>year_created</th>
      <th>total_revenue</th>
      <th>revenue_category</th>
      <th>revenue</th>
      <th>original_media</th>
      <th>creators</th>
      <th>owners</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>book sales</td>
      <td>9.1250</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Box Office</td>
      <td>5.8960</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Home Video/Entertainment</td>
      <td>4.1940</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>0.4350</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Middle-earth (The Lord of the Rings)</td>
      <td>1937</td>
      <td>19.9</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>0.2250</td>
      <td>Novel</td>
      <td>J. R. R. Tolkien</td>
      <td>Tolkien Estate (books) Warner Bros. (AT&amp;T) (fi...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Merchandise, Licensing &amp; Retail</td>
      <td>1.2700</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Video Games/Games</td>
      <td>0.7610</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Box Office</td>
      <td>0.1471</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Naruto</td>
      <td>1999</td>
      <td>10.3</td>
      <td>Home Video/Entertainment</td>
      <td>0.1040</td>
      <td>Manga</td>
      <td>Masashi Kishimoto</td>
      <td>Masashi Kishimoto Shueisha (Hitotsubashi Group...</td>
    </tr>
    <tr>
      <th>120</th>
      <td>League of Legends (LoL)</td>
      <td>2009</td>
      <td>10.1</td>
      <td>Video Games/Games</td>
      <td>10.0980</td>
      <td>Video game</td>
      <td>Riot Games</td>
      <td>Tencent</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 8 columns</p>
</div>



<h2 align='center'> A Peek at some Functions </h2>

<h3> Pivot data from wide to long </h3>
<br><br>

Examples adapted from [Rdatatable](https://rdatatable.gitlab.io/data.table/articles/datatable-reshape.html#using-measure-to-specify-measure-vars-via-separator-or-pattern) and [pandas' melt](https://pandas.pydata.org/pandas-docs/stable/user_guide/reshaping.html#reshaping-by-melt)


```python
index = pd.MultiIndex.from_tuples([('person', 'A'), ('person', 'B')])

df = pd.DataFrame({'first': ['John', 'Mary'],
                   'last': ['Doe', 'Bo'],
                   'height': [5.5, 6.0],
                   'weight': [130, 150]},
                   index=index)
                   
df
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
      <th></th>
      <th>first</th>
      <th>last</th>
      <th>height</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">person</th>
      <th>A</th>
      <td>John</td>
      <td>Doe</td>
      <td>5.5</td>
      <td>130</td>
    </tr>
    <tr>
      <th>B</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>6.0</td>
      <td>150</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(index=['first', 'last'])
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
      <th>first</th>
      <th>last</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>Doe</td>
      <td>height</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>height</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>John</td>
      <td>Doe</td>
      <td>weight</td>
      <td>130.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>weight</td>
      <td>150.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(index="*st")
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
      <th>first</th>
      <th>last</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>Doe</td>
      <td>height</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>height</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>John</td>
      <td>Doe</td>
      <td>weight</td>
      <td>130.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>weight</td>
      <td>150.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(
    index = "*st", 
    names_to = "dimension", 
    values_to = "value_in_metres"
)
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
      <th>first</th>
      <th>last</th>
      <th>dimension</th>
      <th>value_in_metres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>Doe</td>
      <td>height</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>height</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>John</td>
      <td>Doe</td>
      <td>weight</td>
      <td>130.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>weight</td>
      <td>150.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(
    index = "*st", 
    names_to = "dimension", 
    values_to = "value_in_metres", 
    sort_by_appearance = True)
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
      <th>first</th>
      <th>last</th>
      <th>dimension</th>
      <th>value_in_metres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>Doe</td>
      <td>height</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>John</td>
      <td>Doe</td>
      <td>weight</td>
      <td>130.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>height</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mary</td>
      <td>Bo</td>
      <td>weight</td>
      <td>150.0</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if there are Multiple names in the columns? </h3>


```python
df = pd.DataFrame(
    {'Sepal.Length': [5.1, 5.9],
     'Sepal.Width': [3.5, 3.0],
     'Petal.Length': [1.4, 5.1],
     'Petal.Width': [0.2, 1.8],
     'Species': ['setosa', 'virginica']}
    )

df
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
      <th>Sepal.Length</th>
      <th>Sepal.Width</th>
      <th>Petal.Length</th>
      <th>Petal.Width</th>
      <th>Species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(
    index = 'Species',
    names_to = ('part', 'dimension'),
    names_sep = '.',
    sort_by_appearance = True
)
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
      <th>Species</th>
      <th>part</th>
      <th>dimension</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>setosa</td>
      <td>Sepal</td>
      <td>Length</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>setosa</td>
      <td>Sepal</td>
      <td>Width</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>setosa</td>
      <td>Petal</td>
      <td>Length</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>setosa</td>
      <td>Petal</td>
      <td>Width</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>virginica</td>
      <td>Sepal</td>
      <td>Length</td>
      <td>5.9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>virginica</td>
      <td>Sepal</td>
      <td>Width</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>virginica</td>
      <td>Petal</td>
      <td>Length</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>virginica</td>
      <td>Petal</td>
      <td>Width</td>
      <td>1.8</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if I want to keep part of the column name as a header ?</h3>


```python
df.pivot_longer(
    index = 'Species',
    names_to = ('.value', 'dimension'),
    names_sep = '.',
    sort_by_appearance = True
)
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
      <th>Species</th>
      <th>dimension</th>
      <th>Sepal</th>
      <th>Petal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>setosa</td>
      <td>Length</td>
      <td>5.1</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>setosa</td>
      <td>Width</td>
      <td>3.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>virginica</td>
      <td>Length</td>
      <td>5.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>virginica</td>
      <td>Width</td>
      <td>3.0</td>
      <td>1.8</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(
    index = 'Species',
    names_to = ('part', '.value'),
    names_sep = '.',
    sort_by_appearance = True
)
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
      <th>Species</th>
      <th>part</th>
      <th>Length</th>
      <th>Width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>setosa</td>
      <td>Sepal</td>
      <td>5.1</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>setosa</td>
      <td>Petal</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>virginica</td>
      <td>Sepal</td>
      <td>5.9</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>virginica</td>
      <td>Petal</td>
      <td>5.1</td>
      <td>1.8</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if there is no defined separator? </h3>


```python
# https://github.com/tidyverse/tidyr/blob/main/data-raw/who.csv
df = pd.DataFrame({'id': [1], 'new_sp_m5564': [2], 'newrel_f65': [3]})
df
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
      <th>id</th>
      <th>new_sp_m5564</th>
      <th>newrel_f65</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_longer(
    index = 'id',
    names_to = ('diagnosis', 'gender', 'age'),
    names_pattern = r"new_?(.+)_(.)(\d+)"
)
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
      <th>id</th>
      <th>diagnosis</th>
      <th>gender</th>
      <th>age</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>sp</td>
      <td>m</td>
      <td>5564</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>rel</td>
      <td>f</td>
      <td>65</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



<h3> Make Implicit Missing Values Explicit </h3>


```python
# https://stackoverflow.com/q/64492818/7175713
df = pd.DataFrame(
    {'id': [1, 1, 1, 2, 2, 2],
     'year': [2000, 2001, 2001, 1999, 1999, 2001],
     'semester': [1, 1, 2, 1, 2, 1]}

)

df
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



<h3> Generate all possible combinations of <em>id</em>, <em>year</em>, and <em>semester</em></h3>
<h3>(whether or not they appear in the data)</h3>


```python
df.complete('id', 'year', 'semester', sort = True)
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



<h3> Cross all possible <em>id</em> values with the unique pairs of </h3>
<h3><em>(year, semester)</em> that already exist in the data </h3>


```python
df.complete('id', ('year', 'semester'), sort = True)
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



<h3> Within each <em>id</em>, generate all possible combinations of </h3>
<h3> <em>year</em> and <em>semester</em> that occur in that group </h3>


```python
df.complete('year', 'semester', by='id', sort = True)
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if I want the years expanded to 2003?</h3>


```python
df.complete(
    'id',
    'semester',
    {'year': range(df['year'].min(), 2003)},
    sort = True
   )
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>2002</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if I also want the semester expanded to 3?</h3>


```python
df.complete(
    'id',            
    {'year': range(df['year'].min(), 2003),
    'semester' : range(1,4)},
    sort = True
           )
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1999</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>2001</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>2002</td>
      <td>3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2</td>
      <td>1999</td>
      <td>3</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2</td>
      <td>2000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2</td>
      <td>2001</td>
      <td>3</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2</td>
      <td>2002</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



<h3> What if I want the years expanded to 2003 per group?</h3>


```python
df.complete('semester',
            {'year': lambda df: range(df.min(), 2003)},
            by = 'id',
            sort = True
           )
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
      <th>id</th>
      <th>year</th>
      <th>semester</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>1999</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>2000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>2001</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>2002</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>1999</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>2000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2</td>
      <td>2001</td>
      <td>2</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>2002</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



<h3> If-Else </h3>


```python
# https://stackoverflow.com/q/54653356/7175713
data = {
    "name": ["Jason", "Molly", "Tina", "Jake", "Amy"],
    "age": [42, 52, 36, 24, 73],
    "preTestScore": [4, 24, 31, 2, 3],
    "postTestScore": [25, 94, 57, 62, 70],
}
df = pd.DataFrame(data, columns=["name", "age", "preTestScore", "postTestScore"])
df
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
      <th>name</th>
      <th>age</th>
      <th>preTestScore</th>
      <th>postTestScore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>42</td>
      <td>4</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>52</td>
      <td>24</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>36</td>
      <td>31</td>
      <td>57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>24</td>
      <td>2</td>
      <td>62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>73</td>
      <td>3</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.case_when(
    df.age == 10, 'baby', # condition, value
    df.age.between(10, 20, inclusive='left'), 'kid',
    df.age.between(20, 30, inclusive='left'), 'young',
    df.age.between(30, 50, inclusive='left'), 'mature',
    'grandpa', # default if False
    column_name = 'elderly'
)
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
      <th>name</th>
      <th>age</th>
      <th>preTestScore</th>
      <th>postTestScore</th>
      <th>elderly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>42</td>
      <td>4</td>
      <td>25</td>
      <td>mature</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>52</td>
      <td>24</td>
      <td>94</td>
      <td>grandpa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>36</td>
      <td>31</td>
      <td>57</td>
      <td>mature</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>24</td>
      <td>2</td>
      <td>62</td>
      <td>young</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>73</td>
      <td>3</td>
      <td>70</td>
      <td>grandpa</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.case_when(
    "age < 10",       "baby",  # condition, value
    "10 <= age < 20", "kid",
    "20 <= age < 30", "young",
    "30 <= age < 50", "mature",
    "grandpa", # default if False
    column_name="elderly",
)
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
      <th>name</th>
      <th>age</th>
      <th>preTestScore</th>
      <th>postTestScore</th>
      <th>elderly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jason</td>
      <td>42</td>
      <td>4</td>
      <td>25</td>
      <td>mature</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Molly</td>
      <td>52</td>
      <td>24</td>
      <td>94</td>
      <td>grandpa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tina</td>
      <td>36</td>
      <td>31</td>
      <td>57</td>
      <td>mature</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jake</td>
      <td>24</td>
      <td>2</td>
      <td>62</td>
      <td>young</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Amy</td>
      <td>73</td>
      <td>3</td>
      <td>70</td>
      <td>grandpa</td>
    </tr>
  </tbody>
</table>
</div>



<h3> Read from the Command Line </h3>


```python
!ls Documents/janitor
```

    iris_zipped.zip  us-counties.txt  zip_error.png


```py
pd.read_csv('Documents/janitor/iris_zipped.zip')
```

<img src = "Documents/janitor/zip_error.png" />


```python
from janitor.io import read_commandline
outcome = read_commandline('unzip -p Documents/janitor/iris_zipped.zip iris_zipped/setosa.csv')

outcome.head()
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
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>
</div>




```python
!wc -l Documents/janitor/us-counties.txt
```

    2183954 Documents/janitor/us-counties.txt



```python
!head -n5 Documents/janitor/us-counties.txt
```

    date,county,state,fips,cases,deaths
    2020-01-21,Snohomish,Washington,53061,1,0
    2020-01-22,Snohomish,Washington,53061,1,0
    2020-01-23,Snohomish,Washington,53061,1,0
    2020-01-24,Cook,Illinois,17031,1,0



```python
df = pd.read_csv('Documents/janitor/us-counties.txt')
df.loc[df.state == 'California']
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
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>2020-01-25</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2020-01-26</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020-01-26</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2020-01-27</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2020-01-27</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2180942</th>
      <td>2022-02-04</td>
      <td>Tulare</td>
      <td>California</td>
      <td>6107.0</td>
      <td>123838</td>
      <td>1256.0</td>
    </tr>
    <tr>
      <th>2180943</th>
      <td>2022-02-04</td>
      <td>Tuolumne</td>
      <td>California</td>
      <td>6109.0</td>
      <td>12130</td>
      <td>163.0</td>
    </tr>
    <tr>
      <th>2180944</th>
      <td>2022-02-04</td>
      <td>Ventura</td>
      <td>California</td>
      <td>6111.0</td>
      <td>174788</td>
      <td>1322.0</td>
    </tr>
    <tr>
      <th>2180945</th>
      <td>2022-02-04</td>
      <td>Yolo</td>
      <td>California</td>
      <td>6113.0</td>
      <td>36798</td>
      <td>281.0</td>
    </tr>
    <tr>
      <th>2180946</th>
      <td>2022-02-04</td>
      <td>Yuba</td>
      <td>California</td>
      <td>6115.0</td>
      <td>16529</td>
      <td>105.0</td>
    </tr>
  </tbody>
</table>
<p>40008 rows × 6 columns</p>
</div>




```python
read_commandline("head -1 Documents/janitor/us-counties.txt; grep California Documents/janitor/us-counties.txt")
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
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-25</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-26</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-26</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-27</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-27</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>40003</th>
      <td>2022-02-04</td>
      <td>Tulare</td>
      <td>California</td>
      <td>6107.0</td>
      <td>123838</td>
      <td>1256</td>
    </tr>
    <tr>
      <th>40004</th>
      <td>2022-02-04</td>
      <td>Tuolumne</td>
      <td>California</td>
      <td>6109.0</td>
      <td>12130</td>
      <td>163</td>
    </tr>
    <tr>
      <th>40005</th>
      <td>2022-02-04</td>
      <td>Ventura</td>
      <td>California</td>
      <td>6111.0</td>
      <td>174788</td>
      <td>1322</td>
    </tr>
    <tr>
      <th>40006</th>
      <td>2022-02-04</td>
      <td>Yolo</td>
      <td>California</td>
      <td>6113.0</td>
      <td>36798</td>
      <td>281</td>
    </tr>
    <tr>
      <th>40007</th>
      <td>2022-02-04</td>
      <td>Yuba</td>
      <td>California</td>
      <td>6115.0</td>
      <td>16529</td>
      <td>105</td>
    </tr>
  </tbody>
</table>
<p>40008 rows × 6 columns</p>
</div>




```python
read_commandline("""mawk -F',' 'NR==1||$3=="California" {print}' Documents/janitor/us-counties.txt""")
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
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-25</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-26</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-26</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-27</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-27</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>40003</th>
      <td>2022-02-04</td>
      <td>Tulare</td>
      <td>California</td>
      <td>6107.0</td>
      <td>123838</td>
      <td>1256</td>
    </tr>
    <tr>
      <th>40004</th>
      <td>2022-02-04</td>
      <td>Tuolumne</td>
      <td>California</td>
      <td>6109.0</td>
      <td>12130</td>
      <td>163</td>
    </tr>
    <tr>
      <th>40005</th>
      <td>2022-02-04</td>
      <td>Ventura</td>
      <td>California</td>
      <td>6111.0</td>
      <td>174788</td>
      <td>1322</td>
    </tr>
    <tr>
      <th>40006</th>
      <td>2022-02-04</td>
      <td>Yolo</td>
      <td>California</td>
      <td>6113.0</td>
      <td>36798</td>
      <td>281</td>
    </tr>
    <tr>
      <th>40007</th>
      <td>2022-02-04</td>
      <td>Yuba</td>
      <td>California</td>
      <td>6115.0</td>
      <td>16529</td>
      <td>105</td>
    </tr>
  </tbody>
</table>
<p>40008 rows × 6 columns</p>
</div>




```python
read_commandline("""xsv search -s state 'California' Documents/janitor/us-counties.txt""")
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
      <th>date</th>
      <th>county</th>
      <th>state</th>
      <th>fips</th>
      <th>cases</th>
      <th>deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-25</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-26</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-26</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-27</td>
      <td>Los Angeles</td>
      <td>California</td>
      <td>6037.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-27</td>
      <td>Orange</td>
      <td>California</td>
      <td>6059.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>40003</th>
      <td>2022-02-04</td>
      <td>Tulare</td>
      <td>California</td>
      <td>6107.0</td>
      <td>123838</td>
      <td>1256</td>
    </tr>
    <tr>
      <th>40004</th>
      <td>2022-02-04</td>
      <td>Tuolumne</td>
      <td>California</td>
      <td>6109.0</td>
      <td>12130</td>
      <td>163</td>
    </tr>
    <tr>
      <th>40005</th>
      <td>2022-02-04</td>
      <td>Ventura</td>
      <td>California</td>
      <td>6111.0</td>
      <td>174788</td>
      <td>1322</td>
    </tr>
    <tr>
      <th>40006</th>
      <td>2022-02-04</td>
      <td>Yolo</td>
      <td>California</td>
      <td>6113.0</td>
      <td>36798</td>
      <td>281</td>
    </tr>
    <tr>
      <th>40007</th>
      <td>2022-02-04</td>
      <td>Yuba</td>
      <td>California</td>
      <td>6115.0</td>
      <td>16529</td>
      <td>105</td>
    </tr>
  </tbody>
</table>
<p>40008 rows × 6 columns</p>
</div>




```python
%%timeit
df = pd.read_csv('Documents/janitor/us-counties.txt')
df.loc[df.state == 'California']
```

    1.54 s ± 39.5 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)



```python
%timeit read_commandline("head -1 Documents/janitor/us-counties.txt; grep California Documents/janitor/us-counties.txt")
```

    131 ms ± 5.5 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)



```python
%timeit read_commandline("head -1 Documents/janitor/us-counties.txt; rg California Documents/janitor/us-counties.txt")
```

    89.4 ms ± 1.29 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)



```python
%timeit read_commandline("""xsv search -s state 'California' Documents/janitor/us-counties.txt""")
```

    377 ms ± 7.25 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)



```python
%timeit read_commandline("""mawk -F',' 'NR==1||$3=="California" {print}' Documents/janitor/us-counties.txt""")
```

    659 ms ± 19.7 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)



```python
%load_ext memory_profiler

%memit df = pd.read_csv('Documents/janitor/us-counties.txt'); df.loc[df.state == 'California']
```

    peak memory: 582.96 MiB, increment: 245.76 MiB



```python
%memit read_commandline("head -1 Documents/janitor/us-counties.txt; grep California Documents/janitor/us-counties.txt")
```

    peak memory: 365.93 MiB, increment: 0.23 MiB


<h2 align = 'center'> Clarion Call </h2>


- Contributions are welcome (docs, code, comments, infrastructure, reviews, feedbacks,...)

<h1 align = 'center'> THANK YOU! </h1>
