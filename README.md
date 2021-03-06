# Resource bundles

A resource bundle is a collection of HTTP responses, represented in a new file format. This repository supports the development of the definition of the resource bundle format as well as uses of this format:
- The resource bundle format ([explainer](./bundle-format.md))
- Faster subresource loading with resource bundles ([explainer](./subresource-loading.md))
- Serving conventions for resource bundles ([explainer](./serving.md))
- JS/web build tool conventions for resource bundles ([explainer](./tools.md))

## Scope

This repository is scoped to be related to proposals which may eventually be involved in improving development and deployment of applications on the standard, multiple-implementation Web platform. Considerations for how these technologies can be deployed outside of the Web are certainly welcome for discussion and influencing the details of the features.

However, larger proposals which are motivated principally by packaging in non-Web environments, or which are explicitly opposed by multiple browser engine maintainers, are out of scope for this effort and can be discussed elsewhere.

In general, efforts may migrate into or out of this repository, if they are considered relevant to the scope and if participants want to develop them in one place or another.

## Implementation

This effort aims to promote software development to implement the resource bundle format and its applications to support the JS/Web ecosystem. We specifically see the need for:
- Browser implementations of resource bundle loading APIs
- Utilities/libraries in various programming languages to pack and unpack resource bundles
- Server support for dynamic chunk serving
- Bundler and framework support for emitting resource bundles
- Polyfills for using/emulating resource bundles in browsers without native support

At this point, these proposals are all very early and are best developed within an experimental plugin, behind a flag, etc.

Resource bundles and their applications are designed to be suitable to gradual adoption--even if implementations exist only in certain parts of the stack, they are still useful.

This repository can host software development for tools and polyfills and also cross-reference related software development done elsewhere.

## Standards venue

The Web Incubator Community Group, which may, in the future, host this repository, is not a standards venue itself; documents developed here are not, by themselves, on a standards track. Instead, WICG serves to provide an open platform and safeguard the intellectual property developed, to enable later standardization.

The resource bundle format itself is planned to eventually become an RFC from the [IETF WPACK WG](https://datatracker.ietf.org/wg/wpack/about/). It will be periodically published as an Internet-Draft. However, a draft is developed in this repository.

Resource and module loading on the Web is generally defined by [WHATWG](https://whatwg.org/) standards like [HTML](https://html.spec.whatwg.org/) and [Fetch](https://fetch.spec.whatwg.org/) and [W3C](https://www.w3.org/) standards like [Resource Hints](https://w3c.github.io/resource-hints/). When the proposals in this repository reach a state of [multi-implementer support and no strong implementer objections](https://whatwg.org/working-mode), with [web-platform-tests](https://github.com/web-platform-tests/wpt/) tests developed, they will be proposed as pull requests to those standards.

## FAQ

#### Q: How does this proposal relate to the Web Package/Web Packaging/Web Bundles/Bundled Exchange effort ([repo](https://github.com/wicg/webpackage))?

**A**: This is the same effort, really, with a particular scope. In particular, this repository has a focus on same-origin static subresource loading, while preserving the semantics and integrity of URLs. The Google Chrome team (including Jeffrey Yasskin and Yoav Weiss) have been collaborating closely on this project. There are different concrete alternatives under discussion (especially in the details of subresource loading, and less so for the bundle format itself), but the idea is to gather more feedback (possibly including prototyping) to draw a shared conclusion.

#### Q: Why the name change, then?

**A**: To express the limited scope (excluding signed exchange, preserving URL semantics) and the fact that this format may be useful outside of the Web. Hopefully, these changes address the previous criticisms of Web Bundles.

#### Q: How does this proposal relate to Signed Exchange?

**A**: [Signed Exchange](https://wicg.github.io/webpackage/draft-yasskin-http-origin-signed-responses.html) is a proposal from the Google Chrome team to allow one "distributor" to serve web content from another "publisher". In its basic form ([shipping in Chrome, Edge, and Opera](https://caniuse.com/sxg), but explicitly opposed by other engines), Signed Exchange does not use bundling, but instead signs an individual HTTP response.

This proposal does not make any special allowances for Signed Exchange, and some coauthors personally oppose the promotion of Signed Exchange through bundling. There has been high-level discussion about a concept of "signed bundles" (which led these two proposals to be coupled at some point), but the overlap is as simple as: if a bundle were signed, there would have to be some kind of section within the bundle to contain the signature for the bundle as a whole (rather than leave signatures to being per-response).

#### Q: Weren't ad blockers and publishers opposed to Web Bundles? How do they feel about this proposal?

**A**: (TODO: Collect the opinions of Brave and Eye/O, and post them here)

[Robin Berjon](https://twitter.com/robinberjon) from the New York Times said,
> It's a useful approach to address the bundling mess we see in JS (and other similar issues), building on smart work from Jeffrey Yasskin and Yoav Weiss but without the bits that help Google take over the Web.

#### Q: How far along is this proposal? Is it about to ship?

**A**: This proposal is very early. Although [Chrome has a flagged experiment for unsigned Web Bundles](https://web.dev/web-bundles/) based on [this simpler explainer](https://github.com/WICG/webpackage/blob/master/explainers/subresource-loading.md), there is no specification or tests, and there are ongoing efforts to iterate on design and communicate with browser vendors, web developers and other web stakeholders before this proposal is ready to ship.

#### Q: How is this work funded? Are there any conflicts of interest?

[Eye/O](https://eyeo.com/) is funding Daniel Ehrenberg's (Igalia) work on resource bundles, and [Bloomberg](https://www.techatbloomberg.com/) had funded it previously. Many others have been collaborating, especially Yehuda Katz (Tilde), Pete Snyder (Brave) and several Google employees (inside and outside of the Chrome team). Google and Brave are also a clients of Igalia, but not funding work on this project.
