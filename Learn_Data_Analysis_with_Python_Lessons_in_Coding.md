![Hình ảnh bìa](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ1COQgFqot4sS02qwcvlsQHTq8vgbZPoKutg&s)

# Learn Data Analysis with Python 
## Lessons in Coding

Tác giả: A.J. Henley & Dave Wolf

Learn Data Analysis with Python: Lessons in Coding 
ISBN-13 (pbk): 978-1-4842-3485-3 ISBN-13 (electronic): 978-1-4842-3486-0 
https://doi.org/10.1007/978-1-4842-3486-0 
Library of Congress Control Number: 2018933537 
Copyright © 2018 by A.J. Henley and Dave Wolf 
his work is subject to copyright. All rights are reserved by the Publisher, whether the whole or 
part of the material is concerned, speciically the rights of translation, reprinting, reuse of 
illustrations, recitation, broadcasting, reproduction on microilms or in any other physical way, 
and transmission or information storage and retrieval, electronic adaptation, computer software, 
or by similar or dissimilar methodology now known or hereafter developed. 
Trademarked names, logos, and images may appear in this book. Rather than use a trademark 
symbol with every occurrence of a trademarked name, logo, or image we use the names, logos, 
and images only in an editorial fashion and to the beneit of the trademark owner, with no 
intention of infringement of the trademark. 
he use in this publication of trade names, trademarks, service marks, and similar terms, even if 
they are not identiied as such, is not to be taken as an expression of opinion as to whether or not 
they are subject to proprietary rights. 
While the advice and information in this book are believed to be true and accurate at the date of 
publication, neither the authors nor the editors nor the publisher can accept any legal 
responsibility for any errors or omissions that may be made. he publisher makes no warranty, 
express or implied, with respect to the material contained herein. 
Managing Director, Apress Media LLC: Welmoed Spahr 
Acquisitions Editor: Steve Anglin 
Development Editor: Matthew Moodie 
Coordinating Editor: Mark Powers 
Cover designed by eStudioCalamar 
Cover image designed by Freepik (www.freepik.com) 
Distributed to the book trade worldwide by Springer Science+Business Media New York, 233 
Spring Street, 6th Floor, New York, NY 10013. Phone 1-800-SPRINGER, fax (201) 348-4505, email 
orders-ny@springer-sbm.com, or visit www.springeronline.com. Apress Media, LLC is a 
California LLC and the sole member (owner) is Springer Science + Business Media Finance Inc 
(SSBM Finance Inc). SSBM Finance Inc is a Delaware corporation. 
For information on translations, please email editorial@apress.com; for reprint, paperback, or 
audio rights, please email bookpermissions@springernature.com. 
Apress titles may be purchased in bulk for academic, corporate, or promotional use. eBook 
versions and licenses are also available for most titles. For more information, reference our Print 
and eBook Bulk Sales web page at http://www.apress.com/bulk-sales. 
Any source code or other supplementary material referenced by the author in this book is available 
to readers on GitHub via the book’s product page, located at www.apress.com/9781484234853. 
For more detailed information, please visit http://www.apress.com/source-code.

