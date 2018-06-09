![Tiwind Web Server](https://github.com/Bluecodelf/tiws/raw/master/md/logo.png)

TIWS 0.1R.1
===========

TiWS - short for Tiwind Web Server, is a toy project meant to experiment with the possibility of
making a dual-client web server: a server that lets other clients generate the content.

Dual-client web server?
-----------------------

TiWS is labelled as *dual-client* because of the way it serves the requested content to the final
user (which I will refer to as the **end client**).

TiWS actually does not serves HTTP content directly, as it actually receives the content from a
content provider (also called the **provider client**) shortly after it receives the request from
the end client.

TiWS also allows non-end clients to communicate between themselves, which means that, for example,
for a single end client request, the authentication might be handled by a client and the actual
requested content by another. In this case, the authentication client, which only adds context to
the end client's request, will be referred to as a **service client**.

A non-end client might both enrich a request and create content (the *response*) from it, which
means that it can be a service and a provider client at the same time.

Any service and/or provider client is called a **weblock**, pronounce *Web Block*.

What TiWS does
--------------

The primary role of TiWS is to provide an event queue to *weblocks*.

Because *weblocks* should only care about the context or the content, TiWS, when receiving an HTTP
request, will deal with encryption, parsing (all non-end client-server communication is made
through some sort of an optimized AST bytecode), load-balancing and caching.

Because of that, when a request is made from an end client, the HTTP request will be parsed,
transformed into an AST, a **transaction** will be opened from it and pushed into the event queue,
a *weblock* will pick up the request, do its work and push back another AST to TiWS that will encode
it into HTTP again. When the response is ready, TiWS will mark the *transaction* as **fulfilled**,
will encode it into an HTTP response again and will send it to the end client.

What TiWS does not
------------------

TiWS does not handle any kind of content generation or business logic: this role is entirely given
to *weblocks*.

Roadmap to 0.1R.2
-----------------

This project is still in its early stages.

- [ ] Refine AST generation.
- [ ] Refine weblock-server communication.
- [ ] Refine how weblocks can communicate between themselves using the event queue.
- [ ] Refine event queue filters.
- [x] Make a cool-ass logo.