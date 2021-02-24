#  Angular Best Practices

1. **Avoid aliasing inputs and outputs:**
Avoid input and output aliases except when it serves an important purpose.
**Why?** Two names for the same property (one private, one public) is inherently confusing.
**Why?** You should use an alias when the directive name is also an input property, and the directive name doesn&#39;t describe the property.
**Don&#39;t prefix output properties:**
    1. Do name events without the prefix on.
    2. Do name event handler methods with the prefix on followed by the event name.
    3. Example Syntax:
 <toh-hero (savedTheDay)="onSavedTheDay($event)"></toh-hero>
2. **Use directives to enhance an element:**
Do use attribute directives when you have presentation logic without a template.
3. **Data Services:**
Talk to the server through a service !!!
 Do refactor logic for making data operations and interacting with data to a service.
 Do make data services responsible for XHR calls, local storage, stashing in memory, or any other data operations.
4. **Lazy Loading Feature Module:**
Utilizing lazy load the modules can enhance your productivity. Lazy Load is a built-in feature in Angular which helps developers with loading the thing which is required. For example, when you use the feature, it loads the components and other things you needed and stops other and unnecessary files to get loaded.
5. **CDK Virtual Scroll:**
CDK Virtual Scroll is a very important tool at your disposal which you can utilize to gain some good performance over your development. For example, if you have a larger file more than a thousand to display at the same time, it will make the application vulnerable and likely to slow down the performances. CDK Virtual Scroll can be found inside the Angular Material Package which helps developers enhance the performance of the applications and visualize the larger file in the browser.
6. **Common practices of Angular &amp; Node.js:**
    1. Add package-lock.json
    2. Add scripts to your package.json
    3. Use a style guide
    4. Embrace async
    5. Handle errors
    6. Import/Require all your dependencies up front
    7. Structure your solution by components
    8. Layer your components
    9. Single responsibility
    10. Wrap common utilities as npm packages
    11. Test your code

    All the above points are explained in Node.js section.

7. **Shared feature module:**
    1. Do create a feature module named SharedModule in a shared folder.
    2. Do declare components, directives, and pipes in a shared module when those items will be re-used and referenced by the components declared in other feature modules.
    3. Consider using the name SharedModule when the contents of a shared module are referenced across the entire application.
    4. Consider not providing services in shared modules. Services are usually singletons that are provided once for the entire application or in a particular feature module. There are exceptions, however. For example, in the sample code that follows, notice that the SharedModule provides FilterTextService. This is acceptable here because the service is stateless;that is, the consumers of the service aren&#39;t impacted by new instances.
    5. Do import all modules required by the assets in the SharedModule; for example, CommonModule and FormsModule.
    6. Do export all symbols from the SharedModule that other feature modules need to use.
    7. Avoid specifying app-wide singleton providers in a SharedModule. Intentional singletons are OK. Take care.
8. **Angular Coding Styles:**
 Follow all the points as a style guide from the JavaScript &amp; Node.js section mentioned above. Apart from that:
    1. Utilize custom prefix to share the feature area for all slider components.
    2. **Separate file names with dots and dashes:**
        1. Do use dashes to separate words in the descriptive name.
        2. Do use dots to separate the descriptive name from the type.
        3. Do use consistent type names for all components following a pattern that describes the component&#39;s feature then its type. A recommended pattern is feature.type.ts.
        4. Do use conventional type names including .service, .component, .pipe, .module, and .directive. Invent additional type names if you must but take care not to create too many.
9. **Delegate complex component logic to services:**
Do limit logic in a component to only that required for the view. All other logic should be delegated to services.
 Do move reusable logic to services and keep components simple and focused on their intended purpose.
10. **Components should only deal with display logic:**
Avoid having any logic other than display logic in your component whenever you can and make the component deal only with the display logic.
**Why ?**
    1. Components are designed for presentational purposes and control what the view should do. Any business logic should be extracted into its own methods/services where appropriate, separating business logic from view logic.
    2. Business logic is usually easier to unit test when extracted out to a service, and can be reused by any other components that need the same business logic applied.
    3. If you have any sort of logic in your templates, even if it is a simple &amp;&amp; clause, it is good to extract it out into its component.
11. **Prevent Memory Leaks in Angular Observable:**
Observable memory leaks are very common and found in every programming language, library or framework. Angular is no exception to that. Observables in Angular are very useful as it streamlines your data, but memory leak is one of the very serious issues that might occur if you are not focused. It can create the worst situation in the middle of development. Here&#39;re some of the tips which follow to avoid the leaks:
    1. **Using &#39;async pipe&#39;:**
 Either you can utilize subscribed observables or use &#39;async pipe&#39; and promise in the view. You should prevent yourself from subscribing observables in the component and binding that in view.
    2. **Using &#39;take(1)&#39;:**
&#39;take(1)&#39; is an operator which completes the emission by taking its value and enables the &#39;take(1)&#39; not to subscribe when a new value is encountered with. It will ensure that you get the data only once. Be secure with &#39;take(1)&#39; and avoid memory leaks easily.
    3. **Using &#39;takeUntil&#39;:**
This (takeUntil) is also an operator to be used when you want to monitor the second Observables and dispose of the subscription after the Observables emits the value or gets completed. In short, it helps you stay fearless from getting your Observables leaked.
12. **Avoid having subscriptions inside subscriptions:**
Sometimes you may want values from more than one observable to perform an action. In this case, avoid subscribing to one observable in the subscribe block of another observable. Instead, use appropriate chaining operators. Chaining operators run on observables from the operator before them. Some chaining operators are: withLatestFrom, combineLatest, etc.
13. **DRY:**
Do not Repeat Yourself. Make sure you do not have the same code copied into different places in the codebase. Extract the repeating code and use it in place of the repeated code.
14. **Using Index.ts:**
&#39;Index.ts&#39; is yet another, the most significant file in Angular which helps to reduce the size of the import statement. The file supports you to export modules in it (Index.ts) while in app.module.ts, you can import the modules.
15. **State Management:**
State Management in Angular helps in managing state transitions by storing the state of any form of data. There are various state management libraries such as NGRX, NGXS, Akita, etc and all with different usages, states, and purposes. All of them are good to use, though NGXS could be the preferred one as most of the developers have referred this as most usable and easy to learn the tool.
16. **Bootstrapping:**
    1. Do put bootstrapping and platform logic for the app in a file named main.ts.
    2. Do include error handling in the bootstrapping logic.
    3. Avoid putting app logic in main.ts. Instead, consider placing it in a component or service.

**References:**

- [https://aglowiditsolutions.com/blog/angular-best-practices/](https://aglowiditsolutions.com/blog/angular-best-practices/)
- [https://angular.io/guide/styleguide](https://angular.io/guide/styleguide)
- [https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/](https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/)

![](RackMultipart20200714-4-l0e8bl_html_d7dec09130297fd1.png)

