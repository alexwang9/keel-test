# Interview transcript

### You

i want to build a project management site that is natively integrated with AI. a user should be able to put a prompt in, and it will generate all the specs and tickets and is natively integrated with an llm so a user can trigger the ticket builds from the site

### Keel

Good start. Two questions:

1. What does "build a ticket" produce? For example, the LLM writes code and opens a pull request in a GitHub repo, or it just shows generated code or output on the ticket. I'd suggest the GitHub PR option. Is that right?
2. Who is this for: solo developers, small teams, or something else?

### You

1. github pr option
2. small teams

### Keel

Next:

1. Auth: I'd suggest sign-in with GitHub (which also gives repo access), with teams/workspaces that share projects. OK?
2. Data model: I'm thinking Team, User, Project (with spec), Ticket (title, description, status, PR link). Anything to add or change?
3. Which LLM provider do you want (e.g. Anthropic, OpenAI), and what should it be hosted on (e.g. Vercel)? And do you have a name for the product?

### You

1. ok
2. nope
3. anthropic, not sure where it should be hosted you give a rec, and come up with a name

### Keel

I've filled in the rest:

- **Name:** Keelboard
- **Hosting:** Vercel for the app and a hosted Postgres database. Ticket builds run as background jobs, since they can take a while.
- **LLM:** Anthropic
- **Auth:** GitHub sign-in, with teams.

Do you want to move anything to out of scope for v1? I'd suggest comments, notifications, and non-GitHub git hosts. If you're happy with the spec, I'll finalize it.

### You

finalize
