# Design

After completing this section you should be able to:

*   Explain the purpose and scope of design.
*   Explain the difference between functional design that aims to make the software fit for purpose according to functional requirements and non-functional design that aims to make the software fit for use according to non-functional requirements.
*   Show how functional and non-functional requirements impact software design.
*   Identify the system components that need to be considered when designing software, including software architecture; user interface; user ergonomics; infrastructure / platform components; tools; operational processes; measures and metrics.
*   Explain why human computer interaction is an important consideration for design of software.
*   Explain why good design leads to better operational software, and why the quality of design can have a direct impact on operational cost as well as quality.
*   Explain how prototyping and modelling can be used to aid analysis and design.

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vRPopOEl-AIie0nwaZejCYHwcF0YsEUton4qjaufmt1zMk9yD1psuSf3CV_1NvjJIZGhGs-HjWq7t_U/embed?start=false&amp;loop=false&amp;delayms=3000" frameborder="0" width="100%" height="444" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Inputs

The inputs for design are requirements. The purpose of design is to solves the problem of how to realise the requirement. There are 5 types of design we need to consider.

1.  Input output design
2.  Process design
3.  Data design
4.  Security and control design

There are often constraints acting on designers. All of the factors below can impact the design stage of the SDLC.

<table>

<thead>

<tr>

<th style="text-align:left">Project</th>

<th style="text-align:left">Technical</th>

<th style="text-align:left">Organisational</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left">Money  
Time  
Skills</td>

<td style="text-align:left">Hardware  
Software  
Legacy  
Standards</td>

<td style="text-align:left">Politics  
Stakeholders  
Standards  
Legislation  
Cultural Differences  
Quality of requirements</td>

</tr>

</tbody>

</table>

## I/O design

Input output design starts with requirements. Usually what needs solving is:

*   **How** will we collect inputs?
*   **How** will we store/process inputs?
*   **How** will we output the stored/processed inputs?

For example say we have the following requirements:

1.  Users need to be able to create an account.

    *   1.1 Users need to enter their email to create an account.
    *   1.2 Users need to enter a password to create an account.
2.  Users need to be logged into the application in order to purchase an item.

    *   2.1 Users need to enter both their email and password to log in.
    *   2.2 It must be clear to the user that they are logged in and a session has started.
    *   2.3 Logged in users need to be able to log out to finish their session.
    *   2.3 Users trying to purchase an item when not logged in need to be prompted to log in and start a session.
    *   2.4 Users who selected an item/s to purchase before logging on should have the item or items they selected still selected after they have logged in.
3.  Users can select items to purchase

    *   3.1 It must be clear to the user how many items they have purchased
    *   3.2 It must be clear to the user what the current total of all the items they have selected is.
    *   3.3 Users need to be able to remove items they have previously selected.

Input output design starts by identifying the inputs. Can you select the inputs from the list below?

