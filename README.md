**Project3: **

**Bank Loan Analysis**

**About Company:**

Lending Club (LC) is one of the largest online credit marketplace,
facilitating personal loans, business loans, and financing for elective
medical procedures. Borrowers access lower interest rate loans through a
fast and easy online or mobile interface. Investors provide the capital
to enable many of the loans in exchange for earning interest. LC operate
fully online with no branch infrastructure, and use technology to lower
cost and deliver an amazing experience. LC pass the cost savings to
borrowers in the form of lower rates and investors in the form of
attractive returns. LC is transforming the banking system into a
frictionless, transparent and highly efficient online marketplace,
helping people achieve their financial goals everyday.

**How LC Operates:**

As a personal loan or business loan borrower, you can get an instant
quote in minutes with no impact to your credit score. Once you select an
offer, you can watch as funds are committed by investors who are
choosing to invest in you and your success.

If you’re investing, you can open an account in minutes and build a
portfolio of hundreds or thousands of loans made to quality borrowers.
You’ll receive monthly payments of principal and interest, which you can
withdraw or reinvest.

If you’re looking for medical financing, you can apply online or
through our network of more than 10,000 providers across the country.

No matter what kind of loan you’re interested in, everything is done
online, so the whole process is fast, convenient and private.

All loans facilitated by Lending Club are issued by a bank and subject
to the same consumer protection, fair lending, and disclosure
requirements as any other bank loan.

**Business Objective:**

The objective of this analysis to understand loans performance in
different dimensions. In order to understand loans performance the
company would like to do following analysis using available data.

Total Loan issuance by yearly & quarterly and calculate growth rate by
quarter on quarter and year on year

Percentage of loans based on reported loan purpose. (Note: Loan purpose
describes the reported intent of borrowers from the most recent
completed quarter and may not reflect actual usage. Investors should
rely on loan grades rather than loan purpose)

Loan Issuance by state –classify the states based on loan issuance by
\$50+ MM, \$25-50 MM, \$10-25 MM and \$0-10 MM

Find the last quarter average interest rates by different term loans
and overall

Find the historical returns by loan grade(Historical performance by
grade for all issued loans) and overall

Find the historical average interest rates by loan terms and loan
grades (also for overall)

What is percentage of loans by different loan grades by each year and
loan term level (also for overall)

What is the loan performance details by different loan grades and
overall

