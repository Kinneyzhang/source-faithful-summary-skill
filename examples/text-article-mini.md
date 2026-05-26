# Mini Example: Text Article

This fictional example shows how the skill handles a written source without timestamps.

## Source excerpt

A policy analyst argues that remote work did not simply move office tasks into homes. It changed coordination costs. The author says remote teams succeed when they make decisions more explicit, write down assumptions, and reduce hidden dependencies. The article also warns that documentation can become performative if no one reads it. The author does not claim every company should be remote; the recommendation is limited to teams whose work can be decomposed and reviewed asynchronously.

## Weak generic summary

The article says remote work is effective when companies document more and communicate clearly.

## Source-faithful summary

The author is not making a blanket pro-remote argument. Their main claim is that remote work changes coordination costs: teams lose some informal office context, so decisions, assumptions, and dependencies must become more explicit. Documentation is presented as a tool for making coordination visible, not as a cure-all; the author warns that unread documentation becomes performative. The recommendation is limited to teams whose work can be decomposed and reviewed asynchronously.

## Decision model map

- Constraint: remote work removes informal shared context.
  - Failure it causes: hidden dependencies and implicit decisions become harder to detect.
  - Author judgment: make decisions and assumptions explicit.
  - Action: document assumptions, reduce hidden dependencies, review work asynchronously.
  - Tradeoff/limit: documentation fails if it becomes unread ritual.
