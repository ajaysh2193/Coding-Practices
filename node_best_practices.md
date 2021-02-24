
# Node.js Best Practices

1. **Use an LTS release of Node.js:**
Ensure you are using an LTS version of Node.js to receive critical bug fixes, security updates and performance improvements.
2. **Start all projects with npm init:**
This will create a new **package.json** for you which allows you to add a bunch of metadata to help others working on the project have the same setup as you.
3. **Add package-lock.json:**
      1. The purpose of the package-lock is to avoid a situation where installing modules from the same package.json results in two different installs.
     2. Package-lock.json was added in npm version 5.x.x, so if you are using major version 5 or higher, you will see it generated unless you disabled it.
    3. The package-lock specifies a version, location and integrity hash for every module and each of its dependencies, the install it creates will be the same, every single time. It won&#39;t matter what device you are on, or when in the future you install, it should give you the same result every time, which is very useful.
    4. Use command &quot;npm ci&quot; to install dependencies with specific versions each time.
4. **Add scripts to your package.json:**
     1. Always add a scripts property and object to your package.json with a start key. It&#39;s value should be the command to launch your app.
     2. There&#39;s a couple of other script hooks worth knowing: preinstall, postinstall, test.
    3. You can add your own custom scripts here, too. They can then be run using npm run-script {name} — a simple way for you to give your team a central set of launch scripts.
5. **Use environment variables:**
Configuration management is always a big topic in any language. How do you decouple your code from the databases, services, etc. that it has to use during development, QA, and production?
 The recommended way in Node.js is to use environment variables and to look up the values from process.env in your code. For example, to figure out which environment you&#39;re running on, check the NODE\_ENV environment variables:
