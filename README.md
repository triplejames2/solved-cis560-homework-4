Download Link: https://assignmentchef.com/product/solved-cis560-homework-4
<br>
The purpose of this exercise is to gain practice with data modification. Using the below diagram as your database schema to answer the questions below. You will be able to execute these scripts against your own database on <a href="http://mssql.cs.ksu.edu"><em>mssql.cs.ksu.edu</em></a><em>, </em>or a new one you create if you installed SQL Server on your own machine.

<strong>Database Diagram</strong>

Reference this diagram as you answer the questions below.

<table>

 <tbody>

  <tr>

   <td colspan="2" width="61">Club</td>

   <td width="36"> </td>

   <td colspan="2" width="61">Meeting</td>

   <td width="36"> </td>

   <td colspan="2" width="61">MeetingAttendee</td>

   <td width="36"> </td>

   <td colspan="2" width="61">Attendee</td>

  </tr>

  <tr>

   <td width="14">PK</td>

   <td width="47">ClubId</td>

   <td width="36"> ________________ PK</td>

   <td width="21"> </td>

   <td width="40">Meetingld</td>

   <td width="36">I        I 0&lt;</td>

   <td width="25">PK, FK1</td>

   <td width="36">Meetingld</td>

   <td width="36">I I</td>

   <td width="15">PK</td>

   <td width="46">Attendeeld</td>

  </tr>

  <tr>

   <td width="14">UK</td>

   <td width="47">Name</td>

   <td width="36"> </td>

   <td width="21">UK, FK</td>

   <td width="40">ClubId</td>

   <td width="36"> </td>

   <td width="25">PK, FK2</td>

   <td width="36">Attendeeld</td>

   <td width="36"> </td>

   <td width="15">UK</td>

   <td width="46">Email</td>

  </tr>

  <tr>

   <td width="14"> </td>

   <td width="47">Purpose</td>

   <td width="36"> </td>

   <td width="21">UK</td>

   <td width="40">MeetingTime</td>

   <td width="36"> </td>

   <td width="25"> </td>

   <td width="36">CreatedOn</td>

   <td width="36"> </td>

   <td width="15"> </td>

   <td width="46">FirstName</td>

  </tr>

  <tr>

   <td width="14"> </td>

   <td width="47">CreatedOn</td>

   <td width="36"> </td>

   <td width="21"> </td>

   <td width="40">Location</td>

   <td width="36"> </td>

   <td colspan="2" width="61"> </td>

   <td width="36"> </td>

   <td width="15"> </td>

   <td width="46">LastName</td>

  </tr>

  <tr>

   <td width="14"> </td>

   <td width="47">UpdatedOn</td>

   <td width="36"> </td>

   <td width="21"> </td>

   <td width="40">CreatedOn</td>

   <td colspan="4" width="134"> </td>

   <td width="15"> </td>

   <td width="46">CreatedOn</td>

  </tr>

  <tr>

   <td colspan="2" width="61"> </td>

   <td width="36"> </td>

   <td width="21"> </td>

   <td width="40">UpdatedOn</td>

   <td colspan="4" width="134"> </td>

   <td width="15"> </td>

   <td width="46">UpdatedOn</td>

  </tr>

 </tbody>

</table>




<strong>Questions</strong>

Write SQL solutions to the following four questions. You can submit them all in one file clearly indicating the question with a comment, or you can submit in multiple files.

<strong>Question 1</strong>

<strong>20 points – </strong>Write the SQL to create each of the tables in the above diagram, using the below requirements.

<ul>

 <li>Create all tables in a schema named “Homework4”. This schema can be created using the <strong>CREATE SCHEMA </strong></li>

</ul>

CREATE SCHEMA Homework4;

Such as statement must be the only one in a batch. For simplicity, then, you <strong>do not need to turn this statement in with your homework. </strong>You can execute it with it being the only statement in your session, or you select this statement only before executing. You may delete it once you’ve executed it.

<ul>

 <li>For data types, you can use the following:</li>

 <li><strong>INT </strong>for all identifiers.</li>

</ul>

■ Also, use the <strong>IDENTITY </strong>property on primary keys rather than a sequence object.

<ul>

 <li><strong>DATETIME2(0) </strong>for <em>MeetingTime</em></li>

 <li><strong>DATETIMEOFFSET </strong>for all columns named <em>CreatedOn </em>and <em>UpdatedOn</em></li>

 <li><strong>NVARCHAR </strong>for all other fields – I’ll let you determine the appropriate maximum number of characters for the <strong>NVARCHAR </strong></li>

 <li>Other column requirements:</li>

 <li>Use the <strong>IDENTITY </strong>property on primary keys rather than a sequence object.</li>

