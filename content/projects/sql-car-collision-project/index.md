---
Title: "Unveiling Insights: Exploratory Data Analysis of California Traffic Collisions using SQl"
tags: [Exploratory Data Analysis, Data Visualization, SQL, DuckDb, JupySQL,Jupyter Notebook ]

Summary: Exploratory data analysis of California Traffic Collisions data using SQL. Obtained insights into collision patterns and trends.
---

## Project Description
In this data analysis project, I performed exploratory data analysis using SQL in Jupyter Notebook to gain insights into traffic collisions in California. Leveraging JupyterSQL and DuckDB, I conducted a comprehensive examination of the California Traffic Collision Data obtained from SWITRS. This dataset covers collisions from January 1st, 2001 until mid-2021, comprising approximately 9,424,334 collision records.

## Project Highlights

### Exploration and Analysis
*(hover over the charts to interact with it)*
- Explored the time duration covered by the database, spanning from January 1, 2001, to June 3, 2021.
- Analyzed the total number of collisions recorded, revealing a staggering count of approximately 9.4 million collisions.

- Identified the year with the highest collisions recorded, with 2002 ranking at the top, followed by 2003 and 2004.
{{< chart >}}
type: 'line',
data: {
  labels: [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021],
  datasets: [{
    label: 'collisions per year',
    data: [522562, 544741, 538954, 538295, 532725, 498846, 501908, 452595, 426228, 416490, 403629, 395901, 383840, 399565, 438169, 491619, 486432, 482296, 470352, 366417, 132770],
    fill: false,
    borderColor: 'black',
    backgroundColor: 'blue',
    pointBorderColor: 'blue',
    pointBackgroundColor: 'blue',
    pointRadius: 4,
    pointHoverRadius: 6
  }]
}
{{< /chart >}}

- Investigated the counties with the highest collisions, with Los Angeles leading with over 2 million entries.
{{< chart >}}
type: 'bar',
data: {
  labels: ['Los Angeles', 'Orange', 'San Bernardino', 'San Diego', 'Riverside', 'Alameda', 'Sacramento', 'Santa Clara', 'Contra Costa', 'San Joaquin'],
  datasets: [{
    label: 'Total collisions per county',
    data: [2851925, 728565, 569376, 535596, 493758, 466969, 403575, 342603, 217025, 209185],
    backgroundColor: 'blue',
    borderColor: '#000000'
  }]
}
{{< /chart >}}

- Examined the impact of alcohol involvement, finding that approximately 10.02% of collisions involved alcohol.
<div style="width: 300px; height: 300px;">
  <canvas id="alcoholDonutChart" width="300" height="300"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
// Data for Alcohol Donut Chart
const alcoholPercentage = 10.02;
const nonAlcoholPercentage = 100 - alcoholPercentage;

// Chart Configuration for Alcohol Donut Chart
const alcoholDonutConfig = {
  type: 'doughnut',
  data: {
    labels: ['Alcohol-Involved', 'Non-Alcohol Involved'],
    datasets: [{
      data: [alcoholPercentage, nonAlcoholPercentage],
      backgroundColor: ['blue', 'gray'],
      borderColor: '#000000'
    }]
  },
  options: {
    responsive: true,
    plugins: {
      legend: {
        display: true,
        position: 'bottom'
      },
      datalabels: {
        color: 'white',
        formatter: function(value, context) {
          return value + '%';
        }
      }
    }
  }
};

// Create Alcohol Donut Chart
const alcoholDonutChart = new Chart('alcoholDonutChart', alcoholDonutConfig);

// Adjust legend display
const alcoholLegend = alcoholDonutChart.legend;
if (alcoholLegend) {
  alcoholLegend.options.position = 'top';
  alcoholLegend.options.align = 'start';
  alcoholLegend.update();
}
</script>

- Explored the gender distribution of parties involved, highlighting that males accounted for 61.27%, females for 38.7%, and non-binary individuals for 0.02% of the total.

<div style="width: 300px; height: 300px;">
  <canvas id="genderDonutChart" width="300" height="300"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
// Data for Gender Donut Chart
const genderData = {
  labels: ['Male', 'Female', 'X'],
  datasets: [{
    data: [61.27, 38.7, 0.02],
    backgroundColor: ['blue', 'pink', 'gray'],
    borderColor: '#000000'
  }]
};

