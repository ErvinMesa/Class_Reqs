# Class_Reqs

## WIP
- [ ] [DASTAL Queues](https://docs.google.com/document/d/1WRBgfmJ1TAKNn47L4OvfOVO3DYKf3Tu4epAfXlw58G0/edit?usp=sharing)
- [ ] [DASTAL ]()

## DONE

- [X] [ReEd](https://docs.google.com/document/d/1-_dCrdQAShw1eHxAJvTA1ClS03o5Zj4qekpMVFkEbGI)


DECLARE @m DATE = '2018-12-31';

use BillingCollection;

SELECT DISTINCT
	FORMAT(EOMONTH('2018-12-31'), N'MMMM dd, yyyy') as From_Date,
	Acct_No,
	(SELECT SUM(Amount) FROM Ledgers WHERE Trans_Date BETWEEN DATEADD(MONTH,-2,EOMONTH(@m)) AND DATEADD(MONTH,-1,EOMONTH(@m)) AND Acct_No = '0111200630') as Day30,
	(SELECT SUM(Amount) FROM Ledgers WHERE Trans_Date BETWEEN DATEADD(MONTH,-3,EOMONTH(@m)) AND DATEADD(MONTH,-2,EOMONTH(@m)) AND Acct_No = '0111200630') as Day30to60,
	(SELECT SUM(Amount) FROM Ledgers WHERE Trans_Date BETWEEN DATEADD(MONTH,-4,EOMONTH(@m)) AND DATEADD(MONTH,-3,EOMONTH(@m)) AND Acct_No = '0111200630') as Day60to90,
	(SELECT SUM(Amount) FROM Ledgers WHERE Trans_Date < DATEADD(MONTH,-4,EOMONTH(@m)) AND Acct_No = '0111200630') as Day90Above
	FROM Ledgers led WHERE Acct_No = '0111200630';