</ul>




11/12/2018                                                                                                                                                                                        Homework 4

o All columns named <em>CreatedOn </em>and <em>UpdatedOn </em>should have a default constraint to capture the current date/time. o All columns should disallow nulls, accomplished by using <strong>NOT NULL.</strong>

We have seen a few different ways to define constraints, but you can use the simple form as in this example.

CREATE TABLE Demo.Person

(

Personld INT NOT NULL IDENTITY(1, 1) PRIMARY KEY, FirstName NVARCHAR(32) NOT NULL,

LastName NVARCHAR(32) NOT NULL,

IsEmployee BIT NOT NULL DEFAULT(0),

Organizationld INT NOT NULL FOREIGN KEY

REFERENCES Demo.Organization(Organizationld),

UNIQUE

(

FirstName ASC, LastName ASC

)

);

Keep in mind that your tables will need to be created in such a way that the tables <em>referenced </em>by foreign keys are created before the tables <em>with </em>foreign keys.

Question 2

<strong>15 points – </strong>Write an insert statement to create two clubs, and a second insert statement to create two meetings for each club (total of 4 meetings). Here is the information for the clubs.

<table>

 <tbody>

  <tr>

   <td width="985"><strong>Name                                                                                                                                                                             </strong><strong>Purpose</strong>ACM               The Association for Computing Machinery is the professional organization for computer scientists.MIS Club                  The Kansas State MIS Club is a student driven organization focused on the management of information systems.</td>

  </tr>

 </tbody>

</table>

Meeting times and location.

When inserting the meetings, do not make any assumptions regarding the <em>ClubId. </em>Start with a derived table providing the information in the second table above, then join to the <strong>Club </strong>table on the name to obtain the <em>ClubId.</em>




Question 3




11/12/2018                                                                                                                                        Homework 4

<strong>10 points – </strong>Write two insert statements to create yourself as an attendee, and that you attended the ACM meeting on October 9, 2018. Use your name and KSU email address for the insertion. Again, do not make an assumption regarding what the automatically generated <em>Attendeeld </em>will be, but since you are just inserting one attendee, you can use a function to obtain the generated <em>Attendeeld.</em>

<strong>Question 4</strong>

<strong>5 points – </strong>Write an update statement to modify the location of the meeting on December 4, 2018 of the MIS Club. The new meeting location should be “Business Building 4001”. Don’t forget to update the <em>UpdatedOn </em>column. Your query should only use the literals for the club name, meeting date/time, and the new location, making no assumptions on identifiers.

<strong>Helpful Tips</strong>

As you work on your solutions, here are a couple tips that you may find useful.

<strong>Refreshing Intellisense</strong>

After creating a new schema or table, IntelliSense, which supports auto-complete while typing, doesn’t always detect the new objects right away, especially if you are trying to use the new objects in a different session than where you created them. In SQL Server Management Studio, you can force it to refresh the cache by using <em>Edit —&gt; IntelliSense -‘ Refresh Local Cache. </em>As a shortcut, I typically just use <em>Ctrl+Shift-FR.</em>

<strong>Recreating Tables</strong>

If you find that you made a mistake and need to re-create your table(s), then you need to drop the table first, using a <strong>DROP TABLE </strong>statement, such as:

DROP TABLE Demo.Person;

Of course, if there is another table referencing the table you need to drop, then you will need to drop it as well. For our purposes, this is the simplest approach since re-creating our tables is painless.

Because recreating our tables is painless, you may also keep a <strong>DROP TABLE </strong>statement using the <strong>IF EXISTS </strong>condition at the top of your script. This will drop the table if it exists, then your <strong>CREATE TABLE </strong>statements should always work.

Let’s look at an example with two tables, <em>Demo.A </em>and <em>Demo.B. </em>The table <em>Demo.B </em>references <em>Demo.A </em>with a foreign key constraint. We will precede the <strong>CREATE TABLE </strong>statements with the conditional <strong>DROP TABLE </strong>statements in reverse order, so there will be no dependency on <em>Demo.A </em>when attempting to drop it.

DROP TABLE IF EXISTS Demo.B;DROP TABLE IF EXISTS Demo.A;

CREATE TABLE Demo.A

(

&lt;column and constraint definitions here&gt;

);

CREATE TABLE Demo.B

(

&lt;column and constraint definitions here&gt;,

);








