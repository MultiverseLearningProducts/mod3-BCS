# Code Development

We are going to learn about the following:

*   Summarise the main features and benefits of version control for the development of code, including change history; concurrent working; tracking and preventing conflicts; traceability; security.
*   Demonstrate how version control, in conjunction with configuration and release management, can be used for software that is being developed for use on multiple platforms.
*   Explain the importance of using coding guidelines and standards.
*   Explain the purpose of a range of programming tools, including compilers; interpreters; debuggers; GUI designers.
*   Explain the purpose and benefit of peer reviews and retrospectives in the development process.

# Inputs

The input for the Development phase are designs.

## The benefits of version control

Version control gives us the following 5 features can you research these and answer the questions below:

*   Change history
*   Concurrent working
*   Tracking and preventing conflicts
*   Traceability
*   Security

???
[q] Which git command lets you view the change history of a project tracked by git?
[ ] git history
[#] git log
[ ] git commits
???

???
[q] If I want to work concurrently on a code base without disturbing the work of other team members what should I do?
[ ] Clone the repo and work locally
[ ] Fork the repo and work on that copy of the project
[#] Create a new branch and work on that branch
???

???
[q] If I make changes that overwrite or alter code from the master branch what might happen?
[#] a merge conflict
[ ] a rebase
[ ] a down-stream commit
???

???
[q] If I want to find out who wrote a particular line of code what traceability tool from git can I use?
[ ] git trace main.js
[#] git blame main.js
[ ] git author main.js
???

???
[q] Which of the following is a valid security concern when using version control?
[#] intellectual property theft
[ ] denial of service attack
[ ] cross site scripting
???

# 📄

Write a piece in your portfolio that demonstrates HOW you use git in your work. Address the five points above and relate them to your role and times you have used these features.

* * *

## Release Management

Throughout the software development process, your code will go through cycles of development, testing, and fixing. Depending on your team, technology, platform, and other variables, you’ll likely have several environments that you use to manage your application. 1 In order to effectively test and release software, it’s imperative to have a simple and reliable release process for getting your code onto your various environments.

Your options for release management are literally endless. You could write your own scripts entirely from scratch or lean on tools like Jenkins, CircleCI, GoCD or TeamCity.

If it’s difficult to release code, you won’t release as frequently, and you may end up facing difficult choices where you need to release an update but fear disrupting your customers or acting to quickly. With a good release process, you should be incredibly confident releasing updates with no interruption to your customers. The best rule of thumb to know if your release process is good is whether you get anxious when releasing updates. That anxiety is often a symptom of a lack of confidence in your processes, and you should probably spend some time streamlining your releases.

Beyond the necessary side of getting your code where it needs to be, one of the biggest benefits of good release management is the ability to rollback in the event of an emergency. No matter how finely tuned your development and release process is, you’ll occasionally have hiccups in production.

![rollback broken code](https://preview.redd.it/o0g6oez12yl01.jpg?width=960&crop=smart&auto=webp&s=d031a34a6f86ebabf21a75155b3dba3b25216958)

When this happens, you’ll want to be able to easily rollback to your previously released codebase without breaking anything. This way, you’re not forced to rush an ill-considered fix out the door. Instead, you just rollback so that you can resolve the issue without affecting customers and then release again when it’s ready.

You might also have different environments that you deploy to:

*   Development
*   Staging
*   QA testers
*   Production

### Continuous deployment

Continuous deployment is one of the most advanced setups for team that have quality and process locked down. In these situations, releases are set up to happen automatically if new code successfully passes all of the automated tests. In order to do this, your team has to have an incredibly level of confidence that new code is tested and working. In this scenario, whenever someone adds new code, it will be run through all of your automated tests and, assuming they pass, put the code into production.

* * *

# 📄

Write a piece in your portfolio that explains the coding guidelines and standards that you have to follow (i.e. code must have tests, code lint rules etc). You should also explain the process of peer reviews and retrospectives that you have to follow in your team.

# 👩‍💻🧑‍💻

In pairs explain the purpose of a range of programming tools, including compilers; interpreters; debuggers; GUI designers.

# 💻

Take one of your repositories that is currently in version control (this should be a personal project). Can you implement a release management strategy for your project? Merging or pushing to master should trigger tests and a deployment.

# Outputs

The output of the development phase is untested working software.