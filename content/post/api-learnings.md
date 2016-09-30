+++
date = "2013-03-26T00:59:34+02:00"
title = "API Learnings"
description = "What I learned from maintaining a small API over the last two years"
draft = true
+++

# Tags and Authorization

> Learning from api failures

#
Your API is important. Make sure every developer that touches the API knows it on the low level.
  Don't abstract low-level immidiatly and forget to verify it is consistent.

## Authorization

Every consumer of your API should authorize/identify itself, even if your service is only used on the internal
network by your own services. Adding authorization gives you a bunch of benefits:

* You can add metrics to measure the usage of different consumers thus help identifying heavy users and contact persons
* If a services gets ddoses or becomes suspicious, it can easily be blocked by disabling the access keys
* You can use them to trigger feature flags and make sure only a certain consumer sees new behavior.
 This makes it easier to test slowly, when you need to verify certain changes don't have a big impact on the system

* It allows you to scope the data and give each consumer his own world. This way, your production installation can be
 utilized by testing frameworks, staging systems etc. Even your developers might not need to install every service
 locally but only the ones they actively develop.

## Labels (or Tags)

Bla bla, primitives, not frameworks. To help this, provide labels so your users can define a simple structure themself.

Thus your main business objects should expose the possibility be labeled/tagged.
This way, consumers can more easily identify their context of the objects.

Keep your structure simple, avoid virtual objects. If you require your users to build
virtual structures for the sake of your opinion, you are doing it wrong. You assume things,
and your assumption is wrong. The real-world will always construct a case where your assumptions break.
Keep it simple and extendable: by providing the primitives.

If you still believe in a nice abstraction layer ontop, your users can always look under the hood
and do stuff directly, when your higher level breaks.
