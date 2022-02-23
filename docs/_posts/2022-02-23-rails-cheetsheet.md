---
title: Rails Cheetsheet
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
rails generate scaffold MyPage field1:integer field2:string

# Generate model, controller, migration for a RESTful API
rails generate scaffold_controller MyPage field1:integer field2:string
```