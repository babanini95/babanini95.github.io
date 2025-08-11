+++
title = 'Diaper Duty Tracker'
author = 'Abdullah Robbani'
date = 2025-08-11T12:25:03+08:00
draft = false
tags = ["go", "cli"]
categories = ["personal project"]
+++

As a new parent and a developer who lives in the terminal, I ran into a recurring problem: my wife would ask, "When was the baby's last diaper change?" and I'd often draw a blank. For a newborn, this is a crucial piece of information. I realized I could solve my own problem with the skills I was learning, and so the **Diaper Duty Tracker** was born.

This project is a command line application built with Go, designed to be a fast, efficient, and user friendly way for parents to track their baby's needs right from the terminal.
<!--more-->
___

## Core Features

The initial version of the application is a complete, standalone CLI tool with a full set of features:

* **Interactive Setup:** A one time `init` command to create a profile for your baby.
* **Smart Logging:** Quickly `log` a diaper change, with flags to specify a past time (`-t "2:30PM"`) or add notes (`-n "..."`).
* **Instant Status:** The `status` command provides an immediate summary of the last change and calculates when the next one is due based on the baby's age.
* **Daily History:** The `history` command gives a clean overview of all changes logged for the day.
* **Easy Configuration:** Users can override the smart defaults and `config` a custom reminder interval.

___

## Technical Stack

My goal was not just to build a script, but to build a professional, maintainable application. The technology choices reflect this:

* **Go & [Cobra](https://cobra.dev/):** Go was the perfect choice for creating a fast, single binary executable that runs natively on any OS. The **Cobra** library provided a powerful framework for building a feature rich and user friendly CLI.

* **SQLite & [`sqlc`](https://sqlc.dev/):** I chose **SQLite** as the database because it's **embedded**, meaning it runs within the application process without needing a separate server. This makes the application completely self contained. To interact with it, I used **`sqlc`** to generate fully **type safe Go code** from my raw SQL queries, which eliminated boilerplate and prevented common runtime errors.

* **[Goose](https://github.com/pressly/goose) & Embedded Migrations:** To manage the database schema, I used **Goose**. In a major architectural improvement, I embedded the SQL migration files directly into the Go binary using `//go:embed`. The application runs these migrations automatically on initialization, providing a **zero setup experience** for the end user. They don't need external `.sql` files or a separate migration tool to get started.

* **Smart & Robust File Handling:** Initially, the app stored its data in the current directory. I quickly evolved this to a more robust solution where the database is stored in a dedicated folder in the user's home directory (`~/.diaper-duty/`). This allows the application to be installed globally via `go install` and run from anywhere on the system without permissions issues.

___

## Future Plans

This initial version lays a solid foundation. The next major step is to evolve the application's architecture by building a background **API server** and a simple, mobile friendly **Web UI**. This will allow non technical users (like my wife!) to use the tracker from their phone's web browser, while the CLI remains fully functional for developer users like me.
___

You can check the repo here: *[github.com/babanini95/diaper-duty](https://github.com/babanini95/diaper-duty)*
