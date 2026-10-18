---
title: "Localizing Black ICE, the Biggest HOI3 Mod, into Chinese"
date: 2026-10-18
layout: post
categories: [personal]
author: Ju Qi
lang: en
translation_key: black-ice-chinese
excerpt: "A game I have played for over a thousand hours, and a wish that sat around for years: if only Black ICE were in Chinese. In 2026 I finally built it — 95.8% of the text, an engine that only understands 8-bit glyphs, and one assembly instruction that clobbered a register."
---

I started playing *Hearts of Iron III* in high school and never really stopped — university and graduate school included, more than a thousand hours in total. Black ICE was always my favourite mod: supply is unforgiving, industry is a real planning problem, and the order of battle of a single armoured corps can eat an afternoon. But my English could not keep up with the reading — three hours of play meant two hours in a dictionary.

So the wish sat there for years: **if only Black ICE were in Chinese.**

In 2026 I finally built it. The repository is [BlackICE-Chinese](https://github.com/Zealoter/BlackICE-Chinese): Black ICE merged with the community's Chinese localization of the game, so that it opens in Chinese and can be played from start to finish.

## The hard part was not translation

The engine was. The stock `hoi3_tfh.exe` only understands 8-bit glyphs, so the Chinese text simply would not display — drop it in and the interface shows blanks or garbage.

Half of the project therefore went into patching the executable:

- reading glyphs at 16 bits instead of 8: 42 patch sites plus an 8 KB new code section;
- fixing a guaranteed `0xC0000005` crash. The root cause was small: inside a code cave, `mov cl,[edx+eax]` clobbered the caller's `ecx`, which held the string capacity 15; the following `cmp ecx,0x10` then took the heap-pointer branch and dereferenced inline characters as a pointer. The fix is two bytes;
- enabling the 4 GB address space (LAA), without which the late-game map runs out of memory.

The patches are made offline; nothing is injected into a running process.

## Where it stands

- 80,195 of 83,751 localization strings translated, **95.8%**;
- general names (21,623 unique names), unit designations (8,472) and cabinet ministers (5,993 unique names) all at **100%**;
- weapon models and specifications deliberately left in English: `381mm MkII`, `Mark 20 Bidder`. Chinese players read those in English anyway, and a forced translation makes them harder to recognise.

What is still missing: a handful of theatre HQ names and one full play-through.

## Why write it down

None of this is useful. It will not become a paper or the first line of a CV. But it is the most complete idea-to-delivery project I have done in years: direction, trade-offs and acceptance were human; AI read assembly, read crash dumps and wrote verification scripts, and also made mistakes that a human had to catch. The tools, the hours and the token usage are all recorded in the repository's `ABOUT.md`, so anyone can check.

I have come to feel that a person should not be judged by papers alone. Projects, questions and long-held interests probably say more about who someone is — which is also why I am putting this material on my homepage.
