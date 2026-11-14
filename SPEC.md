<!-- keel:spec v1 -->

# Keel

## Problem

Project management tools require manually writing specs and tickets, and don't connect to AI that can actually build the work.

## Goal

A project management site where a user enters a prompt, AI generates the specs and tickets, and the user can trigger an LLM to build each ticket from within the site.

## Target users

Small teams building software

## Project type

Web app: Web-based project management site with native LLM integration

## Core features

### F1. Prompt to specs and tickets

User enters a prompt describing a project; an LLM generates a spec and a set of tickets.

Acceptance checks:

- Submitting a prompt creates a project with a generated spec
- Generated tickets appear in the project's ticket list

### F2. Trigger ticket build

User can trigger an LLM to build a ticket from the site; the result is a pull request in the connected GitHub repo.

Acceptance checks:

- Each ticket has a Build button
- Clicking it starts a build and the ticket shows its status
- On success the ticket links to a GitHub pull request

## Out of scope

- Comments on tickets
- Notifications
- Git hosts other than GitHub

## Data model

### Entities

- **Team**: A group of users sharing projects.
  Fields: id, name
- **User**: A person signed in via GitHub.
  Fields: id, githubId, name, email
- **Project**: A project with its AI-generated spec and linked GitHub repo.
  Fields: id, teamId, name, prompt, spec, githubRepo
- **Ticket**: A unit of work generated from a project spec.
  Fields: id, projectId, title, description, status, buildStatus, prUrl

### Relationships

- Team → User (many-to-many): Users belong to teams.
- Team → Project (one-to-many): A team has many projects.
- Project → Ticket (one-to-many): A project has many tickets.

## Integrations

- **GitHub**: LLM-built tickets produce a branch and pull request in the team's GitHub repo.
- **Anthropic API**: Generates specs and tickets from prompts and builds code for tickets.

## Auth

Sign in with GitHub OAuth, which also grants repo access for PRs. Users belong to teams that share projects.

## Deployment target

Vercel for the web app, with a hosted Postgres (e.g. Neon or Supabase) and background jobs for long-running ticket builds.

## Constraints and preferences

None.
