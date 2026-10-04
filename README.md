# Andre Balassiano

Full-stack web developer in Vancouver, BC. I used to be a physician. I practiced in Brazil, moved to
Canada, and retrained at BCIT, where I finished the Computer Systems Certificate with distinction.

I build web applications end to end, TypeScript on both sides, Express and Prisma over PostgreSQL on
the server and React on the client. I keep the layers separate, validate input before it reaches a
handler, write tests that fail for the right reasons, and leave comments that explain why rather
than what.

**I'm looking for a full-time junior full-stack role.**
[andrebalassiano@gmail.com](mailto:andrebalassiano@gmail.com) ·
[LinkedIn](https://linkedin.com/in/andrebalassiano/)

## superForum

A Reddit-style forum with communities, posts, comments, voting and user profiles. Two halves in one
repo, deployed as two services.

**[Live demo](https://superforum.vercel.app)** ·
**[Source](https://github.com/andrebalassiano/superForum)**

The API is TypeScript on Express 5, with Prisma over PostgreSQL and authentication handled by
Supabase. The client is React 19 with TanStack Query. A few things I'd point at if you're reading
the code:

- Every write is authenticated with a token the server verifies, and the user's identity comes from
  that token rather than from the request body. Ownership is checked in the service layer, so "that
  isn't yours" answers 403 and "that doesn't exist" answers 404.
- Vote counts are denormalized. The score moves as a delta inside the same transaction as the vote
  itself, and the client mirrors that with an optimistic update that patches every cached copy of
  the post and puts the old values back if the request fails. A profile's reputation is the same
  quantity summed over everything you've written, and it goes the other way: computed on read,
  stored nowhere, because nothing sorts by it and a stored copy could only drift from the votes
  behind it.
- Pagination is cursor-based with a stable tiebreak and an index behind it. The client consumes it
  with infinite scroll.
- 109 integration tests drive the real API against PostgreSQL in Docker, 37 more cover the client in
  React Testing Library, and both suites run in CI on every push.

But the part that taught me the most was deploying it. Three separate things broke, and not one of
them could have broken on my machine.

superForum started as a two-person project with Luiz Tatemoto during its first few weeks. Everything
after that, including the architecture, the React client, the tests and the deployment, is my own
work.

## Also

- [Paws](https://github.com/andrebalassiano/Paws), a responsive pet-adoption site in plain HTML, CSS
  and JavaScript.
- [Petsome](https://www.figma.com/proto/bn1NHUOJ3P6FBfD8XMMqBo/Petsome-screens--prototyped-?node-id=1-2&starting-point-node-id=1%3A2),
  a Figma prototype for a pet health tracker, built after interviewing 18 people.

## Tools I reach for

TypeScript, Node.js, Express, Prisma, PostgreSQL, Supabase, React, TanStack Query, React Router,
Tailwind, Vitest, Supertest, React Testing Library, Docker, GitHub Actions.
