## Navigation

##### Design of Computing Algorithms - COS 485
Link: https://github.com/cpr016-school-projects/Algorithms

##### Capstone - Object Oriented Design and Programming - COS 420
Link: https://github.com/cpr016-school-projects/Capstone

##### Mobile Application Development - COS 470
Link: https://github.com/cpr016-school-projects/Mobile-App-Development

##### Computer Graphics - COS 452
Link: https://github.com/cpr016-school-projects/Computer-Graphics

##### Database Systems - COS 457
Link: https://github.com/cpr016-school-projects/Database-Systems

##### Graphical User Interface Design - COS 368
Link: https://github.com/cpr016-school-projects/GUI-Design

---

# Database Systems - COS 457
There are three primary objectives of the course. The first is to
acquaint the students with the purposes, concepts, and terminology
associated with database management systems, so that the student
understands what functions these systems provide. In particular,
the course teaches the data definition, data manipulation, and control
features of the standard relational language, SQL, especially its
querying capability via the SELECT statement.

The second purpose is to instruct the student in a design methodology
for the development of specific databases using commercial database
system packages. Particular attention is paid to conceptual or semantic
modeling of the application in the design and to rational choice of
physical file structures. Included in this area are the features of
the Entity-Relationship(ER) model, the relational model, and functional
dependency theory.

The course will also provide the student with knowledge of the
languages and techniques for making a database accessible over the 
internet, and discuss the SQL injection attack hazard in connection
with the JDBC interface to databases.



## Querying Assignment

QUERY SPECS FOR FIFTEEN(15) QUERIES
===================================

1. Produce a table with columns sname, age and stname for all senators who are
either female Republicans greater than 50 years old or male Democrats
less than 50 years old.

Eliminate duplicates and order by sname.

2. Produce a table with all sextuples 
(stname, cname, sname, age, totrev, population) where sname and cname are
from the same state and that state is stname, the total revenue of the 
corporation is more than three halfs of the population of the state and 
the senator is a female Democrat.

Eliminate duplicates and order by stname, cname, and sname.


3. Produce a table with all (cname, legnum, sname) triples where
sname sponsors legnum, legnum favorably affects cname, cname has 
contributed to sname, and cname and sname are from different states,
and sname is a Republican and cname has total revenue >= 10,000,000


Eliminate duplicates and order by cname, legnum, sname.

To obtain full credit you must use (inner) joins of all the needed
tables in the from clause, and impose filtering conditions that refer
to single tables in the where clause.

4. Produce a table with all (cname, u, v, w, x, y, z) septuples
where cname is the name of a corporation that has made at least one
contribution and whose average contribution is at least as large as
the average of all contributions, and

u is the date of the first contribution by cname
v is the date of the most recent contribution by cname
w is number of contributions cname has made
x is the sum of the amounts of those contributions
y is the average amount of those contributions
z is the number of different senators that cname has contributed to

You may assume that the contributes table is not empty, so there will
be an average contribution amount.

Eliminate duplicates and order by cname.

To obtain full credit you must use group by with aggregate operators
and a having clause to filter the groups.

5. Produce a table with all (sname, u, v, w, x) quintuples where sname
is a senator and the rest are boolean values, specifically

u is true if sname sponsors a bill, else false
v is true if sname opposes a bill, else false
w is true if sname has received a contribution else false
x is true if sname has cast a vote that is either Yea or Nay, else false

Eliminate duplicates and order by sname.

To obtain full credit you use outer joins in the from clause, no where 
clause filter, and appropriate expressions in the select list to obtain the
other columns.  No need to aggregate here and no aggregate operators should
be used.

6. Produce a table with all sextuples (sname, u, v, w, x, y, z)
where sname is a senator and

