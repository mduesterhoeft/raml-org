---
layout: page
title: "RAML is Turning 1.0!"
date: 2014-10-14
categories : [uncategorized]
author: Uri Sarid
tags :
comments: true
---

Almost exactly a year ago, the [RAML workgroup](http://raml.org/about.html#about-workgroup) released the first public version of the [RESTful API Markup Language spec](http://raml.org/spec.html "RAML 0.8 spec"), RAML 0.8, along with some tooling and a website. It's been one heck of a year, in which we saw massive adoption across users and companies large and small; active discussions online and at conferences and meetups; a community of tool developers [on raml.org](http://raml.org/projects.html) and [on github](https://github.com/search?o=desc&q=%22raml%22+created%3A%3E2013-07-01&s=updated&type=Repositories&utf8=%E2%9C%93) with a vibrancy we could only dream of; and virality: developers leveraging other developers' work in a chain of value. A great example of that was the Google Cloud Platform's documenting their [Kubernetes (docker management) API with RAML](https://github.com/GoogleCloudPlatform/kubernetes/tree/master/api), using Kevin Resker's community contribution of [RAML to HTML](https://github.com/kevinrenskers/raml2html). Equally amazing, at least to those of us in the RAML workgroup, was the robustness of that original RAML spec: we haven't had to touch it since its birth, and yet the value chain keeps growing. It's far from perfect, but it works, it elegantly solves a real problem, and it's furthering the cause of good API design for lots of people. We firmly believed, from the get go, that in order to know if this will really work, and to steer it in the right direction, we should set it loose with minimal "pushing" and just see where people take it. And listen. If something keeps chafing, let's revisit it to see if we can smooth it out. If some area is really valuable but is hampered by a design flaw, let's put time into that. Let's concentrate first on solving real problems. It's a bit like the old adage about where to put down sidewalks on a new campus lawn: watch where the students go on their own, and where you see the grass wearing down, that's where you should put down a path. So, a year in and after many conversations, we believe we've found a few paths to lay down. We've summarized them in [a series of github issues, labeled "milestone 1.0,"](https://github.com/raml-org/raml-spec/milestones/v1.0) and have started to collect a bit of final feedback. They fall into a few categories:

*   [Consistency](https://github.com/raml-org/raml-spec/issues?q=milestone%3Av1.0+label%3Aspec-consistency): Some of the changes improve consistency with existing standards, such as the meaning of URL vs URI, or within the RAML spec itself. For example, `baseUri` should have been called `baseUrl` and, rather than living with that forever, we'll fix it now. Many of these are small, but will not be backwards-compatible; a few are larger, such as specifying that by "markdown" we mean "github-flavored markdown", or improving OAuth support.

*   [Expanding current capabilities](https://github.com/raml-org/raml-spec/issues?q=milestone%3Av1.0+label%3Aspec-expand-current): There were a number of areas where it was clear that API authors could get a lot more mileage from existing capabilities, so we mostly just removed restrictions, e.g. allowing arrays and maps to be passed as parameters to resourceTypes and traits, allowing parametrized !includes, allowing enums of various types, etc.

*   [New capabilities](https://github.com/raml-org/raml-spec/issues?q=milestone%3Av1.0+label%3Aspec-new-capability): Most of these are quite significant, and I'd like to highlight a few here:
    *   [Express JSON, e.g. in examples or in schemas, in YAML block syntax](https://github.com/raml-org/raml-spec/issues/116). There are actually no new capabilities here at all, just syntactic sugar — but it should go a long way to making API specs less crufty and more readable and writeable.
    *   [YAML merge syntax instead of lists](https://github.com/raml-org/raml-spec/issues/103). When you want to compose together multiple structures such as traits, e.g. pulling in external trait libraries but adding to them some more specific traits, YAML offers you two options: either have the structures be lists, which are themselves composable, or use YAML merge syntax (`<<`) to extend maps with new properties. In RAML 0.8 we chose the former, but we've seen that dealing with lists has been confusing for many users, and that the merge syntax will be much clearer and cleaner.
    *   [The bodies property](https://github.com/raml-org/raml-spec/issues/107). RAML 0.8 did not allow for multiple examples in a body property. Examples could not be specified globally, whereas schemas could be, even though examples are more commonly used than schemas -- and with this limitation, examples were often embedded in the API spec, making it harder to see the API's structure at a glance. To address these and other related limitations, a new global structure is proposed, bundling everything about a request or response body in a named entity. We feel this approach will also promote cleaner modeling, the "M" in RAML.

There are some necessary breaking changes. An API spec using all of 1.0 will not be valid RAML 0.8, and vice versa. But APIs expressed in 1.0 will be very familiar to anyone who's used 0.8, and in some cases, the only way to tell will be to look at the top line for `#%RAML 0.8` or `#%RAML 1.0`. Above all, the gating criteria for all candidates is whether they preserve the spirit of RAML that's gotten us this far: do they leave the RAML specification as clean, as clear, as approachable, and as useful as REST itself. We'll let the list of candidates "bake" in the coming weeks to encourage as much feedback as possible before we finalize the RAML 1.0 specification. [**Please comment and engage in the discussion!**](https://github.com/raml-org/raml-spec/milestones/v1.0) While that's happening, it's also time to start preparing the ecosystem. Parsers will need to accommodate the changes in 1.0\. For some time, the 0.8 and 1.0 specs will have to coexist, so tools will probably want to support APIs written in both RAML 0.8 and 1.0\. And of course examples, documentation, and the RAML spec itself will need to be revised. With tooling in place, individual API specs will choose whether to take advantage of 1.0, and new API specs will probably be written only in 1.0\. We'll deprecate 0.8 as soon as 1.0 is out, and eventually, 0.8 will will be declared obsolete. Here is an example showing some RAML 1.0 features:

![RAML_1_0_example_1.png](/post_images/RAML_1_0_example_1.png "RAML_1_0_example_1.png")

_RAML 1.0 Example_