TKDIS BASH UTILS
=================

Small bash utilities for handling TKDIS format that e-banks (at least here in Slovenia) still use the most.

Commands
--------

	tkdis2tsv - get tab separated data from fixed width
	tkdis2tsv short - get only the rows that seem generally usefull

	income - filter just income

	amount-more X - pass thru transactions with amount more than X
	amount-less Y - pass thru transactions with amount less than Y

	sort-by-company - as named

	sum-amounts - sum amounts by company
	sum-amounts ext - sum amounts by grouping and showing transactions and summing them


Few examples
------------

count payments by companies (alphabetically sorted)

	cat sample.tkdis | ./tkdis2tsv short | ./income | ./amount-more 8 | ./amount-less 50 | ./sort-by-company | cut -f 19 | uniq -c


using additional command to sum / count transactions
	
	cat sample.tkdis | ./tkdis2tsv short | ./income | ./amount-more 8 | ./amount-less 50 | ./sum-amounts

Output:

	1      9.8	       MOJE PODJETJE DOO
	1      9.8	       AGENCIJA JUG TIMOTEJ BAN S.P.
	2      58.8	       METELKO ROBERTA S.P.
	1      9.8	       ZETA VARNOST IN ZASCITA DOO
	SUM:   5502.2

get sums of all income invoices between 2 prices

	cat sample.txt | ./tkdis2tsv short | ./income | ./amount-more 8 | ./amount-less 50 | ./sum-amounts ext > sums.tsv

Output:

	101000048385244	20	10.08.12	9.8	0001252012	PIPAN POP	METELKO ROBERTA S.P.
	101000048385244	20	11.05.12	9.8	00522012	PIPAN POP	METELKO ROBERTA S.P.
	101000048385244	20	14.05.12	9.8	00522012	PIPAN POP	METELKO ROBERTA S.P.
	101000048385244	20	17.05.11	20.55	11001223	PIPAN POP	METELKO ROBERTA S.P.
	101000048385244	20	25.11.11	9.8	11005841	PIPAN POP	METELKO ROBERTA S.P.
			12	128.35	

	031141000099193	20	08.03.12	40.8	00262012	JURCKA 1	ZAVOD ZA RAZVOJ VESELJA
	031141000099193	20	19.09.11	40.8	11003423	JURCKA 1	ZAVOD ZA RAZVOJ VESELJA
				ALL:	177	5148.27


# open TSV file with libreoffice

	libreoffice --calc sums.tsv &

# this will be also usefull to import bank data in http://www.cebelca.biz
