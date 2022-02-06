# What query or client technology should we use  for GraphQL requests ?

{% embed url="https://react-query.tanstack.com/comparison" %}

{% embed url="https://www.npmtrends.com/apollo-client-vs-react-query" %}

{% embed url="https://clevertech.biz/insights/why-we-choose-react-query-as-a-server-state-management-solution" %}

### Context and Problem Statement[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#context-and-problem-statement) <a href="#context-and-problem-statement" id="context-and-problem-statement"></a>

With the creation of the new contractor client app in 2021, the front-end developer team began to question if we should continue to use [Apollo Client](https://www.apollographql.com/docs/react/) or switch to another technology such as [React Query](https://react-query.tanstack.com).

### Decision Drivers[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#decision-drivers) <a href="#decision-drivers" id="decision-drivers"></a>

* We use apollo client for a long time in aos-client-app ( > 2 years ) and we faced some issues over time :
  * complexity with the test utils
  * difficulties updating cache or maintaining cache updates over time
  * major breaking changes every year
  * difficulties to use with debounced calls or states updates
* At the beginning of 2021, the entire dev team discussed using the [Apollo Federation](https://www.apollographql.com/docs/federation/) but as time passed, we started to consider using [Schema Stitching](https://www.graphql-tools.com/docs/schema-stitching/) from GraphQL Tools instead. This decision takes us a step away from the full Apollo ecosystem that we had before and it's now pretty clear that we don't necessarily gain any benefits from keeping it.
* other technologies of querying/fetching in react haven't stopped to gain popularity since 2020 ( [github star history of some popular libraries](https://star-history.t9t.io/#facebook/relay\&apollographql/apollo-client\&tannerlinsley/react-query\&vercel/swr) )
*

![](<../../.gitbook/assets/react\_clients\_github\_star\_history (1).png>)

### Considered Options[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#considered-options) <a href="#considered-options" id="considered-options"></a>

* [tannerlinsley/react-query](https://github.com/tannerlinsley/react-query)
* [apollographql/apollo-client](https://github.com/apollographql/apollo-client)
* [vercel/swr](https://github.com/vercel/swr)

### Decision Outcome[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#decision-outcome) <a href="#decision-outcome" id="decision-outcome"></a>

\-- NOT DECIDED YET --

### Pros and Cons of the Options[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#pros-and-cons-of-the-options) <a href="#pros-and-cons-of-the-options" id="pros-and-cons-of-the-options"></a>

The maintainers of react-query realized a comparison between them and the other libraries. You can see it here [https://react-query.tanstack.com/comparison](https://react-query.tanstack.com/comparison).

#### tannerlinsley/react-query[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#tannerlinsleyreact-query) <a href="#tannerlinsleyreact-query" id="tannerlinsleyreact-query"></a>

Supported Query Syntax Promise, REST, GraphQL

React-query is agnostic, meaning it can be used for more than just graphql based servers. It's great for doing ssr and its popularity is rapidly growing since 2020. It's been created by [Tanner Linsley](https://twitter.com/tannerlinsley) how also created the really good [react-table](https://react-table.tanstack.com) that we already use.

Even with fewer integrations with apollo based servers, this library has the same features comparing to apollo-client and is also more practical comparing subjects like debouncing/throttle calls, refetching strategies, disabling/pausing queries, updating queries or cache. You can also find some cool additional features like query cancellation, suspense support, prefetching, query persistence, easy ssr ...

On a personal point, even if I don't use react-query for a long time, I feel like the documentation is easier to understand than apollo-client, with more examples and tutorials.

On the other hand, there are important "defaults" or opinionated choices because queries are refetched automatically in the backgrounds in some situations or are silently retried 3 times before displaying an error.

But as a user and developer, I actually agree with most of these choices.

Some examples :

* [simple](https://react-query.tanstack.com/examples/simple)
* [ssr](https://react-query.tanstack.com/guides/ssr#\_top)
* [w/ GraphQL-Request](https://react-query.tanstack.com/examples/basic-graphql-request)

You can find more examples on: [https://react-query.tanstack.com/examples/simple](https://react-query.tanstack.com/examples/simple) .

* Good, because it offers an easy and unified way of handling different data query types ( graphql, rest, promises, etc... )
* Good, because it provides simple cache mechanism, but also a lot of features to manage it ( e.g., prefetching, query persistence, etc... )
* Good, because it offers a lot of features, some missing in other libraries like Lagged Query Data, Render Optimization, Auto Garbage Collection, Offline Mutation Support, Query Cancellation, Partial Query Matching ...
* Good, because the devtools of react-query is directly in-app and not in another tab of the devtool
* Good, because the documentation is simple and clear
* Good, because of its growing popularity and open-source support
* Good, because it allows us to dissociate fetching clients/logics like apollo, graphql-request, axios, websockets, etc... from the way of handling requests and cache over an application.
* Good, because React Query provides a way to continue to see an existing query's data while the next query loads
* Bad, because it needs to be used with other libraries to have the same comfort when replacing something very abstracted like apollo-client
* Good/Bad, because we need to use some additional solution for requesting like GraphQL-Request or Axios. Even if it's opinionated, the fetching method isn't and it does let you space to setup your own abstractions.

**The Subscription/Websocket Support question**[**​**](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#the-subscriptionwebsocket-support-question)

React-Query doesn't have built-in support for graphql subscriptions or any type of websocket communication by default.

But it's actually really easy to create a solution to handle websocket connections and subscriptions.

Here's a user suggestion using `useQuery` [https://github.com/tannerlinsley/react-query/discussions/1506#discussioncomment-256924](https://github.com/tannerlinsley/react-query/discussions/1506#discussioncomment-256924).

And here's an article written by @tkdodo who wrote a lot of good tutorials and simple articles about what is possible to do with react-query [https://tkdodo.eu/blog/using-web-sockets-with-react-query](https://tkdodo.eu/blog/using-web-sockets-with-react-query).

With libraries like [https://github.com/enisdenjo/graphql-ws](https://github.com/enisdenjo/graphql-ws) it can be very easy to integrate websocket support with or without react-query.

#### apollographql/apollo-client[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#apollographqlapollo-client) <a href="#apollographqlapollo-client" id="apollographqlapollo-client"></a>

Supported Query Syntax : GraphQL

Apollo Client is a fully-featured caching GraphQL client with integrations for React, Angular, and more. It allows you to easily build UI components that fetch data via GraphQL.

We use this technology for a long time now and it has evolved a lot since its beginning.

The apollo client package comes with a full ecosystem with server-side and cloud integrations. But for the client-side part, it's more abstracted than react-query and fully built around GraphQL.

* Good, because it's a great library and it's easy to use
* Good, because the normalized cache mechanism is structured and practical when you're using queries using the same types and fields.
* Good, because the API for queries, lazy-queries, mutations, subscriptions, etc. is very simple and easy to use
* Good, because the data returned by the client is immutable and it's a common best practice
* Good, the apollo framework is well-known inside the community and people already know how to use it without needing additional training
* Bad, because the cache can be a bit difficult to update in some cases and more strict than the react-query cache.
* Bad, because a lot of patterns and protocols used by apollo ( subscriptions ) evolved a lot and it's common to have breaking changes between major versions
* Bad, because the package exposes a lot of features that are not really useful for us or legacy like hoc(s) and developers tend to use the hooks for anything, without really knowing what's best ( ex: using useMutation hooks over client.mutate promises when it's not needed, causing useless rerenders )
* Bad, every time we want to use an apollo technology, we have to fight against using their premium solution "apollo studio"

#### vercel/swr[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#vercelswr) <a href="#vercelswr" id="vercelswr"></a>

Supported Query Syntax: Promise, REST, GraphQL

The name "SWR" is derived from stale-while-revalidate, a cache invalidation strategy popularized by HTTP RFC 5861. SWR first returns the data from cache (stale), then sends the fetch request (revalidate), and finally comes with the up-to-date data again. The API of swr and react-query are very close.

```
// react-queryconst { data, error } = useQuery('key', fetcher);// swrconst { data, error } = useSWR('/api/user', fetcher);
```

Copy

Some examples:

* [simple](https://swr.vercel.app/examples/basic)
* [nextjs-ssr](https://swr.vercel.app/examples/ssr)

The swr modules can be used on the fly when react-query needs a little configuration and a global client provided above, before the use of any hook.

* Good, swr is built for performance and it seems like a good choice in term of optimization
* Good, swr deep compares data changes by default
* Good, the package use tree-shaking to save unused code
* Good, because it supports a lot of features like suspense, prefetching, pagination, auto-revalidation etc...
* Good, really simple to use
* Good/Bad, the documentation is clear but very basic
* Good, because it allows us to dissociate fetching clients/logics like apollo, graphql-request, axios, websockets, etc... from the way of handling requests and cache over an application.
* Bad, mainly designed for rest calls, it needs to be used with other libraries to alllow a good api with graphql requests
* Bad, no official devtools
* Bad, no support for graphql subscriptions and difficult to use with websockets

### Nots[​](https://docs.go-aos.io/architecture-decisions-records/Front-End/GraphQL%20React%20Client#nots) <a href="#nots" id="nots"></a>

Every solution has full typescript support ( written in typescript ). Every solution is really good, but I think the true comparison here lay between react-query and swr.![](<../../.gitbook/assets/react\_clients\_github\_star\_history (1) (1).png>)
