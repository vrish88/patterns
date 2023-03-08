# Implement the client or server, not both

> Current JavaScript solutions suffer from "Double MVC". You need both server and client-side MVC stacks. Conceptual complexity is very high.

– from [dhh](https://twitter.com/dhh/status/75281941422800896?lang=en) in _2011_

**There exist many applications which have a server that stores state, validates inputs, and presents information to the client. The clients in these applications are javascript running in the browser which do all the same things. Most applications _start off this way_ and are doomed to duplicate behaviors/structure across both server and client in perpetuity.**

There is only so much time in the day. There are only so many technologies that people can have expertise in. We are finite beings in a finite existence. As such, our software development ought to concentrated to achieve the maximum result with as minimal of effort. This can be thought of as a [Complexity Budget](https://htmx.org/essays/complexity-budget/):

> An explicit or implicit allocation of complexity across the entire application.

In most web applications today there exists complexity in the server and in the client. Historically this has been the dividing line for most web tooling. For example, the Java framework Spring has established itself on the server side. Tools like React make it easier to build out the client into a more robust locus of behavior. Recently there has been more of a blurring of this line with technologies like WASM and Server Side React (SSR).

The industry has responded to this divide, recognizing the need for client leaning apps. Companies like [supabase](https://supabase.com/), [Apollo](https://www.apollographql.com/), or [Algolia](https://www.algolia.com/) exist because customers would rather pay for a backend than build it themselves. There are whole movements like the [Jamstack](https://jamstack.org/) which exist to drastically limit the complexity of running a server. React has built in functionality to be _rendered on the server_ thus allowing developers to write code for the client which can have the benefits of delivered from a server (ie SEO, time to first paint, etc.)

However, the industry has also recognized the need for server leaning apps as well. Running in the opposite direction, Ruby on Rails is doubling down on its [Hotwire](https://hotwired.dev/) technology and sending _HTML_ to the browser. Others are seeing the value in this and are calling for [a return to REST as Roy Fielding originally defined it](https://hypermedia.systems/book/hypermedia-reintroduction/). People built [HTMX](https://htmx.org/) to facilitate the exchange of HTML (like Hotwire) so that the "client" in the server/client model can be the browser instead of a custom written Javascript application.

While it would be wonderful to leverage all of these tools produced by industry, the reality often is that we can't. Either they haven't been approved, they cost too much, or we just don't know about them. How are we to budget our complexity? We can leverage the tools we do have available to help our apps shift towards the client or towards the server. This could be to build an abstraction on our server that handles CRUD generically so that we can focus on our client. It could be to shift to using web apps that produce html instead of json so that we can focus on our server. Once the need is identified, behaviors can change.

A useful heuristic is: how much is side opposite the lean being configured vs implemented? Client leaning apps should try to select server side technologies which only need to be configured. For instance, to use [supabase's services](https://supabase.com/docs/guides/getting-started/quickstarts/reactjs) all that needs to be done is to configure a database schema. Now creating a database schema is no small feat, but it is significantly less than also creating all the mechanisms for your client to interact with the data.

**Therefore, build applications which _lean_ towards the server or the client. For new applications, make it an architectural decision during the D&F process. For existing applications, identify where it naturally leans and make intentional moves to reinforce that structure.**

---
## Open Questions
* How to identify the lean?
  * What activities can be done?
  * What observed actions can be made on an existing codebase?