Replicated Seldon Starter
==================

Example project showcasing how power users can combine several Replicated tools in order to manage
Replicated YAML for a [SeldonIO](https://www.seldon.io) ML project using a git repository.

### Prequisites

- [node](https://nodejs.org/en/download/)
- `make`
- A git repository created to manage your Replicated YAML. We'll use github in this example.

### Get started

This repo is a [GitHub Template Repository](https://help.github.com/en/articles/creating-a-repository-from-a-template). You can create a private copy by using the "Use this Template" link in the repo:

![Template Repo](https://help.github.com/assets/images/help/repository/use-this-template-button.png)

You should use the template to create a new **private** repo in your org, for example `mycompany/replicated` or `mycompany/replicated-starter-kubernetes`.

Once you've created a repository from the template, you'll want to `git clone` your new repo and `cd` into it locally.


#### Configure environment

You'll need to set up two environment variables to interact with vendor.replicated.com,


```
export REPLICATED_APP=...
export REPLICATED_API_TOKEN=...
```

`REPLICATED_APP` should be set to the app slug from the Settings page:

<p align="center"><img src="./doc/REPLICATED_APP.png" width=600></img></p>

Next, create an API token from the [Teams and Tokens](https://vendor.replicated.com/team/tokens) page:

<p align="center"><img src="./doc/REPLICATED_API_TOKEN.png" width=600></img></p>

Ensure the token has "Write" access or you'll be unable create new releases. Once you have the values,
set them in your environment.

You can ensure this is working with

```
make list-releases
```

#### Iterating on your release

Once you've made changes to `replicated.yaml`, you can push a new release to a channel with

```
make release
```

By default the `Unstable` channel will be used. You can override this with `channel`:

```
make release channel=Beta
```

If you have nodejs installated, you can lint your YAML before releasing with

```
make lint
```

or even

```
make lint release
```

### Adding ML Models

There is an example model written as a `SeldonDeployment` in `base/seldon-deployment-mc.yaml`. You can change the image there, or add additional
`SeldonDeployment` objects in that folder. You'll also need to add them to the list of `resources` in `base/kustomization.yaml`.

The [source of the example ML model being deployed](./mean_classifier_example) image is from the Seldon core Examples, and is reproduced here.

The [Seldon operator chart](https://github.com/SeldonIO/seldon-core/tree/master/helm-charts/seldon-core-operator) is templated out by [Replicated Ship](https://github.com/replicatedhq/ship) in `base/seldon-core-operator/rendered.yaml`, and will be deployed alongside the app to power any `SeldonDeployment`s.

### Integrating with CI

Often teams will use one channel per developer, and then keep the `master` branch of this repo in sync with their `Unstable` branch.

The project includes CI configs for [Travis CI](https://travis-ci.org), [CircleCI](https://circleci.com), and [Gitlab CI](https://about.gitlab.com/product/continuous-integration/).

All CI configs will:

**On pull requests**:

- Install dependencies
- Lint yaml for syntax and logic errors

**On merges to the github `master` branch**:

- Install dependencies
- Lint yaml for syntax and logic errors
- Create a new release on the `Unstable` channel in Replicated

These behaviors are documented and demonstrated in the [replicated-ci-demo](https://github.com/replicatedhq/replicated-ci-demo) project.

### Tools reference

- [replicated-lint](https://github.com/replicatedhq/replicated-lint)
- [replicated vendor cli](https://github.com/replicatedhq/replicated)

### License

Replicated starter files are licensed under an MIT License

Seldon source is licensed under an Apache 2 license, which is included in [mean_classifier_example](./mean_classifier_example)
