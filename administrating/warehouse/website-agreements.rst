******************
Website Agreements
******************

Although Indicia is primarily designed so that each client website sharing a 
single warehouse has exclusive access to its own pot of data, there are 
situations where sharing records across website boundaries can be very useful. 
Examples include:

* Sharing verification effort across several different portals. For example, a
  website for general recording and a website for recording bumblebees could
  use a shared verification portal for all bumblebee records, so that experts
  do not need to log into 2 different systems. 
* Offering reporting across records captured via multiple portals. 
* Providing centralised administration of several surveys, e.g. the onward 
  transfer of the records to the NBN Gateway could be handled in one place.

Sharing effort in this way not only reduces the amount of time spent on each 
task but saves the need to configure Indicia pages for each purpose on every
website. 

The way this is achieved is via a **website agreement**. Website agreements are
a powerful mechanism for reducing the overall effort required for managing 
online recording. In addition by website agreements can increase the feeling of
belonging to a wider community by sharing records across the boundaries between
different client websites, as long as the client websites share a single 
warehouse. A website agreement is created on the warehouse and includes a 
definition of what the agreement does and does not allow. For example, an 
agreement could define that all participating websites must provide their 
records to other participating websites for reporting purposes, or that 
providing records to other websites for reporting is optional. The agreement can 
define the possible providing and receiving of records for each of the following 
tasks:

* reporting
* peer review
* verification
* data flow
* moderation

For each of these tasks, it can define if the data sharing is:

* Not allowed
* Optional, but requires an administrator to set it
* Optional
* Mandatory

Then the warehouse is used to configure which websites are participating in the 
agreement and, for each website, which of the optional data sharing options it
will participate in. Let's take the example of `iRecord <http://www.brc.ac.uk/irecord>`_, 
which provides a central reporting and verification portal for a number of other 
websites. The website agreement defines that

* providing of records for reporting is optional.
* receiving of records for reporting is optional but requires an administrator 
  to set this option.
* providing of records for verification is optional.
* receiving of records for verification is optional but requires an 
  administrator to set this option.

The administrator of the warehouse then adds iRecord itself to the website 
agreement and defines that iRecord can receive records for both verification
and reporting. Then, the administrator of each website (not the warehouse, so 
they do not have full admin rights) adds their own site to the website 
agreement. In doing so they are unable to choose options to receive data for
verification or reporting because these options would require full admin rights,
but can opt in to either providing records for the reporting in iRecord and/or 
providing records for the verification system in iRecord.