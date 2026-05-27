# Embabel Ticket Triage Agent

A **business-oriented AI agent** built with **Spring Boot**, **Java**, and **Embabel** that performs **enterprise ticket triage**:

* Classifies incoming tickets
* Assesses priority
* Routes them to the correct team
* Dynamically **replans** when information is incomplete or uncertain

This project is **not** a chatbot. It demonstrates how to implement **agentic workflows** in a **deterministic, testable, production-oriented** way on the JVM.

---

## Table of Contents

* [Features](#features)
* [Architecture](#architecture)
* [How the Agent Works](#how-the-agent-works)
* [Getting Started](#getting-started)

    * [Prerequisites](#prerequisites)
    * [Configuration](#configuration)
    * [Run locally](#run-locally)
* [Try It](#try-it)
* [Why Embabel?](#why-embabel)
* [Status](#status)

---

## Features

* Built with **Embabel 0.3.1**
* Invoke the agent via **REST API** (programmatic invocation)
* Combine **deterministic business logic** with **LLM-based decisions**
* Automatic **replanning** driven by domain types and missing signals
* **Tracing** for observability (see which actions executed and why)

---

## Architecture

* **Spring Boot**: runtime + REST API
* **Embabel**: agent execution + planning + replanning
* **OpenAI**: selected classification/prioritization steps
* Agent implemented as a **Spring-managed bean**

### Design principles

* Strongly typed domain model (no string-based state machine)
* Small, focused actions
* Clear separation between business logic and LLM usage
* Deterministic execution where possible

---

## How the Agent Works

The ticket triage agent performs these steps:

1. Extract signals from the incoming ticket
2. Classify the ticket category
3. Assess priority
4. Decide the target team
5. Return a structured response (including an execution trace)

If classification is uncertain, the agent **replans automatically** and triggers an additional action to resolve the uncertainty using an LLM.

---

## Getting Started

### Prerequisites

* Java 21+
* Maven
* OpenAI API key

### Configuration

Set your OpenAI API key as an environment variable:

```bash
export OPENAI_API_KEY=your_key_here
```

### Run locally

```bash
mvn spring-boot:run
```

The application starts on:

```text
http://localhost:8080
```

---

## Try It

The repository includes an IntelliJ **HTTP Client** file: `requests.http`

It contains multiple example requests, including:

* Normal incident (no replanning)
* Uncertain case (replanning triggered)
* Security incident (deterministic fast-path)
* Service request (LLM-based priority)
* Outage with VIP deadline

Each response includes a **trace** showing exactly which actions executed.

---

## Why Embabel?

Embabel is designed for building **enterprise-grade AI agents** on the JVM:

* Deterministic and explainable planning
* Type-safe, testable actions
* LLMs used as tools (not orchestration)

This project illustrates those principles in a minimal but production-aligned setup.

---

## Status

This is a **demo and reference implementation**.

It is intentionally simple, but architecturally aligned with how real production agents should be built.


---

🔗 [patbaumgartner.com](https://patbaumgartner.com) · [More talks & projects on GitHub](https://github.com/patbaumgartner)
