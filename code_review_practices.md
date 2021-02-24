
## Code Review Standard
### For the developer - Before you create a pull request
Whenever you want to explain your code to other developers along with the intention of your changes. Don’t litter the code with code comments and ask yourself these questions to determine if it’s too difficult to understand:

* Can I split this code into smaller functions?
* Can I rename this function to something more obvious? Ask your team for function name suggestions if you like.
* How can I simplify my code further so it isn't as complex?
* Irrespective of what you pick, you should write a test.

### For the reviewer
In doing a code review, you should make sure of the following:
* **Design**- The code is well-designed.
* **Functionality**- The functionality is good for the users of the code.
* **Integration**-Any UI changes are sensible and look good.
* **Dependencies**- Any parallel programming is done safely.
* **Complexity**-The code isn’t more complex than it needs to be.
* **Sanity**-The developer isn’t implementing things they might need in the future but don’t know they need now.
* **Tests**- Code has appropriate unit tests.
* **Context**- Tests are well-designed.
* **Naming**-The developer used clear names for everything.
* **Comments**- Comments are clear and useful, and mostly explain why instead of what.
* **Documentation**-Code is appropriately documented .
* **Consistency**-The code conforms to our style guides.

Make sure to review every **line** of code you’ve been asked to review, look at the **context**,
make sure you’re **improving code health**, and compliment developers on **good things** that they do.


## Speed of Code Review
- Code reviews should be performed for every codebase exceeding 500 lines of code.
- Code should be pushed regularly from local development to public and made available for code review as soon as feature development is complete and a pull request is created
- Code should be reviewed in no more than 48 hours after the pull request is being created and assigned (i.e. first thing in the next morning).


## Speed of resolving conflicts
A developer should resolve conflicts in no more than 5% of their active development time. They should do the fixes on priority and respond to the PR comments appropriately. 
After the developers have made changes from their end, they should create a pull request and ask for code review over the latest changes and follow the same guidelines until code is merged into master branch.

## Writing code review comments
When a developer disagrees with your suggestion, first take a moment to consider if they are correct. Often, they are closer to the code than you are, and so they might really have a better insight about certain aspects of it. Does their argument make sense? Does it make sense from a code health perspective? If so, let them know that they are right and let the issue drop.

However, developers are not always right. In this case the reviewer should further explain why they believe that their suggestion is correct. A good explanation demonstrates both an understanding of the developer’s reply, and additional information about why the change is being requested.

In particular, when the reviewer believes their suggestion will improve code health, they should continue to advocate for the change, if they believe the resulting code quality improvement justifies the additional work requested. **Improving code health tends to happen in small steps.**

Sometimes it takes a few rounds of explaining a suggestion before it really *sinks in*. Just make sure to always stay *polite* and let the developer know that you hear what they’re saying, you just don’t agree.

**It’s OK to say “It’s all good”**
Don’t get picky, you don’t have to find an issue in every review. Reviews are meant to be constructive!

* Be kind.
* Explain your reasoning.
* Balance giving explicit directions with just pointing out problems and letting the developer decide.
* Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.

## How to perform code review manually
Feedback can be provided in Github as below:
![](https://rangleio.ghost.io/content/images/2018/06/1_MzzWcjVofsMGyRws4zcUKA.gif)
