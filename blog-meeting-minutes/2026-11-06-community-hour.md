---
title: Community Hour – 06.11.2026 (INVALID TEST FILE
description: "Unclosed quote and broken YAML
authors: [stephanbcbauer
tags: community-hour, : meeting-minutes
date: 2026-13-45
---

# Community Hour – Invalid Markdown Test

<!-- This file is intentionally broken for build/preview tests -->

## Unclosed JSX / HTML

<div className="agenda">
  <details>
    <summary>Agenda
  </div>

## Bare curly braces (MDX expression error)

The config value is {connector.version and must be >= {2.0

## Bare angle brackets (MDX tag error)

Use <EDC-Connector> with a version <0.8 or a link <https://example.com

## Broken import / export

import { Foo } from './does-not-exist'
export const broken = {

<Foo prop={unclosed />

##No space after heading hash
####### Seven hashes heading

## Broken table

| Item | Owner | Status
|---|---
| Release 26.12 | @stephanbcbauer | open | extra | cells |

## Unclosed code fence

```yaml
key: value
  bad-indent: [unclosed
