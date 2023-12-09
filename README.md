# HR Data Analytics

## Problem Statement
AtliQ Technologies is a fast growing software and data solution company in India, the HR of the company wants to know the working preferences of employees from the employees presence data. Consuming huge Excel data was not easy and the HR found difficulty in taking some critical decisions which are dependent on the employees presence onsite. So, the HR along with other stakeholders decided to hire a data analyst and develop a dashboard in Power BI for their quick decision making regarding their business needs.

### Requirements from the Stakeholders
- What is the working preferences of employees; work from home or work from office?
- What is the reason behind work from home?
- Which day in a week are employees present the most?
- How can we optimize the woking space in the office and save cost on infrastructure?
- What are the reasons behind majority of people taking sick leaves?

### Attendance Key	
- **P**	- Present 
- **PL** - Paid Leave 
- **SL**	- Sick Leave 
- **HPL**	- Half day PL 
- **HSL**	- Half day SL
- **WFH**	- Work from home 
- **FFL**	- Floting festival leave 
- **HFFL**	- Half Day Floting festival leave 
- **BL** 	- Birthday Leave 
- **LWP**	- Leave without pay
- **HLWP** - Half day Leave without pay
- **BRL** - Bereavement Leave
- **HBRL** - Half Bereavement Leave
- **HWFH**	- Half Work From Home
- **WO**	- Weekly Off
- **HO**	- Holiday Off
- **ML**	- Menstrual Leave
- **HML**	- Half Day ML

### Dataset
Attendance Sheet 2022-2023_Masked 
- Contains 3 attendance sheets - April 2022, May 2023, June 2022 

### Data Transformation in Power Query
- Imported all the sheets in the Power Query.
- Performed data transformation and unpivoted all the date columns into single column in April 2022 sheet.
- Created New Parameter using the current sheet for filtering rows.
- Created a function that encapsulates all the data transformation steps performed above.
- Added the newly created function as a calculated column across all 3 sheets.
- Then deleted some columns which were not important, final sheet had 5 columns (Sheet Name, Employee Code, Name, Date, Value).
- The final sheet was the sheet combining all the 3 sheets - April 2022, May 2022, June 2022