**console.log(&quot;Running in :&quot; + process.env.NODE\_ENV);**
6. **Use a style guide:**
Follow all the points as a style guide from the JavaScript section mentioned above.
 Why to use a style guide ?
    1. Well, we&#39;ve all had those moments where we open a new file from another project for the first time or the file came from a different developer, we then spend the next hour reformatting the braces to be on different lines, changing the spaces to tabs, and vice versa. The problem here is a mixture of opinionated developers and no team/company standard style guide.
    2. It&#39;s far easier to understand code on a codebase if it&#39;s all written in a consistent style. It also reduces the cognitive overhead of whether you should be writing with tabs or spaces. If the style is dictated (and enforced using JSHint, ESlint or JSCS) then all of sudden, the codebase becomes a lot more manageable.
    3. You don&#39;t have to come out with your own rules either, sometimes it&#39;s better to pick an existing set of guidelines and follow them. Here are some good examples:
        1. Airbnb - https://github.com/airbnb/javascript
        2. Google - https://google.github.io/styleguide/javascriptguide.xml
        3. jQuery - https://contribute.jquery.org/style-guide/js/
        4. Standard JS - [http://standardjs.com/](http://standardjs.com/)

        Just pick one and stick with it!

    5. Utilize ES6 Features.
    2. Prefer const over let. Ditch the var.
    3. Per file, the code must not exceed the 400 lines limit.
    4. Per function, the code must not exceed from 75 lines.
    5. If you often prefix names for field, table, and database, then you need to avoid this for Interface names like iShape, AbastractShape, etc.
    6. Always leave one empty line between imports and module such as third party and application imports and third-party module and custom module.
    7. **Use TypeScript instead of JavaScript while writing the code:**
Using TypeScript helps in maintaining single coding language principle across a MEAN stack application.
    8. **Declare Variable Type Instead of Using &#39;any&#39;:**
 While working on TypeScript, developers generally end up typing &#39;any&#39; to declare variables. If you are not specifying the variables and constants, they will be assumed by the value and as a result, will be assigned to it. If it happens, you are now in trouble as it will create some unintended issues, anytime.
    9. **Use arrow function expressions:**
 Though it&#39;s recommended to use async-await and avoid function parameters when dealing with older APIs that accept promises or callbacks - arrow functions make the code structure more compact and keep the lexical context of the root function (i.e. this).
    10. **Detect code issues with a linter:**
Use a code linter to check basic quality and detect anti-patterns early. Run it before any test and add it as a pre-commit git-hook to minimize the time needed to review and correct any issue. For Example: ts-lint.
1. **Embrace async:**
We all have heard about promises, maybe even heard a little about async-await and generators in ES2016. The key idea behind all these techniques is making your code asynchronous.
 Use async-await, avoid callbacks.
 There are plenty of great articles about how to use promises, generators and async-await.
    1. **Promises** - [https://web.dev/promises/](https://web.dev/promises/)
    2. **async-await** - [https://www.twilio.com/blog/2015/10/asyncawait-the-hero-javascript-deserved.html](https://www.twilio.com/blog/2015/10/asyncawait-the-hero-javascript-deserved.html)
    3. **Generators** - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators\_and\_Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)
2. **Handle errors:**
    1. Having an error bring down your entire app in production is never a great experience. Good exception management is important for any app, and the best way to deal with errors is to use the async structures above. For example, promises provide a .catch() handler that will propagate all errors to be dealt with, cleanly.
    2. **Handle errors centrally, not within an Express middleware:**
 Error handling logic such as mail to admin and logging should be encapsulated in a dedicated and centralized object that all endpoints (e.g. Express middleware, cron jobs, unit-testing) call when an error comes in.
    3. **Document API errors using Swagger or GraphQL:**
Let your API callers know which errors might come in return so they can handle these thoughtfully without crashing. For RESTful APIs, this is usually done with documentation frameworks like Swagger. If you&#39;re using GraphQL, you can utilize your schema and comments as well.
    4. **Catch unhandled promise rejections:**
Any exception thrown within a promise will get swallowed and discarded unless a developer didn&#39;t forget to explicitly handle it. Even if your code is subscribed to **process.uncaughtException**! Overcome this by registering to the event **process.unhandledRejection**.
3. **Ensure your app automatically restarts:**
    1. Okay, so you followed the best practice to handle errors. Unfortunately, some error from a dependency still, somehow, brought down your app.
    2. This is where it&#39;s important to ensure you use a process manager to make sure the app recovers gracefully from a runtime error. The other scenario where you need it to restart is if the entire server you&#39;re running on went down. In that situation, you want minimal downtime and for your application to restart as soon as the server is alive again!
    3. Please use pm2 to solve this situation. To handle restarting after the server crashes, you can follow the PM2 guide for you platform: [https://pm2.keymetrics.io/docs/usage/startup/](https://pm2.keymetrics.io/docs/usage/startup/)
4. **Cluster your app to improve performance and reliability / Utilize all CPU cores:**
By default Node.js is run in a single process. Ideally, you want one process for each CPU core so that you can distribute the workload across all the cores. This improves scalability of web apps processing HTTP requests and performance in general. In addition to this, if one worker crashes, the others are still available to handle requests.
 One of the other benefits of using a process manager like PM2 is that it supports clustering out of the box: [https://pm2.keymetrics.io/docs/usage/cluster-mode/](https://pm2.keymetrics.io/docs/usage/cluster-mode/)
5. **Import/Require all your dependencies up front:**
You should always load all your dependencies upfront and configure them upfront. That way, you&#39;ll know from the startup if there is a problem, not three to four hours after your app has gone live in production!
6. **Get your frontend assets out of Node:**
Serve frontend content using dedicated middleware (nginx, S3, CDN) because Node performance really gets hurt when dealing with many static files due to its single-threaded model.
7. **Use a logging library to increase errors visibility:**
    1. log is great but it has limits in a production application. Trying to sift through thousands of lines of logs to find the cause of the bug… which we will have to do at some point, is painful!
    2. A mature logging library can help with this. First, they allow you to set levels for each log message — whether it&#39;s a debug, info, warning, or error. In addition, they typically allow you to log to different files or even remote datastore.
    3. [https://www.loggly.com/](https://www.loggly.com/). Loggly allows us to quickly search all our log messages using patterns. In addition, it can alert us if a threshold is reached — for example, if a web application starts returning **500 SERVER ERROR** messages to users for a period longer than 30 seconds, Loggly can send a message and we can figure out what&#39;s going on.
    4. Use winston as a logging library - [https://github.com/winstonjs/winston](https://github.com/winstonjs/winston).
8. **Structure your solution by components:**
The worst large application&#39;s pitfall is maintaining a huge code base with hundreds of dependencies - such a monolith slows down developers as they try to incorporate new features. Instead, partition your code into components, each gets its own folder or a dedicated codebase, and ensure that each unit is kept small and simple.
9. **Layer your components, keep Express within its boundaries:**
Each component should contain &#39;layers&#39; - a dedicated object for the web, logic, and data access code. This not only draws a clean separation of concerns but also significantly eases mocking and testing the system.
10. **Single responsibility:**
Apply the single responsibility principle (SRP) to all components, services, and other symbols. This helps make the app cleaner, easier to read and maintain, and more testable.
11. **Shared feature module:**
    1. Do create a feature module named SharedModule in a shared folder.
    2. Do declare components in a shared module when those items will be re-used and referenced by the components declared in other feature modules.
    3. Consider using the name SharedModule when the contents of a shared module are referenced across the entire application.
    4. Consider not providing services in shared modules. Services are usually singletons that are provided once for the entire application or in a particular feature module. There are exceptions, however. For example, in the sample code that follows, notice that the SharedModule provides FilterTextService. This is acceptable here because the service is stateless;that is, the consumers of the service aren&#39;t impacted by new instances.
    5. Do export all symbols from the SharedModule that other feature modules need to use.
    6. Avoid specifying app-wide singleton providers in a SharedModule. Intentional singletons are OK. Take care.
12. **Wrap common utilities as npm packages:**
In a large app that constitutes a large code base, cross-cutting-concern utilities like logger, encryption and alike, should be wrapped by your own code and exposed as private npm packages. This allows sharing them among multiple code bases and projects.
13. **Separate Express &#39;app&#39; and &#39;server&#39;:**
Avoid the nasty habit of defining the entire Express app in a single huge file - separate your &#39;Express&#39; definition to at least two files: the API declaration (app.js) and the networking concerns (WWW). For even better structure, locate your API declaration within components.
14. **Be stateless, kill your servers almost every day:**
Store any type of data (e.g. user sessions, cache, uploaded files) within external data stores. Consider &#39;killing&#39; your servers periodically or use &#39;serverless&#39; platform (e.g. AWS Lambda) that explicitly enforces a stateless behavior.
15. **Security Best Practices:**
    1. **Embrace linter security rules:**
Make use of security-related linter plugins such as eslint-plugin-security to catch security vulnerabilities and issues as early as possible, preferably while they&#39;re being coded. This can help catching security weaknesses like using eval, invoking a child process or importing a module with a string literal (e.g. user input).
    2. **Limit concurrent requests using a middleware:**
DOS attacks are very popular and relatively easy to conduct. Implement rate limiting using an external service such as **cloud load balancers, cloud firewalls, nginx, rate-limiter-flexible** package, or (for smaller and less critical apps) a rate-limiting middleware (e.g. **express-rate-limit** ).
    3. **Extract secrets from config files or use packages to encrypt them:**
Never store plain-text secrets in configuration files or source code. Instead, make use of secret-management systems like Vault products, Kubernetes/Docker Secrets, or using environment variables. As a last resort, secrets stored in source control must be encrypted and managed (rolling keys, expiring, auditing, etc). Make use of pre-commit/push hooks to prevent committing secrets accidentally.
    4. **Use Helmet:**
If you&#39;re writing a web application, there are a lot of common best practices that you should follow to secure your application:
        1. XSS Protection.
        2. Prevent Clickingjacking using **X-Frame-Options**.
        3. Enforcing all connections to be HTTPS.
        4. Setting a **Context-Security-Policy** header.
        5. Disabling the **X-Powered-By** header so attackers can&#39;t narrow down their attacks to specific software.

        Instead of remembering to configure all these headers, Helmet will set them all to sensible defaults for you, and allow you to tweak the ones that you need.

    1. **Avoid using the Node.js crypto library for handling passwords, use Bcrypt:**
 Passwords or secrets (API keys) should be stored using a secure hash + salt function like bcrypt, that should be a preferred choice over its JavaScript implementation due to performance and security reasons.
    2. **Validate incoming JSON schemas:**
 Validate the incoming requests&#39; body payload and ensure it meets expectations, fail fast if it doesn&#39;t. To avoid tedious validation coding within each route you may use lightweight JSON-based validation schemas such as jsonschema, ajv or joi.
    3. **Support blacklisting JWTs:**
When using JSON Web Tokens (for example, with Passport.js), by default there&#39;s no mechanism to revoke access from issued tokens. Once you discover some malicious user activity, there&#39;s no way to stop them from accessing the system as long as they hold a valid token. Mitigate this by implementing a blacklist of untrusted tokens that are validated on each request.
    4. **Prevent brute-force attacks against authorization:**
 A simple and powerful technique is to limit authorization attempts using two metrics:
        1. The first is the number of consecutive failed attempts by the same user with a unique ID/name and IP address.
        2. The second is the number of failed attempts from an IP address over some long period of time. For example, block an IP address if it makes 100 failed attempts in one day.
        5. **Run Node.js as non-root user:**
        There is a common scenario where Node.js runs as a root user with unlimited permissions. For example, this is the default behaviour in Docker containers. It&#39;s recommended to create a non-root user and either bake it into the Docker image (examples given below) or run the process on this user&#39;s behalf by invoking the container with the flag &quot;-u username&quot;.
    6. **Limit payload size using a reverse-proxy or a middleware:**
 Mitigate this limiting the body size of incoming requests on the edge (e.g. firewall, ELB) or by configuring express body parser to accept only small-size payloads.
    7. Hide error details from clients.
1. **Performance Best Practices:**
    1. **Don&#39;t block the event loop:**
        1. Avoid CPU intensive tasks as they will block the mostly single-threaded Event Loop and offload those to a dedicated thread, process or even a different technology based on the context.
        2. **Prevent evil RegEx from overloading your single thread execution:**
    Prefer third-party validation packages like validator.js instead of writing your own Regex patterns, or make use of safe-regex to detect vulnerable regex patterns.
    2. **Prefer native JS methods over user-land utils like Lodash:**
 It&#39;s often more penalising to use utility libraries like lodash and underscore over native methods as it leads to unneeded dependencies and slower performance. Bear in mind that with the introduction of the new V8 engine alongside the new ES standards, native methods were improved in such a way that it&#39;s now about 50% more performant than utility libraries.
    3. **Use Gzip Compression:**
        1. Gzip is a software application used for file decompression and compression. Today, most clients and servers support gzip.
        2. The server compresses the response before sending it to the browser when a gzip compatible browser requests a resource, reducing time lag and latency.
        3. It can improve the overall performance of your application if you use gzip both when you respond to clients and when you make requests to remote servers.
    2. **Monitor your applications:**
        1. Getting notified when something goes wrong with your application is critical on production applications. You don&#39;t want to check your Twitter feed and see thousands of angry users telling you your servers are down or your app is broken and has been for the last few hours. So having something monitoring and alerting you to critical issues or abnormal behaviour is important.
        2. We already discussed PM2 for process management. In addition it&#39;s developers**(KeyMetrics.io)** run a process monitoring SaaS with integration with PM2 baked in. It&#39;s very simple to enable and they have a free plan which is a great starting point for a lot of developers. Once you&#39;ve signed up for KeyMetrics, you can simply run:
**$ pm2 interact [public\_key] [private\_key] [machine\_name]**
 This will start sending memory &amp; CPU usage data, plus exception reporting to key metrics servers to view from their dashboard. You can also view latency of your http requests, or set up events when problems occur (for example timeouts to downstream dependencies).
        3. In addition, Loggly (that was mentioned earlier) also provides monitoring based on logs. Both tools in combination can provide you with a way to quickly react to problems before they get out of hand.
3. **Test your code:**
    No matter what stage you are on a project, it&#39;s never too late to introduce testing. My advice is start small, start simple. I&#39;d also highly recommend writing a test for every bug that gets reported. That way you know:
    1. How to reproduce the bug (make sure your test fails first!).
    2. That the bug is fixed (make sure you test passes after you fix the issue).
    3. That the bug will never occur again (make sure you run your tests on every new deployment).

    There&#39;s a lot of testing libraries. For example: Jasmine, Mocha &amp; Chai. If you&#39;re writing a web application too, then use **Supertest** to black box test your web end points.
**Check your test coverage, it helps in identifying wrong test patterns:**
 Code coverage tools like **Istanbul/NYC** are great for 3 reasons:

    1. it comes for free (no effort is required to benefit the reports).
    2. it helps to identify a decrease in testing coverage.
    3. and last but not least it highlights testing mismatches: by looking at colored code coverage reports you may notice, for example, code areas that are never tested like catch clauses (meaning that tests only invoke the happy paths and not how the app behaves on errors). Set it to fail builds if the coverage falls under a certain threshold.

**References:**

- [https://github.com/goldbergyoni/nodebestpractices](https://github.com/goldbergyoni/nodebestpractices) (Best among all)
- [https://www.codementor.io/@mattgoldspink/nodejs-best-practices-du1086jja](https://www.codementor.io/@mattgoldspink/nodejs-best-practices-du1086jja)
- [https://www.cognitiveclouds.com/insights/what-are-the-best-practices-for-node-js-development/](https://www.cognitiveclouds.com/insights/what-are-the-best-practices-for-node-js-development/)
