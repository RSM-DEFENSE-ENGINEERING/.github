# RSM Defense Engineering Git Guide
This document will provide guide lines and standards to promote clean maintainable code.
## Secret Storage
- Prefer storing API Tokens/secrets in environment variables and use libraries like os in python, std::env in rust, or node's process.env to retrieve
This prevents them for being stored in our github repos.
- For local testing use .env files to store environment variables but **ENSURE** .env file is added to the .gitignore file.
- If you must use a .json again add it to the .gitignore file
- [If you are unsure how to best use .gitignore](https://github.com/github/gitignore)

## Readmes
- Readmes should contain
1. Basic summary and overview of the project
2. Information required to get a dev environment up and running... for most this will be a simple pip install -r requirements.txt
3. Include steps to compile, bundle(if necessary), and deploy. If hosted on cloud service a deployment script is preferred
i.e. this script deploys the alert closer to the lambda function w/ proper AWS role
```bash
cargo lambda build --release
cargo lambda deploy --binary-name test-stellar --iam-role arn:aws:iam::216570687663:role/lambda-s3-alert-closer \
    stellar-alert-closer
```
4. Any other special requirements

## Commits
- When commiting changes to code each commit should be as small as possible following guidelines set by "atomic commits"
They should change one thing only
- Commit messages should be descriptive they should finish the sentence
**If applied, this commit will** <your commit message>
- They should be written in the imperative form, i.e. Fix bug xyz **NOT** fixed bug xyz
- Where possible apply fix:, feat:, docs: to front of commit message to indicate where change was made
### Examples of good commit messages:
- Feat: Add concurrency to http request
- Fix: Bug with input field not rendering

## Branches
- When making changes to code base create a new branch and follow commit naming convention:
- In a project where CAB needs to be invovled in creating changes the main branch should be **LOCKED** for direct commits
    It should only be altered through a pull request approved by reviewers

## Comments & Documentation
- All Code should be well documented such that someone familiar with the language can understand what is going on
- NOTE: Assume person reading code can understand basics, i.e. this would be over commenting to compensate for bad code
```rust
//Import utilities module
mod collin's_module;
//Set host
static x: &str = "google.com";
```
- Allow code to document itself through proper variable naming, we can refactor above to to maintain meaning without comments
```rust
mod utils;
static base_url: &str = "google.com";
```
- For documentation comments use your language's industry standard
- - For python this means PEP 257 -- Docstring Conventions
- - For rust, [RustDoc](https://doc.rust-lang.org/beta/rust-by-example/meta/doc.html)
- - For javascript, just use typescript or JsDoc if you must use javascript
- Changes to be made later or possible improvements can be denoted with a comment like //TODO: <Message>

## Formatting
- Please use your language standard formatting rules, for python this means PEP
- For javascript it's the wild west but keep it consistent
- Neovim and VSCode both have extensions to autoformat on save

## Code Review
TODO
Talk about what we would like to see, i.e. Every CAB member could be code reviewer or it could just be one member who acts for CAB

### Testing
Do we want to enforce unit test or just strongly suggest?? test requirements seems annoying and perhaps overkill... talk more about this
