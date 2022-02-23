---
title: Rails Cheatsheet
tags: rails ruby
---

## CLI

```bash
# Run local server
rails server

# Launch console
rails console

# Yarn install
rails yarn:install
```

## Scaffold

### Generation

```bash
# Generate view, model, controller, migration
rails generate scaffold Article word_count:integer content:text

# Generate model, controller, migration for a RESTful API
rails generate scaffold_controller Article word_count:integer content:text
```

## Model and Migration

### Types

- integer
- primary_key
- decimal
- float
- boolean
- binary
- string
- text
- date
- time
- datetime
- references
- belongs_to

### Generation

```bash
# Generate a model
rails generate model MyModel field1:integer field2:references

# Generate a migration to add a reference from article to author
rails generate migration AddAuthorToArticle author:references
```

> The table which belongs to another will possess the _id column. i.e. `add_reference :table_which_belongs_to, :table_to_which_is_belonged`.

### Database operation

```bash
# Migrate
rails db:migrate

# Rollback last migrate
rails db:rollback
```