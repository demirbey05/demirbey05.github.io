---
title: "Erdős Problem Solver"
date: 2026-04-26
draft: false
tags: ["Go", "AI", "agents", "open-source"]
summary: "A Go CLI agent that fetches unsolved Erdős problems and uses LLMs to generate formal proof attempts."
weight: 1
---

## Erdős Problem Solver Agent

An AI-powered CLI tool that automatically discovers and attempts to solve open mathematical problems from the [Erdős Problems](https://www.erdosproblems.com/) database.

### Features

- 🔍 Scrapes and parses open problems with associated prizes
- 🤖 Supports multiple LLM providers (OpenAI, Gemini, Anthropic) via `anyllm`
- 📝 Generates structured formal proof attempts
- ♻️ Continuous execution loop across multiple problems
- ⏱️ Robust error handling with retry logic and configurable timeouts

### Tech Stack

`Go` · `anyllm` · `colly` · `GitHub Actions`

### Links

- **Source Code**: [github.com/demirbey05/erdos-agent](https://github.com/demirbey05/erdos-agent)
- **Blog Post**: [Building an AI Agent to Solve Open Mathematical Problems](/posts/erdos-agent/)
