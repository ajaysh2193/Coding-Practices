# Best Practices in API Documentation

APIs are only as good as their documentation. A great API can be rendered useless if people don’t know how to use it, which is why documentation can be crucial for success in the API economy. But creating and maintaining good documentation that’s easy to read, enjoyable to interact with, and sets the consumer up for success can be extremely challenging. Creating great documentation requires effort and patience, but it has direct implications on API adoption and maintainability.
API is meant to solve real world problems faced by companies in a specific industry, and will directly be integrated into applications by software engineers. As such, there are two types of potential audiences of our API, who will influence our API’s consumption and adoption curve.
1) **Decision Makers:** These are the people who evaluate your API’s services, and decide if it makes sense for the development team to spend time exploring the service
2) **Users:** These are the people who will be directly working with your API. They need to learn the ins and outs of your API, and how it applies to their use case. This could mean learning how to call and integrate with many, or all, of the resources you expose.

### Fundamental of good API Documentation:
The following sections should be included in the API Documentation as they have become fundamental for good API Documentations:

- **Authentication:** 
	This is the information about using authentication schemes to start consuming our API. Most APIs have authentication schemes, and consumers have to authenticate before gaining access to the API. Make sure this section is properly documented, and hand-holds users to successfully authenticate against the API.
- **Error Messages:** 
Error messages are important because they tell end consumers when they're integrating with your API services in an incorrect way. Explain your error standards, and also provide solutions on how to overcome them when an end consumer gets an error.
- **Resources:**
Pay attention to your API’s resources and their associated request and response cycles. Resources are the core components of your API, which users will be interacting with constantly. List all of the resources your API exposes, and understand how consumers may integrate with them. This will give you a good idea of how to better document the requests and responses under these resources.
Know more about resources :[https://restful-api-design.readthedocs.io/en/latest/resources.html](https://restful-api-design.readthedocs.io/en/latest/resources.html)
- **Terms of use:**
This is the legal agreement between the consumer and your organization, defining how the consumer should ideally use your services. Include API limits under best practices, with terms and conditions. Constraints also need to be clearly stated so that consumers understand what API usage and practices are permitted.
- **Change Log:**
Detail updates and versions of your APIs and how that might affect API consumers. This will help consumers know the stability of your API and see if any changes need to be made for an effective API call.

### Few Pointers to help writing a good API documentation

- **Avoid Jargons:** Keep in mind that many people working with the API may not have intimate knowledge of the domain or jargon you may be using. Documentation should cater to the “very technical” developer audience, and the less technical decision makers (like Product Managers). A big mistake technical writing teams make is assuming their audience is fully technical and have complete understanding of how to work with APIs. Start your documentation by writing in plain English, and have easy-to-understand domain explanations for every resource. Avoid using too much technical jargon, and write in a way that can be easily understood by people who are new to the API or industry.

- **Treat Your Requests and Responses:** Give the documentation of your request-response cycles the care they deserve. Having too much information available for the end consumer is never an issue, especially when they’re trying to integrate your services into their applications, so describe your request-response cycles in detail. Document every call your API could offer, with context around the parameters and responses. Responses are the guides for your consumers, indicating whether they’re on the right track, or providing guidance with error messages to help them succeed. Your API users should know exactly what to expect from a successful API call. Describe the full sample response body in every supported format. Think of not only the format, like XML or JSON, but also of HTTP headers, error codes, and messages. Examples in parameters and responses are also important. Provide examples in every single object which your API is supposed to return, as well as examples of parameters that users can add for a successful API call.
- **Fill Documentation with Resources:** There’s additional information and resources you can provide your consumers to be successful with your API. We can supplement your documentation with additional resources like:
	1) **Getting Started Guide:** The Getting Started guide provides a detailed account of how to quickly start working with your API. The emphasis in the guide should be on ensuring consumers reach success with your API as quickly as possible, hand holding them throughout this journey.
	2) **SDK and Libraries:** Code libraries help developers quickly call different resources. Having quick and easy methods in different languages to work with your API helps developers feel more comfortable working with the API.
	3) **Interactive Console:** Encourage prospects to immediately test what they read in the API documentation with the API console. Experimentation is powerful, and a console makes getting started easy, with limited liability from the consumer’s perspective. It’s a relatively simple effort to create a console or a sandbox environment for people to interact with your API, but can go a long way in helping developers to know the value of your API visually. Tools like Swagger and Postman API helps in these cases.
