# How to document and review code using Git

This document is a condensed extract of the principles of using the [git](https://git-scm.com/) version control system.
For more detailed explanation, please read the [references](#references).
It is assumed here that the usage of git is already known.


## Commit messages

The commit messages are important component of the product source, they
 - document the intentions, goals of the authors in the evolution of the code;
 - help the reviewer.

The documentation stored in the commit messages (git history) is directly coupled with the code,
unlike an attached documentation which can be easily forgotten to be kept up to date with the code
and also the reference to the code is not direct.


### The format and content of the commit message

- [ ] A commit message shall consist of a _short first line_ (subject)
and optionally, an empty line followed by a detailed _description_ in multiple lines.

- [ ] The _short first line_ of the commit message
 - shall describe the goal or the reason of the change in
   - plain English and
   - imperative present;
 - shall start with a short prefix referring to the corresponding component or task ID;
 - shall have _no_ punctuation at the end.

Examples:

| right |
|-------|
| scripts: enable tests to be able to run in a self-contained environment |
| Makefile: fix typo |

| wrong | suggested replacement |
|-------|-----------------------|
| fix some bugs | module: fix the lowercase function to make also XYZ letters lowercase |
| sum: sum items in the sum function | module: calculate total energy |
| some_file.cpp | module: add parity check |

[Git](https://en.wikipedia.org/wiki/Git) was originally developed to document the changes
of the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel),
therefore further good examples can be found in the [Linux kernel repository](https://github.com/torvalds/linux/commits/master).

- [ ] The detailed description shall be written in plain English _with_ punctuation.

- [ ] Avoid
 - using verbs with general meaning, e.g.: "update", "improve", these are only for last resort in trivial cases;
 - meaningless or too general description, e.g.: "fix the problem", "fix logging";
 - describing what is also visible in the change.


## Rule of thumb in committing

- [ ] One commit shall include only the simple described change.

The following actions, neither the same type, should not be mixed, commit them separately:
 - non trivial changes keeping the same functionality (refactor)
 - implementation of a requirement
 - bug or typo fix
 - whitespace changes, especially far from the interesting code change

When the first short line cannot be composed briefly and clearly,
it indicates that some of the above actions may be mixed.

- [ ] The description of the goal and the reason of adding or modifying some code
should be placed into the commit messages, but not into the source code.

- [ ] Commented out code must not be committed, it must be deleted.

- [ ] Commits to be reviewed should contain finished work.
Temporary modification (e.g. implementation) of the same lines of the same file
should be squashed into a single commit before code review.


## Preparing commits for review

The git version control system supports rearranging commits with _interactive rebase_.
So, during implementation phase, there is no need to make perfect commits.
Right before code review, it is enough to fine tune the topic branch
to help the reviewer and to make the git history clear and helpful for later use.

- [ ] The aim is to get the _minimum number of commits_ each of them having the _minimal scope_:
 - Temporary and fixup commits should be _squashed_;
 - Commits having multiple scope should be _split_.

- [ ] Also commit messages can be easily _reworded_.

See also: [Git rebase in depth].


## Code Review

Pros:
 - everybody can make mistakes that can be noticed easier by others;
 - the cheapest error detection and correction;
 - more maintainable code, better solutions;
 - helps knowing code base;
 - helps learning.

- [ ] The _developer_, who has changed the code,

shall ask the _reviewer_ for reviewing the changes.

- [ ] The developer has the responsibility to manage the review process.

- [ ] The reviewer shall check
 - the format of the commit messages;
 - the content of the commits, the changes;
 - that the commit messages are truly describe the changes;
 - the complexity of the commits, one commit should have one simple goal.

- [ ] The review comments should be constructive:
 - Give suggestions, if it is possible;
 - Give a reason for the suggestion, if it is not trivial;
 - Give a reason why rejecting a suggestion;
 - Avoid fake reasoning, e.g.: "it is working", "it is good like that";
 - Avoid emotional opinion, e.g.: "I do not like it", "it is strange", "you are not competent";
 - Avoid suggestions based on personal preferences in a solution or readability.

- [ ] The review comments shall be reacted.

- [ ] A suggestion shall be accepted, if there is no reason to reject it.


## References

[Git rebase in depth]

[Git rebase in depth]: https://git-rebase.io

https://wiki.openstack.org/wiki/GitCommitMessages

https://chris.beams.io/posts/git-commit/

https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53
