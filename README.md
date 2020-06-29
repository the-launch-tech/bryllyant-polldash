# PollDash

### Thoughts

This was very fun. I've never used TypeORM or NestJS and got rather obsessed. I wish I had scoped things a little better, and that I had more time to learn this particular query building syntax so I could be more concise. There are similarities with the Laravel Eloquent ORM, but TypeORM isn't quite as developed yet - but as far as JS ORM's it's great.

I initially approached things very methodically with the aim of building something that had an architecture that could be expanded with more features rather than just meeting the short-term requirements - just in principle. If I had more time I would continue refactoring the things that were completed towards the end. I also would have used Bootstrap or Material Design instead of doing all the SCSS in order to reduce some overhead in style writing.

---

### Setup

1. Add the .env files to /client and /server roots.
2. Using `NodeJS 14.4.0`

---

### Start Commands [https://medium.com/@gausmann.simon/nestjs-typeorm-and-postgresql-full-example-development-and-project-setup-working-with-database-c1a2b1b11b8f]

##### Server (NestJS, Typescript, Postgres, TypeORM)

1. `npm i`
2. `npm run typeorm:migration:run` - Runs migration
   - `npm run typeorm:migration:revert` - Reverts migration
3. `npm run prod:build` - Builds /dist
4. `npm run prod:start` - Starts from /dist/main.js

##### Client (Server Side Rendered ReactJs, NodeJS, Express)

1. `npm i`
2. `npm run prod:build` - Builds production bundles
3. `npm run prod:start` - Starts Express server for SSR, ready

---

### Features

- Multiple admins with individually scoped Users, Groups, Polls, Questions, and Distributions (of polls)
- Admins can create other Users, or Admins
- Users can be placed into admin Groups and Groups can be Distributed Polls
- Repeater field can be used to build Polls with Questions
- Each Distribution can be tracked, and each question is a "yes" | "no" enum response. The statistics are monitored.
- JWT authentication implemented for role-based access control using NestJS decorators
- Normal users can login, but only have partial access to views
- You may be logged out to take the survey you are sent, or logged in
- The survey email can be mocked but it can also be sent with SendGrid API
- On boot we seed the table with our admin@example.com
- The survey link uses a decoded JWT token for tracking
- More stuff...

---

### Pages

##### Home `/`

a. Public
b. Landing page

##### Login `/users/login`

a. Public
b. login page

##### Register `/users/register`

a. Public
b. registration page (for self-registering users open to all-admin scopes)

##### Dashboard Main `/auth/{id}`

a. User Controlled
b. general information

##### User Management `/auth/{id}/users`

a. dmin Controlled
b. create and view your scoped users

##### Group Management `/auth/{id}/groups`

a. dmin Controlled
b. Create groups and add users. Users that self register are availaable to your scope.

##### Poll Delegation `/auth/{id}/polls`

a. dmin Controlled
b. Create Polls and send distributions. You can use SendGrid, or Mock the email.

##### Distribution Meta `/auth/{id}/distributions`

a. dmin Controlled
b. Mocks links go here. We dig into each admin-created distribution of a poll. A Poll can be distributed multiple times, and each distribution has responses. Here we can view a lot of details about the distribution(s) state.

##### Response History `/auth/{id}/responses`

a. User Controlled
b. View Auth Responses, Received Responses, and Sent Distributions. General Overview.

##### Single User `/auth/{id}/users/{userId}`

a. dmin Controlled
b. Accessible only through link in Response History. View individual user statistics.

### Issues Encountered

1. On initial compile of NestJS: `No valid exports main found for '/Users/danielgriffiths/Desktop/bryllynt-dash/polldash/node_modules/uuid'`
   - Solution: Update NodeJS to 14.4.0
2. Experimenting with TypeORM, wish I could be more acquainted with the Entity and Repository API's.

---
