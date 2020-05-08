# Full node <-> light wallet

What would help in terms of light wallets and being able to provide a full transaction history for addresses would be that a light wallet would be able to call an API of a full node with a *public_identifier* and get all relevant transactions.

Since, for some addresses, this would be a resource and bandwidth-heavy operation for the node providing the data, I propose to agree on a standard which is used both by light wallet developers and the Open-DB transactional data facilitators.

An example of such as standard, which Github adheres to for their resource-heavy API tasks, would be to:

- enforce query pagination (*per_page* and *page* header)
- enforce a ratelimit

I propose for the implementation to be as simplistic as possible, with no changes made to the nyzoVerifier codebase, but with separate code facilitating the *setup* and *run* procedure of the API service.

Following endpoint would help the light wallet display the correct amount of available pages:

- request method = *amount_of_transactions* with 1 argument: *public_identifier*

Following endpoint would facilitate the delivery of transactions to the light wallet:

- request method = *individual_transactions* with 2 arguments: *page* and *per_page*

This endpoint would send the timestamp of the last transaction along with its response, since the light wallet would need to be aware of any new incoming transactions, which would avoid the end-user of making data interpretation mistakes, as he will be alerted of a new incoming transaction.

# Setting up a new full node

It would be beneficial if the same mechanism allowed for aspiring full node operators to contact already existing full node operators with a request to download the entire, unconsolidated history.

I imagine it would be beneficial if the existing full node operator had **the choice** to enable this, and to set an *optional* price at which he is willing to send such a large amount of data.

I imagine it would be beneficial if the existing full node operator had **the choice** to enable the same mechanism, but for consolidated blocks or consolidated blockfile ZIPs.

As an alternative to this, the aspiring full node operator can opt to fetch [the entire history from the nyzo.co website](https://nyzo.co/blockFiles) or to rely on community provided ZIP files, uploaded on a cloud-host such as MEGA