Table of Contents 
Chapter 1: How to Use This Book����������������������������������������������������������1 
Installing Jupyter Notebook ����������������������������������������������������������������������������������1 
What Is Jupyter Notebook? �����������������������������������������������������������������������������2 
What Is Anaconda? ������������������������������������������������������������������������������������������ 2 
Getting Started ������������������������������������������������������������������������������������������������ 3 
Getting the Datasets for the Workbook’s Exercises�����������������������������������������4 
Chapter 2: Getting Data Into and Out of Python ������������������������������������5 
Loading Data from CSV Files��������������������������������������������������������������������������������� 5 
Your Turn����������������������������������������������������������������������������������������������������������7 
Saving Data to CSV �����������������������������������������������������������������������������������������������7 
Your Turn����������������������������������������������������������������������������������������������������������8 
Loading Data from Excel Files�������������������������������������������������������������������������������8 
Your Turn����������������������������������������������������������������������������������������������������������9 
Saving Data to Excel Files �����������������������������������������������������������������������������������10 
Your Turn��������������������������������������������������������������������������������������������������������11 
Combining Data from Multiple Excel Files ���������������������������������������������������������� 11 
Your Turn��������������������������������������������������������������������������������������������������������13 
Loading Data from SQL ��������������������������������������������������������������������������������������� 13 
Your Turn��������������������������������������������������������������������������������������������������������14 
www.allitebooks.com 
iv 
Saving Data to SQL ���������������������������������������������������������������������������������������������15 
Your Turn��������������������������������������������������������������������������������������������������������16 
Random Numbers and Creating Random Data ���������������������������������������������������16 
Your Turn��������������������������������������������������������������������������������������������������������18 
Chapter 3: Preparing Data Is Half the Battle���������������������������������������19 
Cleaning Data ������������������������������������������������������������������������������������������������������ 19 
Calculating and Removing Outliers ���������������������������������������������������������������20 
Missing Data in Pandas Dataframes��������������������������������������������������������������22 
Filtering Inappropriate Values������������������������������������������������������������������������ 24 
Finding Duplicate Rows ���������������������������������������������������������������������������������26 
Removing Punctuation from Column Contents ����������������������������������������������27 
Removing Whitespace from Column Contents ����������������������������������������������28 
Standardizing Dates ��������������������������������������������������������������������������������������29 
Standardizing Text like SSNs, Phone Numbers, and Zip Codes ���������������������31 
Creating New Variables ���������������������������������������������������������������������������������������32 
Binning Data �������������������������������������������������������������������������������������������������� 33 
Applying Functions to Groups, Bins, and Columns ����������������������������������������35 
Ranking Rows of Data �����������������������������������������������������������������������������������37 
Create a Column Based on a Conditional ������������������������������������������������������38 
Making New Columns Using Functions ��������������������������������������������������������� 39 
Converting String Categories to Numeric Variables���������������������������������������40 
Organizing the Data ��������������������������������������������������������������������������������������������42 
Removing and Adding Columns��������������������������������������������������������������������� 42 
Selecting Columns�����������������������������������������������������������������������������������������44 
Change Column Name ����������������������������������������������������������������������������������� 45 
Setting Column Names to Lower Case ����������������������������������������������������������47 
Finding Matching Rows ���������������������������������������������������������������������������������48 
Filter Rows Based on Conditions �������������������������������������������������������������������50 
TABLE OF CONTENTS TABLE OF CONTENTS 
www.allitebooks.com 
v 
Selecting Rows Based on Conditions ������������������������������������������������������������51 
Random Sampling Dataframe �����������������������������������������������������������������������52 
Chapter 4: Finding the Meaning ���������������������������������������������������������55 
Computing Aggregate Statistics��������������������������������������������������������������������������55 
Your Turn��������������������������������������������������������������������������������������������������������57 
Computing Aggregate Statistics on Matching Rows �������������������������������������������58 
Your Turn��������������������������������������������������������������������������������������������������������59 
Sorting Data �������������������������������������������������������������������������������������������������������� 59 
Your Turn��������������������������������������������������������������������������������������������������������60 
Correlation ����������������������������������������������������������������������������������������������������������60 
Your Turn��������������������������������������������������������������������������������������������������������62 
Regression ���������������������������������������������������������������������������������������������������������� 62 
Your Turn��������������������������������������������������������������������������������������������������������63 
Regression without Intercept ������������������������������������������������������������������������������64 
Your Turn��������������������������������������������������������������������������������������������������������64 
Basic Pivot Table �������������������������������������������������������������������������������������������������65 
Your Turn��������������������������������������������������������������������������������������������������������68 
Chapter 5: Visualizing Data ����������������������������������������������������������������69 
Data Quality Report ��������������������������������������������������������������������������������������������� 69 
Your Turn��������������������������������������������������������������������������������������������������������71 
Graph a Dataset: Line Plot �����������������������������������������������������������������������������������71 
Your Turn��������������������������������������������������������������������������������������������������������74 
Graph a Dataset: Bar Plot ������������������������������������������������������������������������������������74 
Your Turn��������������������������������������������������������������������������������������������������������76 
Graph a Dataset: Box Plot �����������������������������������������������������������������������������������76 
Your Turn��������������������������������������������������������������������������������������������������������79 
TABLE OF CONTENTS TABLE OF CONTENTS 
www.allitebooks.com 
vi 
Graph a Dataset: Histogram ��������������������������������������������������������������������������������79 
Your Turn��������������������������������������������������������������������������������������������������������82 
Graph a Dataset: Pie Chart ����������������������������������������������������������������������������������82 
Your Turn��������������������������������������������������������������������������������������������������������86 
Graph a Dataset: Scatter Plot ������������������������������������������������������������������������������86 
Your Turn��������������������������������������������������������������������������������������������������������87 
Chapter 6: Practice Problems �������������������������������������������������������������89 
Analysis Exercise 1 ���������������������������������������������������������������������������������������������89 
Analysis Exercise 2 ���������������������������������������������������������������������������������������������90 
Analysis Exercise 3 ���������������������������������������������������������������������������������������������90 
Analysis Exercise 4 ���������������������������������������������������������������������������������������������91 
Analysis Project ��������������������������������������������������������������������������������������������� 91 
Required Deliverables �����������������������������������������������������������������������������������93 
Index ���������������������������������������������������������������������������������������������������95