// Chart Configuration for Gender Donut Chart
const genderDonutConfig = {
  type: 'doughnut',
  data: genderData,
  options: {
    responsive: true,
    plugins: {
      legend: {
        display: true,
        position: 'bottom',
        align: 'start'
      },
      datalabels: {
        color: 'white',
        formatter: function(value, context) {
          return value + '%';
        }
      }
    }
  }
};

// Create Gender Donut Chart
const genderDonutChart = new Chart('genderDonutChart', genderDonutConfig);
</script>

- Uncovered the most frequent PCF (Primary Collision Factor) violation category, identifying speeding as the primary factor.

<canvas id="barChart" width="400" height="400"></canvas>

  <script>
    // Data for Bar Chart
    const pcfViolationData = {
      labels: [
        'Speeding',
        'Improper Turning',
        'Automobile Right of Way',
        'DUI',
        'Unsafe Lane Change',
        'Traffic Signals and Signs',
        'Unsafe Starting or Backing',
        'Unknown',
        'Wrong Side of Road',
        'Other than Driver (or Pedestrian)'
      ],
      datasets: [{
        label: 'Number of Collisions',
        data: [2911725, 1627618, 1111967, 695636, 653108, 514782, 352417, 293802, 219298, 203446],
        backgroundColor: '#4287f5',
        borderColor: 'black',
        borderWidth: 1
      }]
    };

    // Chart Configuration for Bar Chart
    const barConfig = {
      type: 'bar',
      data: pcfViolationData,
      options: {
        responsive: true,
        plugins: {
          legend: {
            display: false
          },
          datalabels: {
            color: 'black',
            anchor: 'end',
            align: 'top',
            formatter: function(value, context) {
              return value;
            }
          }
        },
        scales: {
          x: {
            grid: {
              display: false
            }
          },
          y: {
            ticks: {
              beginAtZero: true
            }
          }
        }
      }
    };

    // Create Bar Chart
    const barChart = new Chart('barChart', barConfig);
  </script>

- Analyzed the relationship between weather conditions, road surfaces, and lighting with traffic collisions.
- Explored hit-and-run cases, identifying the prevalence of non-hit and run incidents, misdemeanors, and felonies.
- Investigated the involvement of different vehicle makes in collisions, ranking the top 7 most frequent makes.
<div style="width: 400px; height: 400px;">
  <canvas id="doughnutChart" width="400" height="400"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
// Data
const degreeOfInjuryData = {
  labels: [
    'No Injury',
    'Complaint of Pain',
    'Other Visible Injury',
    'Possible Injury',
    'Severe Injury',
    'Suspected Minor Injury',
    'Killed',
    'Suspected Serious Injury'
  ],
  datasets: [{
    data: [45.37, 35.48, 13.55, 2.85, 2.37, 1.49, 0.77, 0.4],
      backgroundColor: [
      '#FF6384',
      '#36A2EB',
      '#FFCE56',
      '#9933CC',
      '#FF9933',
      '#00CCCC',
      '#6B6B6B', // Black color for "Killed"
      '#FF3300'
    ],
    borderColor: '#000000' // Black border color for the donut chart
  }]
};

// Chart Configuration
const doughnutConfig = {
  type: 'doughnut',
  data: degreeOfInjuryData,
  options: {
    responsive: true,
    plugins: {
      legend: {
        display: true,
        position: 'bottom'
      },
      datalabels: {
        color: 'white',
        formatter: function(value, context) {
          return value + '%';
        }
      }
    }
  }
};

// Create Chart
const doughnutChart = new Chart('doughnutChart', doughnutConfig);
</script>

- Analyzed the age distribution of victims, revealing higher frequencies among individuals aged 10-20 and 20-30.

## GitHub Repository
For a detailed exploration of the analysis and access to the SQL code, please visit my [GitHub repository](https://github.com/vaadewoyin/SQL-Analysis-of-California-Traffic-Collisions). The repository contains the Jupyter Notebook, SQL queries, and associated files related to this project.

## Conclusion
This SQL analysis project provides valuable insights into traffic collisions in California, covering various aspects such as time duration, total collisions, counties, alcohol involvement, gender distribution, PCF violation categories, weather conditions, and much more. 