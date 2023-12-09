# Employees Presence Insight

## Problem Statement
AtliQ Technologies is a fast growing software and data solution company in India, the HR of the company wants to know the working preferences of employees from the employees presence data. Consuming huge Excel data was not easy and the HR found difficulty in taking some critical decisions which are dependent on the employees presence onsite. So, the HR along with other stakeholders decided to hire a data analyst and develop a dashboard in Power BI for their quick decision making regarding their business needs.

### Requirements from the Stakeholders
1. What is the working preferences of employees; work from home or work from office?
2. What is the reason behind work from home?
3. Which day in a week are employees present the most?
4. Which days in a week employees prefer WFH the most?

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
- The final sheet is the table combining all the 3 sheets - April 2022, May 2022, June 2022

- **Created Calculated Columns in the table using DAX**
  - WFH Count = SWITCH(TRUE(),      
  'Final Data'[Value] = "WFH",1,      
  'Final Data'[Value] = "HWFH",0.5,0)

  - SL Count = SWITCH(TRUE(),        
  'Final Data'[Value] = "SL",1,        
  'Final Data'[Value] = "HSL",0.5,0)

  - Month = STARTOFMONTH('Final Data'[Date])     

### Created Dashboard
![employee](https://github.com/guddushah/HR-Data-Analytics-PowerBI/assets/40028193/cacae0aa-6789-4f11-9f94-cd5cd4b0d863)

### Dashboard Live here
https://app.powerbi.com/view?r=eyJrIjoiZmY0Nzc3NWYtMjM4Zi00ODliLTk0ZmQtNDgzYzBmMWJlYjcwIiwidCI6Ijc5OWU3OTRjLTllYWMtNGUxZi05ZjY0LTE0ODhjYjMyMjRlNiJ9

## Key Insights Obtained from the Dashboard
1. On average, Employees work 10 % of the total working days from home, for example, out of 100 working days people prefer 10 days work from home.
2. The reason behind 10 % WFH, is some people only work from home and some of them ends of working half of the time from home.
3. Employees are mostly present on Monday of a week.
4. Thursday and Friday are the days in a week when mostly employees prefer WFH.
5. The Employees presence is slowly declining every month.
6. WFH is slightly increasing every month.
7. Employees taking sick leaves are increasing every month.
8. On average, employees are taking most of sick leaves on Monday.

   
### Creating Measures using DAX
1. **Total Working Days**      
- Total Working Days =       
  Var totaldays = COUNT('Final Data'[Value])     
  Var normworkdays = CALCULATE(COUNT('Final Data'[Value]),'Final Data'[Value] in {"WO", "HO"})      
  return       
  totaldays-normworkdays

2. **WFH**                 
   WFH = SUM('Final Data'[WFH Count])            
    
2. **Present Days**              
   Present Days=               
   Var presentdays = CALCULATE(COUNT('Final Data'[Value]),'Final Data'[Value] in {"P"})               
   RETURN               
   presentdays + [WFH]                 

4. **Presence %**               
   Presence % = DIVIDE([Present Days],[Total Working Days],0)

5. **WFH %**             
   WFH % = DIVIDE([WFH],[Present Days],0)

6. **SL**      
   SL = SUM('Final Data'[SL Count])

7. **SL %**        
   SL % = DIVIDE([SL],[Present Days],0)    
