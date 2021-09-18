# W5D2 Notes

## Relationship Types
1. One-to-Many
  - ex) users table + blogs table: one user can have many blogs but not the other way
2. one-to-one
  - ex) It's explicitly defined. If you set blogs.user_id as INTEGER UNIQUE, a user can only write one blog
  - one-to-one is rare. 
3. Many-to-Many
  - ex) when many users writes many blogs AND many users can write a same blog

## https://app.diagrams.net/