???
[q] Can you identify the correct list of inputs?
[#] email, password, item
[ ] email, password, total, items
[ ] email, password, item, session, items, total
???

???
[q] Can you identify the correct list of outputs?
[ ] session, items, total, user
[#] session, items, total
[ ] session, items, total, item
???

Once we have identified the inputs from the requirements then we need to design a way to collect those inputs. We need to decide what we should do with those inputs, for example they may need processing, or storing. Then we can design a way to access the outputs for the requirements.

For example we might collect the email and password in a web form, send those inputs to our server. The server can store those inputs (when creating an account), or process them (when logging in). Logging in or creating a session is our first output the server takes an email and password and returns a new session.

### Use case diagram

Use case diagrams are a way to express all these inputs and outputs. These diagrams can help designers to express their input output design.

![use case diagram](https://user-images.githubusercontent.com/4499581/75772283-8ee84480-5d43-11ea-9c95-defd5db09005.jpg)

In the rectangle are the requirements. Around the rectangle are different types of users who either provide inputs or consume outputs. What is interesting about the diagram are the places when the line from a user to a requirement crosses the edge of the rectangle. These intersections are the places that need input output design.

### UI

Considering the diagram above can you describe one of the forms that you might need to design? Include in your description the kinds of data your form would have to collect and what might happen to that data.

## Process Design

To realise requirements sometimes you need to combine a series of processes together. This is process design. Following on from our order system we have just been looking at:

![process diagram](https://user-images.githubusercontent.com/4499581/75778926-9feb8280-5d50-11ea-8179-519a861ecf95.jpg)

In this example the website is a simple static site hosted on [surge](https://surge.sh), the organisation runs its own bespoke accounting software solution on its own servers. The databases are hosted on AWS (amazon web services) and exposed via a RESTful API. Authentication of http requests is done via a dedicated service which is also hosted on AWS.

To place an order this is the process.

1.  A user requests the website hosted on surge
2.  Surge responds with the website index page
3.  From the website a request with items to order is sent to an Auth service on AWS
4.  That Auth service validates the request then forwards the order onto the API
5.  The API processes the order by reading and writing to the databases
6.  The API responds to the request with a status

A user will be free to select items. Then they will be able to place an order. If they are logged in and have an active session then we will create an Order record, and update the Users orders collection.

### High level to lower level

Our process design at the moment is quite high level, we can now go into more and more detail as we design the system in more and more detail.

![fractal](https://media.giphy.com/media/5MHFuFtdsKENi/giphy.gif)

For example in the diagram above we have an Authentication step in our process. That might need a more detailed design. Below is an activity diagram that shows how to handle incoming requests.

![activity diagram](https://user-images.githubusercontent.com/4499581/75785433-a16e7800-5d5b-11ea-9edc-405fb8d53d29.jpg)

## Data

Next we might want to start thinking about our data structures. In OO (object orientated) programming our data structures are mirrored in code and in the datastore. For example our program might have an **Order** class that we interact with in our program, and each instance of an **Order** is also persisted as a row in a datastore.

Data design starts with the requirements. Once it is clear what needs to be persisted often data is then **_normalised_**.

### Normalisation

This is a technique in data design. The aim is redundancy-free data structures. That means data structures that…

*   do not contain data that can be derived
*   only contain one copy of each logical point
*   contain the very latest value for each data item
*   combine items into logical groups based on underlaying data dependencies.

A good example of normalisation is the way we can store a one-to-many relationship in a relational database. For example our Customers will have many orders. To normalise that data structure we should store the Customer once. Then use their id in the Orders table to create that relationship.

# 👨🏽‍🎓 Design brief

Design what you think would be a good starting point for the data in our ordering system. Create your designs using UML. When you have finished you should upload your work [here](https://applied.whitehat.org.uk/mod/assign/view.php?id=7120&action=editsubmission).

[[[[Data Design Assignment](https://applied.whitehat.org.uk/mod/assign/view.php?id=7120&action=editsubmission)]]]

## Security and control design

These are the mechanisms we design to ensure the system has integrity. The safeguards we introduce for the inputs and outputs of our system. For example; validating inputs from the user. Restricting write access to certain tables. Restricting read access for certain users.

![ordering system](https://user-images.githubusercontent.com/4499581/75792946-9240f780-5d66-11ea-9183-389a2758c527.jpg)

???
[q] In our ordering system above which part of the design is responsible for security and control?
[ ] Customers
[ ] Accounts
[ ] Website
[ ] Accounting
[#] Authentication
[ ] API
[ ] Users
[ ] Orders
???

## Scope

Let us now consider the design phase in the context agile and waterfall software development methodologies.

<table>
<thead>
<tr>
<th style="text-align:left">Methodology</th>
<th style="text-align:left">Design notes</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><img src="https://user-images.githubusercontent.com/4499581/75794619-f2d13400-5d68-11ea-97ea-85e4a63a720f.jpg" alt="waterfall"></td>
<td style="text-align:left"><h3>Waterfall</h3><p>In the waterfall method all the design work is done before the developers start to write any code. The scope of the design stage in waterfall is large.</p></td>
</tr>
<tr>
<td style="text-align:left"><img src="https://user-images.githubusercontent.com/4499581/75794618-f2389d80-5d68-11ea-989d-ede01ad61484.jpg" alt="v-model"></td>
<td style="text-align:left"><h3>V-Model</h3><p>In this method the designs created service as both instructions and verification. The design stage is often divided into system design and component design. The design stage is large in scope.</p></td>
</tr>
<tr>
<td style="text-align:left"><img src="https://user-images.githubusercontent.com/4499581/75794616-f1a00700-5d68-11ea-97ed-d8fd88a3ed27.jpg" alt="incremental"></td>
<td style="text-align:left"><h3>Incremental</h3><p>In the incremental method the design work is done before development begins. The designs might be created for all the different increments, so a set of designs for increment1, then another set of designs for increment2 etc. Whilst the scope of an increment is limited the design phase is not.</p></td>
</tr>
<tr>
<td style="text-align:left"><img src="https://user-images.githubusercontent.com/4499581/75794612-efd64380-5d68-11ea-9478-458e5a348aea.jpg" alt="iterative"></td>
<td style="text-align:left"><h3>Iterative</h3><p>With the iterative method design work is contained within an iterative cycle so is much shorter and smaller in scope.</p></td>
</tr>
</tbody>
</table>

## Outputs

The outputs of the design stage might be:

*   Use Case diagrams
*   Process diagrams
*   Data models
*   Class diagrams
*   Control flow diagrams
*   UI/Component/Form designs

## Thinking time 🤔

Can you explain in your opinion why [human computer interaction](https://www.interaction-design.org/literature/topics/human-computer-interaction) is an important consideration for the design of the software you create? Finally in your own words what would you say is the **purpose** of the design stage of the SDLC.

[[[[Human Computer Interaction Assignment](https://applied.whitehat.org.uk/mod/assign/view.php?id=7995&action=editsubmission)]]]

???
[q] What is the next stage of the SDLC?
[ ] Implementation
[#] Development
[ ] Testing
???