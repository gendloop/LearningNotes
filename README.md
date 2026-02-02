# template-GitbookProject

Used for creating Gitbook project repositories.

## Sample

Visit [https://gendloop.github.io/template-GitbookProject/](https://gendloop.github.io/template-GitbookProject/).

## Usage

1. Click on `Use this template` in the top right corner.
2. Wait for the `Init` workflow of the new project to complete.
3. At this point, the `Job/deploy` under `Actions/Gitbook_Deploy` may report an error, don't worry, continue with the following steps.
4. Click on the project's `Settings` => `Pages` => Change Source to `GitHub Actions` under `Build and deployment`.
5. Rerun `deploy`, and it should succeed.
6. Modify the configuration file `book.json` according to personal accounts, etc.
7. After making a modification, the website content will be refreshed.

## References

1. [learningnots/GitBook](https://www.yuque.com/gendloop/learningnotes/git-book)
