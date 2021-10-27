# HBase Shell Commands

# HBase provide 4 dimension data model
 They are Row key,Column,Column family,Timestamp
1.) Row key :- Uniquely indentifies a row.
2.) Column family :- Can have different Columns for each row.
3.) Column :- Columns are units with in a column family.
4.) TimeStamp :- Used as the version no. for the values stored in a column .

# open HBase Shell -> hbase shell

# Show tables :- list

# create table student with 3 column  :-  create 'students','personal_details','contact_details','marks'

# Adding records using put :- 
 i) put 'students','student1','personal_details:name','Gaurav Rawat'
 ii) put 'students','student1','personal_details:email','gaurav141999@gmail.com'

# To see all the record of student table :- scan 'students'
  scan will give a range of rows or all the rows .However if you want specific row then use get.
  
# Just display personal details for student1
  get 'students','student1',{COLUMN => 'personal_details'}
  
# Just display personal details for particular column family
 get 'students','student1',{COLUMN => 'personal_details:name'}

# delete email id column for student1
  delete 'students','student1','personal_details:email'

# describe
  describe 'students'
 
# Table exists or not
  exists 'students'
 
# Drop table
To drop a table we need to disable it first
The data is present in memstore and flush has not happened.When we disable the table the content of  memstore is flushed to the disk and then we can drop the table
command :- disable 'student'
           drop 'student'
           
# Get names in the records
  scan 'census',{COLUMNS => ['personal_details:name']}
  
# Limit
  scan 'census',{COLUMNS => ['personal_details:name'],LIMIT => 1}
 
# StartRow and StopRow
  scan 'census',{COLUMNS => ['personal_details:name'],LIMIT => 1,STARTROW => "1",STOPROW => "3"}

# Count :- counts no. of records
 count 'students'

# Filter
Some Commonly used filter function are :-
i.) Value Filter
ii.) Qualifier Filter
iii.) Family Filter

These filters are like Java methods which take two input parameters- a logical operator and a comparator.

scan 'census',{FILTER => "ValueFilter(=,'binary:Maries')"}
scan 'census',{FILTER => "QualifierFilter(=,'substring:Name')"}


 

  
