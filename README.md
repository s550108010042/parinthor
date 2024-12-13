select aaa.*
,DD1.[Call_Log] as 'Call_Log_1Day_CA'
,DD2.[Call_Log] as 'Call_Log_2Day_CA'
,DD3.[Call_Log] as 'Call_Log_3Day_CA'
,DD4.[Call_Log] as 'Call_Log_4Day_CA'
,DD5.[Call_Log] as 'Call_Log_5Day_CA'
,DD6.[Call_Log] as 'Call_Log_6Day_CA'
,DD7.[Call_Log] as 'Call_Log_7Day_CA'
,DD8.[Call_Log] as 'Call_Log_8Day_CA'
,DD9.[Call_Log] as 'Call_Log_9Day_CA'
,DD10.[Call_Log] as 'Call_Log_10Day_CA'
,DD11.[Call_Log] as 'Call_Log_11Day_CA'
,DD12.[Call_Log] as 'Call_Log_12Day_CA'
,DD13.[Call_Log] as 'Call_Log_13Day_CA'
,DD14.[Call_Log] as 'Call_Log_14Day_CA'
,DD15.[Call_Log] as 'Call_Log_15Day_CA'
 
    ,DDC1.[Call_Log] as 'Call_Log_1Day_C'
    ,DDC2.[Call_Log] as 'Call_Log_2Day_C'
    ,DDC3.[Call_Log] as 'Call_Log_3Day_C'
    ,DDC4.[Call_Log] as 'Call_Log_4Day_C'
    ,DDC5.[Call_Log] as 'Call_Log_5Day_C'
    ,DDC6.[Call_Log] as 'Call_Log_6Day_C'
    ,DDC7.[Call_Log] as 'Call_Log_7Day_C'
    ,DDC8.[Call_Log] as 'Call_Log_8Day_C'
    ,DDC9.[Call_Log] as 'Call_Log_9Day_C'
    ,DDC10.[Call_Log] as 'Call_Log_10Day_C'
    ,DDC11.[Call_Log] as 'Call_Log_11Day_C'
    ,DDC12.[Call_Log] as 'Call_Log_12Day_C'
    ,DDC13.[Call_Log] as 'Call_Log_13Day_C'
    ,DDC14.[Call_Log] as 'Call_Log_14Day_C'
    ,DDC15.[Call_Log] as 'Call_Log_15Day_C'

from [CI_Datawarehouse].[dbo].[Audit_No] aaa
left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, 0,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, 0,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD1 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD1.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -1,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -1,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD2 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD2.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -2,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -2,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD3 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD3.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -3,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -3,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD4 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD4.[Audit_Trail:_Audit_Trail_No.]
Left Join  
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -4,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -4,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD5 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD5.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -5,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -5,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD6 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD6.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -6,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -6,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD7 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD7.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -7,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -7,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD8 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD8.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -8,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -8,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD9 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD9.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -9,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -9,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD10 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD10.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -10,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -10,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD11 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD11.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -11,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -11,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD12 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD12.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -12,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -12,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD13 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD13.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -13,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -13,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD14 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD14.[Audit_Trail:_Audit_Trail_No.]
Left Join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -14,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on concat(aud.[Customer_Name],aud.[Emp_ID]) = concat(auc.[Customer_Name],auc.[agent_id])
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -14,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DD15 on aaa.[Audit_Trail:_Audit_Trail_No.] = DD15.[Audit_Trail:_Audit_Trail_No.]
 
 

left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, 0,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, 0,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC1 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC1.[Audit_Trail:_Audit_Trail_No.]



left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -1,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -1,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC2 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC2.[Audit_Trail:_Audit_Trail_No.]





left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -2,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -2,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC3 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC3.[Audit_Trail:_Audit_Trail_No.]




left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -3,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -3,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC4 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC4.[Audit_Trail:_Audit_Trail_No.]






left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -4,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -4,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC5 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC5.[Audit_Trail:_Audit_Trail_No.]



left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -5,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -5,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC6 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC6.[Audit_Trail:_Audit_Trail_No.]




left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -6,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -6,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC7 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC7.[Audit_Trail:_Audit_Trail_No.]



left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -7,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -7,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
        ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC8 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC8.[Audit_Trail:_Audit_Trail_No.]







left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -8,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -8,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC9 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC9.[Audit_Trail:_Audit_Trail_No.]




left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -9,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -9,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC10 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC10.[Audit_Trail:_Audit_Trail_No.]




left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -10,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -10,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC11 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC11.[Audit_Trail:_Audit_Trail_No.]





left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -11,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -11,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC12 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC12.[Audit_Trail:_Audit_Trail_No.]



left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -12,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -12,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC13 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC13.[Audit_Trail:_Audit_Trail_No.]





left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -13,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -13,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC14 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC14.[Audit_Trail:_Audit_Trail_No.]






left join
(
        Select
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date],
        MAX(res.[CLID]) as 'Call_Log'
        FROM
        (
                select
                aud.[Audit_Trail:_Audit_Trail_No.],
                aud.[Audit_Trail:_วันที่ที่สร้าง],
                aud.[Customer_Name],
                aud.[Emp_ID],
                concat(aud.[Customer_Name],aud.[Emp_ID]) as 'KEY',
                DATEADD(DAY, -14,  aud.[Audit_Trail:_วันที่ที่สร้าง]) as 'Min_date',
                auc.[CLID],
                auc.[Created_Date]
                From [CI_Datawarehouse].[dbo].[Audit_No] aud
                Left join [CI_Datawarehouse].[dbo].[Audit_Trail_Call] auc on aud.[Customer_Name]= auc.[Customer_Name]
                where  
                (auc.[Created_Date]>= DATEADD(DAY, -14,  aud.[Audit_Trail:_วันที่ที่สร้าง]) and auc.[Created_Date] <= aud.[Audit_Trail:_วันที่ที่สร้าง])
                ) res
        Group by
        res.[Audit_Trail:_Audit_Trail_No.],
        res.[Audit_Trail:_วันที่ที่สร้าง],
        res.[Customer_Name],
        res.[Emp_ID],
        res.[KEY],
        res.[Min_date]
) DDC15 on aaa.[Audit_Trail:_Audit_Trail_No.] = DDC15.[Audit_Trail:_Audit_Trail_No.];




