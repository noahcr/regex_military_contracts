# regex_military_contracts
In-progress RegEx code to scrape Dept. of Defense contract announcements for relevant data.

The Department of Defense announces new contracts on a nearly daily basis - many are in the hundreds of millions of dollars, and some excede $1 billion. But aggregate data about the contracts isn't released until the fiscal year is closed. This regular expression script aims to pluck data fields from the contract announcements as they come out, capturing the company, location, amount, description of work, unique ID, etc. 

The expression is still a work in progress, and needs to be tweaked in order to accommodate irregularities in the format of contract announcements. For example, most announcements place the 13-digit unique ID at the very end, but some place it right after the description of the award, near the top. As this expression becomes more sophisticated, it will accomodate these differences. For now, here is an example of a conventional contract announcement, and how the regular expression works:

Example of Contract Announcement:

"Lockheed Martin Corp., Orlando, Florida, was awarded a $14,220,326 cost-plus-fixed-fee contract to operate and sustain the National Cyber Range capability which is designed to allow potentially virulent code to be introduced and studied on the range without compromising the range itself. Work will be performed in Orlando, Florida, with an estimated completion date of May 25, 2019. Fiscal 2014 research, development, test and evaluation funds in the amount of $5,555,539 are being obligated at award. This was a sole-source acquisition. U.S. Army Program Executive Office Simulation, Training and Instrumentation, Orlando, Florida, is the contracting activity (W900KK-14-C-0020)."

Here is the regular expression (<a href="https://regex101.com/r/zJ5uC5/1">You can see how it works in a RegEx tester here</a>):


<b>^[^,]*)[,]([*]?)\s([^,]*,\s[^,]*)[^$]*(\$\d+[^ ]*)\s+(.+?(?=contract))contract([^.]*)[^(]*\((\w{6}-\w{2}[^)]*)</b>



Here is the regular expression broken down into its individual functions:

<b>^[^,]*)</b> = Name of company

<b>([*]?)</b> = Potential asterisk, which signifies a small business/woman-owned business classification

<b>([^,]*,\s[^,]*)</b> = Location of company

<b>(\$\d+[^ ]*)</b> = Dollar amount of contract

<b>(.+?(?=contract))</b> = Type of contract ("cost-plus-fixed fee", "firm fixed price" etc)

<b>([^.]*)</b> = Description of work to be completed

<b>(\w{6}-\w{2}[^)]*)</b> = Unique ID


This expression works on many of the conventionally-formatted contract announcements; it does not yet scrape the completion date, the location of work, or how many bids were received for the contract.

















