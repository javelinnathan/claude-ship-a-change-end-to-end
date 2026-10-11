# Notes

## Plan
Add `PUT /users/:id`: an `updateUser` helper in `db/store.js`, then a route in
`routes/users.js` that validates the body (400), looks up the user (404), and
returns the updated user (200). Validation runs before the lookup so a bad body
is always a 400. I added a string/non-empty check beyond the falsy check POST
uses, to cover the README's "invalid fields". A non-numeric id falls through to
404, matching `GET /users/:id`. The plan was not edited after it was drafted.

## Model
Sonnet 5.5. The change is small and follows existing patterns, so a faster
model was enough.

## Commits
1. `Add updateUser to the in-memory store`: data layer only.
2. `Add PUT /users/:id endpoint`: route and validation.
3. `Add NOTES.md`: this file.

## Review
Checked that `npm run lint` is clean and `npm test` is green, and that the
validation order matches what `tests/update-user.test.js` expects (400 for
user 1 with a missing email, 404 for user 9999 with a valid body). One
behaviour to be aware of: `updateUser` mutates the stored object in place,
which is consistent with how `createUser` stores objects in the array.
