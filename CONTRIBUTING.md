# Contributing

Thanks for helping make the lessons clearer and more useful.

Small fixes are welcome as pull requests. If you want to add a lesson or make a large change, open an issue first so we can agree on where it belongs and avoid doing the same work twice.

## Writing

- Use everyday English and explain a technical term when it first appears.
- Say exactly what the reader should do and what they should expect to see.
- Connect each paragraph to the one before it instead of using short, disconnected statements.
- Keep examples safe to run on a local computer.
- Do not test a public system or any system you do not own without written permission.
- Link to the source when a claim, command or version depends on outside documentation.

## Changing the Curriculum

The files in `curriculum/` contain three learning paths. Keep each topic under the path where a learner would need it, and check that the table of contents still points to the right headings.

Before opening a pull request, run:

```bash
npx --yes markdownlint-cli2 "**/*.md"
```

In the pull request, explain what you changed, why it helps and how you checked it.

By contributing, you agree that your changes may be shared under the repository's [CC BY 4.0 license](LICENSE).
