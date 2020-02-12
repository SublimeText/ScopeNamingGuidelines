# Scope Naming Guidelines (for Sublime Text)

This repository holds
a collection of documents
providing guidelines for scope naming in syntax definitions
for [Sublime Text][].

**Currently a work in progress.**


## Motivation

Spawned from an idea posted [in the Packages repository][idea],
the repository was created
to

1. streamline the process of deciding on guidelines for scope naming,
1. provide more details on corner cases,
1. give concrete examples,
1. and create a referenceable collection of documents.

As such, all documents are assigned a unique number
that is determined incrementally on merge
and follow a template that ensures the above goals are met.
Documents may be modified and are versioned following [SemVer][].


## Workflow

1. A Pull Request is proposed for an existing document
   or a new document is added.
   - Newly added documents must be named following `000-<title>.md`
     and follow the provided template,
     as well as our [contribution guidelines](./CONTRIBUTING.md).
   - The new version according to [SemVer][] must be provided,
     based on the current changeset.
     The first version is always `1.0.0`.
     Furthermore,
     an incrementing pre-release identifier of `-rfc.0` is added.
1. The pull request is discussed
   and iterated on based on feedback by the community.
   For each iteration, the pre-release version is increased
   to create a unique reference for this version.
1. Eventually, a majority of \[certain people?\]
   and the maintainer of the document, if any,
   approve of the PR or reject it.
   **\[TO BE DECIDED\]**
1. If approved, the PR is merged and open metadata inserted.

<!-- TODO refine -->


[Sublime Text]: https://sublimetext.com/
[idea]: https://github.com/sublimehq/Packages/issues/1440
[SemVer]: https://semver.org/

## Copyright

<p xmlns:dct="http://purl.org/dc/terms/">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <span rel="dct:publisher" resource="[_:publisher]">the contributors</span>
  of this work have waived all copyright and related or neighboring
  rights to this work.
</p>

See [LICENSE](./LICENSE) for the full text.
