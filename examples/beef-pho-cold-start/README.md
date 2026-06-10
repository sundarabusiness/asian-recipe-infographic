# Beef Pho — cold-start test artifact

This example is different from the others: it was produced by an agent that had never seen this project before.

The test: a Grok CLI session was given one message — the repo URL and "can you use it to make me a beef pho recipe?" No mention of SKILL.md, no mention of the agent's image capability, no coaching. The maintainer answered any questions the way a stranger would.

What the agent did on its own:

- Found SKILL.md and followed the two-deliverable structure
- Discovered its own image tool and produced the 9:16 front image
- Ran the verifier rules and said so: 4 servings, conservative fish sauce for a full pot of broth, no duplicate ingredients
- Picked up the project philosophy from the docs — its tips section opens with the safe-baseline principle and closes with adjust-at-the-table
- Hit the one known gap: its environment had no PDF tool, attempted to build one, and delivered DOCX/HTML/Markdown as the "or equivalent" fallback (tracked as a project issue)

Files here are exactly what the agent produced, unedited.
