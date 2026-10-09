---
title: "StudyQuest: revision as a ranked game"
date: 2026-10-09 12:00:00 +0100
categories: [Projects]
tags: [typescript, nextjs, react, postgresql]
---

StudyQuest is a revision web app for GCSE and A-level students that works like a ranked game. You revise with flashcards and quizzes, earn coins for work the server can verify, and play timed 1v1 quiz battles against other students on an Elo ladder.

The code is on [GitHub](https://github.com/ezawn/ranked-study-app). I built it with AI assistance from Claude Code.

## What it does

- **Ranked 1v1 battles.** Two players get the same questions for two minutes, and the result moves their Elo rating across eleven ranks.
- **A question bank** covering Maths, Further Maths, Physics, Chemistry, Biology and Computer Science at GCSE and A-level.
- **Flashcards** scheduled by adaptive spaced repetition, plus a cram mode.
- **Quizzes** with multiple-choice and written questions, where written answers are marked by AI.
- **A daily quiz** with streaks, and communities for sharing sets with a class.

## How it is built

The app uses Next.js, React and TypeScript, with PostgreSQL and Prisma for the database.

**The server decides everything.** The browser never decides a score, a deadline or a reward. Correct answers are stripped from everything sent to the browser, deadlines are stored on the server, and every coin award is a ledger row with a unique key, so submitting twice pays once.

**Matchmaking.** A player is paired with the closest-rated opponent in their rank. The longer they wait, the wider the range of ranks the matchmaker will accept.

**Battle scoring.** Only correct answers earn points, and the total is scaled by how reliable the player was. That means a fast, accurate player beats a slow one, and guessing loses.

**Generated questions.** Questions are produced by code from a seed. Each generator re-checks its own answer a second way before the question can be stored.

## What I would add next

- **Artwork** for the character cosmetics, which are placeholders for now.
- **WebSockets** for battles, which currently poll the server for the opponent's progress.
- **Team battles** between communities.
