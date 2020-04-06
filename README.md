# TRUSTOS DOCS

## Documentation

### Setting up your own staging repo and publication website

You can easily build your own staging repo following these steps:

1. Go to http://readthedocs.org and sign up for an account.
2. Create a project.
   Your username will preface the URL and you may want to append `-trustos` to ensure that you can distinguish between this and other docs that you need to create for other projects. So for example:
   `yourgithubid-trustos.readthedocs.io/en/latest`.
3. Click `Admin`, click `Integrations`, click `Add integration`, choose `GitHub incoming webhook`,
   then click `Add integration`.
4. Fork [TrustOS on GitHub](https://github.com/telefonica-tid/trustos).
5. From your fork, go to `Settings` in the upper right portion of the screen.
6. Click `Webhooks`.
7. Click `Add webhook`.
8. Add the ReadTheDocs's URL into `Payload URL`.
9. Choose `Let me select individual events`:`Pushes`、`Branch or tag creation`、`Branch or tag deletion`.
10. Click `Add webhook`.

Now anytime you modify or add documentation content to your fork, this
URL will automatically get updated with your changes!

### Building the docs on your machine

Here are the quick steps to achieve this on a local machine without
depending on ReadTheDocs, starting from the main trustos
directory. Note: you may need to adjust depending on your OS.

Prereqs:
 - [Python 3.7](https://wiki.python.org/moin/BeginnersGuide/Download)
 - [Pipenv](https://docs.pipenv.org/en/latest/#install-pipenv-today)

```
cd trustos/docs
pipenv install
pipenv shell
make html
```

This will generate all the html files in `docs/build/html` which you can
then start browsing locally using your browser. Every time you make a
change to the documentation you will of course need to rerun `make
html`.