u is the number of s (identified by a (legnum, vdate) pair
  that the senator attended and cast a vote (including Abstain)
v is the number of times the senator voted Yea on a roll call
w is the number of times the senator voted Nay on a roll call
x is the date of the most recent Yea vote cast, or 'n/a' if v is 0
y is the date of the most recent Nay vote cast, or 'n/a' if w is 0
z is the date of the earliest Abstain vote cast, or 'n/a' if sname
  never voted Abstain

Eliminate duplicates and order by sname.

To obtain full credit you must use outer join with group by and
aggregate operators.

Every senator should have exactly one row.

Hint: you can use the case expression within the aggregate expression to
obtain some of the counts that involve filters.  Some may require you
to cast the result to varchar before using coalesce.


7. Produce a table with all (cname, u, v, w, x, y, z)
septuples where cname is the name of a corporation and

u is the number of distinct senators that cname has contributed to
v is the maximum, over all sums of contributions to individual senators,
  that cname made, that is, suppose you had a table with two columns

  senator1   sum of cname's contributions to senator1
  senator2   sum of cname's contributions to senator2
  senator3   sum of cname's contributions to senator3
  ... 

  v would be the maximum of the second column, or 0 if
  cname made no contributions to any senators
w is like v, only the minimum of the second column; again, 0 if
  cname made no contributions to any senator
x is the average of all contributions cname has made, 0 if
  none were made
y is the count of bills that favorably affect cname
z is the count of bills that unfavorably affect cname

Eliminate duplicates and order by cname.

To obtain full credit, the query should have the structure

select c.cname,
   (nested selected for u) as u,
   coalesce((nested select for v), 0) as v,
   ...etc.
from corporations c
order by c.cname;

that is, all the values u through z must be obtained within the
select list using primarily nested select statements with an 
external reference to c.cname.  Most are straightforward.
v and w are quite tricky, but can be accomplished with 
a group by including a having clause which uses the
relationalOp all to find the maximum and minimum of the sums.



8.  A table with all (sen1, sen2) pairs where sen1 and sen2 are two
different senator snames, with sen1 < sen2, and sen1 and sen2 were 
present for exactly the same subset of roll calls, that is for 
every roll call rc, sen1 cast a vote in rc iff sen2 cast a vote in rc.
Recall, a roll call is identified by a (legnum, vdate) pair that 
occurs in a row of the votes table.

Eliminate duplicates and order by sen1, sen2.

To obtain full credit, you must use the not exists contruct.

Note, this defines an equivalence relation on senators.

Hint: basically you do not want to find a roll call where sen1 voted
and sen2 did not, nor a roll call where sen2 voted and sen1 did not.

9. A table with all sname values such that for every bill x,
if x has ever been the subject of a roll call vote, then 
sname has voted on some roll call vote involving x. Note,
if the bill x was voted on in >1 roll call, sname need not
have cast a ballot in all of the roll calls, but just in some
one of them.

Eliminate duplicates and order by sname.

To obtain full credit you must use exists/not exists.

Hint:  the following set up can be made to work

select x.sname
from senators x
where  not exists(select 1
                  from legislation y
                  where y has been voted on in some roll call
                     and x has never cast a ballot on a roll call
                         involving y
                 )
order by x.sname;

with appropriate nested queries with external references to x and
and y.

10. All (cname, ageave) where cname is a corporation and ageave is the average
age for the set of senators who have voted Yea in a roll call involving some
bill favorably affecting cname or Nay in a roll call on some bill unfavorably
affecting cname and whom cname has contributed to.  
If that set is empty, ageave should be 0.

Eliminate duplicates and order by cname.


11. All (sname, sum) where sname is a senator, and sum is the sum of
all contributions to sname from corporations who are favorably affected
by some bill that sname sponsors.  Note, sum should be 0 if sname does
not sponsor any bills or there are no such contributions to sname from 
corporations favorably affected by a bill sname sponsors.

Eliminate duplicates and order by sname.


12. Redo #7 using the WITH construct to contruct two initial tables.  One
with all (cname, sname, sum) triples where cname is a corporation, sname
is a senator, and sum is the sum of all contributions from cname to sname,
or 0 if there are none, the other with all 
(cname, favaffecting, unfavaffecting) triples where cname is a corporation
and the other two components are y and z from #7.  Use the same column
labels from #7 so the results should be identical.

Eliminate duplicates and order by cname.

Hint: even with the two precalculated tables, you will need to do a nested
select to obtain the average of all contributions made by the corporation.

13. Recall a roll call is identified by (vdate, legnum) pair that occurs
in a row of votes.  Produce a table with all

(vdate, legnum, ryeas, rnays, rabs, dyeas, dnays, dabs, oyeas, onays, oabs)

eleven-tuples where vdate,legnum are a roll call, ryeas is the count of
Republican Yea votes on that roll call, rnays the count of Republican Nays,
rabs is the count of Republican Abstains, and the d- and o- columns
are the analogous counts for the Democrats and neither Republican
nor Democrat categories (o for "other").

Eliminate duplicates and order by vdate, legnum.

There are many ways to do this, but the slickest and perhaps most efficient is
to do a single group by on votes joined with senators using clever case
expressions to count the correct values for the tally columns.


14. This query is intended to measure the extent of partisanship on
a particular roll call vote, that is, mark the vote as showing
a great partisan divide.  Ignore abstentions, and for each roll call
count the Yea's and Nay's for the two major parties, Democrat and Republican.
Produce a table of (legnum, vdate, w, x, y, z, partisan) septuples where

a. legnum, vdate identify the roll call
b. w is 'Yea' if the there were more Democratic Yea votes than Nay votes,
   'Nay' if more Democratic Nay votes than Yea votes, and 'Even' if the counts were
   the same.
c. x is the fraction of Democratic vote counts that went with the prevailing
   vote of the party, or 0.500, if the the counts were even; for example, 
   suppose there were 30 Democrat Yeas and 10 Democrat Nays.  Then
   30/(30 + 10), which is 0.75, is the fraction of the vote that went with
   the prevailing vote.
d. y is analogous to w, but for Republicans
e. z is analogous to x, but for Republicans
f. partisan is true exactly when w and y are neither of them  'Even' and are
   not equal, and x and z are both >= 0.6

Eliminate duplicates and order by legnum and vdate.

Hint: You should be able to adapt the solution to the previous query to
obtain this.  Use the WITH construct to build up to the result.  To get
accurate results you should cast the operands to the division the numerator
when w is not 'Even' to double precision, for example

cast(dyeas to double precision)/(dyeas + dnays)

Integer division would truncate and the result would always be 0 or 1.  Note,
if the denominator were 0, then the yeas and nays would both be 0, so w would
be 'Even'.  Do not perform the division when the counts are equal, and you
will never divide by 0.


15. Recall, every roll call is identified by a legnum and a vdate.  

Produce a table with a row for each roll call with columns

vdate of the roll call

legnum of the roll call

moneyfor   the sum of all contributions made strictly prior to the roll call
by corporations favorably affected by legnum(0 if none)

moneyagainst  the sum of all contributions made strictly prior to the roll 
call by corporations unfavorably affected by legnum(0 if none) 

passed  true if the count of Yea votes in the roll call is greater than the sum of the
counts of Nay and Abstain votes in the roll call, else false

moneyTalks true if (moneyfor > moneyagainst and passed) or (moneyagainst >
moneyfor and passed = false), else false

Eliminate duplicates and order by vdate, legnum.


You should use WITH to build up to this gradually.