Find Net Annualized returns by vintage by different loan grades and
different loan terms (also for overall

What is loan status migration over 9 months (Net Charge offs: 120+days
delinquency)

**Input Data**

**Loans Data(4 Files):**

These files contain complete loan data for all loans issued through the
time period stated, including the current loan status (Current, Late,
Fully Paid, etc.) and latest payment information. The file containing
loan data through the "present" contains complete loan data for all
loans issued through the previous completed calendar quarter.

**Declined Loan Data(3 Files): **

These files contain the list and details of all loan applications that
did not meet Lending Club's credit underwriting policy.

**Detailed Data Dictionary: **

The Data Dictionary includes definitions for all the data attributes
included in the Historical data file and the In Funding data file.

**Expected outcome:**

As per basic expectations, you need to come up with the analysis as per
the business objective. Please refer analysis samples to get understand
the questions

**(Optional)** The data is very rich. You can come with many analysis
related to

Loans performance

Understanding on rejection of loans

Investor performance

Delinquency rates by each quarter or year

Prepayment rates by each quarter or year

Cumulative charge offs

***Solution:***

Let’s assume that the data resides in RDBMS and we will use Sqoop to
transfer the data to HDFS.

Using the following SQL statements, load the dataset onto MySQL:

CREATE TABLE IF NOT EXISTS LC\_loan\_stats(

id varchar(50),

member\_id varchar(50),

loan\_amnt varchar(10),

funded\_amnt varchar(10),

funded\_amnt\_inv varchar(10),

term varchar(50),

int\_rate varchar(50),

installment varchar(10),

grade varchar(50),

sub\_grade varchar(50),

emp\_title varchar(50),

emp\_length varchar(50),

home\_ownership varchar(50),

annual\_inc varchar(10),

verification\_status varchar(50),

issue\_d varchar(50),

loan\_status varchar(50),

pymnt\_plan varchar(50),

url varchar(200),

descr varchar(200),

purpose varchar(50),

title varchar(50),

zip\_code varchar(50),

addr\_state varchar(50),

dti varchar(10),

delinq\_2yrs varchar(5),

earliest\_cr\_line varchar(50),

inq\_last\_6mths varchar(5),

mths\_since\_last\_delinq varchar(5),

mths\_since\_last\_record varchar(5),

open\_acc varchar(5),

pub\_rec varchar(5),

revol\_bal varchar(50),

revol\_util varchar(50),

total\_acc varchar(5),

initial\_list\_status varchar(50),

out\_prncp varchar(5),

out\_prncp\_inv varchar(5),

total\_pymnt varchar(10),

total\_pymnt\_inv varchar(10),

total\_rec\_prncp varchar(10),

total\_rec\_int varchar(10),

total\_rec\_late\_fee varchar(10),

recoveries varchar(10),

collection\_recovery\_fee varchar(10),

last\_pymnt\_d varchar(50),

last\_pymnt\_amnt varchar(10),

next\_pymnt\_d varchar(50),

last\_credit\_pull\_d varchar(50),

collections\_12\_mths\_ex\_med varchar(5),

mths\_since\_last\_major\_derog varchar(5),

policy\_code varchar(50),

application\_type varchar(50),

annual\_inc\_joint varchar(10),

dti\_joint varchar(5),

verification\_status\_joint varchar(50),

acc\_now\_delinq varchar(5),

tot\_coll\_amt varchar(10),

tot\_cur\_bal varchar(10),

open\_acc\_6m varchar(5),

open\_il\_6m varchar(5),

open\_il\_12m varchar(5),

open\_il\_24m varchar(5),

mths\_since\_rcnt\_il varchar(50),

total\_bal\_il varchar(10),

il\_util varchar(5),

open\_rv\_12m varchar(5),

open\_rv\_24m varchar(5),

max\_bal\_bc varchar(10),

all\_util varchar(10),

total\_credit\_rv varchar(10),

inq\_fi varchar(5),

total\_fi\_tl varchar(5),

inq\_last\_12m varchar(5));

CREATE TABLE IF NOT EXISTS LC\_loan\_reject\_stats(

amount\_requested varchar(10),

application\_date varchar(50),

loan\_title varchar(50),

risk\_score varchar(5),

debt\_to\_income\_ratio varchar(50),

zip\_code varchar(50),

state varchar(50),

employment\_length varchar(50),

policy\_code varchar(50)

);

LOAD DATA INFILE '/home/cloudera/localdata/LCData/LoanStats3a.csv' INTO
TABLE LC\_loan\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES
TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/LoanStats3b.csv' INTO
TABLE LC\_loan\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES
TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/LoanStats3c.csv' INTO
TABLE LC\_loan\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES
TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/LoanStats3d.csv' INTO
TABLE LC\_loan\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES
TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/RejectStatsA.csv' INTO
TABLE LC\_loan\_reject\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/RejectStatsB.csv' INTO
TABLE LC\_loan\_reject\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\\n' IGNORE 2 LINES;

LOAD DATA INFILE '/home/cloudera/localdata/LCData/RejectStatsD.csv' INTO
TABLE LC\_loan\_reject\_stats FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\\n' IGNORE 2 LINES;

mysql&gt; select count(\*) from LC\_loan\_stats;

+----------+

| count(\*) |

+----------+

| 756897 |

+----------+

1 row in set (3.19 sec)

mysql&gt; select count(\*) from LC\_loan\_reject\_stats;

+----------+

| count(\*) |

+----------+

| 5398863 |

+----------+

1 row in set (3.47 sec)

Let’s use **Sqoop** now to load the data into **Hive**:

sqoop import \\

-m 1 \\

--connect jdbc:mysql://localhost/alabs \\

--username root \\

--password cloudera \\

--compression-codec snappy \\

--as-parquetfile \\

--warehouse-dir /user/hive/warehouse \\

--table LC\_loan\_stats \\

--split-by id \\

--hive-import

Check the table in hive:

hive&gt; select count(\*) from LC\_loan\_stats;

OK

756897

sqoop import \\

-m 1 \\

--connect jdbc:mysql://localhost/alabs \\

--username root \\

--password cloudera \\

--compression-codec snappy \\

--as-parquetfile \\

--warehouse-dir /user/hive/warehouse \\

--table LC\_loan\_reject\_stats \\

--hive-import

Check the table in hive:

hive&gt; select count(\*) from LC\_loan\_reject\_stats;

OK

5398863

We now have all the data loaded in Hive. Let’s create some views in hive
for analysis:

CREATE VIEW IF NOT EXISTS loananalysis AS

SELECT CAST(loan\_amnt AS DOUBLE) loan\_amnt,

CAST(funded\_amnt AS DOUBLE) funded\_amnt,

SUBSTR(term,1,3) loan\_term\_mnths,

CAST(REGEXP\_REPLACE(int\_rate,'\\%','') AS DOUBLE) int\_rate,

grade grade,

TO\_DATE(FROM\_UNIXTIME(UNIX\_TIMESTAMP(issue\_d,'MMM-yyyy')))
issue\_date,

loan\_status loan\_status,

purpose purpose,

UPPER(addr\_state) addr\_state,

CAST(total\_rec\_prncp AS DOUBLE) total\_rec\_prncp,

CAST(total\_rec\_int AS DOUBLE) total\_rec\_int,

TO\_DATE(FROM\_UNIXTIME(UNIX\_TIMESTAMP(last\_pymnt\_d,'MMM-yyyy')))
last\_pymnt\_date

FROM LC\_loan\_stats;

**Analysis using Hive:**

**--** Total Loan Issuance

SELECT sum(loan\_amnt) as total\_loan, year(issue\_date) as issue\_year

FROM loananalysis

GROUP BY year(issue\_date)

ORDER BY issue\_year;

![](./screenshots/media/image1.tiff){width="5.957624671916011in"
height="2.956521216097988in"}

-- Loan Issuance By State

SELECT sum(loan\_amnt) as total\_loan, addr\_state as state

FROM loananalysis

GROUP BY addr\_state

ORDER BY state;

![](./screenshots/media/image2.tiff){width="6.263606736657918in"
height="3.1478258967629045in"}

-- Loan Issuance By Purpose

SELECT sum(loan\_amnt) as total\_loan, purpose

FROM loananalysis

GROUP BY purpose

ORDER BY total\_loan DESC;

![](./screenshots/media/image3.tiff){width="6.166666666666667in"
height="6.736111111111111in"}

-- Yearly Average Interest Rate By Loan Term

SELECT avg(int\_rate) as avg\_int\_rate, loan\_term\_mnths,
year(issue\_date) as issue\_year

FROM loananalysis

GROUP BY loan\_term\_mnths, year(issue\_date)

ORDER BY issue\_year;

![](./screenshots/media/image4.tiff){width="6.263888888888889in"
height="6.217391732283464in"}

-- Grades over time

SELECT grade, count(grade), year(issue\_date) as issue\_year

FROM loananalysis

GROUP BY grade, year(issue\_date)

ORDER BY issue\_year;

![](./screenshots/media/image5.tiff){width="6.263888888888889in"
height="8.108333333333333in"}

-- Loan Performance

SELECT loan\_status, sum(loan\_amnt) as total\_loan\_amnt,
year(issue\_date) as issue\_year

FROM loananalysis

GROUP BY loan\_status, year(issue\_date)

ORDER BY issue\_year;

![](./screenshots/media/image6.tiff){width="6.263888888888889in"
height="6.704348206474191in"}

-- Loan Rejection By Purpose

SELECT loan\_title, count(\*) as applications

FROM lc\_loan\_reject\_stats

GROUP BY loan\_title

ORDER BY applications DESC;

![](./screenshots/media/image7.tiff){width="6.262869641294838in"
height="3.3391305774278215in"}

-- Loan Rejection Stats By Year

SELECT
year(TO\_DATE(FROM\_UNIXTIME(UNIX\_TIMESTAMP(application\_date,'yyyy-MM-dd'))))
as application\_year,

sum(amount\_requested) as loan\_amnt,

avg(CAST(risk\_score AS DOUBLE)) as avg\_risk\_score,

avg(CAST(REGEXP\_REPLACE(debt\_to\_income\_ratio,'\\%','') AS DOUBLE))
as avg\_DE\_ratio

FROM lc\_loan\_reject\_stats

GROUP BY
year(TO\_DATE(FROM\_UNIXTIME(UNIX\_TIMESTAMP(application\_date,'yyyy-MM-dd'))))

ORDER BY application\_year;

![](./screenshots/media/image8.tiff){width="6.263888888888889in"
height="2.657638888888889in"}

**Analysis using Tableau:**

![](./screenshots/media/image9.tiff){width="6.263888888888889in"
height="4.2972222222222225in"}

![](./screenshots/media/image10.tiff){width="6.263888888888889in"
height="4.102083333333334in"}

![](./screenshots/media/image11.tiff){width="6.263888888888889in"
height="4.127083333333333in"}

![](./screenshots/media/image12.tiff){width="6.263888888888889in"
height="4.136111111111111in"}

![](./screenshots/media/image13.tiff){width="6.263888888888889in"
height="4.138888888888889in"}

![](./screenshots/media/image14.tiff){width="6.263888888888889in"
height="4.10625in"}

![](./screenshots/media/image15.tiff){width="6.263888888888889in"
height="4.061805555555556in"}

![](./screenshots/media/image16.tiff){width="6.263888888888889in"
height="4.122916666666667in"}

![](./screenshots/media/image17.tiff){width="6.263888888888889in"
height="7.138194444444444in"}**\
**

![](./screenshots/media/image18.tiff){width="6.263888888888889in"
height="5.011111111111111in"}
