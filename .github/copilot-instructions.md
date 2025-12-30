---
description: AI rules derived by SpecStory from the project AI interaction history
globs: *
---

## HEADERS

This file defines all project rules, coding standards, workflow guidelines, references, documentation structures, and best practices for the AI coding assistant. It is a living document that evolves with user interactions and project needs.

## TECH STACK

*   Rust (latest stable)
*   Iced GUI framework
*   GStreamer (version >= 1.14) - Multimedia framework
*   Homebrew (macOS package manager)

## PROJECT DOCUMENTATION & CONTEXT SYSTEM

All project documentation is stored in markdown format.
Each user interaction is saved as a separate markdown file named with a timestamp and a short description of the interaction. These files are stored in a directory structure that reflects the project's organization.

## CODING STANDARDS

*   Follow Rust's official coding guidelines.
*   Write clear, concise, and well-documented code.
*   Use descriptive variable and function names.
*   Adhere to the principle of least privilege.
*   Handle errors gracefully and provide informative error messages.
*   Avoid using reserved keywords as identifiers. If you must, use the `r#` prefix (e.g., `r#gen`), but it's clearer to just rename the variable.
*   When using `std::env::set_var`, enclose it in an `unsafe` block.

## WORKFLOW & RELEASE RULES

*   Use Git for version control.
*   Follow a branching strategy (e.g., Gitflow).
*   All code changes must be reviewed before being merged.
*   Automated tests must pass before each release.
*   Releases should be tagged with semantic versioning.

## DEBUGGING

*   Use the `cargo build` command to compile the project and check for errors.
*   Use the `cargo test` command to run automated tests.
*   Use the `println!` macro for debugging output.
*   Use a debugger (e.g., lldb) for more advanced debugging.
*   Set the `CARGO_PROFILE_DEV_BUILD_OVERRIDE_DEBUG=true` environment variable to enable debug information generation for build dependencies.

## DEPENDENCY MANAGEMENT

*   Use `cargo add <dependency>` to add new dependencies.
*   Use `cargo update` to update dependencies.
*   Use `cargo outdated` to check for outdated dependencies.
*   Use `rustup update && rustup upgrade && cargo install-update --all` to update Rust and installed cargo tools.
*   If `cargo outdated` fails due to feature conflicts, use `cargo add <dependency>` to explicitly add the dependency with the required features.

## THIRD-PARTY LIBRARIES

*   When incorporating third-party libraries, always evaluate their license and security implications.
*   Prefer well-maintained and widely used libraries.
*   Keep track of all third-party libraries used in the project, including their version and license.

## MACOS SPECIFIC RULES

*   When using GStreamer on macOS, ensure it and its plugins are installed via Homebrew:
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    brew install gstreamer gst-plugins-base
    brew install gst-plugins-good gst-plugins-bad gst-plugins-ugly gst-libav
    ```
*   After installing GStreamer, set the `PKG_CONFIG_PATH` environment variable:
    ```sh
    export PKG_CONFIG_PATH="/opt/homebrew/lib/pkgconfig:$PKG_CONFIG_PATH"
    ```

## MAINTENANCE RULES

*   Periodically clean up the `.cargo` folder to free disk space and resolve potential build or dependency issues. Recommended steps:
    1.  Remove unused crate versions: `cargo cache -a` (requires `cargo install cargo-cache`).
    2.  Remove old, unneeded binaries: `rm ~/.cargo/bin/<unneeded-binary>`.
    3.  Clean up build artifacts in your project: `cargo clean`.
    4.  Optionally, clear the registry cache manually: `rm -rf ~/.cargo/registry/cache`.
    *   Avoid deleting the entire `.cargo` folder unless absolutely necessary.