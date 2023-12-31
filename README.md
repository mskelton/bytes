# Bytes

The source repository for my website's "bytes" (mini posts).

## How it works

Changes to this repo will be published via a webhook to my website. My
website then will pickup those changes and index the content into the
database which will then present the content to the users.

This technique works well as it doesn't require me to redeploy my website
when adding bytes, and it also allows me to add bytes while working on
other feature branches for my website without worrying about switching
between branches.
