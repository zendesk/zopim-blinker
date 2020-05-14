[![Build Status](https://travis-ci.org/jek/blinker.svg?branch=master)](https://travis-ci.org/jek/blinker)
[![codecov](https://codecov.io/gh/zendesk/zopim-blinker/branch/master/graph/badge.svg)](https://codecov.io/gh/zendesk/zopim-blinker)


# Blinker

## Description
Blinker provides a fast dispatching system that allows any number of
interested parties to subscribe to events, or "signals".

Signal receivers can subscribe to specific senders or receive signals
sent by any sender.

Blinker requires **Python 2.4 or higher, Python 3.0 or higher, or Jython 2.5 or higher.**

## Owners

While anyone can contribute to the repository, the primary owner of this repository is **[Pikachu](https://cerebro.zende.sk/teams/pikachu)**, located in Singapore.

| Channel  | Contact                                                           |
|----------|-------------------------------------------------------------------|
| Slack    | [Pikachu](https://zendesk.slack.com/archives/ask-pikachu)         |
| Email    | pikachu@zendesk.com                                               |
| GitHub   | [@zendesk/pikachu](https://github.com/orgs/zendesk/teams/pikachu) |

We are working in **Singapore Time** (SGT) (UTC +8).

## Table of Contents

* [Example Usage](#example-usage)
* [Changelog Summary](#changelog-summary)
* [Contributing](#contributing)

## Example Usage
```
>>> from blinker import signal
>>> started = signal('round-started')
>>> def each(round):
...     print "Round %s!" % round
...
>>> started.connect(each)

>>> def round_two(round):
...     print "This is round two."
...
>>> started.connect(round_two, sender=2)

>>> for round in range(1, 4):
...     started.send(round)
...
Round 1!
Round 2!
This is round two.
Round 3!
```

See the [Blinker documentation](https://pythonhosted.org/blinker/) for more information.

## Changelog Summary
<details>
    <summary>
        1.5 (June 23, 2017)
    </summary>

- Add support to connect via multiple objects using `connect_via_multiple`
</details>

<details>
    <summary>
        1.4 (July 23, 2015)
    </summary>

- Verified Python 3.4 support (no changes needed)

- Additional bookkeeping cleanup for non-ANY connections at disconnect
  time.
  
- Added Signal._cleanup_bookeeping() to prune stale bookkeeping on
  demand
</details>

<details>
    <summary>
        1.3 (July 3, 2013)
    </summary>

- The global signal stash behind blinker.signal() is now backed by a
  regular name-to-Signal dictionary. Previously, weak references were
  held in the mapping and ephermal usage in code like
  ``signal('foo').connect(...)`` could have surprising program behavior
  depending on import order of modules.
  
- blinker.Namespace is now built on a regular dict. Use
  blinker.WeakNamespace for the older, weak-referencing behavior.
  
- Signal.connect('text-sender') uses an alterate hashing strategy to
  avoid sharp edges in text identity.
</details>


For older versions, see details [here](https://github.com/zendesk/zopim-blinker/blob/master/CHANGES).

## Contributing

- [Useful guide to good commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- Commit messages should _not_ contain issue key. Put them in the PR instead. There is nothing wrong with having the issue IDs in the commits, but putting them only in the PR will save some characters per commit.
- Each commit message should be a representative of what that commit contributes to the repo, not something unhelpful like "Add tests", or "Cleanup" or "JIRA-123FU". By looking at the message one should have a reasonable understanding of the purpose behind the commit.
- You need 2 :+1:s and a green Travis build to merge PRs.
- For major changes, get someone from Pikachu to review the PR. (Ping [#ask-pikachu](https://zendesk.slack.com/archives/ask-pikachu))
