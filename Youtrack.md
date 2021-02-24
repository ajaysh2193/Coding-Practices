# Best Practices for YouTrack 

The Youtrack project management tool adapts easily to the business processes and tracks tasks, identifies bugs, plans sprints, and creates workflows. YouTrack allows the connection to a version control system (VCS) and supports direct integration with multiple repositories, such as GitHub, GitLab and Bitbucket. Unlike other issue trackers, Youtrack can be customised to be agile, monitor the development progress, bring IDE-style intelligence, and import projects, users, and issues from Jira, and other trackers.

## # Important Terms and Concepts

1) **Agile:** the name coined for the wider set of ideas that Scrum falls within; the Agile values and principles are captured in the Agile Manifesto.
2) **Daily Scrum:** a fifteen-minute daily team meeting to share progress, report impediments and make commitments. During the Daily scrum each team member answers three questions:

		a.   "What have I done since the last Scrum meeting? (i.e. yesterday)"
		b.  "What will I do before the next Scrum meeting? (i.e. today)"
		c.  "What prevents me from performing my work as efficiently as possible?"

3) **Epic:** a very large user story that is eventually broken down into smaller stories; epics are often used as placeholders for new ideas that have not been thought out fully. There's nothing wrong with having an epic, as long as it is not high priority.

4) **Estimation:** the process of agreeing on a size measurement for the stories in a product backlog. Done by the team, usually using Planning Poker.

5) **Product Backlog:**   A prioritized list of work to be performed in a project. In the Scrum framework, this evolves with the business need and the environment .

6) **Scrum:** A methodology originally refined in 1995 by Ken Schwaber and Jeff Sutherland from work done by Hirotaka Takeuchi and Ikujiro Nonaka. Named after the SCRUM in Rugby, this is the most recognized Agile framework. It is an iterative methodology that treats major portions of development as a controlled black box. Iterations called sprints are used to evolve the product which is ready to ship after each sprint [Schwaber, Ken "SCRUM Development Process"].

7) **Scrum Roles:**  There are three core roles in Scrum: The Product Owner, The Scrum Master, and the Scrum team (also called the development team). These are the people responsible for completing the project objectives.

8) **Scrum Goal:**  The sprint goal is what is to be accomplished by the end of the sprint. Its a summary of the activities/results elaborated by the product backlog items that the Product Owner would like to accomplish during the sprint.

9) **Sprint Review:**  The sprint review meeting takes place at the end of each sprint. The delivery team shows what they accomplished during the sprint. Activity attributes are reviewed, modified, and reconciled at every sprint review meeting.

10) **Task Estimation:**  The team breaks down the selected Product Backlog items into tasks and then the tasks are estimated by the team members according to their complexity, risk involved, potential time required, and so on using team exercises.

11) **User Story:** A User Story is a statement (or a group of statements) that expresses the desired end user functionality. User Stories are generally simple, short, and easy to implement. Longer User Stories are further broken down into multiple User Stories.

12) **Velocity** the rate at which a team completes work, usually measured in story points. In Scrum, velocity is how much product backlog effort a team can handle in one sprint. This can be estimated by viewing previous sprints, assuming the team composition and sprint duration are kept constant. It can also be established on a sprint-by-sprint basis, using commitment-based planning.

13) **Work In Progress:** Refers to work that has been undertaken but not yet completed. If large segments of the project are WIP, it can pose several problems. Identifying bottlenecks in the project becomes difficult when several tasks are WIP at the same time. Each WIP requires capital and does not contribute to ROI until it becomes a completed, usable product. Kanban boards are effective in placing limits on WIP.

 ## Scrum Practices

Practices are described in detailed:

[![](https://www.guru99.com/images/11-2014/agile_Processesv1_4.png)]

## Process flow of Scrum Methodologies:

Process flow of scrum testing is as follows:

-   Each iteration of a scrum is known as Sprint
-   Product backlog is a list where all details are entered to get the end-product
-   During each Sprint, top user stories of Product backlog are selected and turned into Sprint backlog (Open Tasks)
-   Team works on the defined sprint backlog
-   Team checks for the daily work
-   At the end of the sprint, team delivers product functionality


## Steps for Effective YouTrack Usage For Scrum

- The project Owner creates a project in the YouTrack.
-  Integrate the Github repositories to the YouTrack. Link to the steps  to integrate the github with YouTrack is below.
[https://www.imaginea.com/optimizing-project-management-with-github-youtrack-integration/](https://www.imaginea.com/optimizing-project-management-with-github-youtrack-integration/)
- The Scrum Master along with the product owners defines the Epics based on the requirements of the entire product as defined by the client or end-user. The Epic estimation is equal to the product estimate. 
- The Scrum Master has the role to create the sprints and define the goal with discussing with the development team for each sprint during the brainstorming session.
- The result of the discussion of the brainstorming session is the creation of the user stories. The scrum master defines the user stories for each of the goal that has to be achieved in the sprint.
- The team divides the user stories in the small task and subtask. 
- In YouTrack, we create a Epic as a swimlanes. For each of the components of the product we create a swimlane. Each swimlane is divided into stages of development as columns. We define columns as [Open, Ongoing, Review, Complete]
- The developer create a card in the YouTrack for each of the task that needs to be done in a sprint to accomplish the goals of the sprint. The creator add the summary, description, estimate, assignee, type and priority.
- The types can be [Epic, Task and Bug]. We define a task as Epic if we need to create a subtask for the task. The task is a single small item of work that helps one particular story reach completion. The bug is defined when the work needs to be done for fixing the issues of any previous completed task.
- All the cards created is initially should be kept in Open Status. Once the developer starts to work on the task, its corresponding card is moved Ongoing Status. When the Pull Request is created for the task then the card is moved Review Status and the card is assigned to the person whom reviewed is assigned in the Pull Request. When the Pull Request is approved the reviewer/developer moves the card to the complete Status.
- If a task cannot be completed in a particular sprint then the task if moved to the next sprint with the comment mentioned in the card about the amount of work completed and percentage of work left to be done.
 
 - To use the github integration with the youTrack, the developer needs to follow either of the two ways: 
	 1) add the task id in the comment of the git.
			 ```
			 eg: git commit -m  "[Message] #TaskID"
			 ```
	2) Open the card in the YouTrack and add the commit ID in the "Add Commit" option present in the bottom right of the comment box. 
